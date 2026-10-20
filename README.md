# VME

VME includes a browser frontend and a Node.js backend with SQLite-backed user accounts, scrypt password hashing, email verification, and secure HTTP-only sessions.

- `frontend/` contains the HTML, CSS, and browser JavaScript.
- `backend/` contains the HTTP server and authentication service.
- User records and sessions are stored in `backend/data/vme.sqlite`.

## Configure email

Registration verification and password reset codes are sent through your SMTP provider. Copy `.env.example` to `.env` and replace the SMTP placeholders with credentials from your provider. Keep `.env` private; it is ignored by Git.

```powershell
Copy-Item .env.example .env
```

If SMTP is not configured, the app still starts, but sign-up and password-reset requests return an explicit configuration error rather than pretending an email was sent.

## Install and run

Use Node.js 22.13 or later. From the project root:

```powershell
npm install
npm start
```

Open <http://localhost:3000>. The backend creates the SQLite database and a private authentication secret on first start. Back up `backend/data/` securely; it contains account data and the secret needed to verify email codes.

## Authentication

- Register with an email address, phone number, account role, and password of at least 12 characters.
- Enter the one-time code sent to that email to verify the account and sign in.
- Sessions use random, server-stored tokens in HTTP-only, same-site cookies. “Remember me” keeps a session for seven days; otherwise it expires after 12 hours and the browser cookie is cleared when the browser session ends.
- Password reset codes are emailed, expire after ten minutes, and invalidate existing sessions when the password changes.

Run the authentication integration test with:

```powershell
npm test
```
