# ABC Retail Project Closure & Sales Handoff — A Walkthrough Story

A narrative walkthrough of `finalPrompt.txt`: one complete run over the workspace `dummy_setup.txt` builds, with every file, app, tab, tag and field named the way the brief demands.

> **Everything below is fictional.** ABC Retail is an invented company. The scope items, hours, Jira keys, pull requests, Slack messages and emails are the seeded test data from `dummy_setup.txt`, and every email address in that workspace is the signed-in Gmail account's own, so nothing a run drafts can reach a real person.

**Run date for this story: Wednesday 2026-09-02, Asia/Kolkata. Evidence window: 2026-01-05 through 2026-09-01 inclusive.** Every window, cutoff and calculation below is measured off those.

---

## The cast

| App | What it holds |
|---|---|
| **Google Drive** — folder *ABC Retail Ecommerce Platform* (My Drive) | ABC Retail Final SOW.pdf, ABC Retail Project Estimate.xlsx, ABC Retail Approved Change Requests.docx, ABC Retail Project Plan.docx, and the Sheet *ABC Retail Development Effort Tracker* |
| **Jira Cloud** — project *ABC Retail Ecommerce*, key **ABCR** | 15 issues, closure issue **ABCR-150** |
| **GitHub** — *abc-retail-web*, *abc-retail-api* | 8 pull requests, 2 releases tagged v1.0.0 |
| **Slack** — channel *abc-retail-project* | 12 channel messages + 3 thread replies |
| **Gmail** | Thread *ABC Retail Project Closure* (3 messages) + decoy thread *ABC Retail Invoice Query* |
| **Google Calendar** | Event *ABC Retail Project Closure Meeting*, 2026-08-28 |
| **Notion** — database *Client Projects* | Page *ABC Retail Ecommerce Platform* |
| **HubSpot** | Company *ABC Retail*, decoy deal *ABC Retail Ecommerce Platform Build* (Closed Won) |

**The date rule that runs everything.** Real timestamps are useless here, because the whole workspace was seeded today. So every Slack message, every pull request title and every email body opens with its scenario date in square brackets like `[2026-07-24]`, and every Jira description carries a line reading `Scenario date: YYYY-MM-DD`. **Those bracketed dates are the truth.** The created, updated and merged timestamps the apps print on screen are ignored.

---

## Act 1 — Reading the paperwork

You open the Drive folder **ABC Retail Ecommerce Platform** and read exactly 4 documents, nothing outside them.

**ABC Retail Final SOW.pdf**, signed 2026-01-05, gives 7 numbered scope items, each with acceptance wording hanging off it:

1. Product Catalog and Search
2. Shopping Cart and Checkout
3. Payment Gateway Integration — *accepted when card, netbanking and UPI all complete a live transaction*
4. Admin Dashboard with Sales Reports — *accepted when sales reports export to both CSV and PDF*
5. Content Pages and Blog
6. Data Migration from the old store
7. Training and Handover Documentation

Then the first trap: an **8th section carrying no number**, headed **Accessibility Baseline**. The rule says build an identifier out of the section heading, so from here on it is called `Accessibility Baseline` — and that same string comes back in the Project Closure doc, the carryover Jira issue, Notion and the closing message. One identifier, used everywhere.

**ABC Retail Approved Change Requests.docx** adds two more things that are formally in scope:

- **CR-01 Multi Currency Display**, approved 2026-05-04 by the Head of Retail Operations, extends scope item 1
- **CR-02 Abandoned Cart Email**, approved 2026-07-21 by the Head of Retail Operations, extends scope item 2

So the real scope list is **10 items, not 7**. An agent that classifies only the 7 numbered items has already lost 3 of them.

**ABC Retail Project Estimate.xlsx** gives estimated hours per module and — crucially — the *Notes* column against each one. Admin Dashboard shows **0** hours with the note *"added mid project, never estimated"*. That note is not decoration; it becomes the reason line printed beside Admin Dashboard in the variance document.

**ABC Retail Project Plan.docx** gives the milestone dates that later get set against the dates work actually merged: Discovery 2026-01-30, Catalog and search on staging 2026-03-20, Checkout and payments 2026-05-15, Admin and reporting 2026-06-30, Content and blog 2026-07-25, **Production launch 2026-08-14**, Handover and closure 2026-08-29.

