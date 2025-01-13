# Top 2025 vulnerabilities you shouldn’t accept in a pentest report [DRAFT]

_We’re finalizing this list and will improve each point with detailed descriptions to ensure clarity and avoid confusion. Feel free to open an Issue, and we’ll do our best to address it._ 

## About This List
As pentesters and security professionals, we often encounter reports filled with issues that are either not vulnerabilities or don’t pose real security risks. This list aims to highlight commonly misreported issues and explain why they don’t qualify as valid vulnerabilities. By understanding these, we can focus on real threats and save time for both testers and clients.

This is a community-driven list, and we encourage contributions! If you’ve come across similar misunderstood or misreported issues, feel free to submit a pull request to add them here. Together, we can build a comprehensive resource for the security community.


### Minor Infrastructure Information Exposure

The exposure of framework names, libraries, or other small details used in an application is generally low-risk unless paired with other vulnerabilities. Such minor leaks are common in areas like error pages, `robots.txt`, response headers, or different error codes.

While these leaks may reveal some information, their **real impact depends on context**. For example:  
- If vulnerable third-party components are revealed, the issue lies in the use of outdated or insecure dependencies—not in the leak itself.  
- Reporting such vulnerabilities should focus on **proven exploitability** rather than simply flagging their presence.
- Pages showing framework names (like "Powered by Django") or small details aren’t a big risk unless they’re combined with other issues.

> When assessing these leaks, ensure the **impact and CVSS score reflect actual risks**, not assumptions. Overreporting minor issues dilutes the value of pentest findings (see the "Reporting Unexploitable Vulnerabilities" section for guidance).


### Reporting Unexploitable Vulnerabilities

Some vulnerability reports are based on observed protection mechanisms or assumptions rather than real exploitation scenarios. In such cases, the vulnerability might already be mitigated by other protection methods or require an unrealistic workflow to exploit.

For instance, **CSRF vulnerabilities** can be mitigated through mechanisms like:
- Authorization headers,  
- Origin header validation,  
- SameSite cookie flags,  
- Properly implemented CSRF tokens on API endpoints, or  
- Requiring data that attackers can’t obtain (e.g., an old password field in a password reset form).

The absence of one mechanism doesn’t automatically mean the CSRF is exploitable. Such findings should be reported as **informational vulnerabilities** with a CVSS score of 0 (if they are in scope), unless exploitability can be clearly demonstrated.

> **Note:** Don’t dismiss a vulnerability outright based on the presence of a protection mechanism. It may be incorrectly implemented or bypassable. Always assess actual exploitability based on detailed reports.

Additionally, the **lack of protection mechanisms** or other informational-level vulnerabilities with a CVSS score of 0 should generally be accepted. While they might not represent immediate risks or require fixes, they could expose potential gaps.

By focusing on proven exploitability and encouraging a layered approach to security, we ensure reports are meaningful while maintaining a roadmap for continuous improvement.

### Problems Without Security-Related Impact

Vulnerabilities should be evaluated based on their **impact on the system**, not just their exploitation mechanisms. Some issues might seem concerning but have no real-world security implications. For instance, exposed data that is already public or forms that don’t require protection against automation often don’t pose a significant risk.

#### Examples of issues with no real impact:

- **Missing protection flags for trivial preference cookies**: These cookies (e.g., `theme=dark`) don’t carry sensitive information and don’t need `HttpOnly` or `Secure` flags.
- **IDOR vulnerabilities that only allow enumeration of public profiles**: Public data, by definition, doesn’t require strict access controls.
- **Abuse of post-auth critical forms**: Forms like profile updates and other critical forms **do not typically require CAPTCHAs**, as authenticated sessions already validate the user. Instead, protections like CSRF tokens, proper session management, rate limiting, and authorization controls should be implemented. These measures prevent abuse, such as automated attacks or unauthorized changes, without disrupting user experience.
- **Autocomplete enabled on non-sensitive fields**: Autocomplete on forms like names or addresses is often a usability feature, not a security vulnerability.
- **Race conditions in non-critical form updates**: Race conditions in things like UI preferences or theme changes don’t impact security. These are usability bugs, not vulnerabilities.
- **Missing rate limits on non-sensitive APIs**: Public APIs like product searches don’t handle sensitive data. Missing rate limits here doesn’t pose a real security risk unless it leads to denial of service.
- **Clickjacking vulnerabilities on pre-authentication pages**: Clickjacking on login or newsletter sign-up pages isn’t relevant if there are no sensitive actions happening before authentication.
- **Exposed API 3rd keys for public services**: Services like Google Maps or Sentry.io require public API keys to function, as these keys serve as "identity" keys rather than authentication keys. Unless they are misconfigured with sensitive permissions, their exposure does not constitute a vulnerability.
- **Suggesting expiration for JWT tokens**: JWT tokens are designed to be stateless, with expiration managed as part of their structure. Asking for token revocation without understanding this design doesn’t make sense.
- **Flagging session timeout durations as too long**: Longer session durations are often intentional, especially in enterprise workflows where usability is a priority. However, pentesters should not assume this is always a design decision. If the timeout is due to a bad default value or poor implementation, it could increase risk. Rather than excluding this entirely, pentesters should provide context in their reports, allowing customers to assess and accept the risk based on their specific needs and environment.
- **Reporting access to Client UI for features without functionality**: Accessing the Client UI for features like admin or high-privilege functionalities without the ability to perform any operations is not a security vulnerability. This often occurs when the frontend renders the UI based on static assets but lacks server-side validation or backend interaction. Unless this leads to sensitive information disclosure or unauthorized actions, it should not be reported as a valid vulnerability. The focus should always be on exploitable backend operations rather than mere UI exposure.
- **Reporting the absence of the `X-XSS-Protection` header**: This header is outdated, as modern browsers no longer support it. A good Content Security Policy (CSP) is more effective.


### Disclaimers and Limitations

1. Findings depend on the application’s environment and use case. Assess each issue based on its unique context.  
2. Minor issues might still matter for compliance or specific business needs (e.g., GDPR, HIPAA).  
3. Use the list as a guide, not a substitute for thorough analysis or validation.  
4. Even trivial findings may support a broader layered security strategy.  
5. CVSS scores are situational; adjust based on specific risks and impact.  
6. Low-risk issues can highlight areas for improvement and should be communicated constructively.  
7. The list is community-driven and should evolve to stay relevant.  



## Credits
Contributors who helped refine and improve this document 

- [vladko312](https://github.com/vladko312)


