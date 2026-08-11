# Host Details Vitals shows Memory as "8.0 KB" instead of "8 GB"

## Summary
The Memory field in the Vitals section shows "8.0 KB". The API's `memory` value (8589934592 bytes) converts to 8 GB, so the number itself is right - it's just labeled with the wrong unit.

## Environment
- Page: Host Details > Details tab > Vitals section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, check the "Memory" field in Vitals.
3. Compare it against the response from `GET https://fleet-cjkn.onrender.com/api/latest/fleet/hosts/1?exclude_software=true` (the same call the Details tab makes) for the same host.

## Expected Result
"Memory" should read "8 GB" (8589934592 bytes ÷ 1024³ = 8).

## Actual Result
"Memory" reads **"8.0 KB"**.

## Evidence
API response:
```json
{
  "memory": 8589934592
}
```
The number shown (8.0) matches the correctly-converted GB value - it isn't being computed wrong, it's just tagged with the wrong unit.

## Notes / Hypothesis
Same shape of bug as [[04-disk-space-unit-label-wrong]]: the math is right, the label is wrong. Might be a shared unit-formatting helper that defaults to "KB" regardless of the unit it actually converted to - worth checking if Memory and Disk space available go through the same formatting code.

## Severity/Impact
Medium - the number itself is trustworthy, but a wildly wrong unit label ("KB" vs "GB") could still mislead anyone using this page for fleet inventory or capacity checks.
