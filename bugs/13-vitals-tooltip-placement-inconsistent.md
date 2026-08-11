# Vitals section: tooltip trigger is on the value instead of the field label for Agent and Disk encryption

## Summary
In the Vitals section, hovering to reveal a tooltip is inconsistent about where the trigger sits. For "Public IP address," the dotted underline (and presumably the tooltip) is on the field *label*. For "Agent" and "Disk encryption," it's on the *value* instead ("1.58.0" and "Off").

## Environment
- Page: Host Details > Details tab > Vitals section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, look at the Vitals section.
3. Compare the dotted-underline (tooltip trigger) placement across fields: "Public IP address" vs. "Agent" vs. "Disk encryption."

## Expected Result
Tooltip trigger placement should be consistent across all fields in the section - either always on the label or always on the value.

## Actual Result
- "Public IP address": underline is on the label.
- "Agent": underline is on the value ("1.58.0"), which opens a tooltip showing `osquery: 5.23.1`, `Orbit: 1.58.0`, `Fleet Desktop: 1.58.0`.
- "Disk encryption": underline is on the value ("Off") instead of the label, and opens a tooltip reading: "The disk might be encrypted, but FileVault is off. The disk can be accessed without entering a password."

## Evidence
Screenshots attached showing both tooltips open on their values (Agent's version breakdown, and Disk encryption's FileVault explanation), alongside "Public IP address" with the underline on its label instead.

## Notes / Hypothesis
Both the Agent and Disk encryption tooltips read as explanations of what the *field* means (what the version numbers represent, what "Off" implies about FileVault) rather than something specific to that one value - which is exactly the kind of content a user would expect to find by hovering the label, not the value. Suggests these fields aren't using the same shared component/prop pattern for attaching tooltips as "Public IP address" does.

## Severity/Impact
Low - doesn't block anything, but makes the hover-for-more-info affordance unpredictable across fields in the same section.