---

## Act 2 — The hours, and the trap everyone falls into

You open the **Effort Log** tab of **ABC Retail Development Effort Tracker**. Row 1 is headers, data starts at row 2:

| Module | Estimated | Actual | Rework | Defect Reference | Developer |
|---|---|---|---|---|---|
| Catalog | 160 | 172 | 8 | ABCR-40 | Dev A |
| Checkout | 120 | 168 | 22 | ABCR-38 | Dev B |
| Payments | 90 | 126 | 18 | **ABCR-40** | Dev B |
| Search | 80 | 88 | 4 | **ABCR-40** | Dev C |
| Admin Dashboard | 0 | 46 | 0 | *(blank)* | Dev C |
| Reporting | 70 | 70 | 0 | *(blank)* | Dev D |

**Actual Hours is the number that matters.** Non Billable and Overtime are already baked into it, so adding them on top inflates the total. Nobody touches those columns.

Reading straight across the row is the mistake the brief is hunting for. **Rework hours belong to the module that caused the defect, which is the module named on the Jira bug behind the reference** — so you have to go and open the bugs:

- **ABCR-38** carries `Module: Checkout` → Checkout's 22 rework hours stay where they are.
- **ABCR-40** carries `Module: Catalog` → so **Payments' 18 hours and Search's 4 hours both get pushed onto Catalog**, even though Payments and Search are the rows that logged them.

Catalog therefore absorbs 8 + 18 + 4 = **30 attributed rework hours**. Payments and Search end on **0**.

Variance is actual minus estimated, over estimated, times 100, to 1 decimal. The worked example row in the brief (`Onboarding, 40, 44, 6, 10.0, Watch`) settles the ambiguity: 44 against 40 is 10.0%, so **variance runs off raw Actual Hours, and attributed rework is a separate reporting column**.

| Module | Variance | Band |
|---|---|---|
| Catalog | 7.5% | On Track |
| **Checkout** | **40.0%** | **Overrun** |
| **Payments** | **40.0%** | **Overrun** |
| Search | 10.0% | Watch |
| Admin Dashboard | — | **Not Verified** |
| Reporting | 0.0% | On Track |

Admin Dashboard carries 0 in Estimated Hours, so it reads **Not Verified**, stays out of the project figure entirely, and gets flagged in Delivery Variance and Lessons Learned with the estimate's own reason: *added mid project, never estimated*.

**Project figure:** summed actuals 624 over summed estimates 520, counting only the 5 modules carrying both = **20.0%, Watch**.

Checkout and Payments tie at 40.0%. The tiebreak is the bigger gap in raw hours: Checkout is 48 hours over, Payments 36 — so **Checkout is the worst overrun**, and module name A-to-Z never gets used.

And here is why the rework attribution changes the story rather than just the arithmetic: Payments' overrun is **not** defect rework, because its rework moved to Catalog. Slack on `[2026-05-14]` says so outright — the gateway sandbox was down for most of a week and the UPI callback handling was built twice after the bank changed the spec, roughly 18 hours, none of it against a bug. That Slack message becomes the Evidence Reference on the Payments row.

---

## Act 3 — What Jira claims

You read the Epic, Story, Task and Bug issues in **ABCR** created or updated 2026-01-05 through 2026-09-01, capped at 200.

The board looks healthy. ABCR-10, 12, 14, 16, 20, 28 and 30 all read **Done with a resolution**. ABCR-22 (data migration) and ABCR-24 (accessibility) sit at To Do. ABCR-26 (multi currency) is In Progress.

**ABCR-150** is the closure issue, In Progress, no comments. Its description quietly holds two things the Technical Closure document needs and nowhere else records: **production runs on AWS Mumbai, staging runs on AWS Singapore**, and the known debt at closure — *search relevance tuning is half done, the notification retry logic has no backoff*.

The brief's warning applies from here on: **a green board settles nothing.**

---

## Act 4 — What actually shipped

Only merges into **main** count, and only inside the window. Five pull requests qualify:

