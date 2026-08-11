# "Add user" premium modal doesn't close on outside click

## Summary
Clicking "+ Add user" on the Host Details page opens a modal gating the feature behind Fleet Premium. Clicking outside the modal (on the dimmed backdrop) doesn't close it - the X button is the only way to dismiss it.

## Environment
- Page: Host Details > Details tab > User section > "+ Add user"
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, click "+ Add user" in the User section.
3. With the modal open, click anywhere outside it (on the dimmed backdrop).

## Expected Result
Clicking outside the modal should close it, matching the standard modal dismiss pattern (click backdrop, click X, or press Escape) used elsewhere in the app.

## Actual Result
Nothing happens when clicking outside the modal. The only way to close it is the X button in the top-right corner.

## Evidence
Screenshot of the open "Add user" modal attached.

## Notes / Hypothesis
Worth checking whether other modals in the app (e.g. "Add report") support backdrop-click-to-close - if they do, this modal is inconsistent with the rest of the product rather than an isolated one-off.

## Severity/Impact
Low-Medium - not blocking, but breaks an interaction pattern users expect from every other modal, which reads as mildly broken.
