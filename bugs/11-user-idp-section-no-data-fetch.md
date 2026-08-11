# "User" (IdP) section always shows "---" - no request ever fetches this data

## Summary
The User section on the Host Details page (Username (IdP), Full name (IdP), Department (IdP), Groups (IdP)) always shows "---" for every field. Checking the `hosts/:id` API response confirms it has no IdP-related fields at all, and no separate request fires anywhere to fetch this data - so the UI has nothing to work with by design or by omission.

## Environment
- Page: Host Details > Details tab > User section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, look at the User section.
3. Open DevTools Network tab and reload/re-navigate to the page.
4. Inspect every request that fires - none of them return IdP-style fields (username, full name, department, groups), and no request beyond the main `GET .../hosts/1` call is made in connection with this section.

## Expected Result
Either the User section fetches and displays real IdP data (if the host has any associated with it), or - if there's genuinely no IdP integration configured for this instance - the section should make that clear rather than presenting four fields that always read "---".

## Actual Result
All four fields permanently show "---". The full `hosts/1` response (checked directly) contains no IdP-related data anywhere in it, confirming the frontend isn't even receiving anything to render here, let alone failing to render it.

## Evidence
- Full `GET .../hosts/1` JSON response inspected directly in DevTools: no `end_users`, no IdP fields, nothing resembling username/department/full name/groups outside of the unrelated local `users` array (OS-level accounts, already shown correctly elsewhere in "Local user accounts").
- Full list of every request fired on a fresh page load (captured from the Network tab) confirms this isn't a filtering mistake - the complete set of XHR calls made for this page is: `me?include_ui_settings=true`, `config`, `mdm`, `macadmins`, `certificates?page=0&per_page=10&order_key=common_name&order_direction=asc`, `1?exclude_software=true` (the main host details call), `activities?page=0&per_page=8`, `upcoming?page=0&per_page=8`, `enroll_secret`. Nothing resembling an end-user/IdP/device-mapping call appears anywhere in that list.
- Notably, several other sections on this same page - MDM, macadmins, Certificates, Activity - each get their own dedicated XHR call and render correctly. The User (IdP) section is the only one with no corresponding request at all.

## Notes / Hypothesis
Tried to confirm against Fleet's REST API docs whether a dedicated endpoint exists for this (e.g. something like a device-mapping/end-user endpoint), but wasn't able to verify one way or the other due to the doc page being too large to fetch in full. That said, the pattern on this page is clear: nearly every section fires its own request, and this is the one exception. That makes "the frontend never wires up a call for this section" a more likely explanation than "there's genuinely no data source for it."

## Severity/Impact
Medium - the section isn't broken in the sense of showing wrong data, but it presents fields that can never populate, which is confusing and makes it unclear whether IdP integration is even supported/configured here.
