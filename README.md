# Project 3: Authentication & Access Management

**Company:** Southstars Retail (Fictional Scenario)  
**Platform:** Microsoft Entra ID  
**Project Type:** Identity and Access Management (IAM) / Cybersecurity  

## 1. Project Overview

Southstars Retail is a fictional retail company seeking to strengthen account security as employees increasingly access Microsoft cloud services. The IT team wants to reduce unauthorized access, protect privileged accounts, improve authentication practices, and establish secure account recovery procedures.

This project evaluates authentication-method configurations in Microsoft Entra ID, develops proposed Conditional Access policies, examines sign-in troubleshooting scenarios, and recommends security improvements.

The project was completed using a Microsoft Entra ID Free tenant for configuration review and documentation. Conditional Access policies were designed as recommendations and were not deployed.

## 2. Project Objectives

- Review available authentication methods and multifactor authentication (MFA) configurations.
- Evaluate authentication options for employees and privileged administrators.
- Design Conditional Access policies for employee and administrator accounts.
- Analyze suspicious sign-in scenarios and appropriate incident-response actions.
- Develop secure account recovery recommendations.
- Identify licensing limitations and define success criteria for future implementation.

## 3. Environment and Scope

**Environment**
- Microsoft Entra ID Free
- Microsoft Entra admin center
- Fictional company scenario: Southstars Retail

**Scope of work**
- Reviewed existing authentication-method policy settings.
- Verified the tenant's Security Defaults configuration.
- Designed two proposed Conditional Access policies.
- Developed sign-in troubleshooting and account recovery scenarios.
- Documented security recommendations and implementation considerations.

**Project limitations**

Conditional Access deployment generally requires Microsoft Entra ID P1 or an eligible higher-level license. The policies in this project are proposed designs, not deployed configurations. Authentication methods were reviewed through the administrative portal. Enabled methods were not assumed to be registered or tested by every user.

## 4. Authentication Methods Review

The Microsoft Entra admin center was used to review the tenant's existing authentication-method policy settings.

### Methods observed as enabled

- Microsoft Authenticator
- FIDO2 security keys
- Temporary Access Pass
- Software OATH tokens
- Email one-time passcode

### Methods observed as disabled

- SMS
- Voice calls
- Hardware OATH tokens
- Certificate-based authentication
- Microsoft Entra Verified ID
- QR code authentication

### Security assessment

Authentication methods serve different purposes and provide different levels of protection.

- **Microsoft Authenticator:** A practical option for everyday employee authentication and MFA.
- **FIDO2 security keys:** A phishing-resistant authentication option recommended for privileged accounts.
- **Temporary Access Pass (TAP):** Can support secure onboarding and authentication-method registration or recovery when configured appropriately.

An enabled authentication method does not necessarily mean an employee has registered or can use it. The organization should verify registration, establish appropriate authentication requirements, and document recovery procedures.

## 5. Security Defaults and Conditional Access

### Security Defaults

Security Defaults provides Microsoft-managed baseline identity protections, including MFA requirements in supported scenarios. Southstars Retail's tenant had Security Defaults enabled.

This provides a baseline without requiring the same licensing as Conditional Access, although it offers less customization.

### Conditional Access

Conditional Access enables more granular access policies based on factors such as users, directory roles, applications, device conditions, locations, and risk signals, subject to licensing and feature availability.

For Southstars Retail, Conditional Access would allow the IT team to define and evaluate more specific access requirements.

## 6. Proposed Conditional Access Policies

The following policies were designed as recommendations for a properly licensed environment. They were not deployed in the project tenant.

### Policy 1: Require MFA for Administrators

**Objective:** Strengthen protection for accounts with elevated privileges.

- **Users:** Accounts assigned relevant administrative directory roles.
- **Resources:** All resources, where broad protection is intended.
- **Grant control:** Require multifactor authentication.
- **Exclusions:** Designated emergency access accounts, subject to strict safeguards and monitoring.
- **Testing:** Validate policy behavior in report-only mode before enabling it.

**Rationale:** Administrative accounts have elevated permissions and can affect users, access, and tenant configuration. Requiring MFA reduces reliance on passwords alone.

The policy should target relevant directory roles rather than relying only on individual names, making it easier to maintain as staff and responsibilities change.

### Policy 2: Require MFA for Employees

**Objective:** Strengthen authentication for regular employees accessing company resources.

- **Users:** All regular employee accounts.
- **Resources:** All resources, if organization-wide protection is intended.
- **Grant control:** Require multifactor authentication.
- **Exclusions:** Designated emergency access accounts, with appropriate safeguards and monitoring.
- **Testing:** Validate policy behavior and expected sign-in outcomes before enabling it.

**Rationale:** Requiring MFA reduces the risk of unauthorized access when an employee's password is compromised.

### Policy testing and emergency access

Before deployment, the IT team should verify policy scope, exclusions, overlapping policies, and expected sign-in behavior. Emergency access exclusions must be reviewed across every applicable policy, not just one policy.

