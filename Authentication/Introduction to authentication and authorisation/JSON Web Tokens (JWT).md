# JSON Web Tokens (JWT) (Simple Version)

## The Big Idea

After you log in, how does the server remember who you are on the next page?

The answer: a **JSON Web Token (JWT)**. Think of it as a **digital keycard**. The server gives it to you after a successful login, and you show it on every future request instead of typing your password again.

---

## 1. The Four-Step Process

Instead of the server remembering every logged-in user, the **client holds the keycard**.

1. **Login:** The user sends their username and password (or other login details) to the server.
2. **Issue:** The server checks them against what was saved at signup. If correct, it creates a JWT and sends it back.
3. **Storage:** The client stores the JWT, usually in a browser cookie or local storage.
4. **Request:** On every request to a protected route, the client sends the JWT. The server verifies it and grants access.

```
Login → Server issues JWT → Client stores it → Client sends it with every request
```

---

## 2. What a JWT Looks Like

A JWT is a long string made of **three parts separated by two dots**:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3OCIsIm5hbWUiOiJKYW5lIERvZSIsImFkbWluIjp0cnVlLCJpYXQiOjE1MTYyMzkwMjJ9.Lfu39gE9OI8rhPXbmJMorXTtVappkNMw9xq-M4HXttA
```

```
HEADER . PAYLOAD . SIGNATURE
```

| Part | What it contains |
|------|------------------|
| **Header** | The token type (JWT) and the algorithm used to secure it (e.g. HMAC SHA256) |
| **Payload** | The actual data ("claims") about the user, like user ID, username, or role |
| **Signature** | A hash made from the header, payload, and a secret key only the server knows |

---

## 3. Important Security Note

The header and payload are only **encoded (Base64)**, **not encrypted**. Anyone can decode and read them.

**Never put sensitive data in a JWT payload**, such as:

- Raw passwords
- Credit card numbers

Safe to store: user ID, username, role.

---

## 4. How the Signature Protects You

The server creates the signature by mixing the encoded header, the encoded payload, and its **secret key**, then hashing them together.

**What if someone tampers with the token?**

Say a user decodes their token, changes their role from `user` to `admin`, and re-encodes it.

1. The server receives the modified token.
2. It recreates the signature using its secret key.
3. Because the payload changed, the new signature **doesn't match**.
4. The server rejects the request with `401 Unauthorized`.

The user can't fake a valid signature because they don't know the secret key.

---

## 5. Stateless Authentication

JWTs allow **stateless authentication**: the server doesn't need to store session data in a database. It simply trusts the token, because a valid signature proves the server created it.

---

## Easy Way to Remember

- **JWT = a keycard** the server hands you after login.
- **Payload = what's printed on the card** (readable by anyone).
- **Signature = the tamper-proof seal** that only the server can create.

---

## Summary

- A JWT proves your identity after login without re-entering your password.
- It has three parts: **Header, Payload, Signature**.
- The payload is readable, so never store secrets in it.
- The signature stops tampering, and a changed token gets a `401`.
- The server stays stateless, since the token itself carries the proof.
