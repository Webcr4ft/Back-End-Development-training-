# Cross-Site Request Forgery (CSRF) (Simple Version)

## The Big Idea

Browsers **automatically attach cookies** to every request sent to a site. That's convenient, but it creates a weakness.

**CSRF** is an attack where a malicious website tricks your browser into sending a fake request to a site where you're already logged in. The server sees your valid cookie and assumes **you** made the request on purpose.

---

## 1. A CSRF Example: The Bank Attack

1. **The Setup:** You log into `trusted-bank.com`. The bank stores a session token in your browser cookie.
2. **The Trap:** Without logging out, you open a new tab and visit `evil-hacker-site.com`.
3. **The Trigger:** That site has a hidden script or form that automatically sends a request to the bank:

   ```
   POST trusted-bank.com/transfer?amount=1000&to=hacker
   ```

4. **The Execution:** Your browser automatically attaches your bank cookie to the request. The bank sees a valid session, assumes it was you, and **transfers the money**.

```
You (logged in) → Visit evil site → Evil site triggers request to bank
→ Browser adds your cookie → Bank trusts it → Money sent
```

### Key takeaway

The malicious site **cannot read your cookie or steal your data**. It just piggybacks on the fact that your browser **automatically sends cookies** to the target server.

---

## 2. Defending Against CSRF

There are two main defenses:

1. The `SameSite` cookie attribute
2. CSRF tokens

---

## 3. Defense #1: The `SameSite` Cookie Attribute

The simplest defense. It tells the browser **when it's allowed to send the cookie** on cross-site requests.

| Setting | Behavior |
|---------|----------|
| `SameSite=Strict` | The cookie is **never** sent if the request comes from a third-party website |
| `SameSite=Lax` | The cookie is sent only on safe navigation (like clicking a normal link), but **blocked** on cross-site form submissions and API requests |

---

## 4. Defense #2: CSRF Tokens

This is the stronger, more robust option.

1. When a user loads a page, the backend generates a **random, unique, unpredictable token**.
2. The token is attached to the frontend form or the user's session.
3. When the client submits a request, it must include the token in a **custom header or form data**.
4. The backend **compares** the submitted token with the one saved in the session.

**Why it works:** A malicious website can't access your frontend, so it can't copy the secret token. Any forged request will be **missing the token and fail validation**.

```
Real request:   Cookie ✅ + Token ✅ → Allowed
Forged request: Cookie ✅ + Token ❌ → Rejected
```

---

## Easy Way to Remember

- **CSRF is like a forged signature on a check.** The bank sees your real account and processes it, even though you never wrote it.
- **SameSite** controls when the browser is allowed to send your cookie.
- **CSRF tokens** are a secret code that only your real site knows.

---

## Summary

- CSRF tricks your browser into making unwanted requests while you're logged in.
- It works because browsers **automatically send cookies**.
- Defend with `SameSite` cookies (simple) and CSRF tokens (robust).
- Together, they make sure requests are **intentional actions by the real user**.
