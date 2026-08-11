# Deleting a host shows a success message, but the host is not actually deleted

## Summary
Using Actions > Delete on "Fleet's Mac" shows a green success toast: "Host 'Fleet's Mac' was successfully deleted." But the host is still listed on the Hosts page afterward, and its Host Details page still loads normally with full data (Status: Online, Issues: 1, Vitals, etc.) - it was never actually removed.

## Environment
- Page: Host Details > Actions dropdown > Delete
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. Click the Actions dropdown > Delete.
3. Confirm the delete in the modal.
4. Note the success toast: "Host 'Fleet's Mac' was successfully deleted."
5. Go back to the Hosts page - "Fleet's Mac" is still listed.
6. Click into it again - the Host Details page loads normally, fully populated, as if nothing happened.

## Expected Result
After a successful delete, the host should no longer appear on the Hosts page, and navigating to its old URL should show a "not found" state rather than loading normally.

## Actual Result
The host persists completely intact - same status, same issue count, same vitals - despite the UI explicitly confirming the delete succeeded.

## Evidence
- Screenshot attached showing the success toast on the Host Details page for "Fleet's Mac," which is still fully loaded with the same data as before deletion.
- DevTools Network tab shows the confirm button doesn't hit any host-delete endpoint at all - it fires `POST https://fleet-cjkn.onrender.com/api/v1/fleet/hosts/1/verify`, status 200, with a response body of `{"message": "..."}` that has nothing to do with deleting a host.

## Notes / Hypothesis
This fully explains the bug: the Delete confirmation button appears to be wired to the wrong endpoint (`.../hosts/1/verify`) rather than an actual delete request. Since that endpoint returns 200, the frontend shows a success toast regardless of the fact that no delete ever happened server-side. This is a false-positive confirmation on a destructive action, which is worse than the delete simply failing outright - the user has no reason to doubt it worked. Also possibly related to [[23-delete-host-modal-wrong-hostname]] (the modal referencing "John's MacBook" instead of the actual host) - both point at the Delete flow being wired up incorrectly end-to-end rather than two unrelated issues.

## Severity/Impact
High - a destructive action reporting false success undermines trust in the entire delete flow, and could easily lead someone to believe sensitive data (unlock PINs, disk encryption keys, per the modal's own warning) has been removed when it hasn't.
