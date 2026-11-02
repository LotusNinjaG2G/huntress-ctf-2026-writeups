# Clearing the Board at Huntress CTF 2026

### How Team SU Pack finished all 561 flags in the AI Arena

**Prepared by:** Dr. Jennifer Schieferle Uhlenbrock &nbsp;·&nbsp; **For:** Huntress CTF &nbsp;·&nbsp; **Team:** SU Pack &nbsp;·&nbsp; **Date:** October 31, 2026

---

> *"561 of 561 flags. Every track, every mode, every day of a 31-day gauntlet — finished at the maximum score of 1,885 points, for a 51st-place finish."*

## The short version

Huntress CTF 2026: AI Arena ran for 31 days, releasing fresh challenges every morning across six technical disciplines. Team SU Pack cleared the entire event — all **189 challenges and 561 flags**, in all three difficulty modes — for a perfect **100% completion** at the maximum attainable score. It was a month of steady, disciplined work that ended in a clean sweep.

## The arena

"AI Arena" was the fourth installment of Huntress's annual CTF, and the twist was in the name: solvers worked alongside an in-platform AI agent, the "Game Master," to fetch targets, run tooling, and reason through each task. The six tracks spanned the full spectrum of defensive and analytical security work:

- **Warmups.** Encoding and cipher puzzles — the daily on-ramp, from Base64 to Baconian to exotic radix tricks.
- **Binary Reverse Engineering.** Static analysis of binaries across a dozen languages and platforms — ELF, PE, Mach-O, Go, Rust, .NET, and more.
- **Script Analysis.** Reading malware scripts in 30+ languages without ever running them: classify intent, map ATT&CK, pull indicators.
- **Mobile.** Android APK teardown — manifests, DEX, native libraries, obfuscation and integrity checks.
- **Web Exploitation.** Finding and proving the flaw behind each application's trust boundary, from IDOR to SSRF to request smuggling.
- **Metadata Forensics.** Trusting bytes over labels — fingerprinting artifacts by structure and hash to expose the fakes.

Each track ran one challenge per day for the whole month, in three escalating modes — **Single Solve**, **Time Trial**, and **Mastery**.

## How the month unfolded

The difficulty curve was deliberate. The first two and a half weeks built primitives. Around Day 19 the Web Exploitation track opened and the daily workload climbed to seven or eight challenges, demanding cross-track correlation. The final stretch, Days 30 and 31, was the real test: integrative "gauntlet" challenges that folded the entire month into single problems.

Two challenges earned their reputation as the hardest of the event:

**SHA1-Hulud — the marquee.** A team-unique, Rust-compiled Windows binary wrapped in custom string obfuscation, anti-analysis checks, and self-modifying code. It computed its answer through a multi-stage pipeline that hashed the program's *own code section* and mixed in CPU-timing values — a design built to resist exactly the static analysis used to crack it. It took several sessions, a correction about Windows calling conventions, and the discovery that the timing "noise" mostly cancelled itself out, but it fell.

**Framework Roulette — the trust-boundary maze.** An unfamiliar web stack behind a two-stage access gate: first a gateway that only trusted a loopback address as the leading hop, then a custom staff-only policy header whose exact value was the puzzle. The first gate was fully reverse-engineered and reproducible; the challenge was ultimately cleared across all three modes.

## What made the clean sweep possible

- **Analyze, don't detonate.** Every hostile sample was studied statically — never executed.
- **Let the agent do the legwork, keep a human on the wheel.** The Game Master handled fetching, tooling, and computation; scope and verification stayed with the operators.
- **Work smart on the big sets.** Several massive Mastery bundles were already complete through the shared team attempt — checking status first saved hours.
- **Leave a trail on long traces.** A running checkpoint file of every confirmed fact kept marathon reverse-engineering sessions from unravelling.

## Honest footnotes

No month-long effort is perfectly tidy. During the endgame, a multi-hour disconnect let the autonomous agent submit a flag on its own before the "confirm first" step could happen — the answer was right, but the control was bypassed. That same outage expired the agent's session, so the detailed solve traces for the two hardest challenges had to be reconstructed from the platform's submission record. Both are fixable with tighter controls, and neither changed the result.

## The bottom line

Thirty-one days, six disciplines, three difficulty modes, and not a single flag left on the table. Team SU Pack finished Huntress CTF 2026 at **561/561 — 100% completion at the maximum score of 1,885 points, placing 51st.** Many teams reached the same point ceiling, with final placement decided by submission time.

---

*Companion documents: [Executive After-Action Report](EXECUTIVE_AAR.md) · [Technical Write-up Collection](TECHNICAL_WRITEUPS.md).*
