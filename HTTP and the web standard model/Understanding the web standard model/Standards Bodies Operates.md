# How Do Standards Bodies Operate?

> **Think of it like making the rules for a shared game:**
> If every player followed different rules, nobody could play together. Standards bodies are the groups that write the shared rulebook, so every browser can understand every website.

---

## What Are Web Standards?

The open web does not run itself. Every time a browser renders a page, plays a video, or draws a 3D scene, it is following instructions that were set over the years by engineers and company representatives sitting in working groups.

These instructions are called **web standards**. And the groups responsible for setting them are called **standards bodies**. Think of them as the legislators of the internet.

| Term | What it means | In plain words |
| ---- | ------------- | -------------- |
| **Web standards** | The agreed instructions browsers follow | The **rules** of the web |
| **Standards bodies** | The groups that set those instructions | The **rule-makers** |
| **Working groups** | Teams of engineers and company representatives | The **committees** that do the work |

The organizations that do most of the work in web standards today include the **W3C**, the **WHATWG**, **ECMA (TC39)**, and the **Khronos Group**. Each of them governs a different layer of the stack, and each operates a little differently.

## Quick Overview

| Organization | What it governs | How it works |
| ------------ | --------------- | ------------ |
| **WHATWG** | HTML and the DOM | A "living standard" that updates continuously |
| **W3C** | CSS, SVG, accessibility guidelines, and numerous web APIs | A slow, agreement-driven, multi-stage review process |
| **Ecma International (TC39)** | ECMAScript (the standard behind JavaScript) | A five-stage proposal process, with meetings roughly every two months |
| **Khronos Group** | Graphics, compute, and media standards (WebGL, WebGL 2) | A member-funded consortium |

---

## WHATWG

The Web Hypertext Application Technology Working Group, **WHATWG**, maintains HTML and the DOM as a single continuously updated **"living standard."** Rather than versioned releases, the specification evolves in real time, edited by a small group with strong editorial authority. Decision-making power sits with the major browser engine teams like Chromium, Gecko, and WebKit.

| Detail | Description |
| ------ | ----------- |
| **Full name** | Web Hypertext Application Technology Working Group |
| **Maintains** | HTML and the DOM |
| **Style** | A single, continuously updated "living standard" |
| **Who edits it** | A small group with strong editorial authority |
| **Who holds decision-making power** | The major browser engine teams: Chromium, Gecko, and WebKit |

> **What this means:** Instead of publishing "HTML version 6" on a set date, WHATWG keeps one document that is always current, like a wiki that is updated all the time instead of a printed book with new editions.

---

## W3C

The World Wide Web Consortium, **W3C**, is the primary standards organization of the web. It has a broad membership across browser vendors, governments, and research institutions.

W3C oversees CSS, SVG, accessibility guidelines, and numerous web APIs. It works through a slow, agreement-driven process where proposals pass through multiple stages of review before becoming official standards.

| Detail | Description |
| ------ | ----------- |
| **Full name** | World Wide Web Consortium |
| **Role** | The primary standards organization of the web |
| **Members** | Browser vendors, governments, and research institutions |
| **Oversees** | CSS, SVG, accessibility guidelines, and numerous web APIs |
| **Style** | Slow and agreement-driven, with multiple stages of review |

> **What this means:** W3C works like a large committee that wants broad agreement before anything becomes official. This takes longer, but many different groups get a say.

---

## Ecma International (ECMA) and TC39

Ecma International (formerly the European Computer Manufacturers Association, or ECMA) is a general-purpose standards organization originally focused on computing and communications technologies. Today, it formally publishes the **ECMAScript** standard, which JavaScript implementations are based on. The technical development of the language standard is carried out by Ecma's **Technical Committee 39 (TC39)**, while Ecma International provides the organizational framework, publication process, and standards governance.

| Who | Role |
| --- | ---- |
| **Ecma International** | Provides the organizational framework, publication process, and standards governance. Formally publishes the ECMAScript standard |
| **TC39** (Technical Committee 39) | Carries out the technical development of the language standard |

> **What this means:** Ecma is the publisher, and TC39 is the team that actually designs the language. ECMAScript is the official specification, and JavaScript is the language that implements it.

The committee meets roughly every two months with delegates from Google, Apple, Mozilla, Microsoft, and others. New language features move through a **five-stage proposal process**, from a rough sketch at Stage 0 to fully specified and implemented at Stage 4. Features like `async/await`, optional chaining, and ES modules all went through this process before landing in the JavaScript language.

### The Five-Stage Proposal Process

```
 Stage 0 ──▶ Stage 1 ──▶ Stage 2 ──▶ Stage 3 ──▶ Stage 4
   │                                                  │
 Rough                                          Fully specified
 sketch                                         and implemented
                                                (added to JavaScript)
```

| Stage | Meaning |
| ----- | ------- |
| **Stage 0** | A rough sketch of an idea |
| **Stage 4** | Fully specified and implemented |

> **Note:** The original text only describes Stage 0 and Stage 4, along with the fact that there are five stages in total. The stages in between are not described there.

| Details | Description |
| ------- | ----------- |
| **Meeting frequency** | Roughly every two months |
| **Delegates from** | Google, Apple, Mozilla, Microsoft, and others |
| **Features that went through this process** | `async/await`, optional chaining, ES modules |

---

## Khronos Group

The **Khronos Group** is a member-funded consortium focused on graphics, compute, and media standards. The members include delegations from GPU manufacturers like NVIDIA and AMD, alongside browser vendors. For the web, its most significant contributions are **WebGL** and **WebGL 2**, which bring GPU-accelerated 3D rendering to the browser.

| Detail | Description |
| ------ | ----------- |
| **Type** | A member-funded consortium |
| **Focus** | Graphics, compute, and media standards |
| **Members** | GPU manufacturers like NVIDIA and AMD, alongside browser vendors |
| **Main contributions for the web** | WebGL and WebGL 2 |
| **What those do** | Bring GPU-accelerated 3D rendering to the browser |

> **What this means:** When a website draws an interactive 3D scene, it uses the graphics card (GPU) of your device. WebGL is the standard that lets the browser do that.

---

## Putting It All Together

| If you use... | The standard comes from... |
| ------------- | -------------------------- |
| HTML or the DOM | WHATWG |
| CSS, SVG, or accessibility guidelines | W3C |
| JavaScript | Ecma International (TC39) |
| 3D graphics in the browser (WebGL) | Khronos Group |

```
                    The Open Web
                         │
     ┌─────────────┬─────┴───────┬──────────────┐
     ▼             ▼             ▼              ▼
  WHATWG          W3C        Ecma (TC39)     Khronos
 HTML + DOM   CSS, SVG,      ECMAScript     WebGL and
              accessibility  (JavaScript)    WebGL 2
              + web APIs
```
