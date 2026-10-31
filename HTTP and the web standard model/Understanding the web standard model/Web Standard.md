# What's the Process for Creating Web Standards?

> **Think of it like proposing a new rule in a big club:**
> Someone notices a problem, writes up an idea, the members argue over the details, a few members try it out, and only when enough of them agree does it become an official rule. It's slow on purpose, because once a rule is in place, millions of websites depend on it.

---

## How Each Body Works Differently

The process of creating web standards varies by body. The W3C runs formal working groups with structured review stages. WHATWG operates more like an open-source project. TC39 holds in-person meetings every two months where delegates vote on whether proposals advance. The Khronos Group gates participation by membership tier.

| Body | How it works |
| ---- | ------------ |
| **W3C** | Runs formal working groups with structured review stages |
| **WHATWG** | Operates more like an open-source project |
| **TC39** | Holds in-person meetings every two months where delegates vote on whether proposals advance |
| **Khronos Group** | Gates participation by membership tier |

However, underneath those differences, the process of turning an idea into a web standard follows an observable pattern.

## The Six Steps at a Glance

| Step | Name | In plain words |
| ---- | ---- | -------------- |
| 1 | **Identifying a Need** | Someone notices a real problem |
| 2 | **Proposal and Early Discussion** | The idea is written down and people react to it |
| 3 | **Writing the Specification** | The idea becomes a precise, formal document |
| 4 | **Review, Objection, and Iteration** | Everyone critiques it and it gets revised |
| 5 | **Implementation and Testing** | Browsers build it and tests check they all behave the same |
| 6 | **Finalization** | The standard becomes official |

```
 1. Identify    2. Propose     3. Write      4. Review      5. Implement    6. Finalize
    a need  ──▶  and discuss ──▶ the spec ──▶ and revise ──▶ and test   ──▶ the standard
                                                 ▲               │
                                                 └───────────────┘
                                          (problems found go back to the editors)
```

---

## 1. Identifying a Need

Standards start with friction, like developers hitting a brick wall, browsers implementing the same behavior in incompatible ways, or a new capability the platform simply doesn't support yet. Someone, somewhere, gets frustrated enough to write it down. That someone can be anyone; a developer, a large company with a product need, or an engineer inside a browser team. What matters at this stage is not authority, but evidence and questions on whether the problem is real, and whether enough people are running into it to justify the web platform's attention.

| Sources of friction | Example |
| ------------------- | ------- |
| Developers hitting a brick wall | A common task needs messy workarounds |
| Browsers behaving in incompatible ways | The same code works in one browser but not another |
| A missing capability | The platform simply can't do something yet |

> **What this means:** Anyone can start the process. What counts is not who you are, but whether you can show the problem is real and that many people face it.

---

## 2. Proposal and Early Discussion

The idea gets written up informally through a GitHub issue, a short document, or an explainer that describes the problem and sketches a possible solution. At this stage, the goal is not to produce a finished specification but to find out whether the problem resonates. Do other developers recognize it? Are browser vendors interested? Is there an obvious solution, or several competing ones? In TC39, this early phase corresponds to Stage 0 and Stage 1. In the W3C, it often happens informally in a Community Group before a formal Working Group is chartered. The WHATWG handles it through open GitHub discussions on its core repositories. The venue differs, but the function is the same.

| Body | Where early discussion happens |
| ---- | ------------------------------ |
| **TC39** | Stage 0 and Stage 1 |
| **W3C** | Informally in a Community Group, before a formal Working Group is chartered |
| **WHATWG** | Open GitHub discussions on its core repositories |

**Questions asked at this stage:**

- Do other developers recognize the problem?
- Are browser vendors interested?
- Is there an obvious solution, or several competing ones?

> **What this means:** This is the "is this worth doing?" stage. Nothing is final, and the goal is to test whether other people care.

---

## 3. Writing the Specification

If the proposal gains traction, someone or a small team has to write the actual specification, or **spec**. A spec is not a blog post or a tutorial, but a precise, formal document describing exactly how a feature must behave in every possible situation. Edge cases, error conditions, interactions with existing features, and security implications all have to be thought through and written down.

| A spec must cover | What it means |
| ----------------- | ------------- |
| **Edge cases** | Unusual situations that rarely happen |
| **Error conditions** | What happens when something goes wrong |
| **Interactions with existing features** | How it works alongside what already exists |
| **Security implications** | How it could be abused, and how to prevent that |

