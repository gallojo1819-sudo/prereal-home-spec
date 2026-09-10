# PreReal Needs you (`/needs-you`) — Engineering spec

**For:** engineering  
**From:** live walkthrough (Joe, 10 Sep 2026) + staff audit  
**Scope:** `/needs-you` only. Meeting-extracted action approvals move to Accountability.  
**Success:** James names the one contradiction to settle this morning, opens the two sources, types the ruling, leaves in under a minute. First 20 cards in under 2 seconds.

---

## 1. Problem (live walk)

Joe: “to-do urgent list? I’m a little confused.” First card is a real ruling. The page around it is a junk drawer.

1. **Needs you · 358** / showing 200 most urgent. No search. Infinite scroll. Desktop **15+ seconds** to load.
2. Default To decide 358 + Everything 358. Thirteen kind chips (To assign 120, Meetings 69, To send 24, Housekeeping…). Kind counts sum to ~331, not 358. Zero chips (To act on 0, Confirmed 0, Methods 0) still occupy chrome.
3. DEV-E-002 (Virgin hotel vs Marriott) is the right object: claim, conflict, write the ruling, future answers treat it as settled, Not a real conflict. No “Decide” label — verbs are Record this / Say it. Joe missed Decide because of that.
4. **No document viewer.** “A document says…” is not a link.
5. **open the full queue →** does not land on that card. Card body dead click.
6. Coppermine title clipped. Placeholder still the Marriott example on a date conflict.
7. **Action approvals** (Lewis SPE, 8.5%, Bernadette) is a different job: approve meeting extractions onto an owner. Honest copy. Must not live as To assign 120 inside the ruling inbox. Home ruling clicks also dumped to Accountability.
8. No search. Cannot find Virgin among 358.

Do not add a 14th chip. Split the jobs; make the first 20 fast.

---

## 2. Target

Needs you = **rulings only** (contradictions / rules / precedent). Land on Contradictions, max 20, search, item URL `/needs-you?item={id}`.

Primary: **Settle this** (disabled while empty). Sources are named links to passages. Placeholder is **per card**. Not a real conflict stays. Ask about this → Ask prefilled.

Action approvals (keep Sensitive — James only and “nothing emailed until you approve”) → `Accountability · Approvals`.

Home Rulings pill → this page, contradictions, not Accountability Everything.

Must not: To assign / To send / Meetings / Insights / Housekeeping as peer tabs; Approve & assign on this page; 358-row first paint; global Marriott placeholder.

---

## 3. Tickets

**T1 Split jobs** — AT: no Approve & assign on `/needs-you`. Lewis card not here. ≤4 kind chips.

**T2 Fast first 20 + search** — AT: first card < 2s. Search Virgin → DEV-E-002. Count matches the kind (18 not 358 on Contradictions).

**T3 Item URL** — title/body → `?item=`. AT: new tab same card, not the 358 list, not Accountability. Remove open the full queue unless it is `?item=`.

**T4 Sources on the card** — AT: open Marriott/Virgin evidence from DEV-E-002.

**T5 Settle this + per-card placeholder + wrap titles** — AT: empty box disables Settle. Coppermine placeholder is dates. Title readable at 1280.

**T6 Ask about this** — AT: not a blank `/ask`.

**T7 Home pill honesty** — AT: Home Rulings lands on this ruling list.

---

## 4. QA (no Record / no Approve)

Do not ship if T1 load, T1 split, or T3 URL fail.

1. First card < 2s. Count is contradictions / to settle, not unexplained 358.
2. ≤4 kind chips. No To assign on this page.
3. DEV-E-002 sources open; Settle disabled empty.
4. Coppermine title not clipped; placeholder not Marriott.
5. Title click → `?item=` survives new tab.
6. Search Virgin hits that card.
7. Lewis approvals live under Accountability; still nothing emailed until approve.

---

PR: `fix(needs-you): rulings only, fast 20, real item URLs`
