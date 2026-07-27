## TC-ADMIN-AUTH-014 — Account lock after third consecutive failed login attempt

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
* Before executing the test, the administrator account is not locked.
* Before executing the test, the following query returns `2` in the `login_attempts` column:

```sql
SELECT
  `username`,
  `login_attempts`,
  `date_valid_from`,
  `date_valid_to`,
  TIMESTAMPDIFF(MINUTE, `date_valid_to`, `date_valid_from`) AS `lock_duration_minutes`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

Expected precondition database result:

* `username` is `admin_for_locking`;
* `login_attempts` is `2`;
* `date_valid_from` is `NULL`;
* `date_valid_to` is `NULL`;
* `lock_duration_minutes` is `NULL`.

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
* The following message is displayed: "This account has been temporarily blocked for 15 minutes."

## Database Verification

Execute the following query after the third failed login attempt:

```sql
SELECT
  `username`,
  `login_attempts`,
  `date_valid_from`,
  `date_valid_to`,
  TIMESTAMPDIFF(MINUTE, `date_valid_to`, `date_valid_from`) AS `lock_duration_minutes`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

Expected database result:

* `username` is `admin_for_locking`;
* `login_attempts` is reset to `0`;
* `date_valid_to` contains the timestamp until which the account was valid before being locked;
* `date_valid_from` contains the timestamp from which the account becomes valid again;
* `lock_duration_minutes` is `15`.

## Postconditions / Cleanup

* Wait until the 15-minute lock period expires, or reset the account lock state in the database if this is allowed for the test environment.
* Verify that the account is unlocked before executing other authentication tests.
