# Unicore Watch 4.0

Standalone watchOS app. Enter credentials on the watch; tokens, device mapping and credentials are kept in Keychain. The paired Watch target remains in the `unicore_mobile_app` repository.

Uses the same 4.0 API implementation as mobile’s paired Watch: authenticated server device resolution, 30-day lookup sessions, cached bearer tokens, one refresh on HTTP 401, explicit login stages and errors, and HTTPS metadata audit logging to `13.214.2.6/admin`. Both attendance actions use actual GPS and verify the approved device before posting. Missing or ambiguous device mappings block attendance.

The UI stays readable on watchOS with a consistent light color scheme. Signing in and looking up devices never submits attendance; check-in/out require a button press. The separate server scheduler operates Wednesday–Friday with check-in 08:30–08:45 and checkout 16:15–16:30 (Asia/Ulaanbaatar).

```sh
python3 test/run_watch_api_tests.py
xcodebuild -project UnicoreWatch.xcodeproj -scheme UnicoreWatch -configuration Release -destination 'generic/platform=watchOS' CODE_SIGNING_ALLOWED=NO build
```

Tests use isolated network and Keychain fixtures; no real attendance is submitted. Distribution signing and TestFlight publication still require access to the requested Apple Developer team. No credentials or signing secrets are committed.
