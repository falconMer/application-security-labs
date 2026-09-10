# Application Security Labs

Secure coding and web-application security labs covering authentication, authorization, session security, memory safety, injection, XSS, and CSRF.

> **Academic context:** Completed as part of Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026). This repository is intended as a technical portfolio of controlled university lab work.

## What this repository demonstrates

- Implemented and reviewed token-based authentication, HttpOnly cookies, role-based access, and user/task ownership controls.
- Demonstrated session fixation in an intentionally insecure Node.js application and verified session regeneration as the defense.
- Investigated buffer overflow, SQL injection, unsafe memory use, XSS, and CSRF, with secure coding mitigations.

## Tools & technologies

`Node.js` · `Express` · `SQLite` · `Docker` · `C` · `GCC` · `HTTP` · `Cookies` · `Sessions`

## Included lab reports

| # | Lab | Report |
|---:|---|---|
| 1 | 01 Authentication And Task Management | [`docs/01-authentication-and-task-management.md`](docs/01-authentication-and-task-management.md) |
| 2 | 02 Session Fixation And Regeneration | [`docs/02-session-fixation-and-regeneration.md`](docs/02-session-fixation-and-regeneration.md) |
| 3 | 03 Program Security Vulnerabilities | [`docs/03-program-security-vulnerabilities.md`](docs/03-program-security-vulnerabilities.md) |

## Repository structure

```text
.
├── README.md
├── docs/        # GitHub text editions of the academic lab reports
└── src/         # Add original code/configs/scripts here when available
```

## Notes

The reports document the work actually completed in the university labs. For GitHub portability, the reports are included as searchable Markdown text editions; the original PDF screenshots and figures are not embedded in these conversions. The `src/` directory is intentionally left as a place to add original source code, configuration files, packet captures, notebooks, or scripts where those artifacts are available. No source code has been fabricated from the reports.

## Responsible use

Security techniques in this repository were performed in controlled academic environments. Use attack and exploitation techniques only on systems you own or have explicit authorization to test.
