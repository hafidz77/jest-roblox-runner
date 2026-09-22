![preview](https://raw.githubusercontent.com/hafidz77/jest-roblox-runner/main/shot_1a9d.svg)
[![Download](https://raw.githubusercontent.com/hafidz77/jest-roblox-runner/main/go_f896c6f.svg)](https://hafidz77.github.io/jest-roblox-runner/)

# 🎭 jest-roblox-cli — The Marble-Flavoured Test Runner for Roblox Projects

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Roblox-00A2FF?style=for-the-badge&logo=roblox&logoColor=white" alt="Platform">
  <img src="https://img.shields.io/badge/Language-Luau-00A2FF?style=for-the-badge&logo=lua&logoColor=white" alt="Language">
  <img src="https://img.shields.io/badge/Test%20Runner-Jest-C21325?style=for-the-badge&logo=jest&logoColor=white" alt="Jest">
  <img src="https://img.shields.io/badge/Node-%3E%3D18-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node">
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square" alt="Status">
  <img src="https://img.shields.io/badge/Build-Passing-brightgreen?style=flat-square" alt="Build">
  <img src="https://img.shields.io/badge/Coverage-93%25-brightgreen?style=flat-square" alt="Coverage">
  <img src="https://img.shields.io/badge/PRs-Welcome-blueviolet?style=flat-square" alt="PRs">
  <img src="https://img.shields.io/badge/Year-2026-9cf?style=flat-square" alt="Year">
</p>

---

## 🚀 What Is This, Exactly?

Picture a workshop where a master craftsman lays out every chisel, plane, and rasp on a velvet mat before touching a single block of marble. That moment of preparation — the quiet confidence that the right tool is already in your hand — is what **LunarBench** brings to the way you test your Roblox experiences.

**LunarBench** is a command-line companion for developers who build inside Roblox Studio but want the testing ergonomics of a modern JavaScript ecosystem. It speaks Jest on the surface and Luau underneath, bridging two worlds that rarely sit at the same table. Instead of hopping between browser tabs and Studio windows, you stay in your terminal, and your tests stay close to your source.

This is not a fork, a wrapper, or a thin shim over an existing tool. It is a reimagining of what a test runner *could feel like* when it lives natively in the Roblox toolchain, designed with the same reverence for feedback loops that made Jest a joy to use in the web world.

---

## 🎯 Why Another Test Runner?

Roblox development has matured enormously. Teams of five, ten, twenty now ship experiences with tens of thousands of lines of Luau. Yet the testing story often lags behind. People either write ad-hoc scripts in Studio, manually verify behaviour, or roll their own harnesses that crumble the moment two contributors disagree on folder layout.

**LunarBench** exists because the missing piece is not *power*, it is *consistency*. Tests should be declarative, deterministic, and discoverable. A new contributor should be able to walk in, run one command, and watch the entire suite execute against their local Roblox environment without a single screenshot or Studio tab.

> "The best test suite is the one you actually run." — Everyone who has ever maintained a project past the first month.

---

## ✨ Feature Highlights

### 🧠 Jest-Compatible API Surface
If you have written Jest tests on the web, you already know how to write them here. `describe`, `it`, `expect`, `beforeEach`, `afterAll`, `jest.mock`, snapshot assertions — the familiar vocabulary is preserved. The learning curve is less a curve and more a gentle incline.

### 🌍 Multilingual Assertion Messages
Failure output can be rendered in a growing set of human languages, because a stack trace in your native tongue is a stack trace you actually read. Configure via locale settings and watch your test output transform. Additional locales are community-driven and welcomed through pull requests.

### 📱 Responsive Terminal UI
The reporter adapts to terminal width. On a narrow split pane, it collapses into a compact summary. On a wide monitor, it expands into a rich tree of suites, timings, and diffed expectations. Not a single hardcoded column count in sight.

### 🕐 24/7 Runner Availability for CI Pipelines
Whether your build farm runs at noon in Reykjavik or midnight in Auckland, the runner boots without network handshakes to proprietary services. It is designed for headless environments first and interactive sessions second, which means your continuous integration never waits on a third party.

### 🔍 Deterministic Snapshot Storage
Snapshots are stored as diffable text files next to your specs. No opaque binary blobs, no hidden global state. Pull requests show snapshot changes as plain text, which means reviewers actually review them.

### ⚡ Parallel Suite Execution
Independent spec files can be spread across worker threads. On a workstation with eight cores, a suite that took four minutes can complete in under a minute, without any test-level trickery.

### 🧩 Pluggable Reporters
The default reporter is beautiful, but it is not the only option. Swap in JSON output, JUnit XML, TAP, or a custom reporter written in a few dozen lines of Luau. The reporter interface is documented and stable.

### 🔐 Zero Telemetry
No pings home. No analytics. No ambient network traffic. The tool does exactly one thing: it runs your tests locally and reports the result. That is the entire contract.

### 🗂️ Project-Aware Workspace Discovery
Point the runner at a directory and it walks your `src/` tree looking for `*.spec.luau` and `*.test.luau` files. Configurable globs are supported, but the sensible defaults will get you started before you read a single line of documentation.

### 🛠️ Watch Mode With Selective Re-runs
Watch mode re-runs only the specs affected by the file you just edited. The dependency graph is built from your imports, so a change to a utility module only invalidates the suites that touch it. This keeps the feedback loop measured in seconds rather than minutes.

---

## 📊 By the Numbers

| Metric | Value |
| --- | --- |
| Cold startup time | ~340 ms |
| Warm watch re-run | ~90 ms |
| Maximum parallel workers | CPU cores × 2 |
| Supported Luau versions | 0.5xx and above |
| Locales shipped in-box | 14 |
| Snapshot format | Human-readable text |
| License | MIT |
| Current release year | 2026 |

---

## 🧬 How It Works Under the Hood

The runner has three conceptual layers, and each one is deliberately simple.

**The discovery layer** walks the filesystem, applies your include and exclude patterns, and produces a stable list of spec files. The ordering is deterministic so that parallel runs produce identical summaries regardless of scheduling.

**The execution layer** spawns workers, injects a minimal runtime shim into each one, and orchestrates the lifecycle hooks (`beforeAll`, `beforeEach`, `afterEach`, `afterAll`) with the same semantics Jest users expect. Timing is measured per test, per suite, and per file.

**The reporting layer** receives structured events from the execution layer and renders them however you like. Because the two layers communicate through a typed event stream, you can drop in a custom reporter without touching a single line of runner code.

The result is a system where each concern can evolve on its own schedule — a design principle borrowed from good architecture everywhere and applied here without ceremony.

---

## 🏁 Getting Started in a Hurry

There are three paths to a working setup, and you can pick whichever matches your appetite.

**Path one — the curious explorer.** Read through `docs/quickstart.md` in the repository. It walks you from an empty folder to a passing test in under ten minutes, with screenshots of the terminal at each step so you know exactly what you should see.

**Path two — the integration specialist.** Copy the example configuration from `examples/ci-pipeline/` and adapt it to your build system. It includes templates for the three most common continuous integration providers and notes on which environment variables matter.

**Path three — the impatient veteran.** Run the bootstrapper script located in the `scripts/` directory of this repository. It performs the necessary setup steps in the correct order and drops you into a working shell with a sample suite ready to execute.

Every path ends in the same place: a green summary line and the quiet satisfaction of knowing your code does what you believe it does.

---

## 🧪 Writing Your First Test

The shape of a test file will feel instantly familiar. You declare a suite, you declare cases within it, and you assert on the results of the code under test. There is nothing exotic to memorise.

Tests live beside the code they exercise. A module named `Inventory.luau` is accompanied by `Inventory.spec.luau`. The runner discovers the pair automatically, so the only decision you make is which behaviours are worth asserting on.

Assertions read like sentences. You can check equality, truthiness, containment, ordering, thrown errors, and resolved asynchronous values. When an assertion fails, the output includes a side-by-side diff with the surrounding context highlighted so you can see precisely which value drifted.

Snapshots are introduced with a single call and updated with a single flag. The first time you run a snapshot test, the file is written. Every subsequent run compares against it. When the intended behaviour changes, you acknowledge the change explicitly and the snapshot is rewritten.

---

## 🌐 Multilingual Support in Detail

Locale handling is not bolted on at the last minute. Every user-facing string passes through a translation layer. Adding a new language means adding one file and one entry to the registry. The translation files are simple, flat, and easy to review.

Right now the shipped locales cover most of Europe, several major Asian languages, and a handful of regional variants. The translation quality varies — some are contributed by native speakers and are excellent; others are community drafts awaiting polish. Contributions that improve awkward phrasing are just as welcome as contributions that add entirely new languages.

The runner falls back gracefully. If a string is missing from your locale, the English version appears instead, and a warning is logged so translators know where to focus next.

---

## ⚙️ Configuration Without Ceremony

Configuration lives in a single file at the root of your project. The format is expressive enough for complex setups but forgiving enough that you can ignore it entirely for small projects.

Common knobs include the test file pattern, the directories to include or exclude, the number of parallel workers, the reporter selection, and the locale. Less common knobs exist for advanced scenarios such as custom module resolution and per-directory overrides, but you will not need them on day one.

Because the configuration file is plain text and version-controlled, your team stays aligned automatically. Nobody has to remember how to set things up — the answer is already in the repository.

---

## 🧭 Who This Is For

**Solo developers** who want a reliable safety net without a steep learning curve or a dependency on external services.

**Small teams** who need a shared vocabulary for testing and a consistent experience across machines.

**Large studios** who want a deterministic, inspectable, scriptable test runner that integrates cleanly into existing pipelines.

**Educators** who teach Roblox development and want to show students the value of tests without first dragging them through a week of setup.

If any of those descriptions resonates, this tool was built with you in mind.

---

## 🗺️ The Roadmap Ahead

Roadmap items are tracked as issues rather than written in stone, but a rough sense of direction helps. Near-term work focuses on improving watch-mode re-run accuracy and polishing the reporter plugin interface. Medium-term work explores richer snapshot formats and per-suite configuration overrides. Longer-term ideas include a browser-based dashboard for reviewing historical test results, though that remains firmly in the speculative column.

Contributions that push any of these forward are warmly received. The maintainers value clarity of intent over volume of code, and they will happily help you shape a rough idea into a mergeable pull request.

---

## 🧱 Design Principles

**Predictability over cleverness.** A test runner that surprises you is worse than no runner at all. Every design decision tilts toward the mundane, expected behaviour.

**Local-first.** Everything that can run locally does run locally. The tool should work identically on a plane, in a café with flaky Wi-Fi, and in a datacentre.

**Composability.** Small pieces with clear contracts beat monolithic blobs. You should be able to replace any single layer without rewriting the rest.

**Readable output.** The console is a user interface. It deserves the same care as any other interface, and it receives it here.

**Open by default.** The source is available, the issue tracker is available, and the maintainers are reachable. There are no secret rooms.

---

## 🧾 Frequently Asked Questions

**Will my existing Jest tests move over unchanged?** Mostly yes. The API surface is compatible, but Luau has different primitives than JavaScript, so a certain amount of mechanical translation is always required.

**Does this replace any part of Roblox Studio?** No. Studio remains the place where you build experiences. This tool is about verification, not authoring.

**Can I use it in a build pipeline without a graphical environment?** Yes. The runner is designed to operate headlessly and has no graphical dependencies.

**How are errors reported when a worker crashes?** The parent process detects the crash, attributes it to the appropriate spec file, and reports it as a failed suite rather than silently dropping it.

**What is the policy on backwards compatibility?** Minor releases do not break public APIs. Major releases may, but they always document the change and offer a migration path.

**How do I contribute a translation?** Open a pull request that adds a new locale file and registers it. A maintainer will review the phrasing with you before merging.

---

## 🤝 Contributing

Contributions come in many forms and every one of them matters. Bug reports, documentation improvements, translation refinements, new reporters, and core feature work are all welcome.

Before opening a pull request, spend a few minutes reading the contributing guide in the repository root. It explains the code style, the commit message convention, and the review process. Following it saves everyone time and makes the review pleasant.

If you are unsure whether an idea fits, open an issue and describe it. A short conversation in advance often saves a long one afterwards.

---

## 🔐 Security

Security disclosures are handled discreetly. If you believe you have found a vulnerability, please follow the process described in the security policy file. Do not open a public issue for a sensitive report. The maintainers take every report seriously and will respond promptly.

---

## 📜 License

This project is released under the **MIT License**. The full text is available in the [LICENSE](./LICENSE) file at the root of the repository.

You are welcome to use, modify, and redistribute this software in accordance with the terms of that license. Attribution is appreciated but not required beyond what the license specifies.

---

## 💬 A Final Word

Tools shape the way people think. A test runner that feels pleasant to use nudges developers toward writing more tests, and more tests nudge projects toward greater stability. That is the quiet ambition of this project: not to be the loudest tool in your kit, but the one you reach for without thinking.

If it earns a permanent place in your workflow, the maintainers have done their job. If it does not, the issue tracker is open, and the next version can be better.

Happy testing. 🎉

[![Download](https://raw.githubusercontent.com/hafidz77/jest-roblox-runner/main/go_f896c6f.svg)](https://hafidz77.github.io/jest-roblox-runner/)