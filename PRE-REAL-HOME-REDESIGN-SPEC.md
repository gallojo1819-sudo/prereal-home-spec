# PreReal Home (`/ceo`) — Engineering spec

**For:** engineering / whoever owns `/ceo`  
**From:** product walkthrough (Joe, 10 Sep 2026) + staff audit  
**Scope:** Home only. Do not redesign Ask, Needs you, Accountability, Records, or Project status in this ticket set. Home must **deep-link into those rooms correctly**.  
**Success:** A principal can answer “what do I do in the next 10 minutes?” from Home without hunting.

---

## 0. How to read this

- **Must** = ship in this sprint or Home still fails.
- **Must not** = do not “improve” by adding more widgets.
- Acceptance tests are click-tests a PM can run on `/ceo` logged in as James (CEO).

Related live routes (do not invent new ones unless noted):

| Room | Canonical URL |
|------|----------------|
| Home | `/ceo` |
| Ask | `/ask` |
| Needs you | `/needs-you` |
| Accountability | `/accountability` |
| Project status | `/goals` |
| Records | `/workspace` |
| Records Find | `/workspace?tab=search` (verify live tab query) |
| Records Timeline | `/workspace?tab=timeline` |
| Records Review | `/workspace?tab=review` |
| Signals | `/signals` |
| Brokerage | `/ceo/brokerage` |
| New Mexico | `/ceo/new-mexico` |

If a query param below does not exist yet, **add it**. Do not fake the filter in the UI while loading the unfiltered list.

---

## 1. Problem (evidence from live walk)

Home is one page with **three columns** that reprint other apps. On laptop width the headers overlap, so it looks like more columns than it is.

Verified on 10 Sep 2026 (James / CEO):

1. **Needs you now** and **Needs your reply** show the **same tasks** (Rural Infrastructure briefing, Friday recurring migrate, NDA). Changing the sort/filter on one affects both.
2. **Task titles are not clickable.** Draft / Ask work and dump into Ask. Manage → full Accountability Mine, not the item.
3. Header pill **4 overdue** opens Accountability **Everything**, not the 4 overdue tasks.
4. **39 on your plate** cannot be told apart from overdue (same dump).
5. **8 closed this week** opens a list titled like “everything,” not this week’s closed work.
6. **65 meetings** and **1,510 documents** both open Records **Find documents**.
7. **Signals** → Executive Signals (purpose unclear). **Brokerage** and **New Mexico** → “coming soon.”
8. **You asked for · 265** — card body is a dead click; 3 months late; user cannot tell what the zone is for.
9. **You might be missing** — Next line truncated; cards not a door; no sources.
10. **85 docs need a project** is the only widget that felt right.
11. Sidebar cannot collapse. Unusable on phone. User would not use Home in the morning.

**Do not “polish” the three-column layout.** The layout is the bug.

---

## 2. Target product (must)

Home is an **exception board**, not a dashboard of everything.

See the wireframe in this file below. One exception list. Honest pills. Unfiled keep. Pulse/insights optional only if they open the right room.

**Must not on Home**

- Two lists of the same Mine tasks.
- “Everything else” stat tiles (Documents / Projects / People / Opportunities).
- A 265-item “You asked for” feed.
- Coming-soon Brokerage / New Mexico chips in the primary header.
- Header overlap / truncated zone titles.

---

## 3. Information architecture

### 3.1 One plate, one list

Merge **Needs you now / Your action items** and **Waiting on you / Needs your reply** into a single list:

**Needs you** = items assigned to the current user that are open, sorted **overdue first**, then due date, then priority.

Show at most **5** rows on Home.

| Kind chip | Source system | When to use |
|-----------|---------------|-------------|
| Task | Accountability Mine | Default action item |
| Reply | Accountability / mail-originated Mine item | If source is email and the job is “answer this” |
| File | Records Review | Unfiled-docs row only |

**Must not** render the same `taskId` twice on Home.

### 3.2 Waiting on others leaves Home

**You asked for · 265** is not a Home job. Remove the feed from Home.

- Optional footer link: **Waiting on others →** `/accountability`

### 3.3 Rulings are a number, not a second task list

On Home: one snapshot pill **Rulings · {open To decide count}** → `/needs-you`

### 3.4 Insights and pulse are secondary

Keep at most 3 insights and 3 project pulse cards below the exception list. They must be real doors. If click cannot open sources or the project, omit the card.

---

## 4. Routing table (must)

| Control on Home | Today (broken) | Required destination |
|-----------------|----------------|----------------------|
| Task **title** | Not clickable | `/accountability?tab=mine&item={id}` |
| Row **Open** | n/a | Same as title |
| **Nudge** (was Draft) | `/ask?...` prefilled | Keep Ask prefill, label **Nudge** |
| **Brief me** (was Ask) | `/ask?...` | Prefill: Brief me on {title} |
| **All my work →** | Unfiltered Mine | `/accountability?tab=mine` |
| Header **Overdue · 4** | Unfiltered Everything | `/accountability?tab=mine&due=overdue` |
| Header **On your plate · 39** | Same dump as overdue | `/accountability?tab=mine` To do |
| **Closed this week · 8** | Everything | `/accountability?tab=mine&view=done&range=this-week` |
| **Meetings · N** | Records Find documents | `/workspace?tab=timeline` |
| **Documents · N** | Records Find documents | `/workspace?tab=search` |
| **Unfiled docs need a project** | Review (good) | `/workspace?tab=review` |
| **Rulings** pill | mixed | `/needs-you` To decide |
| Insight card | Needs you or dead | Sources / `/goals?project=` — never `/needs-you` |
| Project pulse card | `/needs-you` | `/goals?project={id}` |
| **Brokerage** / **New Mexico** | Coming soon | **Remove from Home header** |

