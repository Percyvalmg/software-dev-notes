# Branching strategies explained
**Source:** [DevOps & AI Toolkit (Viktor Farcic)](https://youtu.be/U_IFGpJDbeU) | *Branching Strategies Explained*

---

## The core idea

The way a team branches says a lot about how it works. It tends to line up with:

- team size
- how often the team deploys
- how much test coverage exists
- how much is automated

The strategy also decides what you can do easily and what becomes painful. Long-lived branches, for example, make continuous integration hard.

This note covers six strategies, ordered from the simplest branching model to the most complex. For each one it explains how the branching works, what it costs, and when it fits.

```
BRANCHING COMPLEXITY  →

Trunk-Based .......... simplest branching
Feature Branches ..... 
Forking .............. 
Release Branches ..... 
Git Flow ............. 
Environment Branches . most complex branching
```

One trade-off is worth stating up front: the simpler the branching, the more you usually need everything around it to be solid. Trunk-based development has the simplest branches but leans hardest on testing and automation.

---

## 1. Trunk-based development

Everyone clones a single branch (`main`, `trunk`, or `master`), makes changes locally, and pushes straight back to it. No branches, no pull requests.

```
   dev A ──┐
   dev B ──┼──►  ●───●───●───●───●   main (trunk)
   dev C ──┘     push directly, no branches
```

The branching is the easy part: nothing to merge, nothing to maintain. The hard part is everything else:

- high code coverage and strong testing habits (often test-first or BDD)
- solid automation, including automated deployment
- feature toggles, so unfinished work stays hidden from users even though the code is already deployed

This strategy is closely tied to continuous deployment. You can do continuous deployment without pushing straight to the main line, but in practice the two usually come together.

---

## 2. Feature branches / GitHub Flow

There's always a main line. When you want to work on a feature or a hotfix, you create a short-lived branch and then open a pull request to merge it back.

```
              ┌──● feature/login ──┐
              │  (hours to ~1 day) │
   main  ●────┴────────────────────┴──►●───●
              cut branch      PR + review + merge
```

The main practice is to work in small pieces with short delivery cycles. On average, a feature is written, tested, reviewed through a pull request, approved, and merged within about a day.

A few things to note:

- it usually pairs with continuous delivery, or sometimes continuous integration
- feature toggles help but aren't required
- pull requests are central, and not only when work is finished; you can open one mid-development to get feedback, keep pushing, and merge once everyone is satisfied

---

## 3. Forking strategy

Forking is much like feature branches, with one difference: instead of branching off the main line, you copy the whole repository. You fork it, work in your own copy, and open a pull request back to the original (upstream) repository.

```
   upstream repo  ●───●───●───●───►  (maintainers have write access)
        │ fork                ▲
        ▼                     │ pull request
   your fork    ●───●───●─────┘
   (full copy, contributor owns it)
```

The usual home for this is open source:

- anyone can read or fork the project, but only maintainers can merge into the original
- maintainers don't have to manage permissions for every contributor; the fork boundary handles access on its own

---

## 4. Release branches

Releases here are long-lived, lasting weeks or months. Each release gets its own branch, there are often extra branches for individual hotfixes, and different teams may work on different releases at the same time.

```
   main ●────────────●───────────────●──►
         \          ▲ \             ▲
          \ release/1 \ (merge)      \ release/2
           ●──●──●─────┘              ●──●──●
              \ hotfix                   \ hotfix
               ●──┘                       ●──┘
```

The trouble starts when you merge into the main line, because every other open branch then has to pull those changes. That brings:

- merge conflicts
- branches drifting apart
- integration that keeps getting pushed back

Work across teams stays disconnected until one team finishes, and only then do the others figure out how to fit their code in with it.

This pattern goes with less frequent deployments, such as every few weeks, once a month, or even less, and it tends to line up with a waterfall way of working.

There is a solid reason to use it, though: software vendors that have to support several versions at once. Kubernetes is a good example. It supports a few recent minor releases, so it needs separate branches to apply hotfixes to older versions.

---

## 5. Git Flow

Git Flow is a more involved model. A `develop` branch acts as the integration point for feature branches. Release branches are cut from `develop` and then merged back into both `develop` and `main`, since `main` reflects production.

```
   main     ●─────────────────────────●────►  (production)
             \                        ▲
   develop ●──●────●────●────●─────────┤
             \    ▲     \      \        \
   feature/1  ●──●│      \      \        \ (release merged to
                  │       \      \          both develop + main)
   feature/2      ●───────┘       \
                                release/x ●──●──┘
```

How the branches connect:

- feature branches come off `develop`
- release branches also come off `develop`, and get merged into both `develop` and `main`
- keeping all of this in sync takes a lot of merging

In many companies this is handled by a dedicated release-management role that does the branching and merging, while other developers mostly just work on `develop`. That split adds real coordination overhead compared with the simpler strategies.

---

## 6. Environment branches

This extends Git Flow by adding a branch for each environment, such as staging and integration, on top of `develop` and the release branches. Changes then have to be merged across all of them, multiplied by however many releases are in flight, plus the hotfixes.

```
   main         ●──────────────────────►  production
   staging      ●──────────────────────►  (branch per environment)
   integration  ●──────────────────────►
   develop      ●──●──●──●──►
                 \  release/1, release/2, ...  \ hotfixes
                  changes must merge across all branches
```

The core problem is the assumption behind it: that you deploy source code to each environment. You don't. The better approach is to build a release artifact once and deploy that same artifact to every environment.

```
   Environment-branch model:  branch-per-env → deploy code to each

   Build-once model:          build once ──►  [ artifact ]
                                                ├─► deploy to staging
                                                ├─► deploy to integration
                                                └─► deploy to production
```

This is the most complex branching model and the most expensive to coordinate.

---

## Which strategy should you use?

The video boils the choice down to a few questions:

```
                     Open-source project?
                                   │
                    ┌────── yes ───┴─── no ──────┐
                    ▼                             ▼
              FORKING            Must support multiple versions
                                 with backported hotfixes?
                                   │
                    ┌────── yes ───┴─── no ──────┐
                    ▼                             ▼
             RELEASE BRANCHES          High coverage + trusted tests
                                       + strong automation?
                                   │
                    ┌────── yes ───┴─── no ──────┐
                    ▼                             ▼
             TRUNK-BASED               Small, self-sufficient team that
                                       splits work into small, fast chunks?
                                   │
                    ┌────── yes ───┴─── no ──────┐
                    ▼                             ▼
             FEATURE BRANCHES          Move toward feature branches
                                       (or release branches)
```

In short:

- trunk-based development if your team has high coverage, trusts its tests, and has strong automation, enough to push straight to the main line
- feature branches if you're a small, self-sufficient team, ideally with a smaller app, and you can break work into small pieces that finish fast
- forking for open-source projects; it's the near-universal choice there
- release branches when you must keep backwards compatibility and apply hotfixes across several supported releases
- if none of those fit, move toward feature branches (or release branches if you need them) rather than the more complex models

---

## Summary table

| Strategy | Branching complexity | Deploy cadence | Best for |
|---|---|---|---|
| Trunk-based | None | Continuous deployment | Teams with strong automation and testing |
| Feature branches | Low | Continuous delivery or integration | Small, fast, self-sufficient teams |
| Forking | Low | Varies | Open-source projects |
| Release branches | Medium | Weeks or months | Vendors supporting multiple versions |
| Git Flow | High | Slower | Teams that need formal release management |
| Environment branches | Very high | Slower | Generally discouraged |

---

## Key takeaways

- How a team branches both reflects and limits its structure, deployment frequency, and testing maturity.
- Simpler branching usually depends on stronger testing and automation. Trunk-based is the clearest case.
- Feature toggles separate "deployed" from "released," which is what makes trunk-based development workable.
- Long-lived branches make continuous integration harder because branches drift apart, integration is delayed, and merge conflicts pile up.
- Deploy releases, not source code. Build the artifact once and promote it across environments. That's why a branch per environment is an anti-pattern.
- For most teams, trunk-based development or feature branches are the sensible defaults. The more complex models earn their keep only for specific needs, such as supporting multiple versions, running an open-source contribution flow, or formal release management.
