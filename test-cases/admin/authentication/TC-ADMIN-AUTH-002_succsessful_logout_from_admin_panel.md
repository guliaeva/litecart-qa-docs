# TC-ADMIN-AUTH-002: Successful logout from Admin Panel

## Requirement

**Requirement:** REQ-ADMIN-AUTH-006  
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

## Steps

1. Open the Admin Login page.

   **Expected result:**

   * The Admin Login page is displayed.
   * The login form is displayed.

2. Log in with valid administrator credentials.

   **Expected result:**

   * The administrator is logged in successfully.
   * The Admin Panel main page is displayed.
   * A success message is displayed: “You are now logged in as %administrator username%”.

3. Click the Sign Out button.

   **Expected result:**

   * The administrator is logged out successfully.
   * The Admin Login page is displayed.
   * The login form is displayed.
   * A success message is displayed: “You are now logged out”.

## Expected Result

The administrator can successfully log out from the Admin Panel and is returned to the Admin Login page.

## Postconditions

* No additional postconditions are required.
