# TC-ADMIN-AUTH-019: Open the Admin Login page with an active remembered session

## Requirement

**Requirement:** REQ-ADMIN-AUTH-009  
**Priority:** High  
**Type:** Positive  
**Automation status:** Planned

## Preconditions

* An active, unlocked administrator account exists.
* Valid administrator credentials are available.
* The administrator is logged out.

## Test Data

* Username: valid administrator username
* Password: valid administrator password
* Remember me: selected
* Admin URL: `/admin/`

## Steps

1. Open the Admin Login page.

   **Expected result:**

   * The Admin Login page is displayed.
   * The login form is displayed.

2. Enter the valid administrator username.

   **Expected result:**

   * The username field accepts the entered value.
   * The entered username is displayed in the field.

3. Enter the valid administrator password.

   **Expected result:**

   * The password field accepts the entered value.
   * The entered password is masked.

4. Select the “Remember me” checkbox.

   **Expected result:**

   * The “Remember me” checkbox is selected.

5. Click the Login button.

   **Expected result:**

   * The administrator is logged in successfully.
   * The Admin Panel main page is displayed.
   * A success message is displayed: “You are now logged in as admin”.

6. Close the browser without logging out.

   **Expected result:**

   * The browser is closed.
   * The administrator does not explicitly log out.

7. Reopen the browser and navigate to `/admin/`.

   **Expected result:**

   * The Admin Login page is displayed.
   * A message is displayed indicating that the administrator is already logged in.
   * The login form is displayed.

## Expected Result

When an administrator opens `/admin/` with an active remembered session, the Admin Login page is displayed with a message indicating that the administrator is already logged in.

## Postconditions

* Log out from the Admin Panel.