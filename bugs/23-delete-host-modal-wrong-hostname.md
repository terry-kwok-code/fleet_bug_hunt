# Delete host confirmation modal shows the wrong hostname

## Summary
Opening the Delete confirmation modal from Actions on "Fleet's Mac" shows the text "This will remove the record of **John's MacBook** and associated data such as unlock PINs and disk encryption keys." - a completely different host name than the one whose page this action was triggered from.

## Environment
- Page: Host Details > Actions dropdown > Delete
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. Click the Actions dropdown.
3. Click "Delete."
4. Read the confirmation text.

## Expected Result
The confirmation text should reference the actual host being deleted: "This will remove the record of **Fleet's Mac** and associated data..."

## Actual Result
The text references "John's MacBook" instead - a host name that doesn't match the page this modal was opened from.

## Evidence
Screenshot attached showing the modal with "John's MacBook" while the host name visible behind it (partially obscured) is for "Fleet's Mac."

## Notes / Hypothesis
This is more than a cosmetic issue - a delete confirmation showing the wrong hostname is actively misleading for a destructive, hard-to-reverse action. Worth urgently checking whether "John's MacBook" is just a hardcoded/stale placeholder string in the modal copy (best case), or whether the underlying delete request could actually be scoped to the wrong host ID (worst case, and far more serious).

## Severity/Impact
High - this is a confirmation dialog for a destructive action (removing a host record and its associated unlock PINs/disk encryption keys). Showing the wrong hostname undermines the entire point of a confirmation step, and if it's more than a display bug, could mean the wrong host gets deleted.
