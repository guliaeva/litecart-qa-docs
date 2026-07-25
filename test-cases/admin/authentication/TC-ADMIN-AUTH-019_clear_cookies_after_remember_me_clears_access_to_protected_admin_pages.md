# TC-ADMIN-AUTH-019: Clear browser cookies after using “Remember me” and verify that protected Admin Panel pages are no longer accessible

## Requirement

**Requirement:** REQ-ADMIN-AUTH-009  
**Priority:** Medium  
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

6. Close the browser without logging out.

   **Expected result:**

   * The browser is closed.
   * The administrator does not explicitly log out.

7. Reopen the browser.

   **Expected result:**

   * A new browser session is started.

8. Clear browser cookies.

   **Expected result:**

   * Browser cookies are cleared successfully.

9. Navigate directly to `/admin/?app=currencies&doc=currencies`.

   **Expected result:**

   * The protected Admin Panel page is not opened.
   * The administrator is redirected to the Admin Login page.
   * The login form is displayed.

## Expected Result

After browser cookies are cleared, the remembered session is removed. The administrator cannot access protected internal Admin Panel pages without logging in again.

## Postconditions

* No additional postconditions are required.