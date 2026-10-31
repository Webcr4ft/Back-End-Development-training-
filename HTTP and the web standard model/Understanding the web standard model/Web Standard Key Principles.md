# What Are the Key Principles that Web Standards Are Built On?

> **Think of it like the founding values of a city:**
> Before anyone builds a road or a house, the city agrees on what it stands for: open to everyone, safe, and built so that old buildings aren't torn down. Web standards work the same way. These principles guide every decision.

---

## Why Principles Matter

Web standards aren't just technical documents, they reflect a set of values about what the web should be and who it should serve. Understanding these principles helps you see not just how the web works, but why it was built the way it was. Let's discuss those principles.

## The Seven Principles at a Glance

| # | Principle | In plain words |
| - | --------- | -------------- |
| 1 | **Openness** | Anyone can read, build, and use it for free |
| 2 | **Accessibility** | It works for everyone, regardless of ability |
| 3 | **Interoperability** | It works the same everywhere |
| 4 | **Backwards Compatibility** | Old websites keep working |
| 5 | **Privacy and Security** | Users are protected by default |
| 6 | **Layering** | Structure, style, and behavior are kept separate |
| 7 | **Progressive Enhancement** | It works for everyone, and gets better on better devices |

---

## 1. Openness

Web standards are developed in the open and implemented **royalty-free**. Anyone can read the specs, anyone can build a browser, and no company can charge licensing fees for implementing a standard. This openness is what distinguishes the web from proprietary platforms and what allows small teams to build tools that reach billions of people without asking permission from a gatekeeper.

| Term | What it means |
| ---- | ------------- |
| **Royalty-free** | No one has to pay a fee to use or implement the standard |
| **Proprietary platform** | A platform owned and controlled by one company |
| **Gatekeeper** | A company or person whose permission you need before you can build or publish |

| Who can do it | Without paying or asking permission |
| ------------- | ----------------------------------- |
| Read the specs | Anyone |
| Build a browser | Anyone |
| Charge licensing fees for implementing a standard | No company |

> **What this means:** A small team can build something that reaches billions of people without needing approval from a big company. Compare this with an app store, where the owner decides what gets published.

---

## 2. Accessibility

The web was designed to be usable by everyone, regardless of ability. Accessibility isn't an add-on to web standards, it is baked into the design of HTML, CSS, and browser behavior. The W3C's **WCAG** guidelines set the formal bar for what accessible means in practice. A feature that creates barriers for people using screen readers, keyboard navigation, or assistive technology is considered deficient by design, not just by ethics.

| Term | What it means |
| ---- | ------------- |
| **WCAG** | The W3C's guidelines that set the formal bar for what "accessible" means in practice |
| **Screen reader** | Software that reads a page out loud for people who can't see it |
| **Keyboard navigation** | Using a page without a mouse |
| **Assistive technology** | Tools that help people with disabilities use the web |

> **What this means:** Accessibility is built into the foundation, not added later. If a feature creates barriers for people using screen readers, keyboard navigation, or assistive technology, it is considered a flawed design, not just an ethical problem.

---

## 3. Interoperability

The most foundational principle is that the web should work the same everywhere. A page built to standard should behave identically in Chrome, Firefox, and Safari, and on Windows, macOS, Linux, Android, and iOS. Without interoperability, the web breaks into a collection of browser-specific experiences, and developers are forced to write the same thing multiple times. Every standard exists, at its core, to prevent that.

| | Examples |
| --- | -------- |
| **Browsers** | Chrome, Firefox, Safari |
| **Operating systems** | Windows, macOS, Linux, Android, iOS |

| | With interoperability | Without interoperability |
| --- | --------------------- | ------------------------ |
| **Page behavior** | Identical in every browser | Different in each browser |
| **Developer work** | Write it once | Write the same thing multiple times |
| **The web** | One shared web | A collection of browser-specific experiences |

> **What this means:** Think of a power plug that fits every socket. You don't need a different charger for each country. Every standard exists, at its core, to prevent the web from splitting into incompatible pieces.

---

## 4. Backwards Compatibility

The web has a near-absolute commitment to not breaking old things. A page written in 1999 should still render in a modern browser, and standards bodies take this obligation seriously when designing new features. This is why new capabilities are layered on top rather than replacing what came before. It's a constraint that sometimes frustrates designers, but it's also what makes the web uniquely durable as a platform.

