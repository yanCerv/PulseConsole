# PulseConsole

**PulseConsole** is a privacy-first, local-first web console for exploring
diagnostic logs produced by [PulseKit](https://github.com/yanCerv/PulseKit).

It gives development and QA teams a focused place to investigate what happened
in an app: service failures, unexpected errors, slow operations, retries, and
diagnostic breadcrumbs. PulseConsole starts with local log files, so opening a
log does not upload it anywhere by default.

## Who it is for

- **QA engineers** investigating an issue found during a test run.
- **iOS developers** diagnosing failures in a networking or service layer.
- **Product teams** reviewing known technical issues before a release.
- **Support and engineering leads** who need a concise, technical incident
  timeline without access to user data.

## What it will do

PulseConsole will import PulseKit JSON Lines (`.jsonl`) diagnostic exports and
make them easier to inspect than raw console output:

- Searchable event and error logs.
- Filters for date, session, service, operation, severity, and error code.
- A session timeline for reconstructing a failing test flow.
- Grouped service failures and slow-operation highlights.
- Lightweight, local incident notes or tickets attached to imported logs.

For example, a QA tester can attach a TicketSeller test log after checkout
fails, filter `PaymentsAPI` errors, inspect the matching session, and record a
small incident for the team to reproduce. The log contains technical context
such as timestamps, HTTP status, retry count, and safe error codes—not email,
tokens, request bodies, or user profiles.

## One console, separate applications

PulseConsole is one product, but its data is organized by **project**. Each app
has its own isolated console view, including its logs, sessions, incidents, and
filters:

- TicketSeller
- PetPulse
- SonicPi

This separation avoids mixing unrelated failures while preserving a consistent
diagnostic experience across apps. A future hosted version may allow a team to
select a project before viewing its logs; the first local version will use the
selected project only as local browser state.

## Privacy-first by design

PulseConsole does not require a backend for its first release. JSONL files are
processed in the browser and remain on the developer's device unless they
explicitly choose to export or upload them in a future version.

PulseConsole is not intended to replace a full crash-reporting platform. It is
an intentionally smaller, inspectable alternative: a companion to PulseKit for
understanding service diagnostics and test incidents with privacy-first
defaults.

## Planned workflow

```text
PulseKit in an iOS app
        ↓
Local JSONL diagnostic export
        ↓
PulseConsole: select project → import log → investigate → record incident
```

## Status

The repository currently contains the product definition. The first build will
be a static TypeScript web application with no login, database, or remote log
ingestion.