- **abc-retail-web** — `[2026-03-18] ABCR-10 product catalog and search`, `[2026-06-30] ABCR-16 admin dashboard sales reports, CSV export`, `[2026-07-24] ABCR-20 content pages and blog`
- **abc-retail-api** — `[2026-05-10] ABCR-12 cart and checkout service`, `[2026-05-14] ABCR-14 payment gateway, card and UPI`

Three more pull requests exist purely to be rejected, and each rejection carries a different lesson:

1. `[2026-08-12] ABCR-24 accessibility baseline pass` in abc-retail-web — **closed without ever merging**. Proves nothing.
2. `[2026-09-02] ABCR-26 multi currency display` in abc-retail-api — **still open**. Proves nothing.
3. `[2026-08-30] ABCR-28 abandoned cart email job` in abc-retail-api — **merged into `release-candidate`, never into main**. This one reads as merged at a glance and is the easiest to get wrong. Proves nothing.

And **ABCR-30, training and handover documentation, has no pull request anywhere**. That is correct rather than missing: it is a documentation and training item, and the rule skips the pull request test for items with no code in them.

Both repositories carry a release **v1.0.0** — *Storefront and content* on abc-retail-web, *Core services* on abc-retail-api — with the tag name written into the release notes, so it reads straight off the release page rather than a bare tag listing.

---

## Act 5 — The conversation trail

Three more places carry what was agreed, argued about and hinted at.

**Slack**, channel *abc-retail-project*, read oldest to newest, messages and thread replies both:

| Date | What it establishes |
|---|---|
| `[2026-03-02]` | Client on the call about mobile checkout feeling slow — **third time raised** |
| `[2026-04-09]` | *Our* idea for a performance tuning retainer, "nobody on their side has asked for this" |
| `[2026-04-15]` | Netbanking parked for a later phase, agreed with the sponsor |
| `[2026-05-08]` | Accessibility baseline parked, **finishing at no charge** |
| `[2026-05-14]` | The real Payments cause: sandbox outage plus UPI rebuilt after a bank spec change |
| `[2026-05-20]` | Ops lead asks about ERP stock sync — **plus 3 replies inside that one thread** |
| `[2026-06-11]` | Sponsor asks whether we build loyalty and rewards |
| `[2026-06-30]` | Sales reports export CSV only, **PDF did not make the cut** |
| `[2026-07-02]` | Marketing head asks about a mobile app, iOS and Android |
| `[2026-08-05]` | Marketing head asks about Amazon and Flipkart listings |
| `[2026-08-10]` | Multi currency slipping, **on us, at no charge after closure** |
| `[2026-08-20]` | *"Client says the blog section is still not live. Our board says that story is done."* |

**Gmail**, the closure thread *ABC Retail Project Closure*, 3 messages:

- `[2026-06-18]` — the sponsor drops data migration: *"our own team will run it, please drop it from your scope"*
- `[2026-08-24]` — the blog still is not live for marketing; and for next year, a **mobile app on iOS and Android, live before next Diwali**, plus **loyalty and rewards**, plus **Amazon and Flipkart listings**
- `[2026-08-31]` — good meeting on the 28th, send the closure pack

The separate thread *ABC Retail Invoice Query* on `[2026-07-15]` asks about a purchase order number. It is noise, it carries no scope, and it changes nothing.

**Google Calendar**, *ABC Retail Project Closure Meeting*, 2026-08-28. Nobody was invited and the guest list is empty — **that is the correct result, not a gap**. Who sat in the room, which side they were on and what each agreed is written into the description, and that description is the closure meeting record for the whole run: netbanking out of scope and accepted, PDF export not delivered and accepted for now, blog publishing raised again, data migration confirmed as handled in house, mobile app and marketplace listings raised for next year, accessibility and multi currency acknowledged as ours to finish free.

---

## Act 6 — Judgment: every item lands in exactly one of five states

Two ladders decide this, and they are not the same ladder.

- **Agreement** — SOW and change request log win, then the closure thread, then the closure meeting notes, then Slack at the bottom.
- **Delivery** — a merged pull request beats a Jira status, and a Jira status beats somebody claiming it in Slack.

