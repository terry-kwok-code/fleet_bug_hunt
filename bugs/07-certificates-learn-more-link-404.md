# "Learn more" link in Certificates section leads to a 404 page

## Summary
The "Learn more" link at the bottom of the Certificates section on the Host Details page points to a URL that doesn't exist, and takes you to Fleet's public 404 page instead.

## Environment
- Page: Host Details > Details tab > Certificates section
- Host: "Fleet's Mac"

## Steps to Reproduce
1. Go to Hosts > open "Fleet's Mac".
2. On the Details tab, scroll to the Certificates section.
3. Click "Learn more" in the helper text below the certificates table ("Showing certificates in the system and login (user) keychain. To get all certificates, you can query the certificates table. Learn more").

## Expected Result
The link should land on a real Fleet docs page explaining how to query the certificates table.

## Actual Result
The link goes to `https://fleetdm.com/learn-more-about/certificates-queryz`, which 404s ("404: We can't find that page!").

## Evidence
- Link target: `https://fleetdm.com/learn-more-about/certificates-queryz`
- Screenshot of the resulting Fleet 404 page attached.

## Notes / Hypothesis
The URL slug ends in "queryz" - that trailing "z" looks like a typo, possibly meant to be "certificates-query" or "certificates-queries". Worth checking whether the correct docs page exists under a different slug and this is just a broken link, versus the destination page never having been published.

## Severity/Impact
Low - doesn't affect any core host details functionality, but it's a dead-end for anyone trying to learn how to query the certificates table from this page.
