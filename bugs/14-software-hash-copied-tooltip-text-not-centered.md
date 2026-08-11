# "Copied!" tooltip text not centered after copying a software Hash value

## Summary
On the Software tab, clicking the copy icon next to a Hash value shows a "Copied!" confirmation bubble, but the text inside that bubble isn't centered/cleanly laid out - it overlaps oddly with the copy icon instead of sitting clearly next to it.

## Environment
- Page: Host Details > Software tab
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. Click the Software tab.
3. Click the copy icon next to the Hash value for "Safari" (`12b701f...`).
4. Look at the "Copied!" confirmation bubble that appears.

## Expected Result
The "Copied!" tooltip text should be cleanly centered/aligned within its bubble, positioned clearly next to (not overlapping) the copy icon.

## Actual Result
The "Copied!" text isn't centered in the bubble, and visually overlaps with the copy icon rather than being cleanly separated from it.

## Evidence
Screenshot attached showing the copy icon and "Copied!" bubble immediately after clicking.

## Notes / Hypothesis
Same general category as [[12-software-filters-modal-centered-header]] - another spot on this page where a small overlay's internal alignment/centering seems off. Worth checking whether this tooltip reuses a shared "copied" component used elsewhere in the app, and whether it's positioned correctly relative to its trigger icon.

## Severity/Impact
Low - purely cosmetic, doesn't affect the actual copy-to-clipboard functionality.
