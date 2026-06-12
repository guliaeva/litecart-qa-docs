## TC-ADMIN-AUTH-007 — Login with password in incorrect keyboard layout

**Requirement:** REQ-ADMIN-AUTH-004
**Priority:** Low
**Type:** Negative
**Automation status:** Planned

## Preconditions

* An active, unlocked administrator account exists.
* Valid administrator credentials are available.
* The administrator is logged out.
* The password entered using an incorrect keyboard layout is not equal to the actual administrator password.
* The `login_attempt` counter is reset before the test.

## Test Data

* Username: valid administrator username
* Password: valid administrator password entered using an incorrect keyboard layout
* Remember me: not selected

## Steps

1. Open the Admin Login page.

   * The Admin Login page is displayed.
   * The login form is displayed.

2. Enter the valid administrator username.

   * The username field is editable.
   * The entered username is displayed in the field.

3. Enter the valid administrator password using an incorrect keyboard layout.

   * The password field is editable.
   * The entered password is masked.

4. Leave the "Remember me" option unselected.

5. Click the Login button.

## Expected Result

* The administrator is not logged in.
* The Admin Login page remains displayed.
* Access to the Admin Panel is not granted.
* The following message is displayed: "You have 2 login attempts left until your account is temporarily blocked".

## Additional Verification

* Optionally verify in the database that the `login_attempt` counter is increased after the failed login attempt.

## Postconditions / Cleanup

* Perform a successful login with valid administrator credentials to reset the failed login attempts counter.
* Log out from the Admin Panel.
