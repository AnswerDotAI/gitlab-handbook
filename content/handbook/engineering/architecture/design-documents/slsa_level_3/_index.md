---
title: "SLSA Level 3 Provenance Attestations"
status: ongoing
creation-date: "2024-12-18"
authors: [ "@nrosandich" ]
coach: "@darbyfrey"
approvers: [  ]
owning-stage: "~devops::software supply chain security"
participating-stages: ["~group::runner", "~devops::verify"]
toc_hide: true
no_list: true
---

{{< engineering/design-document-header >}}

## Summary

This document outlines the technical vision, principles, and key architectural decisions for implementing SLSA Level 3 compliance within GitLab CI/CD pipelines. The solution will provide a reusable, modular, and secure way to generate, sign, and verify provenance for artifacts while hardening pipeline identity and build infrastructure.

## Proposal

We propose a phased implementation of SLSA Level 3 compliance across GitLab CI/CD pipelines using modular and reusable components. Each phase addresses a critical step:

1. In-Pipeline Provenance Generation and Verification using Sigstore: Generate and verify provenance attestation within the pipeline.
1. Generate Provenance Statement in Control Plane: Shift provenance generation from Runner to GitLab Rails backend to enhance trust.
1. Sign Provenance Statement in Control Plane: Move signing operations to dedicated service for better security.
1. KMS Integration for out-of-Pipeline Signing: Enable external, KMS-based artifact signing for enhanced security and compliance.
1. Hardening Pipeline Identity: Strengthen runner identity and build trust into the infrastructure.

This phased approach ensures an MVP can be delivered early, with incremental security and compliance enhancements added over time.

## Goals

- Embed GitLab-specific platform data (pipeline variables, commit IDs) into provenance for traceability.
- Support out-of-pipeline signing via secure KMS or HSM, isolating signing keys from build environments.
- Strengthen runner identity to provide trustworthy attestation of build provenance.
- Align with SLSA Level 3 compliance requirements while minimizing disruption to existing workflows.
- Ensure security, scalability, and ease of adoption across GitLab environments.

## Non-Goals

- Achieving SLSA Level 4 compliance, which requires isolated and verifiable builds (future consideration).
- Collecting dependencies of all possible programming ecosystems (focus on key ecosystems first).
- Replacing GitLab’s existing artifact storage and distribution mechanisms.

## Terminology/Glossary

- SLSA: Supply-chain Levels for Software Artifacts, a framework for improving supply chain security.
- Provenance predicate: Metadata that describes how an artifact was built, including the source code, dependencies, and environment.
- Provenance statement: Document that binds a provenance predicate to a software artifact.
- Provenance attestation: Envelope that combines a provenance statement with a signature.
- Sigstore: An open-source tool for signing, verifying, and storing software artifacts securely (cosign and gitsign).
- OIDC Token: Short-lived, identity-based tokens issued by GitLab CI for secure signing.
- Runner: A build agent that executes GitLab CI/CD pipeline jobs.
- KMS: Key Management Service, an external system to securely manage cryptographic keys.
- HSM: Hardware Security Module, hardware-based systems for secure key storage and signing.
- VSA: Verification Summary Attestation, an attestation that an artifact has been verified to meet certain requirements.
- GitLab Rails backend: The GitLab Rails backend that provides a trusted environment for security-critical operations, separate from the build environment.
- Signing Service: A dedicated service within the GitLab infrastructure responsible for SLSA statement signing operations, isolated from the CI/CD execution environment.

## Assumptions

- Provenance Generation: Use Sigstore Cosign (CLI, client, or port) to generate provenance attestations.
- OIDC-based keyless signing: Use Signstore Fulcio for OIDC-base keyless signing.
- Transparency log: Use Sigstore Rekor transparency log.
- Signing Methods:
  - In-pipeline signing via OIDC-based short-lived credentials for fast MVP.
  - Out-of-pipeline signing via KMS for long-term secure artifact signing.
- Runner Hardening: Explore options for strong runner identity using hardware-based solutions (TPM, secure enclaves).

