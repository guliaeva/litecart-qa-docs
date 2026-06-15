## TC-ADMIN-AUTH-008 — Access protected internal Admin Panel URL without authentication

**Requirement:** REQ-ADMIN-AUTH-001, REQ-ADMIN-AUTH-002
**Priority:** High
**Type:** Negative
**Automation status:** Planned

## Preconditions

* The administrator is logged out.
* At least one protected internal Admin Panel URL is available for testing.
* The list of protected internal Admin Panel URLs is documented in the test environment or test data documentation.

## Test Data

* Protected internal Admin Panel URL: 
`/admin/?app=currencies&doc=currencies

## Steps

1. Open the protected internal Admin Panel URL directly in the browser address bar.

## Expected Result

* The user is not granted access to the requested protected Admin Panel page.
* The Admin Login page is displayed.
* The current URL contains `login.php`.
* The current URL contains a `redirect_url` parameter.
* The `redirect_url` parameter contains the originally requested protected Admin Panel URL in encoded form.
