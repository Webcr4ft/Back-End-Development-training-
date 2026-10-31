# What Does the Lifecycle of Web Standards Features Look Like?

> **Think of it like the life of a product:**
> It starts as an idea, gets designed, gets tested, goes on sale, and one day may be retired. The web works the same way for each new feature, but "retiring" is very slow, because old websites still need to work.

---

## What Is a Feature Lifecycle?

In the last lesson, we looked at the process for creating web standards: how proposals are written, reviewed, and eventually finalized.

The lifecycle of a web standard feature is related, but on a more granular scale. It follows a single feature from the moment someone identifies a problem all the way to it shipping in every major browser (and possibly being deprecated in the end).

Think of the process as the rulebook, and the lifecycle as what actually happens when you play the game.

| | Process (last lesson) | Lifecycle (this lesson) |
| --- | --------------------- | ----------------------- |
| **Focus** | How standards are created in general | What happens to one single feature |
| **Analogy** | The rulebook | Playing the game |
| **Scale** | Broad | Granular |

## The Six Stages at a Glance

| Stage | Name | In plain words |
| ----- | ---- | -------------- |
| 1 | **Proposal** | Someone writes down a problem |
| 2 | **Incubation** | The community discusses and stress-tests the idea |
| 3 | **Specification** | The idea becomes exact, formal rules |
| 4 | **Interoperability Testing** | Tests check that every browser behaves the same |
| 5 | **Finalization** | The feature is official and ships to users |
| 6 | **Deprecation** | The feature is phased out |

```
 1. Proposal ──▶ 2. Incubation ──▶ 3. Specification ──▶ 4. Interoperability ──▶ 5. Finalization ──▶ 6. Deprecation
                      │                                        Testing                                      │
                      ▼                                           │                                         ▼
                 Many ideas die here                    Problems go back to                    Supported, but developers
                                                        the spec or browsers                   should stop using it
                                                                                               (removed from the spec later)
```

---

## 1. Proposal

Every feature starts with a problem someone cared enough to write down. A developer, a browser engineer, or a company files a GitHub issue or explainer describing what the web can't currently do and why it should. At this stage, the idea is loose, with more questions than answers. The goal is simply to find out whether anyone else recognizes the same pain.

| Detail | Description |
| ------ | ----------- |
| **Who can start it** | A developer, a browser engineer, or a company |
| **How** | By filing a GitHub issue or explainer |
| **What it describes** | What the web can't currently do, and why it should |
| **State of the idea** | Loose, with more questions than answers |
| **Goal** | Find out whether anyone else recognizes the same pain |

> **What this means:** This is the "does anyone else have this problem?" stage.

---

## 2. Incubation

If the proposal resonates, it enters a period of open discussion and early design. Competing approaches get sketched out, use cases are gathered, and the community stress-tests the idea. Many proposals die here, possibly because the problem turns out to be too niche, or no solution can satisfy everyone. The ones that survive emerge with a clearer shape and at least some browser vendor interest behind them.

| What happens | Description |
| ------------ | ----------- |
| **Open discussion and early design** | The community talks about the idea in public |
| **Competing approaches** | Different solutions get sketched out |
| **Use cases gathered** | Real situations where the feature would help |
| **Stress-testing** | The community tries to find weaknesses in the idea |

| Outcome | Why |
| ------- | --- |
| **Dies** | The problem is too niche, or no solution can satisfy everyone |
| **Survives** | It emerges with a clearer shape and at least some browser vendor interest behind it |

> **What this means:** Think of it as an incubator for an egg. Many ideas don't hatch, and the ones that do come out with a clearer shape.

---

## 3. Specification

A surviving proposal gets written up as a formal spec. Every edge case, error condition, and interaction with existing features has to be defined clearly. This is the point where a good idea meets hard reality. Vague concepts have to become exact rules that two independent engineers could read and implement identically.

| A spec must define | What it means |
| ------------------ | ------------- |
| **Every edge case** | Unusual situations that rarely happen |
| **Every error condition** | What happens when something goes wrong |
| **Interactions with existing features** | How it works alongside what already exists |

> **What this means:** "Make it faster" is a vague concept. A spec turns it into exact rules, so that two different engineers reading it build the same thing.

---

## 4. Interoperability Testing

Before a feature can be considered stable, it has to behave the same way in every browser. The **W3C Web Platform Tests** suite is the main tool for verifying this. It is a shared battery of tests that Chrome, Firefox, Safari, and others all run against their implementations. Diverging results mean either the spec is ambiguous, or someone has a bug. Either must be resolved before the feature moves forward.

| Term | What it means |
| ---- | ------------- |
| **Interoperability** | Different browsers working the same way |
| **W3C Web Platform Tests** | A shared battery of tests that Chrome, Firefox, Safari, and others all run against their implementations |

| Test result | What it tells you |
| ----------- | ----------------- |
| All browsers pass | The feature behaves the same everywhere |
| Results diverge | Either the spec is ambiguous, or someone has a bug. Either must be resolved before the feature moves forward |

> **What this means:** Imagine giving the same exam to Chrome, Firefox, and Safari. If they give different answers, someone needs to fix either the exam instructions (the spec) or the student (the browser).

---

## 5. Finalization

Once multiple independent implementations pass the tests, the feature is finalized. For W3C, it is a recommendation, for TC39, it is stage 4, and it is a stable entry in the WHATWG living standard. The flags come down and the feature ships to users. At this point, it becomes part of the baseline web platform, something every developer can rely on indefinitely.

| Body | What finalization looks like |
| ---- | ---------------------------- |
| **W3C** | A recommendation |
| **TC39** | Stage 4 |
| **WHATWG** | A stable entry in the living standard |

| What happens | Description |
| ------------ | ----------- |
| **The flags come down** | The hidden switches used for testing are removed |
| **The feature ships to users** | Everyone can use it |
| **It joins the baseline web platform** | Something every developer can rely on indefinitely |

> **What this means:** Once a feature reaches this stage, you can use it in your websites with confidence.

---

## 6. Deprecation

Not every standard ages well. Some features get superseded by better ones, others turn out to have security or privacy implications that weren't apparent at the time. When a feature needs to go, it gets formally deprecated. That is, supported but marked as something developers should stop using. Eventually, it is removed from the spec. Removal from browsers is slow and cautious, because the core promise of the web is that old pages keep working. Some deprecated features linger in browsers for decades solely for the backwards-compatibility obligation.

| Reasons a feature gets deprecated | Description |
| --------------------------------- | ----------- |
| **Superseded** | A better feature replaces it |
| **Security or privacy implications** | Problems that weren't apparent at the time |

| Phase | What happens |
| ----- | ------------ |
| **Deprecated** | Still supported, but marked as something developers should stop using |
| **Removed from the spec** | Eventually, the feature is taken out of the standard |
| **Removed from browsers** | Slow and cautious, because the core promise of the web is that old pages keep working |

> **What this means:** "Deprecated" means "still works, but don't use it in new code." Browsers keep supporting some of these features for decades, so that old websites don't break.

---

## Putting It All Together

| Stage | Main question | Possible result |
| ----- | ------------- | --------------- |
| 1. Proposal | Does anyone else recognize this problem? | Moves on, or is dropped |
| 2. Incubation | Can the community shape a workable idea? | Many proposals die here |
| 3. Specification | Can it be defined as exact rules? | A formal spec |
| 4. Interoperability Testing | Do all browsers behave the same way? | Fix the spec or the bugs |
| 5. Finalization | Do multiple implementations pass the tests? | The feature ships to users |
| 6. Deprecation | Is the feature still a good idea? | Marked as "stop using," removed from the spec eventually |