## Design Details

### High Level Architecture

```mermaid
flowchart TD
    %% Define styles for improved visual appearance
    classDef phaseStyle fill:#f9f9f9,stroke:#333,stroke-width:2px,rx:10px,ry:10px
    classDef componentStyle fill:#e1ebff,stroke:#4b6bdc,stroke-width:1px,rx:5px,ry:5px
    classDef storageStyle fill:#ffe6cc,stroke:#d79b00,stroke-width:1px,rx:5px,ry:5px
    classDef serviceStyle fill:#d5e8d4,stroke:#82b366,stroke-width:1px,rx:5px,ry:5px
    classDef signatureStyle fill:#fff2cc,stroke:#d6b656,stroke-width:1px,rx:5px,ry:5px
    classDef securityStyle fill:#f8cecc,stroke:#b85450,stroke-width:1px,rx:5px,ry:5px
    classDef controlPlaneStyle fill:#e1d5e7,stroke:#9673a6,stroke-width:1px,rx:5px,ry:5px
    subgraph BuildEnvironment["Build Environment"]
        Runner["Runner"]
        BuildJob["CI/CD Build Job"]
        Artifacts["Job Artifacts"]
    end
    subgraph FutureWork["Dependency tracking"]
        VirtualRegistry["Virtual Registry<br>(Dependency Proxy)"]
        Dependencies[(Package & Container<br>Dependencies)]
    end
    subgraph ControlPlane["Controle Plane"]
        subgraph GenerateProvenanceInControlPlane["Phase 2: Generate Provenance in Control Plane"]
            RailsBackend["GitLab Rails Backend"]
            DB[(GitLab Database)]
        end
        subgraph SignProvenanceInControlPlane["Phase 3: Sign Provenance in Control Plane"]
            GlgoService["glgo Service<br>(Signing Service)"]
        end
        Rekor["Transparency Log<br>(Rekor)"]
        PermanentAttestation["Permanent Signed<br>Attestation"]
    end
    subgraph Phase4["Phase 4: Get private key from KMS"]
        ExternalKMS["External KMS"]
    end
    
    %% Relationships between components with labeled edges
    Runner -->|"Request job payload<br>with proof of identity"| RailsBackend
    RailsBackend -->|"Return job payload"| Runner
    Runner -->|"Executes"| BuildJob
    BuildJob -->|"Upload"| Artifacts
    BuildJob -->|"Request Dependencies"| VirtualRegistry
    VirtualRegistry <-->|"Fetch/Track"| Dependencies
    
    %% Phase 1 flow for early implementation
    VirtualRegistry -->|"Provide Dependency Data"| RailsBackend
    RailsBackend <-->|"Query job parameters"| DB
    
    RailsBackend -->|"Send Provenance<br>Statement"| GlgoService
    GlgoService -.->|"Future Integration"| ExternalKMS
    GlgoService -->|"Return Signed<br>Attestation"| RailsBackend
    GlgoService -->|"Publish Attestation<br>Digest"| Rekor
    RailsBackend -->|"Upload"| PermanentAttestation
    
    %% Apply styles
    class FutureWork phaseStyle
    class Phase4 phaseStyle
    class Artifacts,DB,Dependencies storageStyle
    class VirtualRegistry,GlgoService serviceStyle
    class ProvenanceSigner,TempSignedAttestation,PermanentAttestation,Rekor,ExternalKMS signatureStyle
    class RailsBackend controlPlaneStyle
```

#### Phase 1: In-Pipeline Provenance Generation and Verification using Sigstore

- Generate provenance attestations using Sigstore tools (cosign).
- Leverage GitLab CI’s OIDC tokens for secure and short-lived credentials.
- Verify provenance attestations and generate Verification Summary Attestations (VSA).
- Build reusable GitLab CI components that can be easily included in pipelines.

#### Phase 2: Generate Provenance Statement in Control Plane

- Move provenance statement generation to GitLab Rails backend.
- Every field of the provenance is generated or verified in the trusted control plane.
- Generate provenance statements that are unforgeable.

