# What Is DNS and How Does It Work? (A High-Level Overview)

## Domain Names

When you visit a website, the first thing you do is type in a web address in your browser.

For example, to go to freeCodeCamp, you would enter `freecodecamp.org` in your browser's address bar.

This is known as a **domain name**. It's a unique human-readable identifier for that resource on the internet.

Domain names are very closely related to the concept of **DNS**, which is the main topic of this lesson. Let's start by talking a little bit about the domain name hierarchy, so you can understand how a DNS works behind the scenes.

---

## The Domain Name Hierarchy

The domain name hierarchy is read **from right to left**, moving from the most general category to the most specific one.

The main structure of a domain name is, from right to left:

| Level | Name | Description | Example in `freecodecamp.org` |
| ----- | ---- | ----------- | ----------------------------- |
| 1 | **Top-Level Domain (TLD)** | The last segment of the domain name, located to the right. Other examples include `.com` and `.edu`. | `.org` |
| 2 | **Second-Level Domain (SLD)** | The name registered by the person or organization. This is what you usually notice first when you see a web address. | `freecodecamp` |
| 3 | **Third-Level Domain (Subdomain)** | Used to identify a specific section of the main domain. | `www` |

About subdomains: `www` stands for "World Wide Web." Nowadays, modern web servers automatically handle domain routing, so you can access a website with or without entering `www`. Other examples of subdomains include `blog.`, `shop.`, `support.`, and `api.`.

```
   www  .  freecodecamp  .  org
    │          │            │
Subdomain     SLD          TLD
(3rd level) (2nd level)  (1st level)

 <───────── read right to left ─────────
   most specific          most general
```

---

## Domain Names vs. IP Addresses

Domain names are very helpful to us as humans because they're easy to remember and type into a browser. However, as you know, **computers work with numbers**. Your browser has to transform the domain name that you entered into something known as an **IP address** to find the website you are looking for.

> **In simple terms:** An IP address is a unique sequence of numbers that identifies a computer on a network, such as the internet.

IP addresses are essential for allowing clients to send requests to the correct servers and get the appropriate responses.

| Standard | Example |
| -------- | ------- |
| **IPv4** | `127.0.0.1` |
| **IPv6** (a newer standard) | `0:0:0:0:0:0:0:1` |

There is a lot to learn about IP addresses, and you might want to explore them in more depth as you continue learning. But for now, you just need to understand that they are the unique numerical addresses used to identify computers on a network.

---

## What Is DNS?

From the concepts of domain names and IP addresses, now we can reach the concept of DNS.

**DNS** stands for **Domain Name System**. This is usually referred to as the **"phone book" of the internet**.

The DNS translates the domain name that you write on your browser to its corresponding IP address. It's a hierarchical and decentralized naming system for computers and devices that are connected to the internet or a specific network.

### How DNS Fits Into the Request-Response Cycle

When the user enters a domain name in the browser, such as `freecodecamp.org`:

1. The DNS maps that name to the IP address of its corresponding server.
2. Once the server has been identified, the client's request is sent to the server.
3. The server handles that request based on how it was programmed.
4. The server finally sends a response to the client.

This completes the request-response cycle.

This is all possible thanks to the DNS that performed that initial conversion to the target IP address.

Let's dive into the details of the DNS resolution process.

---

## The DNS Resolution Process

DNS resolution works by sending a query through a **chain of DNS servers**.

### Step by Step

**1. The user enters a domain name.**
When you (the user) enter a domain name on the browser, the client sends a request to a local DNS server. This local DNS server is known as the **Recursive Resolver**. This is usually managed by your internet service provider (ISP).

**2. The Recursive Resolver asks the Root Servers.**
The Recursive Resolver forwards that request to **Root Servers**. These are general servers that do not have direct information about IP addresses. They work by directing the Recursive Resolver to a more specific server, specifically to the **Top-Level Domain (TLD) Server** for the particular top-level domain of the request. For example, the server responsible for all `.org` domains.

**3. The Recursive Resolver asks the TLD Server.**
The Recursive Resolver then queries the Top-Level Domain (TLD) Server. This server returns the address of the specific **Authoritative Name Server** that holds the records for the domain that was requested (for example, `freecodecamp.org`).

**4. The Recursive Resolver asks the Authoritative Name Server.**
The Recursive Resolver starts a final query to the corresponding Authoritative Name Server. If the DNS record is found, it is returned to the Recursive Resolver.

**5. The client receives the IP address.**
When the Recursive Resolver receives the IP Address, it delivers it to the client, so you can start browsing the website.

### Visual Summary

```
 ┌────────┐  1. "freecodecamp.org?"   ┌────────────────────┐
 │ Client │ ────────────────────────▶ │ Recursive Resolver │
 │(browser)│                          │   (usually ISP)    │
 └────────┘                           └────────────────────┘
     ▲                                   │  ▲    │  ▲    │  ▲
     │                     2. Ask        │  │    │  │    │  │
     │                                   ▼  │    │  │    │  │
     │                           ┌─────────────┐ │  │    │  │
     │                           │ Root Server │─┘  │    │  │
     │                           └─────────────┘    │    │  │
     │            "Ask the .org TLD Server"         │    │  │
     │                                              ▼    │  │
     │                           3. Ask     ┌──────────────┐ │
     │                                      │  TLD Server  │─┘
     │                                      │   (.org)     │
     │                                      └──────────────┘
     │            "Ask the Authoritative Name Server"  │
     │                                                 ▼
     │                           4. Ask     ┌─────────────────────────┐
     │                                      │ Authoritative Name Server│
     │                                      │   (freecodecamp.org)    │
     │                                      └─────────────────────────┘
     │                                                 │
     └──────── 5. IP address returned ◀────────────────┘
               (via the Recursive Resolver)
```

### Quick Reference: Who Does What?

| Component | Role |
| --------- | ---- |
| **Recursive Resolver** | The local DNS server that receives the client's request and queries the other servers. Usually managed by your ISP. |
| **Root Servers** | General servers with no direct IP information. They direct the resolver to the correct TLD Server. |
| **TLD Server** | Responsible for a specific top-level domain (like `.org`). Returns the address of the Authoritative Name Server. |
| **Authoritative Name Server** | Holds the records for the requested domain and returns the DNS record. |

---

## DNS Records

The Authoritative Name Server returns **DNS Records**, not just IP addresses. DNS Records are structured text entries that contain important information about a domain, such as:

- Subdomain information
- How long the information should be cached
- Information required to perform the service requested

---

## Caching

To optimize the process, the Recursive Resolver **caches** the DNS Record temporarily to speed up the process. This way, you won't be making the same request repeatedly in a short time period. That makes the overall process much more efficient.

---

## Why DNS Matters

As you can see, DNS Servers are essential because they provide the initial, critical step of translating domain names into IP addresses. This translation process allows every client to locate and connect to the correct server. Without this directory system, the client-server model, the backbone of the modern web, would not be functional.
