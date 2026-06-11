# Admin Authentication Checklist

## Scope

This checklist covers authentication and access control checks for the LiteCart Admin Panel.

## Preconditions

* At least one administrator account exists in the system.
* The administrator account is active and not locked.
* Valid administrator credentials are available.
* At least one protected internal Admin Panel URL is known.

## Checklist

### Login

#### Positive cases

* Login with valid username and valid password
* Login with valid username entered in uppercase and valid password

#### Negative cases

* Login with invalid username and valid password
* Login with valid username and invalid password
* Login with valid username and valid password entered in uppercase
* Login with username entered using an incorrect keyboard layout and valid password
* Login with valid username and password entered using an incorrect keyboard layout

### Access Control

* Access protected internal Admin Panel URL without authentication
* Redirect to originally requested protected Admin Panel URL after successful login

### Failed Login Attempts and Account Lock

* Login with invalid credentials for the first time and verify that the message indicates 2 attempts remaining
* Login with invalid credentials for the second consecutive time and verify that the message indicates 1 attempt remaining
* Login with invalid credentials for the third consecutive time and verify that the administrator account is temporarily locked
* Attempt to log in with valid credentials while the administrator account is locked
* Login successfully on the third attempt after two consecutive failed login attempts
* After two failed login attempts followed by a successful login and logout, perform one new failed login attempt and verify that the message indicates 2 attempts remaining
* Verify that a locked administrator account is automatically unlocked after the configured lock period

### Remember Me

* Login with valid administrator credentials and the "Remember me" option selected
* Access a protected internal Admin Panel URL after closing and reopening the browser without logging out
* Open the `/admin/` URL with an active remembered session and verify that the Admin Login page is displayed with a message indicating that the administrator is already logged in
* Log out after using "Remember me" and verify that protected internal Admin Panel pages are no longer accessible without a new login
* Clear browser cookies after using "Remember me" and verify that protected internal Admin Panel pages are no longer accessible without a new login

### Logout

* Logout from the Admin Panel
* Access protected internal Admin Panel URL after logout and verify that a new login is required