#### Phase 3: Out-of-Pipeline Signing

- Move signing operations from CI/CD pipelines to a signing service running on the backend.
- Enhance security by isolating signing operations from build environment.
- Provide centralized management of signing processes.
- Ensure clean separation between build and signing trust boundaries.

#### Phase 4: KMS Integration for out-of-pipeline Signing

- Enable integration with external KMS (AWS KMS, Google KMS) or HSM solutions.
- Use long-term signing keys stored securely outside the pipeline.
- Support multiple key management solutions to accommodate various enterprise environments.

#### Phase 5: Hardening Pipeline Identity

- Introduce strong runner identity using secure hardware (TPM, HSM, secure boot).
- Embed runner identity into the provenance metadata.
- Ensure that the runner environment is verified and trusted.

#### Follow-up Work: Enhanced Data Collection

- Integrate tools to collect granular build metadata (go mod graph for Go, Maven dependency trees for Java).
- Use GitLab's Virtual Registry (formerly Dependency Proxy) to track resolved dependencies requested by CI/CD build jobs.
- Update provenance structure to include enriched metadata.

### Implementation Details

#### Sigstore and GitLab OIDC Integration

- How Sigstore Will Be Used:
  - Sigstore tools, specifically cosign, will be leveraged to sign and verify provenance.
  - cosign can utilize GitLab CI’s OIDC integration to securely authenticate the job and issue short-lived credentials. These credentials will sign the provenance file.
  - The OIDC token provided by GitLab is scoped to the running pipeline job, making it ephemeral and secure.
- GitLab OIDC Integration Workflow:
  - GitLab generates an OIDC token in the CI component and exposes it as an environment variable.
  - Sigstore’s cosign uses the OIDC token to authenticate the GitLab CI job with Sigstore’s transparency log (Rekor).
  - Sigstore validates the identity and grants signing capability for the duration of the job.
  - cosign generates a signed provenance file (JSON format) and uploads it to GitLab’s artifacts store.
- OIDC Configuration in GitLab:
  - Enable GitLab OIDC support by using the existing ID Token feature.
  - Use GitLab CI/CD’s environment variables to expose tokens and necessary metadata.

#### GitLab CI Components

<details>
<summary>Provenance Signer Component</summary>

The provenance signer component will abstract away the complexity of provenance generation and signing. It will be implemented as a GitLab CI Component using a template YAML file.

**Component Overview**

- Input Variables:
  - TARGET_ARTIFACT: Path to the artifact or build output.
  - BUNDLE_FILE: Path to generate the bundle file. This contains everything needed to verify the artifact.
  - RUNNER_METADATA_FILE: This is the default filename when artifacts aren't explicitly named.
- Output:
  - Signed provenance file uploaded as a pipeline artifact.

**Example reusable Component YAML**

```yaml
# .gitlab/components/provenance-signer.yml
component:
  inputs:
    variables:
      TARGET_ARTIFACT: ""  # Path to the artifact
      BUNDLE_FILE: "provenance.json" # Output bundle file
      RUNNER_METADATA_FILE: "artifacts-metadata.json" # This is the default filename when artifacts aren't explicitly named

  id_tokens:
    GITLAB_OIDC_TOKEN:
      aud: sigstore

  variables:
    REKOR_SERVER: "https://rekor.sigstore.dev"
    FULCIO_SERVER: "https://fulcio.sigstore.dev"

  image: alpine:latest

  before_script:
    - apk add --update cosign jq

  script:
    - echo "Fetching GitLab Runner metadata..."
    - export RUNNER_METADATA=$(jq -c . ${RUNNER_METADATA_FILE})

    - echo "Generating predicate for ${TARGET_ARTIFACT}..."
    - echo "${RUNNER_METADATA}" | jq -c .predicate > predicate.json

    - echo "Attesting provenance for ${TARGET_ARTIFACT}..."
    - cosign attest-blob --predicate predicate.json \
        --type slsaprovenance1 \
        --oidc-issuer "${CI_SERVER_HOST}" \
        --fulcio-url "${FULCIO_SERVER}" \
        --rekor-url "${REKOR_SERVER}" \
        --identity-token "${GITLAB_OIDC_TOKEN}" \
        --bundle "${BUNDLE_FILE}" \
        --new-bundle-format \
        "${TARGET_ARTIFACT}"

    - echo "Performing self-verification to ensure provenance is valid..."
    - cosign verify-blob-attestation --type slsaprovenance1 \
        --bundle "${BUNDLE_FILE}" \
        --certificate-identity-regexp ".*" \
        --certificate-oidc-issuer "${CI_SERVER_URL}" \
        "${TARGET_ARTIFACT}"
    - echo "Self-verification successful! Provenance is valid."

  artifacts:
    paths:
      - ${BUNDLE_FILE}
    expire_in: 7d
```

