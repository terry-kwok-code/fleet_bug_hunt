# "Last fetched" timestamp doesn't update after a refetch completes

## Summary
After clicking Refetch on the Host Details page and waiting for it to finish on the backend, the "Last fetched" label next to the host name still shows the old timestamp - even after a full page reload. The API has the correct, updated timestamp the whole time.

## Environment
- Page: Host Details > Details tab (header area, next to host name)
- Host: "Fleet's Mac" (host ID 1)

## Steps to Reproduce
1. Open Host Details for "Fleet's Mac" and note the "Last fetched" timestamp in the header.
2. Click Refetch.
3. Poll the API until the backend confirms the refetch finished: `refetch_requested` flips from `true` to `false`, and `detail_updated_at` advances to a new timestamp.
4. Reload the page in the browser.

## Expected Result
"Last fetched" should reflect the new `detail_updated_at` value (e.g. "a few minutes ago").

## Actual Result
"Last fetched" still shows the stale value ("about 2 hours ago"), even after a full page reload.

## Evidence
API response right after clicking Refetch:
```
refetch_requested: True
detail_updated_at: 2026-08-11T16:19:07Z
```
API response once the backend finishes:
```
refetch_requested: False
detail_updated_at: 2026-08-11T16:33:07Z
```
`seen_time` also advanced (to `2026-08-11T16:36:57Z`), confirming the host is actively checking in and the data is genuinely fresh. Despite this, the UI header kept showing "Last fetched about 2 hours ago" after a full page reload.

## Notes / Hypothesis
Since the correct, updated timestamp is present in the API response the browser receives, this looks like a frontend rendering issue rather than a backend or caching problem - the header likely isn't reading `detail_updated_at` from the response, or it's bound to a different/stale field.

## Severity/Impact
Medium - Refetch itself works correctly on the backend, but the UI gives users no reliable way to confirm a refetch actually completed, which undermines trust in the feature.
