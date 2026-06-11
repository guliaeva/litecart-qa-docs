# Admin Authentication Requirements

## Scope

This document describes authentication and access control requirements for the LiteCart Admin Panel.

## Preconditions

- At least one administrator account exists in the system.
- The administrator account is active and not locked.

## Requirements

### REQ-ADMIN-AUTH-001 — Access to the Admin Panel

The Admin Panel shall be accessible only to authenticated administrator users.
Unauthenticated users shall not be able to access protected Admin Panel pages.
Priority: High

---

### REQ-ADMIN-AUTH-002 — Redirect to the Admin Login page

The system shall redirect unauthenticated users to the Admin Login page when they try to access a protected Admin Panel URL.
This can be verified by opening a protected Admin Panel page without an active session.
Priority: High

---

### REQ-ADMIN-AUTH-003 — Login with valid credentials

The system shall allow an administrator to log in using valid credentials.
Valid username and valid password are required.
Priority: High

---

### REQ-ADMIN-AUTH-004 — Login with invalid credentials

The system shall not allow login with invalid credentials.
Invalid username and/or invalid password shall not grant access to the Admin Panel.
Priority: High

---

### REQ-ADMIN-AUTH-005 — Password case sensitivity

The system shall treat the password as case-sensitive.
A password entered with a different letter case shall not be accepted.
Priority: High

---

### REQ-ADMIN-AUTH-006 — Username case sensitivity

The system shall treat the administrator username as case-insensitive.
The administrator shall be able to log in when the username is entered using a different letter case, provided that the password is valid.
Priority: Medium

---

### REQ-ADMIN-AUTH-007 — Failed login attempts limit

The system shall temporarily lock the administrator account after three consecutive failed login attempts.
The locked account shall not be able to log in until the lock period expires or the account is unlocked.
Priority: High

---

### REQ-ADMIN-AUTH-008 — Failed login attempts reset after successful login

The system shall reset the failed login attempts counter after a successful login.
If an administrator enters invalid credentials and then successfully logs in with valid credentials, previous failed attempts shall not be counted toward the next account lock.
Priority: High

---

### REQ-ADMIN-AUTH-010 — Remember me authentication persistence

The system shall keep the administrator authenticated after the browser session is closed if the "Remember me" option was selected during login.
The remembered authentication shall remain active until the administrator explicitly logs out or until the remember-me session expires according to the application session policy.
When the administrator opens a protected internal Admin Panel page with an active remembered session, access shall be granted without requiring a new login.
Priority: Medium

## Observed Behavior

The `/admin/` URL displays the Admin Login page even if the administrator has an active remembered session.
When an authenticated administrator opens `/admin/`, the system displays a message indicating that the administrator is already logged in.
Protected internal Admin Panel URLs remain accessible without a new login until the administrator explicitly logs out.

---

### REQ-ADMIN-AUTH-009 — Logout

The system shall allow an authenticated administrator to log out.
After logout, the administrator shall no longer have access to protected Admin Panel pages without logging in again.
Priority: High

---

### Open Questions

OQ-ADMIN-AUTH-001 — Account lock duration
The duration of the temporary account lock after three failed login attempts is currently unknown.
Status: To be verified


