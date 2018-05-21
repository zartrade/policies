# 9. Configuration Management Policy

## 9.1 Applicable Standards

### 9.1.1 Applicable Standards from the HITRUST Common Security Framework

* 06 - Configuration Management

### 9.1.2 Applicable Standards from the HIPAA Security Rule

* 164.310(a)(2)(iii) Access Control & Validation Procedures

## 9.2 Configuration Management Policies

1. No systems are deployed into Shape Software environments without approval of the Shape Software CTO.
2. All changes to production systems, network devices, and firewalls are approved by the Shape Software CTO before they are implemented to assure they comply with business and security requirements.
3. All changes to production systems are tested before they are implemented in production.
4. Implementation of approved changes are only performed by authorized personnel.
5. All frontend functionality (developer dashboards and portals) is separated from backend (database and app servers) systems by being deployed on separate servers or containers.
6. All software and systems are tested using unit tests and end to end tests.
7. All committed code is reviewed using pull requests to assure software code quality and proactively detect potential security issues in development.
8. Shape Software utilizes development and staging environments that mirror production to assure proper function.
9. All formal change requests require unique ID and authentication.
10. Shape Software uses the [Security Technical Implementation Guides (STIGs)](http://iase.disa.mil/stigs/) published by the Defense Information Systems Agency as a baseline for hardening systems.
    * Windows-based systems use a baseline Active Directory group policy configuration in conjunction with the Windows Server 2012 STIG.
    * Linux-based systems use a Red Hat Enterprise Linux STIG which has been adapted for Ubuntu and improved based on the results of subsequent vulnerability scans and risk assessments.
11. Clocks are continuously synchronized to an authoritative source across all systems using NTP or a platform-specific equivalent. Modifying time data on systems is restricted.

## 9.3 Provisioning Production Systems

1. Before provisioning any systems, ops team members must file a request in the Shape Software Quality Management System.
   * Quality Management System access requires authenticated users.
   * The CTO grants access to the Quality Management System following the procedures covered in the [Access Establishment and Modification section](#7.2-access-establishment-and-modification).
2. The CTO, or an authorized delegate of the CTO, must approve the provisioning request before any new system can be provisioned.
3. Once the system has been provisioned, the ops team member must contact the security team to inspect the new system. A member of the security team will verify that the secure baseline has been applied to the new system, including (but not limited to) verifying the following items:
   * Removal of default users used during provisioning.
   * Network configuration for system.
   * Data volume encryption settings.
   * Intrusion detection and virus scanning software installed.
   * All items listed below in the operating system-specific subsections below.
4. The new system may be rotated into production once the CTO verifies all the provisioning steps listed above have been correctly followed and has marked the Issue with the `Approved` state.

### 9.3.1 Provisioning Linux Systems

1. Linux systems have their baseline security configuration applied via Salt states. These baseline Salt states cover:
   * Ensuring that the machine is up-to-date with security patches and is configured to apply patches in accordance with our policies.
   * Stopping and disabling any unnecessary OS services.
   * Installing and configuring the OSSEC IDS agent.
   * Configuring 15-minute session inactivity timeouts.
   * Installing and configuring the ClamAV virus scanner.
   * Installing and configuring the NTP daemon, including ensuring that modifying system time cannot be performed by unprivileged users.
   * Configuring LUKS volumes for providers that do not have native support for encrypted data volumes, including ensuring that encryption keys are protected from unauthorized access.
   * Configuring authentication to the centralized LDAP servers.
   * Configuring audit logging as described in the [Auditing Policy section](#8.-auditing-policy).
2. Any additional Salt states applied to the Linux system must be clearly documented by the ops team member in the DT request by specifying the purpose of the new system.

## 9.4 Software Development Procedures

1. All development uses feature branches based on the main branch used for the current release. Any changes required for a new feature or defect fix are committed to that feature branch.
   * These changes must be covered under 1) a unit test where possible, or 2) integration tests.
   * Integration tests are _required_ if unit tests cannot reliably exercise all facets of the change.
2. Developers are strongly encouraged to follow the [commit message conventions suggested by GitHub](https://github.com/blog/926-shiny-new-commit-styles).
   * Commit messages should be wrapped to 72 characters.
   * Commit messages should be written in the present tense. This convention matches up with commit messages generated by commands like git merge and git revert.
3. Once the feature and corresponding tests are complete, a pull request will be created using the GitHub/GitLab web interface. The pull request should indicate which feature or defect is being addressed and should provide a high-level description of the changes made.
4. Code reviews are performed as part of the pull request procedure. Once a change is ready for review, the author(s) will notify other engineers using an appropriate mechanism, typically via an `@channel` message in Slack.
   * Other engineers will review the changes, using the guidelines above.
   * Engineers should note all potential issues with the code; it is the responsibility of the author(s) to address those issues or explain why they are not applicable.
5. If the feature or defect interacts with ePHI, or controls access to data potentially containing ePHI, the code changes must be reviewed by two members of Shape Software's Blue Team (software security team) before the feature is marked as complete.
   * The Blue Team members will provide a security analysis of features to ensure they satisfy Shape Software's compliance and security commitments.
   * This review must include a security analysis for potential vulnerabilities such as those listed in the [OWASP Top 10](https://www.owasp.org/index.php/Top10) or the [CWE top 25](http://cwe.mitre.org/top25/).
   * This review must also verify that any actions performed by authenticated users will generate appropriate audit log entries.
   * Blue Team members are required to undergo annual training on identifying the most common software vulnerabilities and will receive ongoing training on Shape Software's compliance and security requirements.
6. Once the review process finishes, each reviewer should leave a comment on the pull request saying "looks good to me" (often abbreviated as "LGTM"), at which point the original author(s) may merge their change into the release branch.

## 9.7 Software Release Procedures

1. Software releases are treated as changes to existing systems and thus follow the procedure described in [§9.4](#9.4-changing-existing-systems).

