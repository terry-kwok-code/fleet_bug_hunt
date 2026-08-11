# Host Details page displays the wrong operating system (shows Ubuntu for a macOS host)

## Summary
The Vitals section on the Host Details page for "Fleet's Mac" shows "Ubuntu 24.04.3 LTS" as the operating system - but this is a macOS host, and the API has the correct value.

## Environment
- Page: Host Details > Details tab > Vitals section
- Host: "Fleet's Mac" (hostname `macos-26-smokes.shared`, platform `darwin`)

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, check the "Operating system" field in Vitals.
3. Compare it against the response from `GET https://fleet-cjkn.onrender.com/api/latest/fleet/hosts/1?exclude_software=true` (the same call the Details tab makes) for the same host.

## Expected Result
"Operating system" should read something like "macOS 26.5.1" (from `os_version` in the API response), matching `platform: "darwin"`.

## Actual Result
"Operating system" shows **"Ubuntu 24.04.3 LTS"**.

## Evidence
API response (`host.os_version`, `host.platform`):
```json
{
  "platform": "darwin",
  "os_version": "macOS 26.5.1",
  "build": "25F80"
}
```
The same Vitals section correctly shows `hardware_model: VirtualMac2,1` and `hardware_serial: ZHRMLR5T26` for this host, so it's not that the whole page is pulling data for the wrong host - just this one field.

## Notes / Hypothesis
This isn't just a formatting issue - "Ubuntu" doesn't match "darwin" or "macOS 26.5.1" in any way. Best guess is the OS field is pulling from a stale/cached value, a mismatched host record, or possibly a hardcoded fallback string that isn't actually reading `os_version`.

## Severity/Impact
High - this is basic identifying info about the host. Showing the wrong OS entirely could send an admin down the wrong path on patching, compliance checks, or policy targeting.
