## TC-ADMIN-AUTH-001 — Login with valid credentials

**Requirement:** REQ-ADMIN-AUTH-003
**Priority:** High
**Type:** Positive
**Automation status:** Planned

### Preconditions

* An active, unlocked administrator account exists.
* Valid administrator credentials are available.
* The administrator is logged out.

### Test Data

* Username: valid administrator username
* Password: valid administrator password
* Remember me: not selected

### Steps

1. Open the Admin Login page.

   * The Admin Login page is displayed.
   * The login form is displayed.

2. Enter the valid administrator username.

   * The username field is editable.
   * The entered username is displayed in the field.

3. Enter the valid administrator password.

   * The password field is editable.
   * The entered password is masked.

4. Leave the "Remember me" option unselected.

5. Click the Login button.

### Expected Result

* The administrator is logged in successfully.
* A success message is displayed: "You are now logged in as admin".
* The Admin Panel main page is displayed.
* The statistics section is displayed.