Emergency access accounts should be tightly controlled, monitored, and protected using an appropriate authentication strategy. The team should also test emergency access procedures to reduce the risk of administrative lockout.

## 7. Sign-In Troubleshooting Scenarios

### Scenario A: Employee cannot complete MFA

**Situation:** An employee enters the correct password but cannot complete MFA because their registered authentication method is unavailable.

**Recommended response:**

1. Verify the employee's identity using approved procedures.
2. Review registered authentication methods and determine whether another valid method is available.
3. If recovery is necessary, follow the organization's secure recovery process, potentially using Temporary Access Pass where appropriately configured.
4. Help the employee restore secure access without permanently removing MFA protection.

**Security consideration:** Authentication settings should not be changed without identity verification, since an attacker could otherwise exploit the recovery process to take over an account.

### Scenario B: Unexpected MFA approval request

**Situation:** An employee receives an MFA request despite not attempting to sign in.

**Recommended response:**

1. Deny the unexpected request and report it to IT support.
2. Review sign-in logs for unfamiliar locations, devices, IP addresses, repeated failures, and unrecognized successful sign-ins.
3. Investigate potential credential or session compromise and check for suspicious authentication-method changes.
4. If compromise is suspected, follow incident-response procedures, which may include temporarily blocking sign-in, revoking active sessions, and resetting the password through a secure process.
5. Restore access after the account has been secured and the investigation supports doing so.

**Security consideration:** An unexpected MFA request may indicate that someone has obtained the employee's password. A password reset alone may not be sufficient if active sessions or other forms of persistence remain.

## 8. Security Recommendations

### Recommendation 1: Require MFA for employees and administrators

Use available identity protections and appropriately licensed access controls to establish consistent MFA requirements. Prioritize protecting privileged accounts because of their elevated permissions.

### Recommendation 2: Adopt phishing-resistant authentication for privileged accounts

Evaluate FIDO2 security keys and other appropriate phishing-resistant authentication options for administrators. Establish procedures for registration, replacement, and recovery.

### Recommendation 3: Establish secure account recovery procedures

Require identity verification before changing authentication methods or resetting access. Document approved recovery procedures and test them using controlled scenarios.

### Recommendation 4: Evaluate Conditional Access licensing

Evaluate Microsoft Entra ID P1 or an eligible higher-level license to support more granular Conditional Access policies. Before implementation, confirm licensing, policy scope, exclusions, and expected user impact.

### Recommendation 5: Monitor sign-in activity

Review available sign-in logs for suspicious activity and investigate unexpected MFA requests, unfamiliar sign-ins, and unusual authentication-method changes. Use the available logging and risk-detection capabilities supported by the organization's licensing.

## 9. Implementation and Validation Plan

The following steps are recommended before rolling out the proposed controls:

1. Verify the existing Security Defaults configuration and review authentication-method policies.
2. Confirm that employees have registered appropriate authentication methods.
3. Establish secure account recovery and emergency access procedures.
4. In a properly licensed environment, evaluate Conditional Access policies in report-only mode and review their expected effects.
5. Test policy scope, exclusions, sign-in behavior, and recovery procedures using appropriate test accounts.
6. Address unexpected results before enabling policies for the organization.
7. Monitor sign-in activity and review the effectiveness of the controls after implementation.

Report-only mode applies to Conditional Access policies. Otherr procedures, such as account recovery, require their own controlled tests.

## 10. Success Criteria

Southstars Retail can evaluate the effectiveness of its improvements using the following measures:

- **Sign-in monitoring:** Review suspicious sign-in activity, MFA-related events, and unauthorized access indicators over time. Investigate changes rather than assuming a reduction in alerts automatically proves that MFA is effective.
- **Account recovery validation:** Measure the percentage of controlled recovery tests completed successfully and verify that identity checks and security procedures are followed.
- **Policy validation:** In a properly licensed environment, confirm that proposed policies apply to intended users and resources without creating unintended access disruptions.
- **Privileged account protection:** Verify that administrative accounts use the intended authentication methods and that emergency access procedures remain functional.

## 11. Project Limitations

- The project used Microsoft Entra ID Free.
- Conditional Access policies were designed and documented but not deployed.
- Authentication-method policies were reviewed, but individual registration and successful use were not comprehensively tested.
- Sign-in troubleshooting scenarios were analyzed as exercises rather than as a live security incident.

## 12. Skills Demonstrated

- Microsoft Entra ID administration and configuration review
- Identity and Access Management (IAM) fundamentals
- Multifactor authentication and phishing-resistant authentication concepts
- Conditional Access policy design
- Privileged account protection
- Sign-in log investigation concepts
- Account recovery and incident-response procedures
- Security control evaluation and implementation planning
- Technical documentation and security recommendations

## Conclusion

This project developed a proposed authentication and access management approach for Southstars Retail. It combined authentication-method evaluation, administrator and employee MFA policy design, sign-in troubleshooting, and secure account recovery recommendations.

The work demonstrates an understanding of how IAM controls can reduce account security risks while accounting for licensing constraints, policy testing, and operational recovery requirements.
