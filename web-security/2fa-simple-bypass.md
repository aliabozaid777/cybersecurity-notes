# 2FA Simple Bypass — Lab Summary

> **Platform:** PortSwigger Web Security Academy  
> **Category:** Authentication / Multi-Factor Authentication  
> **Status:** Solved  
> **Environment:** Authorized training lab only

## Overview

This lab demonstrated a logic flaw in the two-factor authentication process.

After entering valid username and password credentials, the application displayed a page asking for a 2FA code. However, the application did not properly enforce the second authentication step before allowing access to the account page.

## Vulnerability

The application trusted that users would complete the 2FA page normally, but it did not verify the 2FA status when the protected page was requested directly.

The vulnerable flow was:

```text
/login → /login2 → /my-account
```

The application allowed direct access to:

```text
/my-account
```

without confirming that the 2FA step had been completed.

## Lab Steps

1. Logged in using the provided lab credentials.
2. Reached the 2FA verification page at `/login2`.
3. Did not submit a valid 2FA code.
4. Changed the URL manually to:

```text
/my-account
```

5. Accessed the account page and completed the lab.

## Impact

An attacker who knows or obtains a valid username and password could bypass the second authentication factor.

Possible consequences include:

- Unauthorized account access
- Account takeover
- Exposure of sensitive user information
- Reduced effectiveness of multi-factor authentication

## Root Cause

The server did not verify the user's 2FA authentication state before returning the protected account page.

The second authentication step was enforced only in the normal user interface flow, not on the server side for every protected request.

## Recommended Fix

The server should:

- Store the 2FA verification state in the user session.
- Verify that state before allowing access to protected pages.
- Redirect unverified users back to the 2FA page.
- Apply authorization checks on every sensitive endpoint.
- Avoid relying only on page navigation or hidden links.

Example secure logic:

```text
if password_verified is false:
    redirect to /login

if two_factor_verified is false:
    redirect to /login2

allow access to /my-account
```

## Key Lesson

A security control is effective only when it is enforced by the server.

Displaying a 2FA page is not enough. Every protected request must verify that the user successfully completed all required authentication steps.

## Tools Used

- Burp Suite Community Edition
- Proxy HTTP History
- Repeater
- Intruder for testing request behavior
- PortSwigger Web Security Academy

## HTTP Status Codes Observed

During testing:

- `200 OK` did not always mean authentication succeeded.
- `400 Bad Request` indicated a malformed request or missing parameter.
- `500 Internal Server Error` indicated that the request or session state was not handled correctly.

The response body must always be reviewed instead of relying only on the status code.

## Ethical Note

This test was performed only inside an authorized PortSwigger training lab.

Do not test authentication bypasses, brute-force attacks, or account access techniques against real websites without explicit permission.
