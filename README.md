# Top 2025 vulnerabilities you shouldn’t accept in a pentest report [DRAFT]

_We’re finalizing this list and will improve each point with detailed descriptions to ensure clarity and avoid confusion._

## About This List
As pentesters and security professionals, we often encounter reports filled with issues that are either not vulnerabilities or don’t pose real security risks. This list aims to highlight commonly misreported issues and explain why they don’t qualify as valid vulnerabilities. By understanding these, we can focus on real threats and save time for both testers and clients.

This is a community-driven list, and we encourage contributions! If you’ve come across similar misunderstood or misreported issues, feel free to submit a pull request to add them here. Together, we can build a comprehensive resource for the security community.

### Suggesting expiration for JWT tokens:
JWT tokens are designed to be stateless, with expiration managed as part of their structure. Asking for token revocation without understanding this design doesn’t make sense.

### Reporting race conditions in non-critical updates:
Race conditions in things like UI preferences or theme changes don’t impact security. These are usability bugs, not vulnerabilities.

### Flagging session timeout durations as too long:
Longer session durations are often intentional, especially in enterprise workflows where usability is a priority. However, pentesters should not assume this is always a design decision. If the timeout is due to a bad default value or poor implementation, it could increase risk.

Rather than excluding this entirely, pentesters should provide context in their reports, allowing customers to assess and accept the risk based on their specific needs and environment.
### Flagging static error pages revealing minor details:
Pages showing framework names (like "Powered by Django") or small details aren’t a big risk unless they’re combined with other issues.

### Identifying missing rate limits on non-sensitive APIs:
Public APIs like product searches don’t handle sensitive data. Missing rate limits here doesn’t pose a real security risk unless it leads to denial of service.

### Reporting non-secure cookies for trivial data:
Cookies storing non-sensitive preferences (e.g., theme=dark) don’t need extra flags like `HttpOnly` or `Secure`. Reporting this is unnecessary.

### Highlighting the lack of CAPTCHA on non-sensitive forms:
Missing CAPTCHA on simple forms like newsletter signups or feedback forms isn’t a security issue; it’s more about spam prevention.

### Reporting clickjacking vulnerabilities on pre-authentication pages:
Clickjacking on login or sign-up pages isn’t relevant if there are no sensitive actions happening before authentication.

### Reporting CSRF vulnerabilities on endpoints protected by API tokens:
CSRF can’t work when API requests require tokens that an attacker can’t forge. Reporting this shows a lack of understanding.

### Reporting lack of rate limiting on admin functionalities:
Admin features like email-sending tools are usually restricted to trusted users. Rate limiting here is less critical.

### Reporting CSRF vulnerabilities where `SameSite=None` is used:
`SameSite=None` isn’t a problem if the app already uses proper token-based CSRF protection.

### Reporting CSRF on APIs protected by Authorization headers:
APIs that require Authorization headers are safe from CSRF because those headers can’t be sent cross-origin.

### Reporting CSRF on forms validated by Orgin headers:
If a server relies solely on the Referer header for CSRF protection, it’s a questionable approach. Referer can be stripped or modified by browsers or proxies, making it unreliable. Using the Origin header for validation is a better practice, as it’s more robust and specifically intended for this purpose. Misinterpreting this could lead to overlooking real vulnerabilities.

### Reporting session hijacking mitigated by short lifetimes:
Short session durations and refresh tokens can reduce the window of opportunity for exploitation but don’t inherently prevent session hijacking. If an attacker can automate exploitation immediately, even short-lived sessions can be compromised. Mitigation should focus on securing session tokens with mechanisms like HTTPS, HttpOnly cookies, and additional validation checks, rather than relying solely on short lifetimes.

### Reporting sensitive data modification risks for users with read-only permissions:
Read-only roles can’t modify data, so reporting risks here without privilege escalation is unnecessary.

### Reporting the absence of the `X-XSS-Protection` header:
This header is outdated, as modern browsers no longer support it. A good Content Security Policy (CSP) is more effective.

### Flagging HTTP headers exposing minor metadata:
Headers like app version or build number don’t pose a risk unless there’s a related vulnerability to exploit.

### Highlighting predictable user IDs for public profiles:
Sequential user IDs for public profiles aren’t a security issue if no sensitive data is exposed.

### Reporting exposed API keys for public services:
Services like Google Maps or Sentry.io require public API keys to function, as these keys serve as "identity" keys rather than authentication keys. Unless they are misconfigured with sensitive permissions, their exposure does not constitute a vulnerability.
