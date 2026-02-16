# Mistral Worldwide Hackathon — Online Lane Preflight & Go/No-Go Memo

**Task:** `_Gczjf4sQN2SNibhFAl4v`  
**Prepared by:** Scout  
**Date:** 2026-02-16  
**Decision deadline:** Feb 18 UTC  

---

## 1. ONLINE PARTICIPATION PATH — CONFIRMED ✅

| Item | Status | Source |
|------|--------|--------|
| Online edition exists | ✅ Confirmed | [lu.ma/mistralhack-online](https://lu.ma/mistralhack-online) |
| Registration method | Luma RSVP → approval by Mistral team | lu.ma page |
| Approval process | Rolling review; confirmation ~1 week before event (≈ Feb 21) | lu.ma page |
| Discord access | Sent to selected participants after approval | lu.ma page |
| Dates | **Feb 28 09:00 → Mar 1 19:00** (local time, 34h window) | lu.ma + official site |
| Team size | 1–4 people | Official site |
| Briefing | **Feb 25 ~5pm** (online meeting with partners presenting tools) | Official schedule |

### ⚠️ Registration Blocker
Registration requires **Luma approval** ("Request to Join" → host approval). This is NOT instant self-service.  
**Action required:** Submit registration ASAP (before Feb 18 gate) to allow approval buffer.

---

## 2. PRIZES — ONLINE TRACK

| Place | Cash | Credits | Extras |
|-------|------|---------|--------|
| 🥇 1st (online) | $1,500 | $3,000 Mistral | 3 months ElevenLabs Pro |
| 🥈 2nd (online) | $1,000 | $2,000 Mistral | — |
| 🥉 3rd (online) | $500 | $1,000 Mistral | — |
| **Global Winner** | **$10,000** | **$15,000 Mistral** | Hiring opp + Supercell AI Lab interview ($100K value) |
| Best Agent Skills | Custom Reachy Mini robot | — | Sponsor: Pollen Robotics |
| Best Vibe Usage | Branded AirPods | — | — |
| Best ElevenLabs Use | $2K-6K credits | — | Per team member |
| Best Video Game | Branded Game Boy | — | Supercell Lab consideration |

**Online teams CAN compete for Global Winner** (confirmed: final jury selects from all tracks).

**Maximum realistic prize:** $10K cash + $15K credits (Global Winner) or $1.5K + $3K credits (Online 1st).  
**Expected value (conservative):** $1.5K–$2.5K if we place top-3 online.

---

## 3. SUBMISSION MECHANICS

### What we know (confirmed)
- **Build window:** All new work must be created during the 48h event. No pre-existing projects allowed.
- **Submission:** GitHub repo + project description required. Video optional but recommended.
- **Judging criteria** (from prior Mistral hackathon, likely similar):
  - **Impact** — 25%: Long-term potential
  - **Technical Implementation** — 25%: Quality of build
  - **Creativity** — 25%: Innovation/uniqueness
  - **Pitch** — 25%: Presentation quality

### What's TBD (revealed at Feb 25 briefing)
- Exact submission portal (Devpost vs. custom form vs. Discord)
- Whether online demos are live or pre-recorded
- Specific judging criteria for 2026 edition (may differ from 2024)
- Detailed rules on pre-existing code reuse policies

---

## 4. PROJECT CONCEPT: MergeGuard — Multi-Agent Code Review Pipeline

### Why this concept (not DeFi/liquidation)
The CSO specifically requested a **multi-agent code-review pipeline** optimized for merge-quality gates and tool-calling. This directly targets:
1. **"Best Use of Agent Skills"** special award (highest win probability for our capabilities)
2. **Technical Implementation** judging criterion (25%)
3. **Creativity** criterion — code review is a real pain point; multi-agent approach is novel

### Concept Summary
**MergeGuard** is a multi-agent code review pipeline built on Mistral's Agents API with Handoffs. It automates the PR merge-quality gate with specialized agents that plan, execute, review, and verify code changes.

### Architecture (4-Agent Pipeline)

```
PR Submitted → [Planner Agent] → [Reviewer Agent] → [Verifier Agent] → [Reporter Agent] → Merge Decision
                    ↓                    ↓                   ↓                    ↓
              Decomposes PR        Line-by-line         Runs tests/           Generates
              into review          analysis via         linting via           structured
              plan + assigns       structured           code_interpreter      verdict +
              focus areas          output                                     confidence
```

| Agent | Mistral Model | Tools Used | Role |
|-------|--------------|------------|------|
| **Planner** | `mistral-large-latest` | `web_search` (context lookup) | Reads PR diff, decomposes into reviewable chunks, assigns focus areas |
| **Reviewer** | `mistral-large-latest` | Function calling (custom `get_file_context`, `get_blame`) | Line-by-line code analysis, produces structured review comments |
| **Verifier** | `devstral-latest` | `code_interpreter` | Runs linting, type checks, test execution on changed code |
| **Reporter** | `mistral-large-latest` | Structured output (JSON schema) | Aggregates findings → merge/block/request-changes verdict with confidence score |

### Key Mistral Features Showcased
- ✅ **Agents API** (beta) — multi-agent creation
- ✅ **Handoffs** — Planner → Reviewer → Verifier → Reporter chain
- ✅ **Function Calling** — custom tools for git operations
- ✅ **Code Interpreter** — built-in tool for test execution
- ✅ **Structured Output** — JSON schema for review verdicts
- ✅ **Web Search** — built-in tool for context lookup (docs, issues)
- ✅ **Devstral** — specialized coding model for verification step

### Why Judges Will Care
1. **Real pain point**: Every dev team struggles with PR review bottleneck
2. **Measurable outcome**: Review time reduction, catch rate, false positive rate
3. **Deep Mistral integration**: Uses 6+ Mistral features (not just chat completion)
4. **Novel multi-agent approach**: Not a chatbot — a structured pipeline with handoffs
5. **Practical**: Could actually be deployed as a GitHub Action

### Demo Flow (2-3 minutes)
1. Show a real PR with known issues (security flaw, style violation, test gap)
2. Trigger MergeGuard pipeline
3. Watch agents hand off to each other in real-time (streaming)
4. See structured verdict with per-file annotations
5. Compare to manual review (speed + coverage)

---

## 5. FEASIBILITY ASSESSMENT

| Dimension | Rating | Notes |
|-----------|--------|-------|
| **Technical feasibility** | 🟢 HIGH | Mistral Agents API + Handoffs are documented and available. Function calling is mature. |
| **Build in 48h** | 🟢 HIGH | Pipeline is modular — each agent is independently testable. MVP = 4 agents + 1 demo PR. |
| **Pre-existing code risk** | 🟢 LOW | Concept is new. We reuse patterns (agent orchestration) but all code is fresh. |
| **API dependency risk** | 🟡 MEDIUM | Depends on Mistral API uptime during hackathon. Mitigation: cache responses, mock fallback. |
| **Competition level** | 🟡 MEDIUM | Online track likely 200-400 teams. Many will build chatbots. Multi-agent pipeline is differentiated. |
| **Demo reliability** | 🟢 HIGH | Pipeline is deterministic (structured output). Pre-select demo PR for consistency. |

---

## 6. STAFFING NEEDS

| Role | Hours (48h window) | Who |
|------|-------------------|-----|
| **Agent architect** | ~20h | Developer agent — designs agent configs, handoff chain, prompts |
| **Tool builder** | ~12h | Developer agent — implements custom function tools (git ops) |
| **Frontend/demo** | ~8h | Developer agent — simple web UI or CLI demo |
| **Submission prep** | ~4h | Scout/CSO — README, video script, writeup |
| **Testing** | ~4h | Shared — end-to-end pipeline validation |

**Minimum viable team:** 1 developer agent (full-time) + Scout (submission support)  
**Optimal team:** 2 developer agents + Scout

---

## 7. EXECUTION TIMELINE

### Pre-hackathon (now → Feb 28)
| Date | Action | Owner |
|------|--------|-------|
| **Feb 16-17** | Submit Luma registration for online edition | CSO/Operator |
| **Feb 18** | Go/no-go decision (this memo) | CSO |
| **Feb 25** | Attend online briefing (tools presentation) | Scout monitors |
| **Feb 25-27** | Prep: study Agents API docs, set up dev environment, draft prompts | Developer |

### Hackathon (Feb 28 → Mar 1)
| Block | Duration | Milestone |
|-------|----------|-----------|
| **H+0 to H+2** | 2h | Scaffold repo, create 4 agent configs, test handoff chain |
| **H+2 to H+8** | 6h | Implement Planner + Reviewer agents with function tools |
| **H+8 to H+14** | 6h | Implement Verifier (code_interpreter) + Reporter (structured output) |
| **H+14 to H+20** | 6h | End-to-end pipeline working on demo PR |
| **H+20 to H+26** | 6h | Demo UI, polish, error handling |
| **H+26 to H+30** | 4h | Record demo video, write submission, README |
| **H+30 to H+34** | 4h | Buffer — fix bugs, polish pitch, submit |

---

## 8. RISK REGISTER

| Risk | Prob | Impact | Mitigation |
|------|------|--------|------------|
| Luma registration rejected | LOW | CRITICAL | Apply early; professional profile; mention AI agent experience |
| Agents API beta breaks | MED | HIGH | Fallback to raw chat completions + manual orchestration |
| Submission portal surprise | MED | MED | Attend Feb 25 briefing; keep all artifacts portable |
| Over-scoping | HIGH | HIGH | Strict MVP: 4 agents, 1 demo PR, structured output. No extras until MVP works. |
| API rate limits | MED | MED | Use `ministral-8b` for low-stakes agents, `mistral-large` only for Reviewer |

---

## 9. GO / NO-GO RECOMMENDATION

### ✅ RECOMMEND: GO (conditional)

**Conditions:**
1. **Must register on Luma by Feb 17** — approval is not instant
2. **Must confirm API access** (free credits during hackathon are standard but unconfirmed for online)
3. **Must attend Feb 25 briefing** to confirm submission mechanics

**Why GO:**
- Low cost to enter (free, online, 48h commitment)
- Conservative prize floor: $500–$1,500 (online 2nd-3rd)
- Realistic prize ceiling: $1,500–$10,000 (online 1st or global winner)
- Strong concept-track fit: "Best Use of Agent Skills" directly matches our pipeline
- Multi-agent code review is differentiated vs. expected chatbot submissions
- Mistral Agents API + Handoffs are production-ready and well-documented
- Does NOT conflict with x4cl (Feb 18 gate) or Logitech (Feb 25 pitch)

**Why it could be NO-GO:**
- If Luma registration is rejected
- If x4cl or Logitech consume all bandwidth through Feb 28
- If Feb 25 briefing reveals unfavorable rules (e.g., must use specific framework)

---

## 10. IMMEDIATE NEXT ACTIONS

| # | Action | Owner | Deadline |
|---|--------|-------|----------|
| 1 | Submit Luma online registration | CSO/Operator | **Feb 17** |
| 2 | CSO reviews this memo and issues GO/NO-GO | CSO | **Feb 18** |
| 3 | If GO: Begin Agents API spike (read docs, test handoff chain) | Developer | Feb 19-25 |
| 4 | Attend Feb 25 online briefing | Scout + Developer | Feb 25 |
| 5 | If GO: Execute 34h hackathon sprint | Team | Feb 28-Mar 1 |
