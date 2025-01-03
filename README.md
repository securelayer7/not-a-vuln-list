# Top 2025 vulnerabilities you shouldn’t accept in a pentest report

## About This List
As pentesters and security professionals, we often encounter reports filled with issues that are either not vulnerabilities or don’t pose real security risks. This list aims to highlight commonly misreported issues and explain why they don’t qualify as valid vulnerabilities. By understanding these, we can focus on real threats and save time for both testers and clients.

This is a community-driven list, and we encourage contributions! If you’ve come across similar misunderstood or misreported issues, feel free to submit a pull request to add them here. Together, we can build a comprehensive resource for the security community.

### Suggesting expiration for JWT tokens:
JWT tokens are designed to be stateless, with expiration managed as part of their structure. Asking for token revocation without understanding this design doesn’t make sense.

### Reporting race conditions in non-critical updates:
Race conditions in things like UI preferences or theme changes don’t impact security. These are usability bugs, not vulnerabilities.

### Flagging session timeout durations as too long:
Some applications need longer sessions for business reasons, like enterprise workflows. This isn’t a vulnerability; it’s a design decision.

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

### Reporting CSRF on forms validated by Referer headers:
If a server relies solely on the Referer header for CSRF protection, it’s a questionable approach. Referer can be stripped or modified by browsers or proxies, making it unreliable. Using the Origin header for validation is a better practice, as it’s more robust and specifically intended for this purpose. Misinterpreting this could lead to overlooking real vulnerabilities.

### Reporting DNS rebinding attacks mitigated by IP range validation:
DNS rebinding isn’t an issue if the app blocks private/internal IP ranges through validation.

### Reporting open redirect vulnerabilities mitigated by state parameter:
OAuth flows with a state parameter protect against misuse. Reporting open redirects in this case is misleading.

### Reporting session hijacking mitigated by short lifetimes:
Short session durations and refresh tokens minimize the impact of stolen sessions, making exploitation impractical.

### Reporting sensitive data modification risks for users with read-only permissions:
Read-only roles can’t modify data, so reporting risks here without privilege escalation is unnecessary.

### Reporting the absence of the `X-XSS-Protection` header:
This header is outdated, as modern browsers no longer support it. A good Content Security Policy (CSP) is more effective.

### Flagging HTTP headers exposing minor metadata:
Headers like app version or build number don’t pose a risk unless there’s a related vulnerability to exploit.

### Highlighting predictable user IDs for public profiles:
Sequential user IDs for public profiles aren’t a security issue if no sensitive data is exposed.
