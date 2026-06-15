## TC-ADMIN-AUTH-012 — Login successfully after two consecutive failed login attempts

**Requirement:** REQ-ADMIN-AUTH-007, REQ-ADMIN-AUTH-008
**Priority:** High
**Type:** Positive
**Automation status:** Planned

## Preconditions

* A dedicated administrator account for account lock testing exists.
* The dedicated administrator username is `admin_for_locking`.
* Valid credentials for `admin_for_locking` are available.
* The administrator is logged out.
* Database access is available.
* Before executing the test, the following query returns `2`:

```sql
SELECT `login_attempts`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

## Test Data

* Username: `admin_for_locking`
* Password: valid administrator password
* Remember me: not selected

## Steps

1. Open the Admin Login page.

   * The Admin Login page is displayed.
   * The login form is displayed.

2. Enter `admin_for_locking` in the username field.

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
* The Admin Panel main page is displayed.
* The statistics section is displayed.
* The following database query returns `0`:

```sql
SELECT `login_attempts`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

## Postconditions / Cleanup

* Log out from the Admin Panel.
