# Application Security Labs

Secure coding and web-application security labs covering authentication, authorization, session security, memory safety, injection, XSS, and CSRF.

> **Academic context:** Completed as part of Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026). This repository is intended as a technical portfolio of controlled university lab work.

## What this repository demonstrates

- Implemented and reviewed token-based authentication, HttpOnly cookies, role-based access, and user/task ownership controls.
- Demonstrated session fixation in an intentionally insecure Node.js application and verified session regeneration as the defense.
- Investigated buffer overflow, SQL injection, unsafe memory use, XSS, and CSRF, with secure coding mitigations.

## Tools & technologies

`Node.js` · `Express` · `SQLite` · `Docker` · `C` · `GCC` · `HTTP` · `Cookies` · `Sessions`

## Included academic work

| # | Lab | Portfolio write-up |
|---:|---|---|
| 1 | Authentication and Task Management | [`docs/01-authentication-and-task-management.md`](docs/01-authentication-and-task-management.md) |
| 2 | Session Fixation and Regeneration | [`docs/02-session-fixation-and-regeneration.md`](docs/02-session-fixation-and-regeneration.md) |
| 3 | Program Security Vulnerabilities | [`docs/03-program-security-vulnerabilities.md`](docs/03-program-security-vulnerabilities.md) |

## Repository structure

```text
.
├── README.md
└── docs/        # Portfolio write-ups derived from the supplied university reports
```

## Evidence policy

This repository uses only the academic reports and evidence that were actually supplied for the portfolio. Some original reports contained terminal/browser screenshots and figures; no additional screenshots, source files, packet captures, or results have been fabricated or claimed. Where a report recorded an incomplete or unsuccessful step, the write-up preserves that limitation.

## Responsible use

Security techniques in this repository were performed in controlled academic environments. Use attack and exploitation techniques only on systems you own or have explicit authorization to test.
