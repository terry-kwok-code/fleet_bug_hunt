# Navigating to a non-existent host ID gets stuck in an infinite loading spinner

## Summary
This Fleet instance only has one host, at ID 1 (`/hosts/1/details`). Navigating directly to `/hosts/0/details` - an ID that doesn't exist - leaves the page stuck showing a loading spinner forever, with no error message, no redirect, and no timeout.

## Environment
- URL: `https://fleet-cjkn.onrender.com/hosts/0/details`
- This Fleet instance has exactly one host (ID 1); ID 0 does not exist.

## Steps to Reproduce
1. Navigate directly to `https://fleet-cjkn.onrender.com/hosts/0/details`.
2. Wait.

## Expected Result
The page should resolve to some kind of error/empty state - e.g. a "host not found" message, a redirect back to the Hosts list, or a 404-style page - within a reasonable time.

## Actual Result
The page shows a loading spinner indefinitely. It never times out, never shows an error, and never redirects anywhere.

## Evidence
Screenshot attached: URL bar showing `/hosts/0/details`, page showing only a centered loading spinner, DevTools Network tab open alongside it.

## Notes / Hypothesis
Likely the request for host ID 0 either never resolves (hangs) or resolves with an error/empty response that the frontend doesn't have handling for, so it just stays in its initial loading state forever instead of falling through to an error UI. Worth checking what the actual API response for a non-existent host ID looks like (e.g. 404 vs empty body vs something else) to see whether this is a frontend error-handling gap or the request itself never completing.

## Severity/Impact
Medium - anyone who reaches an invalid host ID (stale link, bookmark, manually edited URL, host later deleted) gets a dead end with no way to recover except manually navigating away - no feedback that anything went wrong.
