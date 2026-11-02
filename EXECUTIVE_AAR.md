# Executive After-Action Report

### Huntress CTF 2026: AI Arena

**Prepared by:** Dr. Jennifer Schieferle Uhlenbrock &nbsp;·&nbsp; **For:** Huntress CTF &nbsp;·&nbsp; **Team:** SU Pack &nbsp;·&nbsp; **Date:** October 31, 2026

---

## 1. Executive summary

Team SU Pack completed every challenge in Huntress CTF 2026: AI Arena — a 31-day, AI-assisted capture-the-flag event — finishing at **561 of 561 flags (100%)** for the maximum **1,885 points**, the maximum attainable score, for a final standing of **51st place** on the live scoreboard. Many teams reached the same point maximum, and placement among them was decided by submission time.

The clear-the-board result was driven by consistent daily execution, an AI-agent-assisted workflow (the in-platform "Game Master"), and disciplined **static-first analysis** of every malware and binary specimen — nothing was executed. Two challenges stood out as the hardest of the month: **SHA1-Hulud** (a self-hashing, anti-analysis Rust PE) and **Framework Roulette** (a multi-stage web trust-boundary puzzle). Both were ultimately solved, with process lessons captured below.

## 2. Outcome at a glance

| Track | Challenges | Modes each | Status |
|---|---:|:--:|:--:|
| 👶 Warmups | 31 | 3 (S/T/M) | 100% ✅ |
| ⚙️ Binary Reverse Engineering | 32 | 3 (S/T/M) | 100% ✅ |
| 📜 Script Analysis | 31 | 3 (S/T/M) | 100% ✅ |
| 📱 Mobile | 31 | 3 (S/T/M) | 100% ✅ |
| 🌐 Web Exploitation | 31 | 3 (S/T/M) | 100% ✅ |
| 🔎 Metadata Forensics | 31 | 3 (S/T/M) | 100% ✅ |
| 🤖 AI Native | 1 | Single | 100% ✅ |
| ℹ️ Information | 1 | Single | 100% ✅ |
| **Total** | **189** | **561 flags** | **561/561** |

## 3. Cadence & timeline

Challenges unlocked daily at 9:00 AM Eastern. The team sustained same-day clears for the full month, with difficulty ramping across three phases:

- **Days 1–18 — Foundations:** one challenge per track per day; orientation and primitive-building (encodings, headers, static triage, single-flaw web/mobile tasks).
- **Days 19–29 — Expansion:** the Web Exploitation track came online and daily counts rose to 7–8 challenges as cross-track, correlation-heavy tasks appeared.
- **Days 30–31 — Capstones:** the hardest, most integrative work — SHA1-Hulud (Day 30) and the Day 31 "gauntlet" finales (Final Boss, The Full Transform, Mobile Arena Gauntlet, Framework Roulette) that composed the entire month into single challenges.

## 4. What worked

- **Static-first discipline.** Every specimen was analyzed without execution — safe handling that never blocked a solve.
- **AI-agent orchestration.** The Game Master agent fetched targets, ran static tooling, and returned answers, with a human/orchestration layer directing scope and verifying before submission.
- **Check status before grinding.** Large Mastery bundles were sometimes already completed via the shared team attempt; querying status first saved substantial effort on Final Boss and The Full Transform.
- **Checkpoint files for long traces.** On very long reverse-engineering traces, a persistent progress file let the analysis survive context compaction and resume from the last unresolved item.
- **Parallel work streams.** Running independent Game Master threads per challenge improved throughput on heavy days.

## 5. Risks, gaps & governance notes

**5.1 Autonomous submission outran the "confirm before submitting" control.** The standing instruction to confirm before submitting any flag was enforced at the orchestration layer, not pushed into the autonomous Game Master agent. During a multi-hour disconnect, the agent kept working and, for at least SHA1-Hulud, submitted on its own once confident. The result was correct, but the control was bypassed.
*Recommendation:* push "do not submit without external confirmation" directly into the autonomous agent's own instructions.

**5.2 Long disconnects can expire the underlying agent session.** The ~4-hour outage expired the Game Master's conversation session server-side, making the detailed solve trace for the two hardest challenges unrecoverable from the chat UI. The exact winning submissions were recovered from the platform's own submission record.
*Recommendation:* assume agent sessions may expire during unattended gaps; capture submitted values at submission time rather than reconstructing later.

**5.3 Flag provenance.** All 561 flags were recovered from the platform's authenticated record of accepted submissions for Team SU Pack, and every one reads back as *correct*. For SHA1-Hulud and Framework Roulette specifically, the flag values are trustworthy but the exact final solve sequence was not auditable from the chat UI after the session expiry.

## 6. Recommendations for next event

| Recommendation | Rationale / action |
|---|---|
| Harden the submission control | Embed the confirmation gate in the autonomous agent itself; capture values at submit time. |
| Plan for session expiry | Treat long unattended windows as session-ending; checkpoint state to durable files. |
| Use checkpoint files proactively | Adopt the progress-file technique at the start of any long binary-RE trace. |
| Status-first on Mastery bundles | Always query shared-attempt status before investing in large multi-set grinds. |
| Keep static-first as policy | It served the whole event with no downside; retain it as the default handling rule. |

## 7. Conclusion

Huntress CTF 2026 was completed in full — a 100% clear across all six tracks and all three difficulty modes, at the maximum point total, for a 51st-place finish. The team demonstrated both breadth and depth (the SHA1-Hulud self-hash and the Framework Roulette trust-boundary chain). The two governance gaps above are the main carry-forward items; neither affected the final result, and both have concrete fixes.

---

*Full per-challenge detail is in the [Technical Write-up Collection](TECHNICAL_WRITEUPS.md); a shareable narrative is in the [Professional Recap](PROFESSIONAL_RECAP.md).*
