# Navigating from Hosts list to Host Details page intermittently fails silently

> Filed as GitHub issue: https://github.com/terry-kwok-code/fleet_bug_hunt/issues/1

## Summary
Clicking a host ("Fleet's Mac") on the Hosts list sometimes doesn't take you to its Host Details page. There's a brief loading flicker, then you're just... still on the Hosts page, with no error shown.

## Environment
- Page: Hosts list > Host Details (`Fleet's Mac`)
- Browser: [fill in browser + version]
- Fleet version / build: [fill in if known]

## Steps to Reproduce
1. Go to the Hosts page.
2. Click "Fleet's Mac" to open its details page.
3. Repeat a few times across fresh page loads - it doesn't fail every time.

## Expected Result
Clicking a host should reliably take you to its Host Details page.

## Actual Result
Sometimes it works fine. Other times you get a brief loading flash and then nothing - you're left on the Hosts page with no error message or any indication that something went wrong.

## Frequency
Intermittent - couldn't get it to fail on demand, but it happens often enough to hit within a handful of attempts.

## Evidence
- Network tab: on a failed attempt, some of the requests that normally fire during a successful navigation are missing entirely. The ones that do fire all return 200.
- Console: no errors logged, even on the failed attempts.
- [Attach a screen recording, plus Network tab screenshots/HAR from both a failed and a successful attempt for comparison]

## Notes / Hypothesis
The pattern - some requests firing, no errors, all 200s, but navigation just not happening - points more toward a client-side race condition than a server issue. My guess is navigation kicks off before all the data it depends on has resolved, or one of the requests gets cancelled (component unmount, deduping, an aborted effect) and the page never gets what it needs to render. Worth checking whether any of the host-details calls depend on the result of an earlier one.

## Severity/Impact
Medium - no data loss and no error, but it silently blocks the main workflow of getting into a host's details, and gives no feedback that anything failed, so it just looks broken and invites repeated clicking.
