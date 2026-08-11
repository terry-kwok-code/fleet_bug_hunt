# "+ Add report" button in Reports section does nothing visible when clicked

## Summary
Clicking "+ Add report" in the Reports section of the Host Details page produces no visible change in the UI - no modal, form, or any confirmation appears. The click does trigger a network request, but the response isn't something the UI could reasonably use to open an add-report flow.

## Environment
- Page: Host Details > Details tab > Reports section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, scroll to the Reports section (shows "No reports").
3. Click "+ Add report".
4. Watch the page - nothing opens, nothing changes.
5. Check the Network tab for the request that fired.

## Expected Result
Clicking "+ Add report" should open some way to add a report to the host (a form or modal), matching the empty-state text: "Add a report to view custom vitals."

## Actual Result
Nothing happens in the UI. The click does fire a request to `https://fleet-cjkn.onrender.com/api/v1/fleet/hosts/1/report_verify`, which returns 200, but with a payload that has nothing to do with reports:
```json
{
  "message": "You found an easter egg! Mention that you found 'swans' during your walkthrough."
}
```

## Evidence
- DevTools Network tab, request to `.../hosts/1/report_verify`, status 200, response body as shown above.
- No modal, form, toast, or any other UI change after clicking.

## Notes / Hypothesis
Regardless of what `report_verify` is actually for, the button gives zero feedback when clicked - no loading state, no dialog, no error. Whether it's calling the wrong endpoint or the real add-report flow just isn't wired up yet, the visible result is a button that looks broken.

## Severity/Impact
Medium - "+ Add report" is presented as a real, clickable action tied to a feature mentioned right in the empty state, but doing nothing on click makes it look non-functional with no indication anything went wrong.
