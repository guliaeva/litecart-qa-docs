## TC-ADMIN-AUTH-014 — Login with valid credentials while account is locked

**Requirement:** REQ-ADMIN-AUTH-007  
**Priority:** High  
**Type:** Negative  
**Automation status:** Planned

## Preconditions

- A dedicated administrator account for account lock testing exists.
- The dedicated administrator username is `admin_for_locking`.
- Valid credentials for `admin_for_locking` are available.
- The administrator is logged out.
- Database access is available.
- The administrator account is temporarily locked.
- Before executing the test, the following query confirms that the account is locked:

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

## Expected precondition database result:

- username is `admin_for_locking`;
- login_attempts is `0`;
- `date_valid_from` contains a future timestamp;
- the account is locked until `date_valid_from`;
- `lock_duration_minutes` is `15` 

## Test Data

- Username: `admin_for_locking`
- Password: valid administrator password
- Remember me: not selected

##Steps 

1 Open the Admin Login page.


*The Admin Login page is displayed.
*The login form is displayed.


2 Enter admin_for_locking in the username field.
*The username field is editable.
*The entered username is displayed in the field.
3 Enter the valid administrator password.
*The password field is editable.
*The entered password is masked.
4 Leave the "Remember me" option unselected.
5 Click the Login button.

## Expected Result
- The administrator is not logged in.
- The Admin Login page remains displayed.
- Access to the Admin Panel is not granted.
- The following message is displayed: "The account is blocked until <unlock date and time>".
- The unlock date and time displayed in the message match the date_valid_from value stored in the database.
- The locked account cannot be used for login until the lock period expires or the account is unlocked.

## Database Verification

Execute the following query after the login attempt with valid credentials:

SELECT
  `username`,
  `login_attempts`,
  `date_valid_from`,
  `date_valid_to`,
  TIMESTAMPDIFF(MINUTE, `date_valid_to`, `date_valid_from`) AS `lock_duration_minutes`
FROM `lc_users`
WHERE `username` = 'admin_for_locking';

Expected database result:

username is admin_for_locking;
- login_attempts remains `0`;
- date_valid_from still contains a future timestamp;
- the unlock date and time displayed in the UI message match date_valid_from;
- the account remains locked until date_valid_from.


##Notes

- Example blocking message: `"The account is blocked until Jun 15 2026 12:08 PM".`
- When the account is locked, the same blocking message is displayed regardless of whether the entered password is valid or invalid.


## Postconditions / Cleanup
Wait until the 15-minute lock period expires, or reset the account lock state in the database if this is allowed for the test environment.
Verify that the account is unlocked before executing other authentication tests.