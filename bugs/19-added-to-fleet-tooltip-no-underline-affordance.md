# "Added to Fleet" shows a tooltip with no underline affordance at all

## Summary
Hovering over the "Added to Fleet" value ("about 20 hours ago") in the Vitals section pops up a tooltip with an exact timestamp (e.g. "11/8/2026, 6:55:00 PM") - but neither the label nor the value has any dotted-underline styling to indicate a tooltip is available there.

## Environment
- Page: Host Details > Details tab > Vitals section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, look at the Vitals section, "Added to Fleet" field.
3. Note there's no dotted underline on either "Added to Fleet" or "about 20 hours ago."
4. Hover over the value anyway.

## Expected Result
If a tooltip exists, the field should carry the same dotted-underline affordance used elsewhere in this section (e.g. "Public IP address," "Agent") so users know to hover it in the first place.

## Actual Result
A tooltip appears showing the exact timestamp, but there's no visual cue beforehand that hovering would do anything - it's fully undiscoverable without trial and error.

## Evidence
Screenshot attached showing the tooltip ("11/8/2026, 6:55:00 PM") open over "Added to Fleet," with no underline visible on either the label or the relative-time value.

## Notes / Hypothesis
This is the inverse of [[18-user-full-name-idp-tooltip-missing]] (underline with no tooltip) and adds to the broader pattern already flagged in [[13-vitals-tooltip-placement-inconsistent]] - tooltip affordance in this section isn't applied consistently: some fields have the underline and the tooltip, some have the underline with no tooltip, and now this one has a tooltip with no underline at all. Suggests the underline styling and the tooltip-attachment logic are two separate things that aren't being kept in sync per field.

## Severity/Impact
Low - not blocking, but a real discoverability gap: relative timestamps like "about 20 hours ago" are exactly the kind of value where users would want the precise timestamp, and there's currently no indication that's available here.