If query params do not exist yet, **add them**. Accountability must honor `item` and `due` on load.

---

## 5. Home zones — build spec

### Shell
- One primary scroll. Collapsible sidebar, persist `localStorage` key `prereal.rail.collapsed`.
- Zone headers: flex, no overlapping titles. Required at 1280 and 1024.

### Header
```
Good {morning|afternoon}, {firstName}.
{Weekday} · Data as of {relative freshness}
```
Remove Signals / Brokerage / New Mexico as primary chips.

### Snapshot pills (max 5)
1. Overdue → Mine overdue
2. On your plate → Mine To do
3. Unfiled → Review
4. Rulings → `/needs-you`
5. Blocked projects → `/goals` (optional)

Never paint `0` then jump. Skeleton until resolved. Fail → — and Retry.

### Needs you list (hero)
Max 5 rows. Sort most overdue. Title is a clickable link. Actions: Open, Nudge, Brief me. No Delete.
Empty: `Nothing waiting on you.`

### Unfiled (keep)
`{n} documents need a project →` Records Review.

### Remove
- Waiting on you · 290
- Needs your reply as a second Mine list
- You asked for · 265 feed
- Everything else tiles
- Coming soon chips
- Overlapping sort controls

---

## 6. Copy deck

| Current | Replace with |
|---------|----------------|
| Needs you now | **Needs you** |
| Your action items | Remove (it is the Needs you list) |
| Waiting on you | Remove |
| Needs your reply | Remove as a list |
| You asked for | Remove from Home |
| Manage → / All mine → | **All my work →** |
| Draft | **Nudge** |
| Ask | **Brief me** |
| You might be missing | **At risk** (optional) |
| Everything else | Remove |
| Newest first (on Home) | **Most overdue** |

---

## 7. Visual constraints

- Gold once: 2px left rule on the first (most overdue) row only.
- Overdue text: `#b91c1c` on white.
- Hit target on Open / title ≥ 32px.
- No Delete on Home rows.
- 1280×800: no “Your ac…” clip; no overlapping headers.

---

## 8. Deep link contract (add if missing)

```
/accountability?tab=mine
/accountability?tab=mine&item={taskId}
/accountability?tab=mine&due=overdue
/accountability?tab=mine&view=done&range=this-week
/goals?project={idOrSlug}
/workspace?tab=timeline
/workspace?tab=search
/workspace?tab=review
/ask?q={prefill}&taskId={id}
```

---

## 9. Tickets (this sprint — max 7)

**T1 Merge the two Mine lists** — AT: no task title twice on `/ceo`.

**T2 Clickable item + deep link** — AT: NDA title lands on that task, not the full list.

**T3 Honest pills** — AT: overdue count = list; meetings URL ≠ documents URL; coming-soon chips gone.

**T4 Kill header overlap + collapse rail** — AT: 1280 and 1024, no text-on-text; rail toggle persists.

**T5 Honest loading** — AT: never show `0 overdue` if 4 will appear.

**T6 Unfiled keep; You asked for / Everything else leave** — AT: those feeds gone from `/ceo`.

**T7 Pulse + insights doors or hide** — AT: Spaceport pulse does not open `/needs-you`.

---

## 10. Out of scope

Do not redesign Ask, Needs you, Accountability, Records, Research, Add Data. No full navy/gold restyle. No Brokerage/NM. No completing/deleting tasks from Home.

---

## 11. QA script (PM, 8 minutes)

1. Reload `/ceo`. No `0` flash.
2. One task list, ≤5 rows, overdue near the top.
3. NDA (or most-late item) title readable and clicks through to that item.
4. Overdue pill → only overdue Mine; count matches.
5. On your plate → Mine To do (39 vs 4).
6. Closed this week → this week or empty.
7. Meetings and Documents → two different Records views.
8. N docs need a project → Review.
9. You asked for and Everything else gone.
10. Project pulse name → `/goals`, not Needs you.
11. Toggle rail; refresh; still collapsed.
12. At 1024, no overlapping headers.

If 3, 4, or 7 fail, do not ship.

---

## 12. Open questions (answer in the PR)

1. Does Accountability honor `?item=` / `?due=overdue`? If no, implement with T2/T3.
2. Real meetings count (Fathom events vs docs named meeting)?
3. Reply vs Task from `source=email`, or all tasks on Home?
4. Insights: hide vs project links only?

---

## 13. Suggested PR

**Title:** `fix(ceo): Home is an exception board, not a duplicate dashboard`

Home is done when the QA script passes, not when the columns look tidier.
