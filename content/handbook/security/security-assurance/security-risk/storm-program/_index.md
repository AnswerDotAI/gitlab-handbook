---
title: "Security Operational Risk Management (StORM) Program & Procedures"
controlled_document: true
---

{{% panel header="**Not a GitLab team member but want to provide feedback on our StORM program?**" header-bg="primary" %}}
We receive [feedback](/handbook/people-group/guidance-on-feedback/#feedback-at-gitlab) from GitLab team members regularly and we wanted to provide a mechanism for non-GitLab team members to provide feedback as well to help us [iterate](/handbook/values/#iteration) and align more closely with [our values](/handbook/values). If you are not a GitLab team member and would like to provide feedback on our Security Operational Risk Management (StORM) program or methodology, plese use this [feedback form](https://docs.google.com/forms/d/e/1FAIpQLSfmD4G6CTdpbCe5Aymoz0oD6Z3Oi1X-2xxYzGNbJ2wcYh6uOA/viewform?usp=sf_link) to submit anonymous feedback.
{{% /panel %}}

## Purpose

The purpose of the Security Operational Risk Management ("StORM") program at GitLab is to enable better [decision-making](/handbook/leadership/making-decisions/) by identifying, monitoring, treating, and reporting on security operational risks in support of GitLab's [strategy](/handbook/company/strategy). The Security Risk Team utilizes the procedures below (formed through consideration of guidance set forth in [NIST's SP 800-39](https://csrc.nist.gov/pubs/sp/800/39/final), [SP 800-30 Rev. 1](https://csrc.nist.gov/pubs/sp/800/30/r1/final), and [ISO 31000 Risk Management Methodology](https://www.iso.org/standard/65694.html)) to ensure that security risks that may impact GitLab are effectively managed.

## Scope

The scope of the StORM program is limited to operational, technology-agnostic security risks. These risks can be identified in many ways including Risk Assessments, reports from team members, [industry trends](https://github.com/jacobdjwilson/awesome-annual-security-reports), or as a result of compliance activities. There may be instances where an application's role is so significant to internal security controls that we may create risks specifically for that system. This will primarily be limited to GitLab.com as its use is pervasive in all that we do.

**Out of Scope** Unless they are related to a StORM risk (for example security compliance observations that span multiple systems), the following risk-types are not in scope for StORM:

1. Operational risks that are not security-related are out of scope (ex. accounting-specific risks)
1. [Individual, system-specific security compliance observations](/handbook/security/security-assurance/observation-management-procedure/) (ex. inadequate password settings for a specific system)
1. [Enterprise Risk Management (ERM)](https://internal.gitlab.com/handbook/internal-audit/erm/) - internal only. Examples of ERM risks can be found on our [Mitigating Concerns](https://internal.gitlab.com/handbook/leadership/mitigating-concerns/) (internal only) handbook page.

## Roles and Responsibilities

A risk governance structure has been put in place to outline the overall roles and responsibilities of individuals as it relates to StORM. The current governance structure is:

| Role | Responsibility |
| ------ | ------ |
| Executive Risk Owner | - Accountable for driving treatment for one or more of GitLab's Top 5 Security Risks <br>- Responsible for identifying one or more Risk Owners. Security Risk recommends identifying at least one Risk Owner per department involved in risk treatment <br>- Responsible for approving the long-term risk treatment plan including the creation of KRs to associated treatment milestones identified by Risk Owners and the Security Risk Team <br>- Note that most Executive Risk Owners will be CEO + 2 (Senior Director or VP-level) and will be responsible for cross-department collaboration to drive risk reduction over time |
| Risk Owners |  - Responsible for the creation of a long-term risk treatment plan including treatment milestones meant to reduce  residual risk over time <br>- Accountable for executing risk treatment activies <br>- Responsible for collaborating with the Security Risk Team to ensure associated risk(s) and treatment status are reported periodically <br>- Note that most Risk Owners will be CEO + 3 (Senior Manager or Director level) |
| Security Risk Manager | This role is assigned per risk to a specific Security Risk team member. Expectations include:<br>- Maintains knowledge on the history, current-state, and direction of their risk<br>- Works with the risk owner or owners to ensure the risk status and treatment is documented<br>- Identifies, monitors, and participates in associated issues/MRs/epics/working groups that are relevant to their assigned risk<br>- Validates remediation activities<br>- Maps risks to relevant <a href="/handbook/security/security-assurance/security-compliance/sec-controls/#gitlab-control-framework-gcf">GCF controls</a>, <a href="https://gitlab.com/groups/gitlab-com/gl-security/security-assurance/-/epics?state=opened&page=1&sort=start_date_desc&label_name[]=Observation+Epics">Root Cause Observation Epics</a>, Security Compliance Tier 3 Observations</a>, <a href="/handbook/security/security-assurance/field-security/field-security-study/">Field Security Study Observations</a>, and other observations noted from security-impacting assessments (internal-only) <br>- Collaborates with Executive Risk Owner and Risk Owners to create and monitor long-term risk treatment plans|
| Security Risk Team | - Coordinates and executes StORM procedures including establishing risk appetite and conducting risk assessments<br>- Maintains the risk register to ensure accuracy and currency<br>- Acts in a Program Management capacity to support the tracking of risk treatment activities<br>- Coordinates peer validation testing after all risk remediation activities have been completed <br>- Periodically reports on the status of security operational risks <br> - Provides management level oversight of the StORM program, including continuing reviews of GitLab's Risk Register and acts as a point of escalation as needed <br>- Responsible for approving significant changes and exceptions to this procedure|

## StORM Procedures

### Establishing Risk Appetite and Tolerance

**Tone at the Top**: GitLab's StORM methodology uses a defined Risk Appetite and Risk Tolerance as primary drivers to determine which risks GitLab are willing to accept/take versus which risks we will need to mitigate. These thresholds are defined by Senior Leadership across the organization to ensure the Tone at the Top is aligned with the StORM program. Risk Appetite and Tolerance are reassessed year-to-year. This is done through an annual Risk Appetite Survey based on the [ISO 31000 Risk Management Methodology](https://www.iso.org/standard/65694.html). The survey is distributed to individuals operating in a Senior Leadership capacity with direct relations to Security Operations. The responses are averaged to arrive at an overall risk appetite and tolerance.

#### How GitLab Determines Risk Appetite

GitLab's security risk appetite is determined based on the total average priority order determined by senior leadership on the following risk strategy statements:

- GitLab should seek solutions to transfer risks to others whenever possible (risk taking vs risk transfer)
- GitLab should balance pursuing opportunities that align with organizational objectives against the associated risks (organizational objectives)
- GitLab should respond to all risks impacting the organization, regardless of the level of impact (risk response approach)
- GitLab should respond to risks based on cost, management priorities, and ROI (risk response drivers)

Each risk strategy statement is ranked in order of priority from Highest priority risk strategy to Lowest priority risk strategy by senior leadership. GitLab utilizes the following risk appetite matrix:

| RISK APPETITE<br>APPROACH | RISK SEEKING | RISK RECEPTIVE | RISK NEUTRAL | RISK AVERSE |
| ---- | ---- | ---- | ---- | ---- |
| **RISK TAKING vs**<br>**RISK TRANSFER** | Aggressive risk<br>taking is justified | Seek opportunities to transfer risks<br>with pre-existing vendors as applicable<br>(e.g. don't bring in a new vendor to<br>transfer risks) | Take a balanced approach to<br>risk taking vs risk transferring | Exercise caution and accept as little<br>risk as possible by identifying risk<br>transfer solutions |
| **ORGANIZATIONAL**<br>**OBJECTIVES** | Willing to accept a large negative<br>impact to the organization to pursue<br>opportunities that align with objectives | Willing to accept some negative impact<br>(e.g. LOW risks) to pursue opportunities<br>that align with objectives | The potential for a negative impact<br>vs objectives are given equal<br>consideration when making a decision | The potential for a negative impact vs<br>objectives are given equal consideration<br>when making a decision |
| **RISK RESPONSE**<br>**APPROACH** | All risks are acceptable as long<br>as they do not impact our legal<br>and regulatory obligations | Determine risk response options to<br>help accept or reduce risk levels<br>through internal initiatives | Risk remediation is favored over<br>risk acceptance | Risks that cannot be effectively<br>treated or transferred are avoided |
| **RISK RESPONSE**<br>**DRIVERS** | No response action required for risks<br>unless they may represent a<br>contract or regulatory violation | Risk response actions take into<br>consideration cost effectiveness,<br>management priorities, and return<br>on investment | Risk response actions emphasize the<br>impact to security over the impact<br>to strategic objectives | Risk response actions are always taken,<br>regardless of cost effectiveness,<br>management priorities, return on investment,<br>and overall organizational objectives |

*GitLab's Risk Appetite Matrix was formed through consideration of guidance set forth in NIST's [SP 800-39](https://csrc.nist.gov/pubs/sp/800/39/final) and [SP 800-30 Rev. 1](https://csrc.nist.gov/pubs/sp/800/30/r1/final).*

Scoring is performed by individuals operating in at least Senior Leadership capacity within GitLab and spans across multiple departments.

#### Translating GitLab's Security Risk Appetite to Risk Tolerance

Our risk appetite is translated to a tolerance which defines a range in which a [risk score value](#risk-factors-and-risk-scoring) is tolerable and does not require remediation or a risk acceptance, i.e., the risk response will be set to "monitor". Risk scores can range from 1 (lowest) to 30 (highest). The range is defined per Risk Appetite in the table below:

|Risk Averse|Risk Neutral|Risk Receptive|Risk Seeking|
|:---------:|:---------:|:---------:|:---------:|
|1-5|1-10|11-15|16-20|

Risk scores above 20 (High or Critical risk rating) are considered too risky to be considered within tolerance. In other words, risks that are rated High and Critical must be treated.

#### Historical and Current Record of GitLab's Security Risk Appetite

|Fiscal Year|Departments|Risk Appetite|
|:-----:|----------|:-----:|
|FY24|All Departments|Risk Neutral|
|FY23|Engineering, Finance, and Legal|Risk Neutral|
|FY22|E-group, Engineering, Finance, and Legal|Risk Neutral|
|FY21|Engineering, Finance, and Legal|Risk Neutral|

### Risk Identification

#### Communication of Risks to the Security Risk Team

There are multiple ways the team can be engaged for risk:

1. (**Preferred**) Submit a [Risk Escalation issue](https://gitlab.com/gitlab-com/gl-security/security-assurance/security-risk-team/storm/-/issues/new?issuable_template=risk-escalation) on the StORM Repo.
1. If the risk is identified within an issue, team members can tag the team directly by @ mentioning `@gitlab-com/gl-security/security-assurance/security-risk-team` on the issue or MR

When documenting risks, team members can leverage [Observation Description guidance](/handbook/security/security-assurance/observation-management-procedure/#drafting-observation-description-guidance) for existing issues/observations or [risk drafting guidance](#risk-drafting-guidance).

#### Risks identified during risk assessments

The Security Risk Team may interview/survey GitLab team members operating in a leadership capacity at GitLab in order to identify security operational risks. Risks identified will always be framed in terms of threat sources and threat events, and then assessed against the likelihood of occurrence and the impact to GitLab if the risk event occurs. Additionally, these risks will be assessed against the current internal controls in place to determine the overall residual risk remaining.

In order to effectively identify, manage, and treat operational risks, GitLab has defined a set of threat source categories alongside specific risk factors and risk scoring definitions. Based on these threat sources, various stakeholders across the organization will be identified to participate in the Risk Identification phase. The identification of threat sources and events in relation to operational risks includes multiple considerations. These threat sources and events have been identified based on their potential to have an impact on mission critical objectives in relation to GitLab's operations.

#### Example Threat Sources and Events Considered

| Threat Source | Example Threat Events |
| :-----------: | --------------------- |
| **Adversarial** | Fraud and theft, insider threat, malicious hacker, and malicious code |
| **Non-Adversarial** | Errors and omission, loss of physical and infrastructure support (e.g. a natural disaster), exposure of sensitive information, changes to systems used to support the business, changes to external environments supporting GitLab, changes to GitLab's business model, or even changes in leadership |

#### Risk Drafting Guidance

StORM Program considerations include both risks (what might happen) and observations (what has happened/non-compliance). For guidance on writing observations, please refer to the[Observation Management Procedure Handbook page](/handbook/security/security-assurance/observation-management-procedure/).

When drafting a risk, start with a risk statement. This will represent the title of the Risk in our GRC system and is an attempt to condense the risk into a single sentence. In the spirit of [low-context communication](/teamops/decision-velocity/#low-context-communication), avoid using single words or short phrases for the risk statement (ex. Supply Chain). As we largely deal with negative risks (vs. positive risks/opportunities), starting the statement with negative language like "Failure to", "Inadequate", "Incomplete", "Lack of", etc. is appropriate, but not required. As risks represent what might happen, use "may" before describing the negative effect it *may* have on the confidentiality, integrity, availability, security, and privacy of GitLab data. Example: *Inadequate physical security controls may result in the loss of GitLab/Customer data and physical assets.* The risk description should contain details related to the assets/resources at risk, the event that may occur, the source that would trigger the event (root cause), and the consequence (impact/loss) [source](https://www.srmam.com/post/how-to-write-a-risk-statement).

#### Risk Factors and Risk Scoring

Risk rating/scoring is a favorite topic of risk management/decision support practitioners and [thought](https://hubbardresearch.com/risk-management-modeling/)-[leaders](https://normanmarks.wordpress.com/2022/07/31/risk-assessment-danger/). Scores are subjective and can be influenced by [unconscious biases](/handbook/company/culture/inclusion/unconscious-bias/) of those applying the scores. To help mitigate this risk, we report on risks and request feedback from management to help calibrate and ensure alignment on our highest priorities.

To score each risk, we leverage a formula based on the Likelihood of the risk event occurring and the Impact to GitLab if the event occurred. Likelihood and Impact scores directly determine the overall inherent risk to GitLab.

##### Determining Likelihood of initiation of a threat event

| Qualitative <br> Score | Risk Level | Scoring Guidelines |
| :--------------------: | :--------: | ------------------ |
| 6 | CRITICAL | No expertise required to initiate a threat event |
| 5 | VERY HIGH | Low level of expertise required to initiate a threat event   |
| 4 | HIGH | Some expertise required to initiate a threat event           |
| 3 | MEDIUM  | Difficult to initiate a threat event, even with expertise    |
| 2 | LOW  | Requires significant expertise to initiate a threat event    |
| 1 | VERY LOW  | Theoretically impossible to initiate a threat event |

##### Determining the impact of a threat event

| IMPACT<br>SCORE | Organizational Output<br>(time, quality, resources) | Brand<br>Reputation | Business<br>Continuity | Customers &<br>Stakeholders | Legal &<br>Regulatory | Financial |
| :---------------: | ------------- | --- | -------- | ---------- | ----------- | ------- |
| VERY LOW (1) | Organizational output is<br>impacted by less than 20% | Limited to reputational damage<br>with no more than one customer<br>within a fiscal period | Outages of non-critical systems<br>that impact GitLab team members | Impact is limited to one<br>customer and/or stakeholder | Breach of company policy<br>occurring once in a fiscal<br>period  | Loss up to $999   |
| LOW (2) | Organizational output is<br>impacted by 30% - 40% | Confined to a limited number of<br>parties (e.g. specific customers)<br>and not publicized | Outages which result in the inability<br>of GitLab to continue sales and finance<br>operations longer than 72+ hours | Impact is limited to 2-3<br>customers and/or stakeholders | Breach of company policy<br>twice within a fiscal period | Loss between $1,000<br>and $9,999 |
| MEDIUM (3) | Organizational output is<br>impacted by 40% - 50% | Public domain publicity but limited<br>to industry channels and not the<br>broader public | Outages that impact GitLab's<br>ability to do business across 3+<br>departments | Impact is limited to 4-5<br>customers and/or stakeholders | Breach of a regulatory and/or<br>contractual obligation | Loss between $10,000<br>and $499,999  |
| HIGH (4) | Organizational output is<br>impacted by 50% - 75% | Wide-spread publicity but limited<br>parties are impacted  | Outages that result in the loss of<br>availability of GitLab for customers<br>for less than 4 hours | Major impact to many<br>customers and/or stakeholders | Regulatory censure and/or action<br>taken against GitLab | Loss between $500,000<br>and $999,999 |
| VERY HIGH (5) | Organizational output is<br>impacted by 75% or more | Widely publicized | Outages that result in the loss of<br>availability of GitLab for customers<br>for 4+ hours | Major impact to all<br>customers and/or stakeholders | Public regulatory fines and/or major<br>litigation against GitLab | Loss of $1,000,000+ |

To arrive at a final impact score, the impact score of all impact categories is averaged.

#### Determining Inherent Risk vs Residual Risk

- Inherent Risk is the risk *before* considering any existing mitigations in place, such as existing controls, internal processes/procedures, etc. and is determined by the following formula:
   > `Inherent Risk = Likelihood x Impact`

- Residual risk is calculated in the same manner as inherent risk, but the likelihood and impact is reassessed based on the known existing controls, processes/procedures, etc. that reduce/mitigate the risk.

#### Determining if a risk is considered Low, Medium, High, or Critical

Once the Inherent and Residual risk score is determined, the following table can be used to determine if a risk is considered Low, Medium, High, or Critical:

|Risk Rating|Risk Score Range|
|:---------:|:--------------:|
|Low|1-10|
|Medium|11-20|
|High|21-25|
|Critical|26-30|

These ratings represent labels for communication purposes rather than what is or is not acceptable. To determine what is an acceptable risk, please refer to [risk tolerances](#translating-gitlabs-security-risk-appetite-to-risk-tolerance).

#### Ad-hoc Risk Identification and Assessment

There may be times that risks are identified outside of traditional risk assessments - such as risks that arise from a security incident, risk identified through regular day-to-day business operations, etc. All security operational risks identified ad-hoc are discussed with the Security Risk Team, an inherent risk score is assigned, and a qualitative analysis done to determine if it should be escalated to the risk register.

### Risk Response

For each risk identified, a formal risk response decision is made to determine how GitLab will handle the risk. As part of the risk response procedures, the Risk Owner will make a determination on whether or not to accept a risk or pursue remediation based on our [Risk Appetite and Tolerances](#establishing-risk-appetite-and-tolerance). Treatment plans will be reviewed by the Security Risk Manager or delegate and approval captured via comment in the GRC application or associated GitLab issue.

| RESPONSE<br>OPTION  | DEFINITION |
| :-----------------: | ------------------------------------------- |
| Monitor (do nothing) | The risk score falls within our [risk tolerance levels](/handbook/security/security-assurance/security-risk/storm-program/#translating-gitlabs-security-risk-appetite-to-risk-tolerance) and no additional actions are required at this time. Risks that have been treated, resulting in a risk score that is within the risk tolerance level will be given the status of Monitor within our GRC system. |
| Remediate the Risk   | The risk is not within our risk tolerance. Complete a risk remediation plan to remediate the risk through: Sharing the risk (identify and implement solutions to share the risk with other parties), Reducing the likelihood of occurrence, and/or Reducing the level of impact to GitLab |
| Accept the Risk | The risk is not within our risk tolerance. Accept or take the risk without executing a remediation plan because the cost to pursue remediation is higher than the potential benefit. |

The risk object in the GRC application will be updated to reflect the agreed upon risk response. If "Remediate the Risk" is selected, the Risk Owner will execute a Risk Treatment Plan. The documented plan and status of the risk treatment will be captured within the GRC application as well. See below for more information about risk response options.

#### Monitor (nothing beyond expected iteration)

In the cases where a risk owner has concluded that a risk is within [tolerance](#translating-gitlabs-security-risk-appetite-to-risk-tolerance), no additional action is required besides ensuring that the StORM Program DRI agrees with the treatment option.

#### Remediate the Risk

When choosing to remediate the risk, a specific path must be selected:

- Remediate by reducing the likelihood that the risk could occur
- Remediate by reducing the impact to GitLab if the risk occurs
- Remediate by sharing or transferring the risk with a third party
- Remediate by avoiding the risk by deciding not to start or continue with the activity that gives rise to the risk

Once a path is selected, the Risk Owner is required to provide a [SMART](https://en.wikipedia.org/wiki/SMART_criteria), detailed plan that includes milestones and due dates for working towards risk remediation. The treatment plan must be achievable and address the root cause of the risk event. Additionally and in alignment with our value of [Transparency](/handbook/values/#transparency), each treatment plan will include a step for documenting the results/outcome of the remediation within the Handbook. If the result of the remediation is considered [not public](/handbook/values/#not-public) and cannot be documented within the Handbook, it should be documented within our Internal Handbook or an internal runbook. The Security Risk Team will leverage these risk treatment plans to track the status of risk remediation.

If the risk treatment plan is executed and results in a downgrading of the residual risk level for the risk (ex. the residual risk level goes from High to Medium), validation of the remediation will be performed and captured within the associated risk object. Quality review of the downgrade support documentation will be completed by the Security Risk Manager and captured via comment in the GRC application.

#### Accept the Risk

In the cases where a risk owner has opted to pursue a risk acceptance, the following approvals will be required based on risk rating that was assigned to the risk undergoing a risk acceptance:

|Risk Level|Approval Level Required|
|-----|-----|
|CRITICAL|Risk Owner + VP Level Approval* + E-group Level Approval|
|HIGH/MEDIUM|Risk Owner + VP Level Approval*|

`*` If the Risk Owner is a VP, no additional VP level approval is required

By accepting the risk, the Risk Owner and risk acceptance approvers (if separate from Risk Owner), agree to reassess the risk on an annual basis to determine whether risk acceptance is the best response option for the respective risk. If risk acceptance is appropriate based on the annual assessment, approvals will be re-obtained based on the risk and approval requirements noted in the table above. Additionally, the Risk Owner will be on point for remediation in the event the risk is realized or risk acceptance is no longer appropriate.

### Risk Tracking and Reporting

Identified risks are formally tracked via an internal risk register. Given the nature of the sensitivity of this information in aggregate, the risk register is [not made public](/handbook/communication/confidentiality-levels/#not-public), and is not distributed externally. However, a publicly viewable GitLab Risk Register Template is available [here](https://docs.google.com/spreadsheets/d/1Lvn-ZjPNcZ-QMh-pkC6HqjwR-acUf70V9w2pquhRmH0/edit?usp=sharing) for those interested in getting some more insight into the type of information tracked in GitLab's risk register. StORM-related risk activities are centralized [within GitLab](https://gitlab.com/gitlab-com/gl-security/security-assurance/security-risk-team/storm-risk-register/-/issues/?sort=weight_desc&state=opened&first_page_size=100) (internal only). 

We report on our top 5 risks on a quarterly basis (the Security Risk Quarterly or "SRQ") in alignment with our values. To learn more about the SRQ, please see our YouTube unfiltered video linked [here](https://www.youtube.com/watch?v=sHZr-5SR7yg). The template we've used can be found [here](https://docs.google.com/document/d/1cpBbn_0kIWpEzbzLrzEcVesN-3Y0y1K6SD6wiv0-Vaw/edit?usp=sharing) for reference. Additionally, we perform an annual exercise to refresh our Risk Appetite and our Top 5 risks.

The StORM program is integrated within daily operations at GitLab. As such, we have mapped our StORM risks to risk sources including [Security Compliance controls and observations](/handbook/security/security-assurance/observation-management-procedure/) and [Product Security's Risk Register](/handbook/security/product-security/security-platforms-architecture/risk-register/). Our mapping exercises are intended to provide a more comprehensive view of our security risk landscape and to enable StORM engineers to more quickly identify and escalate risks. 

GitLab team members can find all Security Risk Quarterly documents in the [SRQ Reports Google Drive folder](https://drive.google.com/drive/folders/18KeZiRGtWuZLke2TxYlhD6Mjgoyv4tBJ). 

## Top 5 Risks

The Security Division's "Top 5 Risks" are established annually and are reported upon quarterly as resources allow via the SRQ. Security Leadership leverages these Top 5 Risks when conducting short and long-term strategic planning activities. We intend to support remediation through assisting with treatment activities and performing design and operating effectives assurance testing on key remediation activities.

### Long-Term Risk Treatment Planning

Executive Risk Owners are accountable for ensuring that long-term treatment plans are established and executed for each of the Top 5 Risks. The Security Risk Team is responsible for coordinating long-term treatment planning with the Executive Risk Owner and the associated Risk Owner(s). The following template is leveraged during planning to ensure consistency in our approach and in reporting:

- Establish success criteria that would move the risk within [tolerance](/handbook/security/security-assurance/security-risk/storm-program/#translating-gitlabs-security-risk-appetite-to-risk-tolerance). These criteria will become Key Results (KRs) and are the milestones used to gauge progress of risk remediation. Completed KRs will correlate to a reduced risk score.
- Identify dependencies for each KR.
- Identify a Risk Owner responsible for delivering each KR. This person should be in the department responsible for implementing the treatment activity.
- Establish realistic target delivery dates for each KR. Due to the nature of operational risks, we expect delivery dates to range up to 4 years in the future. Try to establish at least one KR per quarter to show incremental progress.
- Scoring: Subtract '10' (our risk tolerance threshold based on the current risk appetite) from the current risk score to identify the reduction required to move the risk within tolerance. Divide this difference by the number of projected KRs. The quotient/remainder is the amount the score will be reduced each time a KR is completed. This number can be adjusted judgmentally as required.

 In the event the Executive Risk Owner chooses not to pursue a Risk Remediation-related KR in a given quarter due to competing priorities, a [Risk Acceptance](/handbook/security/security-assurance/security-risk/third-party-risk-management/#tprm-security-notice-process) should be formalized to document the business rationale. This Risk Acceptance should contain rationale explaining why the risk of delaying additional Risk Remediation is less than the risk of not fulfilling the competing priority.

### StORM Reporting Schedule

The table below outlines planned/completed activities for FY25.

|Timing|Activities|
|-----|-----|
|Q1| SRQ |
|Q2| SRQ and Annual Refresh Planning |
|Q3| SRQ with refreshed risk appetite and Top 5 risks |
|Q4| SRQ |

## Exceptions

The only exceptions to this procedure are those risks that are out of scope (as defined above).

## References

- GitLab Handbook References:
  - [GitLab's Communication Page, Not Public Section](/handbook/communication/confidentiality-levels/#not-public)
- External References
  - [NIST SP 800-30 Rev. 1](https://csrc.nist.gov/pubs/sp/800/30/r1/final)
  - [ISO 31000 Risk Management Methodology](https://www.iso.org/standard/65694.html)
