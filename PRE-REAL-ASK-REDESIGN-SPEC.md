# PreReal Ask (`/ask`) — Engineering spec

**For:** engineering  
**From:** live walkthrough (Joe, 10 Sep 2026) + staff audit  
**Scope:** Ask only.  
**Success:** James asks a company question, gets a document-cited answer, can open the source, and can return to that thread tomorrow.

---

## 1. Problem (live walk, 10 Sep 2026)

1. **Old threads do not open.** Clicking a past thread shows the current Ask, not that conversation. No usable thread URL.
2. **What is PreReal?** returned `Error: canceling statement due to statement timeout` as if it were an answer, with Why / Add to silo memory / Share still attached.
3. After the error, scope jumped **Cart Barn → Everything**. Continue-where-you-left-off chips were generic marketing, not the failed question.
4. Useful **short answer was buried** under GOALS DETECTED / Approve agent cards (Virgin Galactic, Sierra County, Brand Manager) on a definitional question.
5. Source chips smashed (`Youareasenior MAandcapital m…`).
6. **Lewis question worked** (James BCatch Up 2026-08-31, citation pills, honesty strip) then dumped **FROM OUTSIDE PREREAL · LIVE WEB RESEARCH · 79** irrelevant CRE articles.
7. Dual project control: Cart Barn chip + Focus on a project dropdown.
8. **Add to silo memory** + answer says silos.
9. Project brief stamped **2026-08-16** (stale). Paperclip destination unknown. Auto unexplained. Placeholder Ask anything...

Do not add more follow-up chips. Thread identity + timeout + web-dump are the bug.

---

## 2. Target

One corpus chip. Real `/ask?conversation={id}`. Answer order: **short answer → honesty → document sources → web (off by default, max 5)**. Errors look like errors. No agent-approve on Q&A. No silo in chrome.

Must not: timeout with Share/Memory; 79 web links on a doc question; two project pickers; thread click that ignores the thread.

---

## 3. IA

Ask = chat with the corpus. Research = run an engine and file. Do not merge.

**One corpus control** — remove Focus on a project dropdown. Chip is Cart Barn | Everything. Paperclip = From Records. Globe = live web, **off** by default when a project is set. Mid-thread switch banners; do not silent-switch Cart Barn → Everything.

**Threads** — every conversation has an id. List click and refresh restore that transcript. Kill “start a new chat (the context still carries).” New question vs Follow up.

**Answer order** — (1) short answer first (2) honesty strip (3) document sources (4) live web collapsed, globe on only, ≤5 (5) follow-ups from this answer only (6) no Goals Detected / Approve on Q&A. Optional one-liner: Save as Accountability task?

**Errors** — `Couldn’t finish that against your documents. [Try again]`. No Why / Memory / Share / continue chips on an error.

---

## 4. Copy

| Current | Replace |
|---------|---------|
| Ask anything... | Ask about {project}’s documents… / Ask across indexed company documents… |
| Focus on a project (optional) | Remove |
| Add to silo memory | Pin to {project} memory (completed answers only) |
| silos in answers | projects |
| CONTINUE WHERE YOU LEFT OFF generic | Follow-ups after a successful answer |
| start a new chat (the context still carries) | New question |
| GOALS DETECTED — APPROVE TO PUT AN AGENT ON IT | Remove from Ask |
| LIVE WEB RESEARCH · 79 | Live web · n≤5 · globe on only |
| statement timeout as the answer | Couldn’t finish that against your documents. [Try again] |
| Not fully backed by your documents | Keep |

Auto menu must name engines in English: Auto = docs first; Library = indexed only; Web = live web.

---

## 5. Tickets

**T1 Threads are real** — `/ask?conversation={id}` restores that transcript. AT: click thread A, see A, not the latest question. URL survives new tab.

**T2 Timeouts are errors** — no action pills on timeout. Bound/fix statement timeout. AT: What is PreReal? returns a short answer, not SQL cancel.

**T3 Docs first, web gated** — globe off ⇒ zero web block. Globe on ⇒ ≤5 under docs. AT: Lewis question, globe off, no 79 CRE blogs.

**T4 One project control + placeholder** — AT: only one Cart Barn control; placeholder names the corpus.

**T5 Answer order + kill agent-approve on Q&A** — AT: What is PreReal? has no Virgin Galactic Approve cards; short answer first.

**T6 silo → project** — AT: no silo in Ask chrome.

**T7 Paperclip = Records picker** — labeled From Records. AT: cancel adds nothing.

---

## 6. Out of scope

Research IA. Make a deck. Local disk upload unless already built (then label it). Approving agents / writing goals from Ask. Sending email. Charter editor.

---

## 7. QA (do not ship if 2, 4, or 5 fail)

1. Cart Barn: one control; placeholder names it.
2. What is PreReal? — no timeout-as-answer; short answer first; no Approve cards.
3. Source chip opens the passage.
4. Lewis question, globe off — citations + honesty, no 79 web links.
5. Open an old thread — old transcript, not the new one. URL works in a new tab.
6. Paperclip → Records picker.
7. Find-in-page silo: no chrome hits.

---

## 8. PR title

`fix(ask): real threads, honest errors, docs-first answers`

Ask is done when yesterday’s thread opens and a company question does not come back with 79 CRE blog links.