</details>

<details>
<summary>Provenance Verifier Component</summary>

The provenance verifier component verifies attestations and generates VSAs. It will be implemented as a GitLab CI Component using a template YAML file.

**Component Overview**

- Input Variables:
  - BUNDLE_FILE: Path to the bundle file that contains the provenance.
  - VERIFICATION_SUMMARY_FILE: Path to generate the verification summary attestation.
  - RESOURCE_URL: Full URL to the published artifact.
  - POLICY_URL: URL to the policy used for verification.
- Output:
  - Verification summary attestation uploaded as a pipeline artifact.

**Example reusable Component YAML**

```yaml
# .gitlab/components/provenance-verifier.yml
component:
  inputs:
    variables:
      BUNDLE_FILE: "cosign-bundle.json" # Path to the bundle file
      VERIFICATION_SUMMARY_FILE: "verification_summary.json" # Output verification summary file
      RESOURCE_URL: "" # Full URL to the published artifact
      POLICY_URL: "https://gitlab.com/slsa-vsa-policy/v1" # Default policy URL

  id_tokens:
    GITLAB_OIDC_TOKEN:
      aud: sigstore

  variables:
    REKOR_SERVER: "https://rekor.sigstore.dev"
    FULCIO_SERVER: "https://fulcio.sigstore.dev"
    VERIFIER_ID: "https://gitlab.com/verifier"
    VERIFIER_NAME: "GitLab Verification Pipeline"
    DOWNLOADED_ARTIFACT: ".tmp/downloaded_artifact"

  image: alpine:latest

  before_script:
    - apk add --update cosign jq curl
    - mkdir -p .tmp

  script:
    - echo "Downloading artifact from ${RESOURCE_URL}..."
    - mkdir -p $(dirname ${DOWNLOADED_ARTIFACT})
    - curl -L -o ${DOWNLOADED_ARTIFACT} ${RESOURCE_URL}

    - echo "Calculating artifact digest..."
    - ARTIFACT_DIGEST=$(sha256sum ${DOWNLOADED_ARTIFACT} | cut -d ' ' -f 1)

    - echo "Downloading policy from ${POLICY_URL}..."
    - POLICY_FILE=".tmp/policy.json"
    - |
      if ! curl -L -f -o ${POLICY_FILE} ${POLICY_URL}; then
        echo "ERROR: Failed to download policy file from ${POLICY_URL}"
        exit 1
      fi

    - echo "Calculating policy digest..."
    - POLICY_DIGEST=$(sha256sum ${POLICY_FILE} | cut -d ' ' -f 1)
    - echo "Policy digest: ${POLICY_DIGEST}"

    - echo "Verifying signed provenance against downloaded artifact..."
    - cosign verify-blob-attestation --type slsaprovenance1 \
        --bundle ${BUNDLE_FILE} \
        --certificate-identity-regexp ".*" \
        --certificate-oidc-issuer ${CI_SERVER_URL} \
        ${DOWNLOADED_ARTIFACT}
    - RESULT="PASSED" # TODO: verify the provenance against the policies

    - echo "Generating verification summary for artifact..."
    - mkdir -p $(dirname ${VERIFICATION_SUMMARY_FILE})
    - jq -n --arg policyUrl "${POLICY_URL}" --arg result "${RESULT}" \
          --arg verifierId "${VERIFIER_ID}" \
          --arg timeVerified "$(date -u +'%Y-%m-%dT%H:%M:%SZ')" --arg resourceUri "${RESOURCE_URL}" \
          --argjson verifiedLevels '["SLSA_L3"]' --arg sha256 "${ARTIFACT_DIGEST}" \
          --arg bundleFilePath "${BUNDLE_FILE}" --arg bundleFileHash "$(sha256sum ${BUNDLE_FILE} | cut -d ' ' -f 1)" \
          --arg policyDigest "${POLICY_DIGEST}" \
          --arg slsaVersion "1.0" '{
        "_type": "https://in-toto.io/Statement/v1",
        "subject": [{
          "name": $resourceUri,
          "digest": { "sha256": $sha256 }
        }],
        "predicateType": "https://slsa.dev/verification_summary/v1",
        "predicate": {
          "verifier": {
            "id": $verifierId
          },
          "timeVerified": $timeVerified,
          "resourceUri": $resourceUri,
          "policy": {
            "uri": $policyUrl,
            "digest": {
              "sha256": $policyDigest
            }
          },
          "inputAttestations": [
            {
              "uri": $bundleFilePath,
              "digest": {
                "sha256": $bundleFileHash
              }
            }
          ],
          "verificationResult": $result,
          "verifiedLevels": $verifiedLevels,
          "dependencyLevels": {
            "SLSA_L3": 3
          },
          "slsaVersion": "1.0"
        }
      }' > "${VERIFICATION_SUMMARY_FILE}"

    - echo "Verification summary generated at ${VERIFICATION_SUMMARY_FILE}"
    - jq . ${VERIFICATION_SUMMARY_FILE}

    - echo "Signing the verification summary attestation..."
    - cosign attest-blob --predicate "${VERIFICATION_SUMMARY_FILE}" \
        --type slsaverificationsummary \
        --oidc-issuer "${CI_SERVER_HOST}" \
        --fulcio-url "${FULCIO_SERVER}" \
        --rekor-url "${REKOR_SERVER}" \
        --identity-token "${GITLAB_OIDC_TOKEN}" \
        --bundle "${VERIFICATION_SUMMARY_FILE}.bundle" \
        "${DOWNLOADED_ARTIFACT}"

    - echo "VSA signed and stored at ${VERIFICATION_SUMMARY_FILE}.bundle"

    - |
      if [ "$RESULT" == "FAILED" ]; then
        echo "Policy verification FAILED. Exiting with error."
        exit 1
      fi

  artifacts:
    when: always
    paths:
      - ${VERIFICATION_SUMMARY_FILE}
      - ${VERIFICATION_SUMMARY_FILE}.bundle
    expire_in: 7d

  allow_failure: true
```

