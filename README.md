# JobHunter MX

[Español](README.es.md) | **English**

> **Status: concept / planning.** No automated job applications or platform integrations are implemented yet.

**JobHunter MX** is an open-source, Android-first job-search assistant designed for the Mexican employment market. Its goal is to run independently on an older Android phone, discover relevant opportunities, rank them, tailor truthful résumé versions, and help manage applications.

The first target device is an **LG X230H running Android 6 (API 23)** with limited memory and storage. The project therefore prioritizes a lightweight native application, local-first persistence, and optional remote AI inference. A laptop or always-on personal server should not be required after setup. Internet connectivity will be needed for job sources and cloud-based AI.

## Why build it?

Looking for work in Mexico often involves checking Indeed, OCC, Computrabajo, Facebook job posts, and individual company sites. Finding suitable jobs, comparing requirements, preparing résumés, and tracking responses are repetitive tasks. JobHunter MX aims to reduce that work while keeping applicants in control.

## Planned features

- **Job intake:** ingest permitted sources, official alerts, user-shared links, email notifications, and potentially authorized provider APIs. Each platform will have an independent adapter; compatibility is not guaranteed.
- **Location-aware discovery:** filter by city, configurable radius, remote/hybrid/on-site preferences, compensation, role and technologies. Location can be a manually selected area; precise GPS is optional.
- **Matching and ranking:** compare job descriptions against a structured skills/experience profile, explaining matches, gaps and deal-breakers. Scores are heuristics, **not** hiring probabilities.
- **AI-powered résumé tailoring:** generate a distinct, ATS-readable résumé for each relevant opening using a verified master profile. Reorder and highlight relevant experience **without inventing jobs, degrees, skills or dates**.
- **Bilingual documents:** support Spanish and English templates, PDF export, and an application-specific history of generated versions.
- **Application workspace:** keep links, contacts, drafts, review status, dates and outcomes; notify the applicant when an application is ready.
- **Autonomous operation:** scheduled background ingestion, deduplication, retry logic and notifications, with Android power-management limits explicitly accounted for.
- **Privacy:** local database, data minimization, explicit permissions, secure credential handling and configurable deletion/export.

## Intended workflow

```text
Allowed job feeds / alerts / shared links
                 |
                 v
       Normalize + deduplicate
                 |
                 v
        Filter + match + rank
                 |
                 v
      Tailor résumé from facts
                 |
                 v
      Review / approved workflow
                 |
                 v
        Track and notify user
```

**Important:** Discovering jobs and preparing drafts can be autonomous; submitting an application depends on the destination site's permissions and flow. The project will **not** aim to bypass CAPTCHAs, evade bot detection, or automate actions prohibited by a service. When needed, the user completes the application manually.

## Technical direction (proposed, not implemented)

| Layer | Candidate technology |
| --- | --- |
| Android app | Kotlin, Android SDK (minimum API 23), lightweight native UI |
| Background work | Android-compatible JobScheduler, or a specifically verified compatible WorkManager version |
| Local state | SQLite / Room with a compatible library version |
| Job adapters | Official/permitted APIs, alerts, email and imported links |
| Matching | Deterministic filters and optional remote LLM |
| Résumé rendering | Lightweight text/HTML templates and PDF generation |
| AI | Configurable remote inference provider; no on-device large model required |
| Notifications | Android notification APIs |

Because Android 6 is old and unsupported, current library compatibility, HTTPS trust stores and background execution must be verified on the physical device. Avoid putting long-lived paid API secrets in the client; a securely scoped token or optional provider-backed relay may be needed for production. No dedicated personal computer is assumed.

## Suggested repository layout

```text
app/                # Native Android application
core/               # Scheduling and orchestration
sources/            # Permitted job-input adapters
matching/           # Filtering, geolocation and scoring
resume/             # Master profile, tailoring and export
applications/       # Drafts and application tracking
storage/            # Database and local files
docs/               # Design notes and source policies
tests/              # Unit and integration tests
```

This is a proposed structure and does not represent files that already exist.

## Roadmap

- [ ] **M0 — Device feasibility:** verify build/install, network/TLS, battery behavior and background scheduling on LG X230H.
- [ ] **M1 — Local MVP:** configure preferences, import jobs from shared links/alerts, deduplicate, filter and track them.
- [ ] **M2 — Matching:** explain relevance and missing requirements using a truthful profile.
- [ ] **M3 — Dynamic CV:** generate and review tailored Spanish/English PDF résumés for each job.
- [ ] **M4 — Notifications:** unattended periodic checks from supported sources and new-match notifications.
- [ ] **M5 — Applications:** assist with form preparation and permitted submission flows, track responses.
- [ ] **M6 — Measurement:** compare response rates across résumé versions while respecting privacy and small-sample limitations.

## Responsible automation

Respect website terms, robots/access rules, rate limits, consent and account security. Never silently submit inaccurate information or claim a job application was sent before confirmation. Avoid collecting Facebook or other platform data by unauthorized scraping. Provide a clear audit trail and a user-controlled pause/stop option.

## Project scope

Initially focused on software engineering jobs in Mexico, but designed so users can configure other professions, locations, sources and languages.

## Contributing

The project is at the planning stage. Design proposals, compatibility investigations for older Android versions, accessibility improvements, documentation and permitted source integrations are welcome. Contribution guidelines and a license will be added as the project develops.

---
*JobHunter MX is an independent community project and is not affiliated with Indeed, OCC, Computrabajo, Meta, or any employer.*
