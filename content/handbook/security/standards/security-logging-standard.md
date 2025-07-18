---
title: GitLab Security Logging Standards
aliases:
- /handbook/security/security-logging-standard
note: Do not remove alias due to extensive external use where it cannot be updated.
---

## Purpose and Scope

The purpose of this security logging standard is to define GitLab's requirements for security logging. This document covers both security logging in GitLab's SIEM (Devo) as well as security logging requirements for systems not sending logs to GitLab's SIEM.

## Roles & Responsibilities

| Role | Responsibility |
|------|----------------|
| GitLab System Owners (as defined in GitLab's tech stack) | Directly Responsible for adhering to the requirements outlined in this standard |
| Security Operations Team | Directly Responsible for the prioritization, onboarding and maintenance of logs in the Security team's SIEM (Security Information Event Management) system, Devo. |

## Security Logging Requirements

Security logs are generated by applications and systems used on GitLab and are primarily used for security monitoring, security incident response and cyber threat hunting.

The GitLab Security Operations team iteratively evaluates the priority of security logs for existing systems, and evaluates requests for new log sources that must be onboarded for improved security observability. The Security Operations team maintains a Single Source of Truth (SSOT) for the security logs in their SIEM.

As new applications, systems and services are onboarded at GitLab, if a system's security logs (e.g. App, OS, transaction logs) are not sent to GitLab's SIEM, security logs must be stored in approved secure storage for a duration aligned with our retention policy.

### Security Log Retention Requirements

| Security Log Description | Retention Requirements |
|--------|-------------|
| Security logs for production systems | 1 year minimum |
| Security logs for critical systems that are not production | 90 days minimum |

### Security Log Collection Requirements

At a minimum, authentication and transaction events must be collected for GitLab production systems and also for non-production critical GitLab systems.

A detailed description of security events and fields is outlined below.

| Security Log Event Type | Required? | Security Log Field |
|--------|-------------|--------------|
| Authentication Events | Yes | User |
| Authentication Events | Yes | Timestamp |
| Authentication Events | Yes | Source IP address |
| Authentication Events | Yes | Destination IP address |
| Authentication Events | Yes | Action that was attempted |
| Authentication Events | Yes | Action result (success or failure) |
| Transaction Events | Yes | User |
| Transaction Events | Yes | Timestamp |
| Transaction Events | Yes | Source IP address |
| Transaction Events | Yes | Action that was attempted |
| Transaction Events | Yes | Action result (success or failure) |
| Data Access Events | No - Dependent on log verbosity | User |
| Data Access Events | No - Dependent on log verbosity | Timestamp |
| Data Access Events | No - Dependent on log verbosity | Source IP address |
| Data Access Events | No - Dependent on log verbosity | Action that was attempted |
| Data Access Events | No - Dependent on log verbosity | Accessed resource |
| Data Access Events | No - Dependent on log verbosity | Action result (success or failure) |
| Alert Events | No - Dependent on log verbosity | Alert name |
| Alert Events | No - Dependent on log verbosity | Timestamp |
| Alert Events | No - Dependent on log verbosity | User |
| Alert Events | No - Dependent on log verbosity | Source IP address |
| Security Alert Events | No - Dependent on log verbosity | Action |
| Security Alert Events | No - Dependent on log verbosity | Additional alert details |