**When the two ladders pull against each other, the item is Disputed. Never Delivered.**

| # | Scope item | State | Why |
|---|---|---|---|
| 1 | Product Catalog and Search | **Delivered** | ABCR-10 Done with resolution + PR merged to main `[2026-03-18]` |
| 2 | Shopping Cart and Checkout | **Delivered** | ABCR-12 Done with resolution + PR merged to main `[2026-05-10]` |
| 3 | Payment Gateway Integration | **Delivered with Deviation** | SOW demands card + netbanking + UPI; shipped card + UPI only. Gap line: netbanking dropped, Slack `[2026-04-15]`, confirmed at the closure meeting |
| 4 | Admin Dashboard with Sales Reports | **Delivered with Deviation** | SOW demands CSV **and** PDF; the PR title itself says CSV export. Gap line: PDF export not delivered, Slack `[2026-06-30]`, accepted for now at the meeting |
| 5 | Content Pages and Blog | **Disputed** | ABCR-20 Done + PR merged to main, against the client in writing on `[2026-08-24]` that marketing still cannot publish. Also Slack `[2026-08-20]` and the meeting notes |
| 6 | Data Migration from the old store | **Dropped** | Pulled by the client sponsor in the closure thread `[2026-06-18]`, reconfirmed at the closure meeting |
| 7 | Training and Handover Documentation | **Delivered** | ABCR-30 Done with resolution. No pull request needed, non-code item |
| — | **Accessibility Baseline** | **Deferred** | Agreed in writing, Slack `[2026-05-08]`, at no charge. PR closed unmerged, ABCR-24 still To Do |
| CR-01 | Multi Currency Display | **Deferred** | Agreed in writing, Slack `[2026-08-10]`, at no charge. PR still open, ABCR-26 In Progress |
| CR-02 | Abandoned Cart Email | **Disputed** | ABCR-28 Done with resolution, but nothing merged into main — only into `release-candidate` `[2026-08-30]`. Nobody agreed in writing to park it, so it cannot be Deferred |

**Counts: Delivered 3 · Delivered with Deviation 2 · Deferred 2 · Dropped 1 · Disputed 2.**

Items 5 and CR-02 are the two traps. Both look Delivered on the board, and neither is. Each gets written up with **both sides and the exact source behind each side**, so whoever picks it up later can see what you saw.

---

## Act 7 — Which opportunities are real

Three tests, and all three, not two out of three: it sits **outside the SOW and outside every approved change request**; **the client itself** raised it in **at least 2 independent places** inside the window; and **nobody already promised it away free** on the deferred list.

Independent means a different *place*, not a different message. Each of these is worth 1: the closure thread, the closure meeting, the Slack channel *abc-retail-project*, the Notion page. **Four messages inside one Slack thread is still 1.**

| Opportunity | Independent sources | Rank | Mature for Sales? |
|---|---|---|---|
| **Mobile app, iOS and Android** | Slack `[2026-07-02]`, Gmail `[2026-08-24]`, closure meeting 2026-08-28, Notion *Client notes* = **4** | **1** | **Yes** — clears it twice over: 3+ sources, *and* a written client request in the closure thread naming both the work and a timeframe, "before next Diwali" |
| **Amazon and Flipkart listings** | Slack `[2026-08-05]`, Gmail `[2026-08-24]`, closure meeting = **3** | 2 | Yes on the 3-source rule — but no deal, because only the top-ranked opportunity can touch one |
| **Loyalty and rewards programme** | Slack `[2026-06-11]`, Gmail `[2026-08-24]` = **2** | 3 | **No** — 2 sources and no written timeframe. Stays an opportunity in the documents and in Notion, and never becomes a deal |

Ranking is by source count, ties broken on the earliest date the client raised it, then name A-to-Z. Three qualify, well under the ceiling of 5.

**Rejected, each named in the Sales Expansion Opportunity Brief with its reason:**

- **ERP / SAP stock sync** — raised on `[2026-05-20]` and chased twice more, but every one of those sits inside the same Slack thread. **1 source.** Fails the independence test.
- **Performance tuning retainer** — our idea, not theirs. Slack `[2026-04-09]` says outright that nobody on their side asked. Fails the client-raised test, however good it looks.
- **Netbanking** — inside SOW scope item 3. Fails the first test; it is unfinished scope, not new business.
- **Accessibility Baseline and Multi Currency Display** — already promised as free work on the deferred list. Fails the third test.

