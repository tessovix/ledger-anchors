# Tessovix ledger anchors

Daily public anchors of the Tessovix usage and contribution-point (CP) ledgers.

Every ledger line stores the SHA-256 of the previous line (`prev_hash`), so no past line can
change without changing every hash after it. Once a day (00:05 UTC) the workflow `.github/workflows/anchor.yml` publishes the line count
and the latest hash (`tail_hash`) of each ledger here, as `anchors/YYYY/YYYY-MM-DD.json` (UTC
date). Files are never overwritten; git history makes any rewrite visible.

## Fields

| Field | Meaning |
|---|---|
| `ledgers.usage.lines`, `ledgers.usage.tail_hash` | Requests served so far and the hash of the last usage line |
| `ledgers.cp.lines`, `ledgers.cp.tail_hash` | CP awards so far and the hash of the last CP line |
| `cp_total` | Sum of all CP awarded (3 decimals) |
| `nodes_connected`, `nodes_verified` | Nodes connected at publish time; verified ones passed the gateway's checks |
| `requests_total`, `uptime_s`, `generated_at_ms` | Request count, gateway uptime, publish time (unix ms) |

## Checking

A ledger with N lines whose last line hashes to `tail_hash` on day D must, on any later day,
still contain those same N lines as its first N lines. If a later anchor cannot be explained
by appending lines, the history was rewritten. Report it to support@tessovix.com.

How CP is computed: https://tessovix.com/earn/

## Uptime

The workflow `.github/workflows/uptime.yml` checks the public endpoints every 15 minutes.
A failed run sends an email to the maintainers.
