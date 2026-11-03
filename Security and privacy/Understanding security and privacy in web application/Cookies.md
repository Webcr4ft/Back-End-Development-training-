# Cookies

## Overview

**Cookies** are small text files that websites save on your device to remember information about you. They make the web feel "stateful": without them, a site would treat every request as coming from a stranger.

---

## 1. How Cookies Are Set and Sent

1. You visit a website.
2. The website server includes a `Set-Cookie` header in its response.
3. Your browser receives the header and saves the cookie on your computer's hard drive.
4. On every later visit to that site, your browser **automatically sends the cookie back** to the server.

```http
# Server response
HTTP/1.1 200 OK
Set-Cookie: session=abc123

# Browser's next request to the same site
GET /dashboard HTTP/1.1
Cookie: session=abc123
```

### What cookies are used for

- **Login sessions:** keeping you signed in as you move between pages
- **Shopping carts:** remembering items you added
- **Preferences and settings:** language, theme, layout
- **Other critical information** the site needs between requests

---

## 2. Security Risks of Cookie Storage

Because cookies are stored locally on your device, they can be stolen:

- A hacker with **physical access** to your device can read them.
- **Malware** can read your local files and extract them.

> **Why this is serious:** A stolen **session cookie** lets an attacker log into your account from a completely different computer **without knowing your password**. The server sees a valid session cookie and assumes the request is from you.

---

## 3. Protecting Cookies with Security Flags

Developers add **flags** (attributes) when setting a cookie to reduce the risk of theft and abuse.

| Flag | What it does | Attack it helps prevent |
|---|---|---|
| `HttpOnly` | Blocks JavaScript from reading the cookie | Session token theft through **Cross-Site Scripting (XSS)** |
| `Secure` | Browser only sends the cookie over encrypted **HTTPS** connections | Cookie sniffing on public Wi-Fi and similar situations |
| `SameSite` | Restricts sending the cookie during cross-site requests | **Cross-Site Request Forgery (CSRF)** |

### `HttpOnly`

Even if an attacker injects malicious JavaScript into a page (XSS), that script **cannot read** the cookie. This protects session tokens.

### `Secure`

The cookie is never sent over plain HTTP, where it could be intercepted. This pairs with HTTPS to keep cookies encrypted in transit.

### `SameSite`

Controls whether the cookie is sent when a request originates from a **different site**. It has two common values:

| Value | Behavior |
|---|---|
| `SameSite=Strict` | The browser **never** sends the cookie on any cross-site request |
| `SameSite=Lax` | The browser sends the cookie on **safe top-level navigation** (for example, clicking a link to the site). It blocks the cookie on cross-site **form submissions** and **API requests** |

> **Strict vs. Lax:** Strict is the most protective. Lax is a balance: users arriving via a normal link stay logged in, but cross-site forms and API calls cannot use the cookie.

### Putting it together

```http
Set-Cookie: session=abc123; HttpOnly; Secure; SameSite=Strict
```

---

## 4. Third-Party Tracking

Cookies also raise major **privacy** concerns, depending on who sets them.

| Type | What it tracks |
|---|---|
| **First-party cookie** | Your actions **only on the specific site you chose to visit** |
| **Third-party cookie** | Your actions **across entirely different websites** |

### How cross-site tracking works

1. Advertising networks place third-party cookies on **thousands of popular sites**.
2. As you browse, the ad network reads **the same cookie** again and again on each of those sites.
3. Over time, it builds a detailed profile of your:
   - Personal interests
   - Search history
   - Online habits

> **Why it matters:** This tracking is invisible. It lets corporations monitor your digital life **without your active knowledge**.

---

## 5. Laws and Default Protections

| Protection | How it helps |
|---|---|
| **Privacy laws (e.g., GDPR)** | Require websites to show **cookie consent banners** so you know what cookies a site is setting |
| **Legal right to refuse** | You can **reject tracking cookies** |
| **Modern browsers** | **Block third-party tracking cookies by default**, giving automatic privacy protection |

---

## Key Takeaways

- **Cookies** are small files that let websites remember you across requests.
- **The risk:** a stolen session cookie gives an attacker access to your account without your password.
- **The defense:** use `HttpOnly` (blocks JavaScript access), `Secure` (HTTPS only), and `SameSite` (limits cross-site sending).
- **The privacy issue:** third-party cookies track you across many sites to build profiles.
- **The safeguards:** laws like GDPR require consent banners, and browsers now block third-party tracking cookies by default.

---

## Questions

*(Add your questions here.)*