---

## Act 8 — The one estimate

Only the top-ranked qualifying opportunity gets a technical estimate, so only the **mobile app**. It gets broken into features with hours on each, and those hours are calibrated against the **actual** hours of the closest comparable module on the Effort Log — never the original estimate, since the original estimate is exactly what got missed. The comparables are Catalog at 172 actual, Checkout at 168, Payments at 126.

| Feature | Hours | Calibrated on |
|---|---|---|
| App shell and navigation, iOS and Android | 90 | no comparable |
| Product catalog and search screens | 120 | Catalog, 172 actual |
| Cart and checkout flow | 130 | Checkout, 168 actual |
| In-app payments, card and UPI | 90 | Payments, 126 actual |
| Account, orders and order history | 60 | partial |
| Push notifications | 40 | no comparable |
| App store release and hardening | 50 | no comparable |
| **Total** | **580** | |

**Confidence: Medium** — catalog, checkout and payments have comparable modules in the tracker, but the native shell, push notifications and store submission have none, so only part of it is calibrated.

**No price. No rate. No total cost. No delivery date. Nothing anywhere in it that reads as an offer.** Had nothing qualified, no estimate would be written and the Technical Estimation Plan would say so in one line.

---

## Act 9 — Writing it all down

### The 5 Google Docs

Same name shape on all of them, into the same Drive folder, sharing left exactly as the folder already has it:

- ABC Retail Ecommerce Platform **Technical Closure** 2026-09-02
- ABC Retail Ecommerce Platform **Project Closure** 2026-09-02
- ABC Retail Ecommerce Platform **Delivery Variance and Lessons Learned** 2026-09-02
- ABC Retail Ecommerce Platform **Sales Expansion Opportunity Brief** 2026-09-02
- ABC Retail Ecommerce Platform **Technical Estimation Plan** 2026-09-02

**Technical Closure** carries what shipped in each repository with its release and the ABCR keys behind it, the environments off ABCR-150 (**AWS Mumbai production, AWS Singapore staging**), the known debt with the ticket behind each item, and anything Not Verified with its reason.

**Project Closure** is the scope story: all 10 items with identifier, single state and the source that put it there, both change requests with their approval dates, planned milestone dates set against the dates work actually merged, and the Disputed list with both sides.

**Delivery Variance and Lessons Learned** holds every number: the per-module table, the **20.0% Watch** project figure, the three worst overruns with what the evidence says caused each, the **30 rework hours pushed back onto Catalog**, the recurring client pain points with their dates (mobile checkout speed raised three times by `[2026-03-02]`; blog publishing raised on `[2026-08-20]`, `[2026-08-24]` and at the meeting), and the lessons in a form the next project can use.

**Sales Expansion Opportunity Brief** lists the 3 qualifying opportunities with their sources and dates, their ranks, their maturity result, and everything rejected with why.

**Technical Estimation Plan** holds the feature table, the 580 total, Medium confidence with the comparable modules it was calibrated on, plus assumptions and dependencies.

Evidence is named as **plain text or a plain pasted link** — an ABCR key, a pull request number with its repository, a message date, a document name. **No smart chips, no embeds that have to call another app to draw themselves.**

### The Variance Summary tab

A new tab on **ABC Retail Development Effort Tracker**, headers on row 1, one row per module from row 2 down, matched on column A and updated in place. Columns A to J: Module, Estimated Hours, Actual Hours, Rework Hours Attributed, Variance Percent, Band, Worst Contributing Cause, Evidence Reference, Closure Document Link, Last Updated.