</details>

<details>
<summary>Example: Adding the Components to a Pipeline</summary>

Here’s how a project would integrate the reusable component into their .gitlab-ci.yml pipeline.

Pipeline YAML Example

```yaml
stages:
  - build
  - provenance
  - publish
  - verify

variables:
  RUNNER_GENERATE_ARTIFACTS_METADATA: "true"
  RUNNER_METADATA_FILE: "artifacts-metadata.json" # This is the default filename when artifacts aren't explicitly named

build_artifact:
  stage: build
  script:
    - echo "Building artifact..."
    - mkdir -p dist
    - echo "Example artifact content" > dist/example-artifact.txt
  artifacts:
    paths:
      - dist/
    expire_in: 7d

generate_provenance:
  stage: provenance
  needs: ["build_artifact"]
  component: .gitlab/components/provenance-signer.yml
  variables:
    TARGET_ARTIFACT: "dist/example-artifact.txt"
    BUNDLE_FILE: "dist/provenance.json"
    RUNNER_METADATA_FILE: "${RUNNER_METADATA_FILE}"

publish_artifact:
  stage: publish
  needs: ["generate_provenance"]
  script:
    - echo "Publishing artifact to package registry..."
    - |
      ARTIFACT_URL=$(curl --header "JOB-TOKEN: ${CI_JOB_TOKEN}" \
        --upload-file dist/example-artifact.txt \
        "${CI_API_V4_URL}/projects/${CI_PROJECT_ID}/packages/generic/artifacts/1.0.0/example-artifact.txt" \
        | jq -r '.location')
    - echo "ARTIFACT_URL=${ARTIFACT_URL}" >> publish.env
  artifacts:
    reports:
      dotenv: publish.env

verify_provenance:
  stage: verify
  needs: ["publish_artifact"]
  component: .gitlab/components/provenance-verifier.yml
  variables:
    BUNDLE_FILE: "dist/provenance.json"
    VERIFICATION_SUMMARY_FILE: "dist/verification_summary.json"
    RESOURCE_URL: "${ARTIFACT_URL}"
    POLICY_URL: "https://gitlab.com/my-policy"
```

