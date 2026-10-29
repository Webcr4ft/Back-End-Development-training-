# Node.js Crypto Module: A Simple Guide

## What Is the Crypto Module?

`crypto` is a core module built into Node.js. It gives you tools for:

- **Hashing** (turning data into a fixed "fingerprint")
- **Encryption and decryption** (scrambling and unscrambling data)
- **Digital signatures** (proving who sent data)
- **Random values** (secure tokens, keys, numbers)

> **Important:** `crypto` gives you low-level building blocks, not ready-made security. Writing your own encryption or login code is risky. In real projects, use trusted libraries like **bcrypt** (password hashing) or **jsonwebtoken** (logins and tokens).

Still, it's useful to understand how the methods work.

## Importing Crypto

```js
const crypto = require("crypto");
```

The methods fall into two groups:

1. **Data transformation:** hashing, encrypting, signing
2. **Keys and randomness:** random values and secrets

---

## Part 1: Hashing and Encrypting Data

### `createHash()`: One-Way Fingerprint

Takes an algorithm like `sha256`, `sha512`, or `md5` and turns data into a hash. It's **one-way**, so you can't reverse it back to the original.

Good for: hashing passwords and fingerprinting files.

The steps:

1. Pick an algorithm
2. Feed in data with `update()`
3. Get the result with `digest()` and an encoding

```js
const crypto = require("crypto");

const hashedPassword = crypto
  .createHash("sha256")
  .update("myStrongPassword")
  .digest("hex");

console.log("createHash result:", hashedPassword);
// createHash result: f92c9cfa0ead1bcec05ca75888a4074ba994ad237e5e2a8c7cc6a620378c061d
```

### `createHmac()`: Hash With a Secret Key

Works like `createHash()`, but also takes a **secret key**. Only someone with that key can verify the hash.

Good for: authentication and checking that data hasn't been changed.

```js
const crypto = require("crypto");

const hashedMessage = crypto
  .createHmac("sha256", "secretkey")
  .update("important-secret-message")
  .digest("hex");

console.log("createHmac result:", hashedMessage);
// createHmac result: da48d6f026b6036286b1fb872c63264130d5cc4271f3a213bb6ddca5a023e77e
```

### `createCipheriv()` and `createDecipheriv()`: Encrypt and Decrypt

These lock and unlock data. Both take three things:

| Input | What it is |
| --- | --- |
| `algorithm` | The encryption method (e.g. `aes-256-cbc`) |
| `key` | The secret used to lock and unlock |
| `iv` | A block of random or unique data used at the start of encryption |

```js
createCipheriv(algorithm, key, iv);
createDecipheriv(algorithm, key, iv);
```

To decrypt, you need the **same key**. With the wrong key, you'll get an error or unreadable gibberish.

Here's a full example:

```js
const crypto = require("crypto");

// Key length must match the algorithm. AES-256 needs 32 bytes
const key = Buffer.from("12345678901234567890123456789012");

// IV for AES is 16 bytes (fixed here just for the demo)
const iv = Buffer.from("1234567890123456");

// Encrypt
const cipher = crypto.createCipheriv("aes-256-cbc", key, iv);
let encrypted = cipher.update("Hello campers!", "utf8", "hex");
encrypted += cipher.final("hex");

console.log("Encrypted data:", encrypted);
// Encrypted data: 4ee93aa398ab44e3540e4a67ca96bc8c

// Decrypt
const decipher = crypto.createDecipheriv("aes-256-cbc", key, iv);
let decrypted = decipher.update(encrypted, "hex", "utf8");
decrypted += decipher.final("utf8");

console.log("Decrypted data:", decrypted);
// Decrypted data: Hello campers!
```

### `sign()` and `verify()`: Digital Signatures

- `sign()` creates a signature from data using a **private key**. It proves the data came from the key's owner and wasn't tampered with.
- `verify()` checks that signature. It fails if the data or signature doesn't match.

---

## Part 2: Random Values and Secrets

### `randomBytes()`: Secure Random Data

Takes a size and generates **cryptographically secure** random bytes. Use it for tokens and keys instead of `Math.random()`, which is **not secure**.

```js
console.log("Random Bytes:", crypto.randomBytes(16));
// Random Bytes: <Buffer 01 88 aa 1e 2c 38 48 39 26 e1 6b a9 d8 c5 ed 49>
```

The output is a Buffer. Convert it to a readable string with `toString()`:

```js
console.log("Random Bytes:", crypto.randomBytes(16).toString("hex"));
// Random Bytes: a6154ef5a296fa176ad0f332bd94d712
```

`"hex"` tells Node to write the bytes as a hexadecimal string.

### `randomInt()`: Secure Random Number

Takes a min and max and returns a secure random integer between them. Good for OTPs (one-time passwords) and random selection.

```js
console.log("Random Int:", crypto.randomInt(0, 100)); // 89
```

Unlike `Math.random()`, attackers can't predict the result.

### `createSecretKey()`: Make a Secret Key

Takes a buffer and wraps it in a `KeyObject`:

```js
const crypto = require("crypto");

const secret = crypto.createSecretKey(crypto.randomBytes(32));
console.log(secret);
// SecretKeyObject [KeyObject] { [Symbol(kKeyType)]: 'secret' }
```

Use `export()` to get the raw bytes back:

```js
const secret = crypto.createSecretKey(crypto.randomBytes(32));
console.log(secret.export());
// <Buffer 53 06 a1 c7 75 69 8b 38 8b a4 b2 f7 1b bc b8 ...>
```

Then use `toString()` to see it as text:

```js
const secret = crypto.createSecretKey(crypto.randomBytes(32));
console.log(secret.export().toString("hex"));
// 32dfe5917668580160986f1623bf8152913329c71163be9c3404a110cd78efd6
```

---

## Other Useful Methods

- `createPublicKey()` and `createPrivateKey()`: work with keys generated elsewhere
- `createDiffieHellman()`: lets two parties create a shared secret without sending the secret directly
- `Certificate()`: works with HTTPS certificates (parse, export, and verify their contents)

---

## Quick Summary

| Goal | Method |
| --- | --- |
| One-way fingerprint | `createHash()` |
| Fingerprint with a secret key | `createHmac()` |
| Encrypt data | `createCipheriv()` |
| Decrypt data | `createDecipheriv()` |
| Sign and verify data | `sign()` / `verify()` |
| Secure random bytes | `randomBytes()` |
| Secure random number | `randomInt()` |
| Create a secret key | `createSecretKey()` |

**Remember:** for real apps, prefer trusted libraries like bcrypt and jsonwebtoken over writing your own security code.
