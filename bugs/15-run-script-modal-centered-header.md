# "Run script" modal has centered header instead of left-aligned title / right-aligned close button

## Summary
Opening the "Run script" modal from Actions shows its title and X close button both centered at the top, instead of the standard left-aligned title / right-aligned X pattern used elsewhere (e.g. "Add user").

## Environment
- Page: Host Details > Actions dropdown > Run script
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. Click the Actions dropdown.
3. Click "Run script."

## Expected Result
The modal header should follow the same layout as other modals in the app: title left-aligned, X close button in the top-right.

## Actual Result
"Run script" and the X both sit centered together in the middle of the header row.

## Evidence
Screenshot attached showing the centered "Run script ✕" header, with "No scripts available for this host" below it.

## Notes / Hypothesis
Same issue as [[12-software-filters-modal-centered-header]] - this is the second modal found with this exact centered-header pattern, which makes it look less like a one-off and more like a shared modal-header variant that's used inconsistently across the app. Worth checking whether both modals share a component/prop that isn't being set correctly, or whether there are two different header components in use and one of them is wrong.

## Severity/Impact
Low - purely visual, doesn't block the Run script flow, but reinforces that this is a recurring pattern rather than an isolated typo.
