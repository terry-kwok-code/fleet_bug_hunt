# Host Details "Labels" section shows empty state despite host having labels

## Summary
The Labels section on the Host Details page says "No labels are associated with this host" - but the API returns 3 labels for this host.

## Environment
- Page: Host Details > Details tab > Labels section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, scroll to the Labels section.
3. Compare it against the response from `GET https://fleet-cjkn.onrender.com/api/latest/fleet/hosts/1?exclude_software=true` (the same call the Details tab makes) for the same host, `labels` array.

## Expected Result
The Labels section should list the 3 labels the API returns: "macOS 14+ (Sonoma+)", "All Hosts", "macOS".

## Actual Result
The Labels section shows the empty state: **"No labels are associated with this host."**

## Evidence
API response:
```json
{
  "labels": [
    { "id": 1, "name": "macOS 14+ (Sonoma+)", "label_type": "builtin" },
    { "id": 11, "name": "All Hosts", "label_type": "builtin" },
    { "id": 12, "name": "macOS", "label_type": "builtin" }
  ]
}
```

## Notes / Hypothesis
All 3 labels here are `"label_type": "builtin"` - worth ruling out whether this section only renders custom/manual labels and is silently skipping built-in ones, versus a broader bug where the `labels` array isn't being read at all.

## Severity/Impact
Medium - hides real fleet-membership info from whoever's looking at this host, and could lead someone to wrongly assume the host isn't covered by any label-scoped policies or configs.
