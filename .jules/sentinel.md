## 2024-05-23 - CSP Implementation in Meta Tags
**Vulnerability:** N/A (Implementation Constraint)
**Learning:** The `frame-ancestors` directive is not supported in CSP `<meta>` tags and will cause browser console errors if included. It is only valid when sent via HTTP headers.
**Prevention:** When implementing CSP via meta tags for static sites, exclude `frame-ancestors` and focus on `script-src`, `style-src`, etc.

## 2026-03-03 - Clickjacking Protection for Static Sites
**Vulnerability:** Clickjacking risk when X-Frame-Options or CSP frame-ancestors headers are unavailable.
**Learning:** Static sites relying on meta tags for CSP cannot use frame-ancestors. Frame-busting JavaScript must be implemented instead to prevent UI redress attacks.
**Prevention:** Always implement frame-busting JS in the main script for statically hosted applications that lack server-level header configuration.

## 2026-03-03 - Execution Continuation in Frame-Busting Scripts
**Vulnerability:** Clickjacking frame-busting logic does not halt execution (DOM clears but script continues).
**Learning:** Frame-busting logic placed inside an IIFE (Immediately Invoked Function Expression) requires explicit halting to prevent the remainder of the script from executing after the clickjacking attempt is detected. However, a global `return;` is illegal in unbundled scripts and causes a `SyntaxError`.
**Prevention:** Always use `throw new Error()` inside clickjacking defense blocks to safely halt script execution and prevent unintended code from running while framed.

## 2024-05-28 - Image Load Denial of Service (Client-side)
**Vulnerability:** Game initialization loop halts forever if an image resource fails to load (e.g. 404).
**Learning:** Client-side initialization loops depending on asynchronous resource loading must handle failure states. A missing `onerror` handler means the counter is never decremented, causing an infinite loading state (DoS).
**Prevention:** Always implement `onerror` handlers on `Image` objects in game initialization loops to gracefully handle resource failures and prevent infinite hangs.
