## 2024-05-23 - CSP Implementation in Meta Tags
**Vulnerability:** N/A (Implementation Constraint)
**Learning:** The `frame-ancestors` directive is not supported in CSP `<meta>` tags and will cause browser console errors if included. It is only valid when sent via HTTP headers.
**Prevention:** When implementing CSP via meta tags for static sites, exclude `frame-ancestors` and focus on `script-src`, `style-src`, etc.
