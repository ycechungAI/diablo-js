## 2024-05-23 - CSP Implementation in Meta Tags
**Vulnerability:** N/A (Implementation Constraint)
**Learning:** The `frame-ancestors` directive is not supported in CSP `<meta>` tags and will cause browser console errors if included. It is only valid when sent via HTTP headers.
**Prevention:** When implementing CSP via meta tags for static sites, exclude `frame-ancestors` and focus on `script-src`, `style-src`, etc.

## 2026-03-03 - Clickjacking Protection for Static Sites
**Vulnerability:** Clickjacking risk when X-Frame-Options or CSP frame-ancestors headers are unavailable.
**Learning:** Static sites relying on meta tags for CSP cannot use frame-ancestors. Frame-busting JavaScript must be implemented instead to prevent UI redress attacks.
**Prevention:** Always implement frame-busting JS in the main script for statically hosted applications that lack server-level header configuration.

## 2026-03-03 - Incomplete Clickjacking Protection Script Halting
**Vulnerability:** Game logic execution after clickjacking detection.
**Learning:** Modifying the DOM (e.g. `document.body.innerHTML`) during frame-busting does not inherently stop the execution of the current script. If not explicitly halted, the script will continue running, potentially executing sensitive logic or causing unexpected errors.
**Prevention:** Always use an early `return;` (if inside an IIFE/function block) or throw an exception to halt script execution immediately when framing is detected and mitigated.
