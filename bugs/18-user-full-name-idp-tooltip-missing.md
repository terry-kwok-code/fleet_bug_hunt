# "Full name (IdP)" label has a tooltip-style underline but no tooltip appears on hover

## Summary
In the User section, "Full name (IdP)" has the same dotted underline styling as "Department (IdP)" - which normally signals a tooltip is available on hover. But hovering over "Full name (IdP)" shows no tooltip at all.

## Environment
- Page: Host Details > Details tab > User section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, look at the User section.
3. Hover over "Department (IdP)" - note whether a tooltip appears.
4. Hover over "Full name (IdP)" - compare.

## Expected Result
Since "Full name (IdP)" has the same dotted-underline affordance as "Department (IdP)," hovering it should show a tooltip, consistent with what that styling signals elsewhere.

## Actual Result
Hovering "Full name (IdP)" produces no tooltip. "Username (IdP)" and "Groups (IdP)" have no underline at all (consistent with having no tooltip), but "Full name (IdP)" has the underline without the corresponding behavior.

## Evidence
Screenshot attached showing the User section: "Department (IdP)" and "Full name (IdP)" both underlined, "Username (IdP)" and "Groups (IdP)" not underlined.

## Notes / Hypothesis
The underline is a visual affordance that's supposed to mean "hover for more info" - having it on a field with no actual tooltip behind it is misleading, since it invites an interaction that does nothing. Possibly related to [[12-user-idp-section-no-data-fetch]], since this whole section has no real data behind it right now - the tooltip content itself may simply not have been wired up yet for this field specifically.

## Severity/Impact
Low - cosmetic/affordance inconsistency, not blocking, but it's a small trust issue when the UI signals an interaction is available and then doesn't deliver one.
