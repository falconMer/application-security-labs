# 01 Authentication And Task Management

[← Repository overview](../README.md) · [Original PDF report](01-authentication-and-task-management.pdf)

> Privacy note: cookie and token values in the page 5 DevTools screenshot have been redacted. Cookie names, flags, and the authentication explanation are preserved.

> Portfolio text edition derived from the original university lab report provided by Smail Mersad. The original report contains screenshots/figures; this Markdown edition preserves the written technical record without inventing additional evidence or assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

---

## Report page 2

```text
1. Simple Access Token Usage

Generation & Storage

During login , the server generates a simple access token using a 32-byte
random value:
// auth.js
const token = crypto.randomBytes(32).toString('hex');
await db.run('INSERT INTO access_tokens (user_id, token) VALUES (?, ?)',
[user.id, token]);
return { type: 'simple', token };

The token is then:

   ● Returned to the server-side route
   ● Stored inside the database table access_tokens, linked to the user via
      user_id
   ● Sent to the browser as a cookie.

DB schema (from db.js) supports this:

  CREATE TABLE IF NOT EXISTS access_tokens (

    id INTEGER PRIMARY KEY AUTOINCREMENT,

    user_id INTEGER,

    token TEXT,

    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY(user_id) REFERENCES users(id)

  );`);
```

---

## Report page 3

```text
Verification

When a protected page is accessed (/tasks-page, /profile,
/admin/tasks-page), the middleware reads the cookie manually:

// auth.js

const cookieHeader = req.headers['cookie'] || "";

cookieHeader.split(';').forEach(pair => {

  const [key, value] = pair.trim().split('=');

  if (key === 'token') token = value;

});

Then it verifies the token:
// auth.js

const row = await db.get(

      'SELECT users.id, users.username, users.role

      FROM access_tokens

      JOIN users ON users.id = access_tokens.user_id

      WHERE token = ?',

      [token]

);

If valid → the user identity is restored into:
req.user = { id: row.id, username: row.username, role: row.role };

If invalid → redirect to /login.
```

---

## Report page 4

```text
2. Session Cookies & Security
Setting the Cookie

After successful login:
res.setHeader('Set-Cookie', `token=${result.token}; HttpOnly; Path=/;
Max-Age=3600`);

Header name:
 Set-Cookie

Value format:
 token=<tokenvalue>; HttpOnly; Path=/; Max-Age=3600

This header sends a cookie named token to the browser, and the browser stores
it automatically.

The Max-Age=3600 attribute makes the cookie last 1 hour instead of
disappearing when the tab is closed.

HttpOnly Flag

I DID use HttpOnly.

   ● Prevents JavaScript (via XSS) from reading the cookie
   ● Protects the authentication token from attacker scripts
   ● Essential for preventing session hijacking
```

---

## Report page 5

```text
DevTools Evidence

3. Retrieving User Identity

From Token to User ID

Once the simple token is verified, the middleware loads the user with:
req.user = { id: row.id, username: row.username, role: row.role };

This allows all following routes to know exactly which user is authenticated.

SQL Join Example

The exact query used:
 const row = await db.get(

      'SELECT users.id, users.username, users.role

      FROM access_tokens JOIN users ON users.id = access_tokens.user_id

      WHERE token = ?',

      [token]

     );

This ensures every request maps a token → user_id securely.
```

---

## Report page 6

```text
4. Creating Tasks (Ownership)

Setting the Owner

The POST /api/tasks route uses the authenticated identity:

await db.run('INSERT INTO tasks (title, owner_id) VALUES (?, ?)', [title,
req.user.id]);

The frontend sends only the task title:
await fetch('/api/tasks', {

      method: 'POST',

      headers: { "Content-Type": "application/json" },

      body: JSON.stringify({ title })

});

(User ID never comes from the client).

Security Consideration

If the client could send owner_id, a malicious user could do:

{ "title": "Hacked", "owner_id": 1 }

→ Creating tasks under another account.

The code implementation prevents this vulnerability (ID spoofing).
```

---

## Report page 7

```text
5. Listing Tasks (Data Isolation)

Filtering by Owner

Users only see their own tasks:
const task = await db.get('SELECT * FROM tasks WHERE id = ?',
[req.params.id]);

The client UI (user_tasks.html) displays only those tasks:

tasks.forEach(task => {

      const div = document.createElement("div");

      div.className = "task";

      div.innerHTML = `

      <span>${task.title}</span>

      <button onclick="deleteTask(${task.id})">Delete</button>

      `;

      container.appendChild(div);

});

SQL Query
SELECT * FROM tasks WHERE id = ?

This enforces per-user data isolation.
```

---

## Report page 8

```text
6. Protecting Pages (Access Control)

Middleware Logic

All protected routes use:
verifySimpleTokenCookie(() => db)

The middleware verifySimpleTokenCookie protects all pages:

   1. Extract token from cookies
   2. If missing → redirect /login
   3. Validate token against DB
   4. If invalid → redirect /login
   5. Else → attach user to req.user and continue

Code:
if (!token) return res.redirect('/login');

if (!row) return res.redirect('/login');

req.user = { id: row.id, username: row.username, role: row.role };

next();

Additionally:
requireRole('admin')

prevents unauthorized users from accessing admin pages.
```

---

## Report page 9

```text
Implementation

Example from index.js:

app.get('/admin/tasks-page', verifySimpleTokenCookie(() => db),
requireRole('admin'), (req, res) => {

      res.sendFile('admin_tasks.html', { root: './' });

    });

This ensures:

    ● Without a token → cannot access protected pages
    ● With invalid token → redirected to login
    ● Admin-only pages require "admin" role
```
