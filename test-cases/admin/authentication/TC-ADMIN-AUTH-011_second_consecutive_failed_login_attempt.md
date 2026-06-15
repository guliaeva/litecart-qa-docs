## TC-ADMIN-AUTH-011 — Second consecutive failed login attempt

**Requirement:** REQ-ADMIN-AUTH-007
**Priority:** High
**Type:** Negative
**Automation status:** Planned

## Preconditions

* A dedicated administrator account for account lock testing exists.
* The dedicated administrator username is `admin_for_locking`.
* Valid credentials for `admin_for_locking` are available.
* The valid password for `admin_for_locking` is not `wr0ngP@ssword`.
* The administrator is logged out.
* Database access is available.
* Before executing the test, the following query returns `1`:

```sql
SELECT `login_attempts`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

## Test Data

* Username: `admin_for_locking`
* Password: `wr0ngP@ssword`
* Remember me: not selected

## Steps

1. Open the Admin Login page.

   * The Admin Login page is displayed.
   * The login form is displayed.

2. Enter `admin_for_locking` in the username field.

   * The username field is editable.
   * The entered username is displayed in the field.

3. Enter `wr0ngP@ssword` in the password field.

   * The password field is editable.
   * The entered password is masked.

4. Leave the "Remember me" option unselected.

5. Click the Login button.

## Expected Result

* The administrator is not logged in.
* The Admin Login page remains displayed.
* Access to the Admin Panel is not granted.
* The following message is displayed: "You have 1 login attempt left until your account is temporarily blocked".
* The following database query returns `2`:

```sql
SELECT `login_attempts`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

## Postconditions / Cleanup

* Perform a successful login with valid credentials for `admin_for_locking` to reset the failed login attempts counter.
* Log out from the Admin Panel.
* Optionally verify in the database that `login_attempts` is reset to `0`.
