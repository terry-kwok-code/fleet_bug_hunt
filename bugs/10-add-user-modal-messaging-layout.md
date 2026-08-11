# "Add user" premium modal messaging/layout feels underdeveloped (design note)

## Summary
The "Add user" modal, which gates the feature behind Fleet Premium, shows a single small line of text ("This feature is included in Fleet Premium. Learn more") centered in a mostly empty modal. This is a design/polish concern rather than a functional bug.

## Environment
- Page: Host Details > Details tab > User section > "+ Add user"
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, click "+ Add user" in the User section.

## Expected Result
A premium upsell moment like this would typically have clearer visual hierarchy - something like an icon/headline, a short description of what the feature actually does, and a clear call-to-action button - rather than one small centered sentence with a lot of surrounding whitespace.

## Actual Result
The modal shows only a small centered line of text with an inline "Learn more" link. It reads as unfinished or placeholder-like relative to the size of the modal, and doesn't explain what "Add user" actually does before gating it.

## Evidence
Screenshot of the modal attached.

## Notes / Hypothesis
Not a functional defect - the modal works as a gate, it just doesn't look intentional. Worth comparing against other premium-gated modals in the app to see if this one is an outlier or if the pattern is consistent (in which case it'd be a broader design note, not specific to this modal).

## Severity/Impact
Low - polish/consistency issue, not blocking any workflow.
