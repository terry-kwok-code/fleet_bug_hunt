# Failing policy modal shows a blank body when the policy has no resolution text, instead of an empty-state message

## Summary
The Policies tab banner says "Click a policy below to see if there are steps you can take to resolve the issue." Clicking the failing policy ("Always failing") opens a modal with just the policy name and a "Done" button - no resolution steps, and no message explaining that none are available.

## Environment
- Page: Host Details > Policies tab
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac" > Policies tab.
2. Note the banner: "This device is failing 1 policy. Click a policy below to see if there are steps you can take to resolve the issue."
3. Click "Always failing" in the policy list.

## Expected Result
Given the API's `policies` data for this host has both `description` and `resolution` set to empty strings for "Always failing," there's nothing for the modal to show - the real gap is that the UI doesn't handle this case. It should show a message like "No resolution steps have been provided for this policy" (or similar), rather than leaving the body completely blank.

## Actual Result
The modal opens with just the policy name as a header and an empty body - no content, no explanation, just "Done."

## Evidence
- Screenshot of the "Always failing" modal, body empty aside from the "Done" button.
- Screenshot of the "Always passing" modal for comparison, same empty-body pattern.
- Confirmed via the host's API response that both policies have `"description": ""` and `"resolution": ""`.

## Notes / Hypothesis
This isn't a data-fetching or rendering bug - the modal is accurately reflecting that there's no description/resolution text for either policy. The actual issue is the missing empty state: since the banner explicitly promises "steps to resolve," a blank modal reads as broken/unfinished rather than "there's nothing configured here yet."

## Severity/Impact
Low-Medium - not blocking, but a genuinely failing policy with a completely blank explanation modal is a poor experience for the person trying to fix it, especially since the surrounding copy sets an expectation of finding help there.