> **What this means:** A spec is like a legal contract, not a how-to guide. It must be so precise that two different teams reading it build the same behavior.

---

## 4. Review, Objection, and Iteration

The draft is published and reviewed publicly, and by the other browser vendors. This is where most of the real work happens. Objections are raised, and the spec is revised. A feature that one major browser engine refuses to implement will rarely become a standard, regardless of its technical merits. Consensus-building at this stage can take a long time. Some proposals stall for years while vendors negotiate over design details. Others die entirely when it becomes clear that no agreement is reachable.

| Possible outcome | What happens |
| ---------------- | ------------ |
| **Agreement reached** | The spec moves forward |
| **Stalled** | The proposal waits, sometimes for years, while vendors negotiate design details |
| **Dies** | No agreement is reachable, so the proposal ends |

> **What this means:** Every major browser team has a kind of veto in practice. If one of them refuses to build the feature, it will rarely become a standard, no matter how good the idea is.

---

## 5. Implementation and Testing

Once a spec is stable enough, browser vendors begin implementing it. This usually starts with a **feature flag** first, so it can be tested without affecting existing users. Implementation often reveals problems that the spec didn't anticipate, which then get sent back to the editors for clarification. A shared test suite verifies that every implementation actually behaves the same way. If Chrome, Firefox, and Safari all pass the same tests, the spec is working. If they diverge, either the spec is unclear, or one of the implementations has a bug.

| Term | What it means |
| ---- | ------------- |
| **Feature flag** | A hidden switch that turns a new feature on for testing only, without affecting regular users |
| **Shared test suite** | One set of tests that every browser must pass |

| Test result | What it tells you |
| ----------- | ----------------- |
| Chrome, Firefox, and Safari all pass | The spec is working |
| They diverge | Either the spec is unclear, or one of the implementations has a bug |

> **What this means:** Writing a spec on paper isn't enough. Browsers actually build it, and the same tests prove they all behave the same way. Problems found here go back to the spec editors.

---

## 6. Finalization

When multiple independent implementations exist, the tests pass, and the community is satisfied, the standard is finalized. In the W3C this means achieving Recommendation status. In TC39, it means reaching Stage 4, after which the feature is included in the next annual ECMAScript release. In the WHATWG, there is no single finalization moment, the living standard simply reflects the current consensus, updated continuously. The whole process can take anywhere from a few months for a small, uncontroversial addition to over a decade for something complex or politically fraught. CSS Grid, for instance, was first proposed in 2011 and didn't ship in all major browsers until 2017. That gap between a good idea and a stable, universally supported standard is where most of the work of the open web quietly happens.

**Conditions for finalization:**

- Multiple independent implementations exist
- The tests pass
- The community is satisfied

| Body | What finalization looks like |
| ---- | ---------------------------- |
| **W3C** | Achieving Recommendation status |
| **TC39** | Reaching Stage 4, after which the feature is included in the next annual ECMAScript release |
| **WHATWG** | No single finalization moment. The living standard simply reflects the current consensus, updated continuously |

### How Long Can It Take?

The whole process can take anywhere from a few months for a small, uncontroversial addition to over a decade for something complex or politically fraught.

```
 Small, uncontroversial addition          Complex or politically fraught feature
 ├── a few months ──┤                     ├────────── over a decade ──────────────▶

 Example: CSS Grid
 2011                                                              2017
  │── first proposed ──────────────────────────────────────────────│
                                                 shipped in all major browsers
```

> **What this means:** The gap between a good idea and a stable, universally supported standard is where most of the work of the open web quietly happens.

---

## Putting It All Together

| Step | Who is involved | Main question |
| ---- | --------------- | ------------- |
| 1. Identifying a Need | Anyone: a developer, a company, a browser engineer | Is the problem real? |
| 2. Proposal and Early Discussion | Developers and browser vendors | Does the problem resonate? |
| 3. Writing the Specification | An individual or a small team | How exactly should it behave? |
| 4. Review, Objection, and Iteration | The public and other browser vendors | Can everyone agree? |
| 5. Implementation and Testing | Browser vendors | Do all browsers behave the same way? |
| 6. Finalization | The standards body and the community | Is it ready to be official? |
