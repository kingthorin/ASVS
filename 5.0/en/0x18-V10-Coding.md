# V10 Secure Coding Architecture and Implementation

## Control Objective

Many ASVS requirements either relate to a particular area of security like authentication or access control or relate to a particular type of application functionality such as logging or file handling.

However, this chapter provides more general guidance on how to build applications and how to write secure code correctly. Not just from the perspective of clean architecture and code quality, but rather specific architecture and coding practices that need to be followed in order for the application to be secure.

This chapter also contains requirements to prevent the introduction of malicious code into the application.

## V1.10 Secure Coding Documentation

Many of the requirements needed for a secure and defendable architecture require having clear documentation around what components are used in the application. This section provides the requirements for this documentation including which of these components are risky due to being poorly maintained, unsupported, end of life, or with a history of significant vulnerabilities and which components perform risky operations such as deserialization of untrusted data, raw file parsing or direct memory manipulation. It also includes mandates defining appropriate timescales for addressing vulnerabilities in 3rd party components.

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **1.10.1** | [DELETED, NOT IN SCOPE] | | |
| **1.10.2** | [MODIFIED, MOVED FROM 14.2.5, MERGED FROM 14.2.4, COVERS 12.3.6] Verify that an inventory catalog, such as software bill of materials (SBOM), is maintained of all third-party libraries in use, including verifying that components come from pre-defined, trusted, and continually maintained repositories. | 2 | |
| **1.10.3** | [ADDED, SPLIT FROM 14.2.6] Verify that application documentation highlights "risky" third party libraries which should include: libraries which perform operations which are dangerous from a security perspective, libraries which are poorly maintained, unsupported, or end of life and libraries which have historically had several significant vulnerabilities. | 3 | 1061 |
| **1.10.4** | [ADDED, SPLIT FROM 1.14.5] Verify that application documentation highlights parts of the application where "risky" operations are being performed. "Risky" in this context means those with a high likelihood of being dangerously exploited such as: deserialization of untrusted data, raw file parsing or direct memory manipulation. | 3 | |
| **1.10.5** | [ADDED, SPLIT FROM 14.2.1, COVERS 1.14.3] Verify that application documentation defines risk based remediation time frames for 3rd party component versions with vulnerabilities and for updating libraries in general, to minimize the risk from these components. | 1 | |

## V10.1 Code Integrity

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **10.1.1** | [DELETED, NOT IN SCOPE] | | |

## V10.2 Malicious Code Search

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **10.2.1** | [DELETED, NOT PRACTICAL] | | |
| **10.2.2** | [DELETED, NOT PRACTICAL] | | |
| **10.2.3** | [DELETED, NOT PRACTICAL] | | |
| **10.2.4** | [DELETED, NOT PRACTICAL] | | |
| **10.2.5** | [DELETED, NOT PRACTICAL] | | |
| **10.2.6** | [DELETED, NOT PRACTICAL] | | |

## V10.3 Application Integrity

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **10.3.1** | [MOVED TO 10.4.10] | | |
| **10.3.2** | [MOVED TO 10.6.2] | | |
| **10.3.3** | [DELETED, NOT IN SCOPE] | | |

## V10.4 Defensive Coding

This section covers vulnerability types including type juggling, prototype pollution, mass assignment, and others which result from the use of insecure coding patterns in a particular language. Some may not be relevant to all languages whereas others will have language specific fixes or may relate to the way that a particular language or framework handles a feature such as HTTP parameters. It also considers the risk of not cryptographically validating application updates.

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **10.4.1** | [ADDED] Verify that the application explicitly ensures that variables are of the correct type and performs strict equality and comparator operations to avoid type juggling or type confusion vulnerabilities caused by the application code making an assumption about a variable type. | 1 | 843 |
| **10.4.2** | [ADDED] Verify that the application avoids DOM clobbering when using client-side JavaScript by employing explicit variable declarations, performing strict type checking, avoiding storing global variables on the document object, and implementing namespace isolation. | 2 | 79 |
| **10.4.3** | [ADDED] Verify that JavaScript code is written in a way that prevents prototype pollution, for example, by using Set() or Map() instead of object literals. | 2 | |
| **10.4.4** | [MODIFIED, MOVED FROM 5.1.2] Verify that the application has countermeasures to protect against mass assignment attacks by limiting allowed fields per controller and action, e.g., it is not possible to insert or update a field value when it was not intended to be part of that action. | 1 | 915 |
| **10.4.5** | [ADDED] Verify that the application only returns data which the user has permission to access. For example, the API response does not return a full object with attributes that contain values the user has no permission to access, despite having permission to access the data object itself. | 1 | |
| **10.4.6** | [ADDED] Verify that the application is able to discern and utilizes the user's true IP address to provide for sensitive functions, including rate limiting and logging. | 2 | 348 |
| **10.4.7** | [MODIFIED, MOVED FROM 5.1.1, LEVEL L1 > L2] Verify that the application has defenses against HTTP parameter pollution attacks, particularly if the application framework makes no distinction about the source of request parameters (query string, body parameters, cookies, or header fields). | 2 | 235 |
| **10.4.8** | [ADDED] Verify that where the application back-end makes calls to external URLs, it is configured to not follow redirects unless it is intended functionality. | 2 | |
| **10.4.9** | [ADDED] Verify that, if the application (back-end or front-end) builds and sends requests, it uses validation, sanitization, or other mechanisms to avoid creating URIs (such as for API calls) or HTTP request header fields (such as Authorization or Cookie), which are too long to be accepted by the receiving component. This could cause a denial of service, such as when sending an overly long request (e.g. a long cookie header field) results in the server always responding with an error status. | 2 | |
| **10.4.10** | [MODIFIED, MOVED FROM 10.3.1, LEVEL L1 > L3] Verify that, if the application has an auto-update feature, updates should be digitally signed, with the digital signature being validated before installing or executing the update. | 3 | 16 |

