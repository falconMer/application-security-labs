# Application Security Labs

Secure coding and web-application security labs covering authentication, authorization, session security, memory safety, injection, XSS, and CSRF.

> **Academic context:** Completed as part of Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026). This repository is intended as a technical portfolio of controlled university lab work.

## What this repository demonstrates

- Implemented token-based authentication with HttpOnly cookies, role-based access, and server-side task ownership assignment; the supplied report's task-listing ownership claim is explicitly reviewed and qualified in the write-up where the shown SQL does not prove per-user isolation.
- Demonstrated session fixation in an intentionally insecure Node.js application and verified session regeneration as the defense.
- Investigated buffer overflow, SQL injection, unsafe memory use, XSS, and CSRF, with secure coding mitigations.

## Tools & technologies

`Node.js` · `Express` · `SQLite` · `Docker` · `C` · `GCC` · `HTTP` · `Cookies` · `Sessions`

## Included academic work

| # | Lab | Portfolio write-up | Original PDF |
|---:|---|---|---|
| 1 | Authentication and Task Management | [`docs/01-authentication-and-task-management.md`](docs/01-authentication-and-task-management.md) | [PDF report](docs/01-authentication-and-task-management.pdf) |
| 2 | Session Fixation and Regeneration | [`docs/02-session-fixation-and-regeneration.md`](docs/02-session-fixation-and-regeneration.md) | [PDF report](docs/02-session-fixation-and-regeneration.pdf) |
| 3 | Program Security Vulnerabilities | [`docs/03-program-security-vulnerabilities.md`](docs/03-program-security-vulnerabilities.md) | [PDF report](docs/03-program-security-vulnerabilities.pdf) |

## Repository structure

```text
.
├── README.md
└── docs/
    ├── *.md   # GitHub-friendly lab write-ups
    └── *.pdf  # Original lab reports (privacy-redacted where noted)
```

The Markdown write-ups and supplied PDF reports form the complete available portfolio evidence. Screenshots, diagrams, and tool output are preserved inside the reports; standalone source code, captures, notebooks, and other artifacts are included only if supplied.

## Evidence policy

Privacy note: cookie and token values in the page 5 DevTools screenshot have been redacted. Cookie names, flags, and the authentication explanation are preserved.

This repository uses only the academic reports and evidence that were actually supplied for the portfolio. Some original reports contained terminal/browser screenshots and figures; no additional screenshots, source files, packet captures, or results have been fabricated or claimed. Where a report recorded an incomplete result or where a written security conclusion is not fully supported by the code snippet shown in the report, the GitHub write-up calls that out explicitly rather than overstating the evidence.

## Responsible use

Security techniques in this repository were performed in controlled academic environments. Use attack and exploitation techniques only on systems you own or have explicit authorization to test.