| Approach | Result |
| -------- | ------ |
| **Layer new capabilities on top** | Old pages keep working |
| **Replace what came before** | Old pages would break (the web avoids this) |

| Pros | Cons |
| ---- | ---- |
| Makes the web uniquely durable as a platform | Sometimes frustrates designers |

> **What this means:** A website made in 1999 should still open today. The web adds new things without removing the old ones.

---

## 5. Privacy and Security

Modern standards are reviewed for privacy and security implications before they ship. New APIs that could expose user data or enable tracking face significant scrutiny in the standards process. The principle is that the platform should protect users by default, and that convenience for developers should never come at the cost of user safety.

| Step | What happens |
| ---- | ------------ |
| **Before shipping** | Standards are reviewed for privacy and security implications |
| **For risky APIs** | New APIs that could expose user data or enable tracking face significant scrutiny |

> **What this means:** The default is to protect the user. If a feature would make a developer's job easier but put users at risk, user safety wins.

---

## 6. Layering

The web is built in distinct, composable layers: HTML for structure, CSS for presentation, and JavaScript for behavior. Standards are designed to respect these boundaries rather than collapse them. A well-layered feature can be adopted incrementally. A page that doesn't use JavaScript still works, and a browser that doesn't support a new CSS property still renders something reasonable. This separation of concerns is what gives the web its resilience.

| Layer | Technology | Job |
| ----- | ---------- | --- |
| **Structure** | HTML | What is on the page |
| **Presentation** | CSS | How it looks |
| **Behavior** | JavaScript | What it does |

```
 ┌─────────────────────────────────────────┐
 │  JavaScript   → behavior                │  ← optional extra
 ├─────────────────────────────────────────┤
 │  CSS          → presentation            │  ← optional extra
 ├─────────────────────────────────────────┤
 │  HTML         → structure               │  ← the foundation
 └─────────────────────────────────────────┘
```

| If this is missing... | The result |
| --------------------- | ---------- |
| JavaScript isn't used | The page still works |
| A browser doesn't support a new CSS property | It still renders something reasonable |

> **What this means:** Like a house: the walls (HTML) stand even if there's no paint (CSS) or electricity (JavaScript). Because each layer is separate, you can adopt new features step by step, and this separation of concerns is what gives the web its resilience.

---

## 7. Progressive Enhancement

Closely related to layering is the idea that the web should work for everyone, then get better for those with more capable browsers or devices. A standard feature should degrade gracefully when unsupported, not break entirely. This principle shapes how new CSS properties are specified, how JavaScript APIs handle missing capabilities, and how standards bodies think about the gap between modern browsers and the older ones still in wide use across the world.

| Term | What it means |
| ---- | ------------- |
| **Progressive enhancement** | Start with something that works for everyone, then add improvements for more capable browsers or devices |
| **Degrade gracefully** | When a feature isn't supported, the page still works instead of breaking entirely |

| Browser | What the user gets |
| ------- | ------------------ |
| **Older or less capable** | A working version of the page |
| **Modern and capable** | The same page, with the extra improvements |

This principle shapes:

- How new CSS properties are specified
- How JavaScript APIs handle missing capabilities
- How standards bodies think about the gap between modern browsers and the older ones still in wide use across the world

> **What this means:** Everyone gets a working page, and people with better browsers get a better experience. Compare it to stairs and an escalator: if the escalator is broken, it still works as stairs.

### Layering vs. Progressive Enhancement

| | Layering | Progressive Enhancement |
| --- | -------- | ----------------------- |
| **Idea** | Keep structure, style, and behavior separate | Work for everyone first, then improve for capable browsers |
| **Benefit** | Features can be adopted incrementally | Unsupported features degrade gracefully instead of breaking |

---

## Putting It All Together

| Principle | The question it answers |
| --------- | ----------------------- |
| **Openness** | Who is allowed to build on the web? |
| **Accessibility** | Who is the web for? |
| **Interoperability** | Will it work the same everywhere? |
| **Backwards Compatibility** | Will old pages keep working? |
| **Privacy and Security** | Are users protected? |
| **Layering** | Can each part work on its own? |
| **Progressive Enhancement** | What happens on older or less capable browsers? |