## V10.5 Security Architecture

## V10.6 Security Architecture and Dependencies

This section includes requirements for handling risky, outdated or insecure dependencies and components through dependency management and using architectural level techniques such as sandboxing, encapsulation, containerization, and network isolation.

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **10.6.1** | [ADDED, SPLIT FROM 14.2.1, COVERS 1.14.3] Verify that the application only contains components which have not breached the documented update and remediation time frames. | 1 | |
| **10.6.2** | [MODIFIED, MOVED FROM 10.3.2] Verify that third-party components and all of their transitive dependencies are included from the expected repository, whether internally owned or an external source, and that there is no risk of a dependency confusion attack. | 1 | 427 |
| **10.6.3** | [ADDED, SPLIT FROM 1.14.5, 14.2.6] Verify that the application implements additional protections around parts of the application which are documented as performing "risky" operations or using "risky" third-party libraries. This could include techniques such as sandboxing, encapsulation, containerization or network level isolation to delay and deter attackers who compromise one part of an application from pivoting elsewhere in the application. | 3 | |

## V10.7 Concurrency

Concurrency issues such as race conditions, TOC/TOU vulnerabilities, deadlocks, livelocks, thread starvation, and improper synchronization can lead to unpredictable behavior and security risks. This section includes various techniques and strategies to help mitigate these risks.

| # | Description | Level | CWE |
| :---: | :--- | :---: | :---: |
| **10.7.1** | [MODIFIED, MOVED FROM 1.11.3] Verify that only thread-safe types are used in multi-threaded contexts, or that non-thread-safe types are properly synchronized to prevent race conditions. | 3 | 362 |
| **10.7.2** | [MODIFIED, MOVED FROM 1.11.2, LEVEL L2 > L3] Verify that concurrent access to shared resources is controlled using synchronization primitives (e.g., locks, mutexes, semaphores) to prevent race conditions and ensure atomic operations on these resources. | 3 | 366 |
| **10.7.3** | [MODIFIED, MOVED FROM 11.1.6] Verify that all access to shared resources is consistently checked and accessed in a single atomic operation to prevent Time-of-Check to Time-of-Use (TOCTOU) race conditions, ensuring resource state consistency between check and use. | 2 | 367 |
| **10.7.4** | [ADDED] Verify that resource acquisition uses a consistent locking strategy to avoid circular dependencies and ensure forward progress, preventing both deadlocks and livelock scenarios. | 3 | 833 |
| **10.7.5** | [ADDED] Verify that resource allocation policies prevent thread starvation by ensuring fair access to resources, such as by leveraging thread pools, allowing lower-priority threads to proceed within a reasonable timeframe. | 3 | 410 |
| **10.7.6** | [ADDED] Verify that locking primitives are only accessible to the owning class or module and are not publicly modifiable, ensuring that locks cannot be inadvertently or maliciously modified by external classes or code. | 3 | 412 |

## References

For more information, see also:

* [Reference on Protecting against DOM Clobbering](https://domclob.xyz/domc_wiki/indicators/patterns.html#secure-patterns--guidelines)
* [OWASP Prototype Pollution Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Prototype_Pollution_Prevention_Cheat_Sheet.html)
* [OWASP Mass Assignment Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html)
* [Software Component Verification Standard V2 L1-3 requirements](https://github.com/OWASP/Software-Component-Verification-Standard/blob/master/en/0x11-V2-Software_Bill_of_Materials.md)
