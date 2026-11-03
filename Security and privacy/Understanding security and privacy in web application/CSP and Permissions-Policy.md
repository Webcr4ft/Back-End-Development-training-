# CSP and Permissions-Policy

## Overview

**CSP (Content Security Policy)** and **Permissions-Policy** are HTTP security headers. They protect web applications by restricting **what resources can load** and **what browser features a page can access**.

| | **CSP** | **Permissions-Policy** |
|---|---|---|
| **Controls** | Which resources can load | Which browser features and hardware can be used |
| **Main protection** | Cross-Site Scripting (XSS) and code injection | Abuse of device features and user privacy |
| **Works by** | Whitelisting trusted source domains | Enabling or disabling features per origin |
| **Example target** | Scripts, styles, images, forms | Camera, microphone, geolocation |
| **Replaced** | Not applicable | The older `Feature-Policy` header |

---

## 1. Content Security Policy (CSP)

CSP acts as a **safety filter** for your frontend scripts, styles, and images.

### The problem it solves

Attackers often try to inject harmful scripts into vulnerable websites (**Cross-Site Scripting, or XSS**). A strong CSP stops this by setting a **strict whitelist of trusted source domains**.

### How it works

1. The server sends the CSP header with the response.
2. The browser reads the **directives** (the individual rules).
3. The browser only allows resources that match the policy.
4. If something violates the policy, the browser **drops it instantly** and **logs a security error**.

**Example:** The `script-src` directive tells the browser which domains may run JavaScript on the page. If a hacker injects a script from an unapproved external server, the browser blocks it.

### What CSP can restrict

- Script sources
- Image sources
- Form destinations
- Stylesheet origins

### Example

```http
Content-Security-Policy: script-src 'self' https://trusted-cdn.com; img-src 'self'
```

| Part | Meaning |
|---|---|
| `script-src 'self' https://trusted-cdn.com` | JavaScript may only load from your own domain and `trusted-cdn.com` |
| `img-src 'self'` | Images may only load from your own domain |

---

## 2. Permissions-Policy

Permissions-Policy controls **browser features and device hardware**. It replaced the older `Feature-Policy` header.

Site owners can explicitly **enable or disable features** for their own page and for any **embedded iframes**. This prevents third-party snippets from abusing user privacy.

### What it can control

- Webcam
- Microphone
- Geolocation tracking

### Why it matters

Suppose your site does not need the user's location, so you block the geolocation API. Even if an attacker **compromises a script on your page**, the browser **refuses to activate** the tracking feature.

### Syntax

The header names the **feature** and defines its **allowed origins**.

| Syntax | Meaning |
|---|---|
| `camera=(self)` | Camera allowed **only on your own domain** |
| `geolocation=()` | Geolocation **disabled for everyone** on the page (empty list) |

### Example

```http
Permissions-Policy: camera=(self), microphone=(self), geolocation=()
```

| Part | Meaning |
|---|---|
| `camera=(self)` | Only your own domain can use the camera |
| `microphone=(self)` | Only your own domain can use the microphone |
| `geolocation=()` | No one can use geolocation |

---

## 3. Using Both Together

| Header | Role |
|---|---|
| **CSP** | Locks down **data delivery** and prevents **code injection** |
| **Permissions-Policy** | Guards the **physical device** and ensures **privacy compliance** |

Modern web developers use both to create a **heavily fortified browsing environment**.

---

## Key Takeaways

- **CSP** whitelists trusted sources so the browser blocks injected scripts (XSS).
- **Directives** like `script-src` define the rules for each resource type.
- **Permissions-Policy** enables or disables features such as the camera, microphone, and geolocation.
- Use `(self)` to limit a feature to your own domain, and `()` to disable it completely.
- CSP protects **what loads**. Permissions-Policy protects **what the page can do**.
- Use **both** for layered defense.

---

## Questions

*(Add your questions here.)*
