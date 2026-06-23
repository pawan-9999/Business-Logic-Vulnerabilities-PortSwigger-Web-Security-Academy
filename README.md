# Business-Logic-Vulnerabilities-PortSwigger-Web-Security-Academy
This repository contains write-ups for Business Logic Vulnerability labs completed on PortSwigger Web Security Academy. These labs demonstrate how attackers can exploit flaws in application workflows and business processes rather than traditional technical vulnerabilities such as SQL Injection or Cross-Site Scripting.
The focus of these labs is understanding how insecure assumptions, inconsistent validation, and improper trust in user-controlled data can lead to privilege escalation, unauthorized actions, and financial impact.

#Lab 1: Excessive Trust in Client-Side Controls
Objective

Purchase a product that exceeds the available store credit by manipulating client-side controls.

Vulnerability

The application relied on client-side validation to enforce product pricing and purchasing restrictions. Sensitive values sent by the client were trusted without adequate server-side verification.

Methodology
Added a product to the shopping cart.
Intercepted the request using Burp Suite.
Identified user-controlled parameters related to product pricing.
Modified the parameter values before forwarding the request.
Observed that the server accepted the manipulated values.
Reduced the effective purchase price and completed the transaction using available store credit.
Impact

An attacker could manipulate pricing information and purchase products at unauthorized prices, resulting in financial loss and compromised business integrity.

Key Takeaways
Never trust client-side controls for security decisions.
Pricing and authorization checks must always be validated on the server.
User-supplied values should be treated as untrusted input.
Lab 2: High-Level Logic Vulnerability
Objective

Exploit flaws in the application's purchasing workflow to acquire an expensive item without sufficient credit.

Vulnerability

The application failed to properly validate cart quantities, allowing negative values to be submitted. This introduced a business logic flaw that could be abused to manipulate the final purchase total.

Methodology
Added a low-cost item to the shopping cart.
Intercepted the cart update request.
Modified the quantity parameter to a negative value.
Forced the application to calculate a negative cart balance.
Added the target product to the cart.
Offset the product price using the manipulated negative balance.
Completed the purchase within the available store credit limit.
Impact

An attacker could exploit flawed business rules to purchase products at significantly reduced prices or potentially obtain items without proper payment.

Key Takeaways
Input validation must include business rule validation.
Negative quantities and edge-case values should be properly handled.
Security testing should include workflow and transaction analysis.
Lab 3: Inconsistent Security Controls
Objective

Gain access to an administrative interface by exploiting inconsistent validation mechanisms.

Vulnerability

The application enforced email-domain restrictions during registration but failed to apply the same validation when users updated their email addresses after account creation.

Methodology
Discovered the restricted administrative functionality.
Registered a standard user account using an approved email address.
Verified the account through the email confirmation process.
Navigated to the account management functionality.
Changed the registered email address to a trusted corporate domain.
Obtained elevated privileges due to inconsistent security validation.
Accessed the administrative interface and completed the lab objective.
Impact

An attacker could escalate privileges and gain unauthorized administrative access by exploiting differences in validation logic across application workflows.

Key Takeaways
Security controls must be applied consistently across all workflows.
Identity and privilege validation should be centralized.
Access control decisions should not rely solely on mutable user attributes.
Skills Practiced
Business Logic Testing
Access Control Assessment
Privilege Escalation Analysis
HTTP Request Manipulation
Burp Suite Repeater
Web Application Security Testing
Input Validation Testing
Workflow Analysis
Tools Used
Burp Suite Community Edition
PortSwigger Web Security Academy
Firefox Browser
HTTP Proxy Interception
Conclusion

These labs highlight that not all security vulnerabilities stem from coding errors or technical flaws. Weak business processes, inconsistent validation, and incorrect trust assumptions can introduce equally severe security risks. Understanding application logic and testing workflows from an attacker's perspective is essential for identifying these vulnerabilities during security assessments.