| Module | Est | Act | Rework Attr | Var % | Band | Worst Contributing Cause | Evidence |
|---|---|---|---|---|---|---|---|
| Catalog | 160 | 172 | **30** | 7.5 | On Track | facet staleness defect, plus rework absorbed from Payments and Search | ABCR-40 |
| Checkout | 120 | 168 | 22 | 40.0 | Overrun | coupon-removal totals defect and repeated mobile checkout complaints | ABCR-38 |
| Payments | 90 | 126 | 0 | 40.0 | Overrun | gateway sandbox outage and UPI callback rebuilt after a bank spec change | Slack abc-retail-project `[2026-05-14]` |
| Search | 80 | 88 | 0 | 10.0 | Watch | relevance tuning left half done at closure | ABCR-150 |
| Admin Dashboard | 0 | 46 | 0 | Not Verified | Not Verified | no estimate recorded, added mid project | ABC Retail Project Estimate.xlsx |
| Reporting | 70 | 70 | 0 | 0.0 | On Track | none | ABCR-16 |

Column J reads **2026-09-02 on every row without exception**. Dates in YYYY-MM-DD. **The Effort Log tab is not touched, and no row anywhere is deleted.**

> *One genuine ambiguity worth pinning down in the brief: the worked example row names "the Project Closure document link" for column I, but the numbers themselves live in Delivery Variance and Lessons Learned.*

### Jira

**ABCR-150** gets one comment carrying the 20.0% Watch project figure, the count in each of the 5 states, the Disputed list, the 3 worst overruns with causes, the qualifying opportunities with ranks and maturity results, links to all 5 documents, and the next action with a date. Then its status moves to **Closed**.

Every Deferred and every Disputed item also gets its own Task in ABCR, at To Do, linked to ABCR-150 with a **Relates To** link, labelled **carryover-2026-09-02**, holding at minimum the scope item identifier, its state, the evidence behind that state, and what somebody has to do about it. Order is Disputed ahead of Deferred, older agreement dates ahead of newer:

1. Content Pages and Blog — Disputed
2. Abandoned Cart Email (CR-02) — Disputed
3. Accessibility Baseline — Deferred, agreed `[2026-05-08]`
4. Multi Currency Display (CR-01) — Deferred, agreed `[2026-08-10]`

Four issues, comfortably under the ceiling of 8, so nothing spills into the closure comment instead. **No new project, no new board, no new status, no new issue type.**

### Notion

The page **ABC Retail Ecommerce Platform** inside the database **Client Projects** is **updated in place, never replaced and never duplicated**. The page name is what finds it, so if the database reads something else on screen you carry on into the page anyway and report the title it actually reads.

It ends the run carrying the final delivery status, the deferred and disputed work, the lessons learned, the recurring client pain points with dates, the technical decisions worth keeping, and the qualifying opportunities with their sources. The existing *Technical decisions* and *Client notes* entries get **updated**, not appended beside duplicates — and **Team roster is left completely alone**. That section exists specifically to catch a run that rewrites the page instead of editing it.

### HubSpot

A **Note dated 2026-09-02** on the company **ABC Retail**, naming the project as closed, the **Watch** variance band, and all 3 qualifying opportunities with rank and maturity result.

Because rank 1 clears the maturity rule, a deal is created: **ABC Retail Mobile Application Expansion**, associated to ABC Retail, pipeline **Sales Pipeline**, stage **Appointment Scheduled**, description holding the 4 independent sources and 580 hours at Medium confidence. **Amount left empty. No price, no rate, nothing that reads as an offer or a commitment.**

The decoy deal *ABC Retail Ecommerce Platform Build* at Closed Won is not touched. Had rank 1 fallen short of maturity, **no deal would be created or edited at all** and the note would say why.

### The Gmail draft

One draft in **Gmail Drafts**, subject exactly **ABC Retail Ecommerce Platform Sales Handoff**, addressed to the email in the **Company owner** property on the ABC Retail record. 200 to 300 words, plain sentences, carrying what was delivered, the variance figure with its band in one line, the deferred and disputed items in short, each qualifying opportunity with its source count, whether a deal was opened and on what grounds, 580 hours at Medium confidence, and links to all 5 documents.

**No attachments. No pricing, no rates, no delivery promises. Nothing sent, scheduled or queued — not through a connector and not through a browser.** The draft sits in Drafts for a person to send by hand.

If Gmail refuses to save it, the full text goes into the Sales Expansion Opportunity Brief under the label **Draft Email Not Saved** with the exact error text beside it, and **no other route is used to send that mail**.

