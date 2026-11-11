| Finding | Evidence | Verdict | Action / Fix (in a real app) |
|---|---|---|---|
| CSP Header Not Set [10038] | /, /ftp, /sitemap.xml missing a Content-Security-Policy header | True Positive | Add a CSP via helmet.contentSecurityPolicy() then restricting ssources to the app's own origin. |

| Storable and Cacheable Content [10049] | robots.txt, static JS chunks, and the root page are all served as cacheable | Partial False Positive | Static assets being cacheable is normal. All flagged URLs here are public static assets or public routes. |

| Deprecated Feature-Policy Header Set [10063] | Feature-Policy header present on root page and JS assets | True Positive | Feature-Policy was replaced by Permissions-Policy. Remove the old header and add Permissions-Policy instead, scoping the specific browser features the app needs to disallow. |

| Cross-Domain Misconfiguration [10098] | CORS-related finding on root, JS, sitemap, CSS | True Positive | Restrict CORS to an explicit allowlist of trusted origins, and never combine Access-Control-Allow-Origin: * with Access-Control-Allow-Credentials: true. |

| Modern Web Application [10109] | Detected on root and two fileServer.js lines | False Positive | ZAP noting the app is a modern SPA, it is not an actual vulnerability. Informational only. |

| Dangerous JS Functions [10110] | chunk-3CyVWL1v.js, main.js | True Positive | ZAP flags usage of functions like eval() or innerHTML in the bundled JS. Replace dynamic eval/innerHTML patterns with safer alternatives. |

| Cross-Origin-Embedder-Policy Header Missing or Invalid [90004] | Present on nearly every URL 10x | True Positive | Add a Cross-Origin-Embedder-Policy: require-corp header to enable full process isolation protections in modern browsers. |

Summary: 0 FAIL-NEW, 7 WARN-NEW, 61 PASS. 5 true positives (CSP, Feature-Policy, Cross-Domain Misconfiguration, Dangerous JS Functions, COEP), 2 false positive/informational (Storable and Cacheable Content, Modern Web Application).