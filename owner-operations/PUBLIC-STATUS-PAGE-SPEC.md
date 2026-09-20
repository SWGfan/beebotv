# Beebo public status page specification

This document describes the **separate** public status page. It must never reuse the owner operations dashboard or expose customer-level telemetry.

## Public-safe content

- Current status for a released service and publicly available region: Operational, Degraded, Maintenance, or Outage.
- Time-stamped incident notices, maintenance windows, and resolved incidents.
- Region names only after that region has a live, customer-available service.
- Broad performance objective bands only when measured and reviewed, for example “typical regional latency range.”
- A link to support and the published privacy policy.

## Never publish

- Household or precise device locations, IP addresses, user names, account IDs, device names, media titles, libraries, individual bandwidth, or connection histories.
- Exact live connection counts for a small region, per-node capacity, raw server metrics, internal IPs, server hostnames, or maintenance access details.
- Planned regions until the service is genuinely available.

## Production controls needed before launch

1. Separate `status.beebo.*` host and independent static or status-service deployment.
2. Read-only, aggregate status feed; no browser access to private operations APIs.
3. Role-based owner dashboard authentication, multi-factor authentication, audit logging, and IP/device session controls.
4. Data minimisation: aggregate by coarse region and require a minimum cohort before an internal map point is shown.
5. Monitoring that checks from more than one external location, plus alerting and an owner incident workflow.
6. Manual approval for all public incident and availability messages.

The owner prototype at `owner-operations/index.html` uses clearly labelled sample data. It is not a source of truth, monitoring system, or deployable public status page.
