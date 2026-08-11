# "Delete" host modal has centered header instead of left-aligned title / right-aligned close button

## Summary
The Delete confirmation modal (Actions > Delete) shows its title and X close button both centered at the top, instead of the standard left-aligned title / right-aligned X pattern used elsewhere (e.g. "Add user").

## Environment
- Page: Host Details > Actions dropdown > Delete
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. Click the Actions dropdown.
3. Click "Delete."

## Expected Result
The modal header should follow the same layout as other modals in the app: title left-aligned, X close button in the top-right.

## Actual Result
"Delete" and the X both sit centered together in the middle of the header row.

## Evidence
Screenshot attached showing the centered "Delete ✕" header.

## Notes / Hypothesis
Third instance of this exact pattern, alongside [[12-software-filters-modal-centered-header]] and [[15-run-script-modal-centered-header]]. At this point it looks less like isolated typos and more like a specific modal-header variant/component that's used inconsistently across several modals in the app, while others correctly use the left-aligned version.

## Severity/Impact
Low - purely visual, doesn't block the delete flow, but reinforces this as a recurring, fixable pattern rather than a one-off.
