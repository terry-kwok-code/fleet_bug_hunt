# Software tab "Filters" modal has centered header instead of left-aligned title / right-aligned close button

## Summary
On the Software tab, clicking "Add filters" opens a "Filters" modal where the title and the X close button both sit centered at the top. Every other modal in the app (e.g. "Add user") uses the standard pattern of a left-aligned title with the X in the top-right corner.

## Environment
- Page: Host Details > Software tab > "Add filters" modal
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. Click the Software tab.
3. Click "Add filters".

## Expected Result
The modal header should follow the same layout as other modals in the app: title left-aligned, X close button in the top-right.

## Actual Result
Both "Filters" and the X sit centered together in the middle of the header row.

## Evidence
Screenshot of the "Filters" modal attached, showing the centered "Filters ✕" header.

## Notes / Hypothesis
Likely a one-off styling issue specific to this modal's header component - possibly missing a `justify-content: space-between` (or equivalent) that the other modals use, or this modal not reusing the shared modal-header component at all.

## Severity/Impact
Low - purely visual, doesn't block filtering functionality, but it's an inconsistency that stands out next to every other modal in the app.
