# Node.js OS Module: A Simple Guide

## What Is the OS Module?

`os` is a core module built into Node.js. It lets your app get information about the **operating system** it's running on, such as:

- OS type and version
- CPU details
- Total and free memory
- Network interfaces
- Current user info

This makes your app more **system-aware**.

## Importing OS

```js
const os = require("os");
```

---

## Quick Reference

| Method | What it tells you |
| --- | --- |
| `platform()` | Which OS you're on (e.g. `darwin`, `win32`, `linux`) |
| `arch()` | CPU architecture (e.g. `arm64`, `x64`) |
| `type()` | Official OS name |
| `release()` | Kernel version number |
| `version()` | Detailed OS version |
| `cpus()` | Info about each CPU core |
| `uptime()` | Seconds since the system booted |
| `totalmem()` | Total memory in bytes |
| `freemem()` | Free memory in bytes |
| `userInfo()` | Current user details |
| `networkInterfaces()` | Network addresses |

---

## System Info Methods

### `platform()`: Which OS Am I On?

Returns the operating system Node is running on:

```js
const os = require("os");
console.log(os.platform()); // darwin
```

Useful for **cross-platform scripts**, where different code runs on different systems:

```js
if (os.platform() === "win32") {
  // Windows specific code
} else {
  // Non-Windows specific code
}
```

### `arch()`: What CPU Architecture?

Returns the CPU architecture Node.js was built for:

```js
const os = require("os");
console.log(os.arch()); // arm64
```

Useful for making sure users download the **correct files** for their system.

Other possible values: `x64`, `arm`, `arm64`, `ia32`, `mips`, `ppc`, and more.

### `type()`: Official OS Name

Returns the OS name so you can identify it in code:

```js
const os = require("os");
console.log(os.type());
// Darwin (the core OS for macOS, iOS, and other Apple products)
```

### `release()`: Kernel Version

The **kernel** is the core part of an OS. It manages system resources and lets hardware and software communicate. `release()` returns its version as a string (like `'20.6.0'`).

Useful for checking compatibility between OS versions and server requirements.

```js
const os = require("os");
console.log(os.release()); // 25.0.0
```

### `version()`: Detailed OS Version

Gives more detail than `release()`:

```js
const os = require("os");
console.log(os.version());
// Darwin Kernel Version 25.0.0: Wed Sep 17 21:41:39 PDT 2025;
// root:xnu-12377.1.9~141/RELEASE_ARM64_T8103
```

---

## Hardware and Resource Methods

### `cpus()`: CPU Core Details

Returns an array with one object per logical CPU core. Useful for **monitoring CPU load**.

```js
const os = require("os");
console.log(os.cpus());

/*
[
 {
   model: 'Apple M1',
   speed: 2400,
   times: { user: 2184260, nice: 0, sys: 1767340, idle: 8344200, irq: 0 }
 },
 {
   model: 'Apple M1',
   speed: 2400,
   times: { user: 2049430, nice: 0, sys: 1641050, idle: 8612980, irq: 0 }
 },
 ...
]
*/
```

Each object shows the CPU model, its speed, and how much time it has spent on different tasks.

### `uptime()`: How Long Has the System Been On?

Returns the time (in seconds) since the system booted. Useful for knowing how long a server has been running.

```js
const os = require("os");
console.log(os.uptime()); // 23047
```

### `totalmem()` and `freemem()`: Memory

- `totalmem()` is the total system memory in bytes
- `freemem()` is the currently free memory in bytes

```js
const os = require("os");
console.log(os.totalmem()); // 8589934592 (8 GB)
console.log(os.freemem()); // 93585408 (87 MB)
```

---

## User and Network Methods

### `userInfo()`: Current User

Returns an object with details about the user running the program:

```js
const os = require("os");
console.log(os.userInfo());

/*
[Object: null prototype] {
 uid: 502,
 gid: 20,
 username: 'user',
 homedir: '/Users/user',
 shell: '/bin/zsh'
}
*/
```

### `networkInterfaces()`: Network Addresses

Returns an object with the network interfaces that have been **assigned an address**:

```js
console.log(os.networkInterfaces());

/*
{
  lo0: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '::1/128',
      scopeid: 0
    }
  ],
  en0: [
    {
      address: '192.168.1.10',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: 'aa:bb:cc:dd:ee:ff',
      internal: false,
      cidr: '192.168.1.10/24'
    },
    {
      address: 'fe80::abcd:1234:5678:9abc',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: 'aa:bb:cc:dd:ee:ff',
      internal: false,
      cidr: 'fe80::abcd:1234:5678:9abc/64',
      scopeid: 2
    }
  ],
  // ...more network interfaces
};
*/
```

A quick guide to reading this:

- `lo0` is the **loopback** interface (your own machine talking to itself, `internal: true`)
- `en0` is your real network connection (Wi-Fi or Ethernet, `internal: false`)
- `family` shows whether the address is **IPv4** or **IPv6**
- `address` is the IP address, and `mac` is the hardware address

---

## Quick Summary

- The `os` module tells your app about the **system it runs on**.
- Use `platform()`, `arch()`, `type()`, `release()`, and `version()` to identify the system.
- Use `cpus()`, `uptime()`, `totalmem()`, and `freemem()` to check **hardware and resource usage**.
- Use `userInfo()` and `networkInterfaces()` for **user and network details**.
