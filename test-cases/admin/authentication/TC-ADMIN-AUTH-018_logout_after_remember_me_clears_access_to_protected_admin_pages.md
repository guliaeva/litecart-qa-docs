# TC-ADMIN-AUTH-018: Log out after using “Remember me” and verify that protected Admin Panel pages are no longer accessible

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
* Protected internal Admin Panel URL: `/admin/?app=currencies&doc=currencies`

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

6. Log out from the Admin Panel.

   **Expected result:**

   * The administrator is logged out successfully.
   * The Admin Login page is displayed.

7. Close the browser.

   **Expected result:**

   * The browser is closed.

8. Reopen the browser and navigate directly to `/admin/?app=currencies&doc=currencies`.

   **Expected result:**

   * The protected Admin Panel page is not opened.
   * The administrator is redirected to the Admin Login page.
   * The login form is displayed.

## Expected Result

After logging out, the remembered session is cleared. The administrator cannot access protected internal Admin Panel pages without logging in again, even if “Remember me” was previously selected.

## Postconditions

* No additional postconditions are required.