## TC-ADMIN-AUTH-009 — Redirect to originally requested protected Admin Panel URL after successful login

**Requirement:** REQ-ADMIN-AUTH-002, REQ-ADMIN-AUTH-003
**Priority:** High
**Type:** Positive
**Automation status:** Planned

## Preconditions

* An active, unlocked administrator account exists.
* Valid administrator credentials are available.
* The administrator is logged out.
* At least one protected internal Admin Panel URL is available for testing.

## Test Data

* Protected internal Admin Panel URL: `/admin/?app=currencies&doc=currencies`
* Username: valid administrator username
* Password: valid administrator password
* Remember me: not selected

## Steps

1. Open the protected internal Admin Panel URL directly in the browser address bar.

   * The Admin Login page is displayed.
   * The login form is displayed.
   * The current URL contains `login.php`.
   * The current URL contains a `redirect_url` parameter.

2. Enter the valid administrator username.

   * The username field is editable.
   * The entered username is displayed in the field.

3. Enter the valid administrator password.

   * The password field is editable.
   * The entered password is masked.

4. Leave the "Remember me" option unselected.

5. Click the Login button.

## Expected Result

* The administrator is logged in successfully.
* A success message is displayed: "You are now logged in as admin".
* The originally requested protected Admin Panel page is displayed.
* The current page is the Currencies page.
* The current URL corresponds to `/admin/?app=currencies&doc=currencies`.
