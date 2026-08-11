# Software tab pagination doesn't reset to page 1 after navigating away and back

## Summary
On the Software tab, if you go to page 2 (or beyond) of the software list, then navigate away (e.g. back to the Hosts overview) and back into the same host's Software tab, the list stays on page 2 instead of starting over from page 1.

## Environment
- Page: Host Details > Software tab
- Host: "Fleet's Mac" (310 software items, paginated)

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac" > Software tab.
2. Click "Next" to go to page 2 of the software list.
3. Navigate away - e.g. click "Back to all hosts" to return to the Hosts overview.
4. Open "Fleet's Mac" again and go to the Software tab.

## Expected Result
Unclear whether there's an intended behavior here - see Notes below. If the intent is "start fresh," the Software tab should load on page 1.

## Actual Result
The Software tab loads back on page 2 (wherever it was left), not page 1.

## Evidence
Screenshot of the software list on page 2, with the "Previous" / "Next" controls visible.

## Notes / Hypothesis
Flagging this as an inconsistency rather than a clear-cut bug - some apps intentionally preserve list/pagination state across navigation as a convenience (so you don't lose your place), and that could be the intent here. But if it's unintentional, it likely means the page number is being read from stale component state or a URL/query param that isn't reset when re-entering the tab fresh. Worth clarifying with the team whether this is by design.

## Severity/Impact
Low - not blocking, and could arguably be either a bug or an intentional convenience. Worth a product decision either way, since right now the behavior isn't clearly signposted to the user (nothing indicates "you're still on page 2 from before").
