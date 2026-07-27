## TC-ADMIN-AUTH-016 — Account is automatically unlocked after lock period

**Requirement:** REQ-ADMIN-AUTH-007
**Priority:** High
**Type:** Positive
**Automation status:** Planned

## Preconditions

* A dedicated administrator account for account lock testing exists.
* The dedicated administrator username is `admin_for_locking`.
* Valid credentials for `admin_for_locking` are available.
* The administrator is logged out.
* The administrator account is temporarily locked after three consecutive failed login attempts.
* Database access is available for verification.
* Before executing the test, the following query confirms that the account is locked:

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
* `login_attempts` is `0`;
* `date_valid_from` contains a future timestamp;
* the account is locked until `date_valid_from`;
* `lock_duration_minutes` is `15` if both `date_valid_to` and `date_valid_from` are present.

## Test Data

* Username: `admin_for_locking`
* Password: valid administrator password
* Remember me: not selected

## Steps

1. Wait until the lock period expires.

   * The current time is later than the unlock time stored in `date_valid_from`.

2. Open the Admin Login page.

   * The Admin Login page is displayed.
   * The login form is displayed.

3. Enter `admin_for_locking` in the username field.

   * The username field is editable.
   * The entered username is displayed in the field.

4. Enter the valid administrator password.

   * The password field is editable.
   * The entered password is masked.

5. Leave the "Remember me" option unselected.

6. Click the Login button.

## Expected Result

* The administrator is logged in successfully.
* A success message is displayed: "You are now logged in as admin".
* The Admin Panel main page is displayed.
* The statistics section is displayed.
* The account is no longer treated as locked.

## Database Verification

Execute the following query after successful login:

```sql
SELECT
  `username`,
  `login_attempts`,
  `date_valid_from`,
  `date_valid_to`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';
```

Expected database result:

* `username` is `admin_for_locking`;
* `login_attempts` is `0`;
* the account is in a valid state.

## Notes

This test is production-safe if the tester waits until the real lock period expires and does not modify the database.

In a non-production test environment, the waiting time may be reduced by updating the unlock timestamp manually:

```sql
UPDATE `lc_users`
SET `date_valid_from` = DATE_ADD(NOW(), INTERVAL 30 SECOND)
WHERE `username` = 'admin_for_locking';
```

After this update, wait until the new `date_valid_from` value has passed and continue with the login steps.

Direct database modification must not be performed in production.

## Postconditions / Cleanup

* Log out from the Admin Panel.
* Verify that `admin_for_locking` is available for further authentication tests.
