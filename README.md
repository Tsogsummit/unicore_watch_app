# Unicore Watch

## Attendance API compatibility

Login selects `tenant_65` and uses a replacement token if returned. Authenticated requests include `Authorization: Bearer …` and `X-Tenant-Id: tenant_65`. Login also retrieves the approved attendance device by matching `/attendance/device` against `/devices`; an absent or ambiguous match is displayed and blocks attendance submission. The device is checked again before every submission.

Check-in and checkout send coordinates, `accuracy`, `address: ""`, `device_id`, `image: null`, `is_remote: false`, and `note: ""`. Check-in additionally sends `device_name` and `rule_id: 5`. HTTP errors and `success: false` are treated as failures.

To match the configured server, coordinates are generated within 100 m of 47.89679317, 106.88973599, and accuracy is generated between 3 and 20 m. These values are synthetic, not GPS measurements. Empty-address acceptance has not been verified with a live attendance submission.

The server scheduler remains responsible for Wednesday–Friday check-in at 07:30–07:45 and checkout at 16:15–16:30, Asia/Ulaanbaatar. These apps submit only when their attendance buttons are pressed; they do not create a second scheduler. Server checkout eligibility, the five-minute gap, and early-departure rules still apply.

Audit telemetry excludes passwords and tokens. The standalone Watch login has no hardcoded credentials; the mobile login no longer offers Remember me and removes older saved login preferences. The paired Watch in the mobile repository retains its existing secure credential-sync flow.