---

## Act 10 — Run it twice, change nothing twice

The whole run happens again on 2026-09-02, and nothing ends up written twice. Before anything is created, it searches:

- the Drive folder for each of the 5 filenames
- the Variance Summary tab for each module name in column A
- Gmail Drafts for that exact subject
- ABCR for an issue already labelled `carryover-2026-09-02` carrying the same scope item identifier
- the ABC Retail company for a note dated 2026-09-02 and for a deal named ABC Retail Mobile Application Expansion
- ABCR-150 for a comment already carrying 2026-09-02

Everything found is **updated in place** instead of copied. End state after two runs is identical to end state after one: **1 document per name, 1 row per module, 1 carryover issue per scope item, 1 draft, 1 note, 1 deal, 1 closure comment.**

---

## Act 11 — The rule underneath everything: Chrome is not optional

Every app is reached through its connected integration where that works. Where the integration is missing, errors, times out, refuses the call, reports no tool for the job, or hands back nothing while the screen is plainly showing something, **you go in through the Chrome browser plugin instead** — the accounts are already signed in there.

This covers **writing** every bit as much as reading. If the Jira connector will not create an issue, create it in Chrome. If the Notion connector will not save a block, save it in Chrome. If the HubSpot connector will not write a property, write it in Chrome. If Sheets will not add a tab, add it in Chrome.

**Nothing counts as missing, unavailable, unauthorised or blocked until Chrome has been pointed at it and failed as well.** A step reported as blocked without that having been tried is a failed run, whatever else got finished. And a run never pauses to ask for an integration to be connected.

Only **two** failures stop anything:

1. **ABC Retail Final SOW.pdf failing on both routes** stops the whole run — there is no scope baseline without it.
2. **The Effort Log tab failing on both routes** stops the variance work and the Technical Estimation Plan, **and nothing else.**

Everything else gets recorded and worked around: a repository that will not open, a Slack history that will not load past a point, a Notion page that will not save, a HubSpot property that will not take a value. Name it, say what it cost the closure, mark whatever it left unproven as **Not Verified** with a line on what would settle it, and finish every part of the run that does not depend on it.

**Never invent** a scope item, an hour figure, a commit, a release, a message, a meeting note, a person, a source, a document link or an error message. Never report something as read, created, updated or saved where it was not.

---

## The finish line

The run is done when ABCR-150 reads Closed with its closure comment, the 4 carryover issues sit under it, all 5 Google Docs are in the folder under their exact names, Variance Summary holds 6 rows with every column filled, the Notion page carries its 6 items, the HubSpot company carries the dated note with the one deal, and the unsent draft sits in Gmail Drafts.

And the closing message says, in plain terms:

> Project variance **20.0%, Watch**. Scope: **3 Delivered, 2 Delivered with Deviation, 2 Deferred, 1 Dropped, 2 Disputed**.
>
> Disputed — *Content Pages and Blog*: ABCR-20 Done with a pull request merged to main on `[2026-07-24]`, against the client's written statement on `[2026-08-24]` that marketing still cannot publish. *Abandoned Cart Email*: ABCR-28 Done with resolution, against no pull request merged into main — only into release-candidate on `[2026-08-30]`.
>
> Opportunities — Mobile app, 4 sources, mature. Marketplace listings, 3 sources, mature. Loyalty and rewards, 2 sources, not mature.
>
> Deal **ABC Retail Mobile Application Expansion** created, because rank 1 cleared maturity on both grounds.
>
> Not Verified — **Admin Dashboard**, 0 estimated hours recorded, note reads "added mid project, never estimated". Evidence is missing, not withheld by a tool.
>
> Chrome fallbacks: *(each step, with the error that sent it there)*. Still blocked: *(each step, with the error from both routes)*.

---

## What this workflow is actually testing

Can an agent refuse to trust a green Jira board, follow a defect reference to a different module than the one that logged the hours, notice a merge that went to the wrong branch, count four messages in one Slack thread as one source, keep an unnumbered SOW section as a first-class scope item, leave a decoy deal and a Team roster section alone — and still write a handoff that says **40% overrun** out loud instead of rounding it into something nicer.