</details>

#### Pipeline Workflow Explanation

- Build Artifact Stage (build_artifact):
  - Builds the artifact (binary, container image, etc.).
  - Saves the artifact as a pipeline artifact.
- Provenance Generation Stage (generate_provenance):
  - Uses the provenance-signer component to:
    - Generate a detailed provenance predicate with build metadata.
    - Calculate the artifact's digest for inclusion in the provenance statement.
    - Sign the provenance using Sigstore's cosign with GitLab's OIDC token.
    - Perform self-verification to ensure the provenance is valid.
    - Uploads the signed provenance as a job artifact.
- Publish Artifact Stage (publish_artifact):
  - Publishes the artifact to a registry or repository.
  - Captures the published artifact's URL for use in verification.
  - This stage separates build/sign from verification, ensuring a true separation of concerns.
- Provenance Verification Stage (verify_provenance):
  - Uses the provenance-verifier component to:
    - Download the published artifact from its URL.
    - Download the required verification policy.
    - Verify the signed provenance against the downloaded artifact.
    - Check SLSA L3 requirements in the attestation.
    - Generate a Verification Summary Attestation (VSA).
    - Sign the VSA using Sigstore's cosign with GitLab's OIDC token.
    - Upload the VSA as a job artifact.
    - Fails the job if verification fails, but allows the pipeline to continue.

### Security Considerations

- Ephemeral OIDC Tokens:
  - The ID token is short-lived and scoped to the current job.
  - This ensures it cannot be reused outside the pipeline execution context.
- Artifact and Provenance Storage:
  - Use GitLab’s artifact storage to securely store both the build artifact and the signed provenance file.
  - Artifacts are automatically managed and can be expired after a specified time.
- Isolation:
  - If using shared runners, ensure sandboxed environments (ephemeral containers).
  - Self-hosted runners should follow security best practices to prevent token leakage.
- Dependency Management:
  - Pin specific versions of Sigstore tools (cosign) to prevent supply chain attacks.
- CI Variables:
  - CI Variables will be included in signed provenance file. But will follow the Visibility setting where `Masked` or `Masked and hidden` variables will not store the value, only the key.
- Separation of Concerns:
  - The separation of provenance generation and verification ensures that verification is truly independent.
  - The VSA is generated by the verifier component, providing a clear chain of trust.

### Component Maintenance and Scalability

- Publish the GitLab CI component in a versioned Git repository to ensure teams can pull stable versions.
- Provide clear documentation and examples for adoption.
- Extend the component in later phases to include additional metadata collection and signing enhancements.

### Decisions

- [001: Verification Component](decisions/001_verification_component.md) - Verify SLSA provenance attestations in a dedicated CI/CD component.
- [002: Provenance Generation Location](decisions/002_provenance_generation_location.md) - Generate SLSA provenance statements in the GitLab Rails backend.
- [003: Attestation Generation & Signing Location](decisions/003_attest_sign_location.md) - Generate and sign SLSA attestation in glgo.
