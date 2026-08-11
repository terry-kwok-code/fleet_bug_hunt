# Software tab search sends a stale/incorrect query value to the API, so results never filter

## Summary
The "Search by name or vulnerability (CVE)" box on the Software tab doesn't filter the list. The browser's own URL correctly updates to reflect what was typed (e.g. `?query=CVE-2026-64783`), but the actual API request fired to the backend uses a completely different, stale `query` value (`query=g`) that doesn't match what was typed at all - so the list stays unfiltered no matter what's searched.

## Environment
- Page: Host Details > Software tab
- Host: "Fleet's Mac" (85 items in this filtered view)

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac" > Software tab.
2. Type a software name into the search box, e.g. "Clock".
3. Observe the result count and list.
4. Clear the search, then type a CVE ID instead, e.g. "CVE-2026-64783".
5. Observe the result count and list again.
6. Open DevTools Network tab and compare the browser's address bar URL against the actual XHR request fired to the API.

## Expected Result
- Searching "Clock" or "CVE-2026-64783" should filter the list to matching results (or show zero results if none match).
- The API request's `query` parameter should match what's shown in the browser's URL and what was actually typed.

## Actual Result
The list stays at all 85 items regardless of what's searched. More specifically: after searching "CVE-2026-64783", the browser address bar correctly shows `fleet-cjkn.onrender.com/hosts/1/software/inventory?query=CVE-2026-64783&order_direction=asc&order_key=name&page=0&fleet_id=-1` - but the actual XHR sent to the API is `GET .../hosts/1/software?...&query=g&order_key=name&order_direction=asc&per_page=20&...`. The value in the request (`g`) isn't even a substring of "CVE-2026-64783", and the response comes back with the full unfiltered 85-item list.

## Evidence
- Screenshot: browser address bar showing `?query=CVE-2026-64783` side-by-side with DevTools Network tab showing the actual request URL containing `query=g`.
- Response body for that request: `"count": 85`, full unfiltered list in the same order as with no search applied at all.

## Notes / Hypothesis
This points at a frontend bug in how the search request is built, not a backend filtering bug - the app's own routing/URL state has the correct, current search term, but whatever builds the actual API call isn't reading that same up-to-date value. Classic shape for a stale-closure/debounce bug: a debounced request handler capturing an old value at the time it was created instead of the current one at the time it fires, so the request never catches up to what's actually been typed. Worth checking the debounce/request-building logic for the search input specifically.

## Severity/Impact
High - search is a core, heavily-relied-on feature for a list this size (85-310+ items depending on filters). With it completely non-functional, there's no practical way to find a specific piece of software or check for a specific CVE without manually paging through the entire list.
