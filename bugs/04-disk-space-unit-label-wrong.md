# Host Details Vitals shows "Disk space available" in KB instead of GB

## Summary
The "Disk space available" field in the Vitals section shows "102.99 KB". The API already returns this value in GB (`gigs_disk_space_available: 102.99`), so the number is correct - just the unit label is wrong.

## Environment
- Page: Host Details > Details tab > Vitals section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, check the "Disk space available" field in Vitals.
3. Compare it against the response from `GET https://fleet-cjkn.onrender.com/api/latest/fleet/hosts/1?exclude_software=true` (the same call the Details tab makes) for the same host.

## Expected Result
"Disk space available" should read "102.99 GB".

## Actual Result
"Disk space available" reads **"102.99 KB"**.

## Evidence
API response:
```json
{
  "gigs_disk_space_available": 102.99,
  "percent_disk_space_available": 78,
  "gigs_total_disk_space": 131.55
}
```
The field name (`gigs_disk_space_available`) and the progress bar next to it (matches `percent_disk_space_available: 78`) both confirm this is meant to be GB, not KB.

## Notes / Hypothesis
Same shape of bug as [[03-memory-unit-conversion-wrong]] - both vitals show "KB" where GB is expected, and in both cases the number itself is correct. Points to a shared unit-label component or helper that's hardcoded to "KB" (or defaulting to it) instead of using the actual unit. Worth checking if Memory and Disk space available share the same rendering code.

## Severity/Impact
Medium - the value itself is right, but labeling it KB instead of GB understates available disk space by about a million times, which could easily mislead someone checking if a host is running low on storage.
