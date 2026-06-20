# Forester — Roles & Workforce Plan

*by Boreal Education*

A lightweight, browser-based board for mapping who owns what across a leadership
team — and for planning how those responsibilities shift as the team grows.

It works as both a **current-state** roles-and-responsibilities tool and a
**forward-looking** workforce-planning tool: model open roles you haven't hired
yet, shift responsibilities onto them, and name people as you fill the seats.
You can also **co-create** a plan with others: share a snapshot, leave comments,
and propose changes for review.

> **Prototype status:** This is a front-end prototype. Data is saved in each
> viewer's own browser, and collaboration happens by passing **snapshots**
> (links or files) back and forth — there are no accounts or live shared editing
> yet. See [Roadmap](#roadmap) for the hosted, multi-user version.

---

## What it does

- **Three time horizons as tabs** — *Today*, *In 6 months*, *In 12 months*. Each
  is its own independent plan, so you can compare scenarios without one
  affecting another.
- **People and open roles** — a column is either a real teammate (has a name) or
  an **open role** (a planned vacancy, shown dashed with an "Open role" badge).
  An open role can still own responsibilities — that's how you justify a hire.
- **Drag to reassign** — drag a responsibility card from one person to another,
  or use the move menu on each card (works on touch and keyboard too).
- **Fill a role** — edit any seat to set a *Role / title* and a *Name*. Leave the
  name blank to keep it an open role; add a name to turn it into a real teammate.
- **Copy forward** — future views start from your real team via *Copy from
  Today* (and 12-month can copy from 6-month), so you plan from reality.
- **Unassigned column** — surfaces responsibilities nobody currently owns.

### Insight layer

- **Capacity / load** — each seat shows a load bar against a *balanced load*
  target you can set, so overloaded people (and overloaded open roles) stand out.
- **Cost roll-up** — give any seat an optional target cost; each view totals
  *headcount cost* and breaks out *cost to hire* (the sum of its open roles).
- **Transition plan** — pick any two horizons and see exactly what changes
  between them: roles to add, seats to fill, responsibilities that move, and the
  headcount-cost delta. This is the path from your current team to the plan.

### Effort & risk

- **Effort weighting** — each responsibility carries an effort level (S / M / L,
  worth 1 / 2 / 3 points). Load is measured in points, so a few heavy
  responsibilities weigh more than several light ones.
- **Key-person risk** — any teammate who alone holds two or more heavy (L)
  responsibilities is flagged, surfacing single points of failure.

### Views & generators

- **By person / By function** — toggle the board between grouping by owner and
  grouping by business area. In the function view each card shows who owns it.
- **Responsibilities generator** — pick a function and a granularity (Broad →
  Granular) and generate a list of responsibilities to drag onto a person or drop
  into Unassigned. Suggestions come from a built-in library (a starting point to
  edit, not a live model — that's a backend upgrade).
- **Job-description drafter** — open roles can generate a posting drafted from the
  responsibilities they own, editable in place with a copy button.

### Collaboration (co-create)

These let more than one person shape a plan, even without a backend. Everything
here is attributed to the **"Your name"** you set once in the Share dialog, and
all of it travels inside a shared plan.

- **Shareable plans** — the **Share** button copies a **link** or downloads a
  **`.json` file** containing your entire board (all three horizons, costs,
  effort, comments, and pending suggestions). Whoever opens it loads an editable
  copy on their device. Open someone's plan by pasting their link/code or
  importing their file. This is a **snapshot**, not live sync — you draft, send,
  they tweak, send back.
- **Comments** — every person/seat and every responsibility has a comment thread.
  Comment buttons show a count (a card with discussion shows a "💬 N" pill; a seat
  with comments turns green). Threads show author and relative time; post with the
  button or **⌘/Ctrl+Enter**, and delete your own.
- **Suggestion mode** — toggle **Suggest** in the header to *propose* changes
  instead of applying them. While on, moving, editing, adding, and deleting a
  responsibility are recorded as **proposals** signed with your name, not changes
  to the board. Proposals render inline — an amber (or red, for removals) ring and
  an **Accept / Reject** banner on the affected card, and dashed **ghost cards**
  for proposed additions. A **"N proposed"** pill opens a review modal to accept
  or reject each one, or **Accept all / Reject all**. Great for a reviewer who
  wants to weigh in without overwriting the owner's work.

---

## Using it

| Action | How |
| --- | --- |
| Switch horizon | Click **Today / In 6 months / In 12 months** |
| Add a person or role | **Add teammate** (Today) or **Add role** (future views) |
| Edit a seat | Click the seat name, or its pencil icon |
| Make an open role a teammate | Edit the seat and add a **Name** |
| Add a responsibility | **Add responsibility** at the bottom of a column |
| Reassign a responsibility | Drag the card, or use its move (↳) icon |
| Set effort | Edit a responsibility and pick S / M / L |
| Generate responsibilities | **Generate** → choose function + granularity |
| Group by business area | **By function** toggle (top right) |
| Draft a job description | Open role → document icon in its header |
| Start a future plan from your team | **Copy from Today / 6 months** |
| Set your name (for sharing/comments) | **Share** → *Your name* |
| Share a plan | **Share** → *Copy share link* or *Download file* |
| Open someone's shared plan | **Share** → paste a link/code, or *Import file* |
| Comment on a person or responsibility | The 💬 comment icon on a seat header or card |
| Propose changes for review | Turn on **Suggest**, then edit as normal |
| Review proposals | **N proposed** pill → Accept / Reject (or per-card banners) |
| Reset everything | **Reset** (clears all changes on this device) |

---

## Running it locally

It's a single static file. The reliable way to preview is over http (opening the
file directly as `file://` can cause the browser to block the CDN scripts):

```bash
# from the folder containing index.html
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## Deploying to GitHub Pages

1. Commit `index.html` to the repository root (see commands below).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose branch **main** and folder **/ (root)**, then **Save**.
5. Wait ~1 minute. Your live URL appears at the top of the Pages screen:
   `https://<your-username>.github.io/<repo-name>/`

To publish an update later, commit a new `index.html` and push — Pages rebuilds
automatically.

---

## Data & privacy

- Edits are stored with the browser's `localStorage`, **per browser and per
  device**. Two people opening the same site will each keep their own copy.
- **Sharing** is explicit and snapshot-based: a link or file you generate
  contains the plan at that moment. Anyone with the link/file can open it, so
  treat them like any document you'd email. A downloaded file works for anyone;
  opening a share **link** on this Pages site requires access to the (private)
  repo, so the file is the most portable option until the hosted version exists.
- Nothing is sent to a server automatically. There is no account system and no
  live shared source of truth yet — that is intentional for a prototype.

---

## Roadmap

The natural next phase is a hosted version with a real backend, which upgrades
today's snapshot-based collaboration into live, multi-user editing:

- A shared, single source of truth (one plan the whole team sees in real time),
  replacing snapshot links/files.
- Accounts / sign-in, so comments and suggestions attribute automatically.
- View-only vs. edit **permissions** by user.
- An audit trail of changes over time (suggestion history, who accepted what).
- **AI-written** responsibility generation and job descriptions, tailored to your
  context (the current versions are library- and template-based).

That requires a backend (e.g. Supabase or Firebase) and is a separate build from
this prototype.

---

## Tech notes

- Single `index.html`, no build step and no install required.
- React 18 (loaded from a pinned CDN) with the component code **precompiled to
  plain JavaScript** — there is no in-browser JSX transpiler, which keeps it fast
  and compatible across browsers (including Safari).
- Styling via the Tailwind CDN.
- State (including comments and pending suggestions) is serialized to
  `localStorage`; the same serialized form is what powers Share links and files.
- If the page can't load its scripts (blocked CDN, offline, etc.) it shows a
  readable error message rather than a blank screen.
