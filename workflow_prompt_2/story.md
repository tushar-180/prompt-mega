# Tender Qualification Workflow — A Walkthrough Story

A narrative walkthrough of `finalPrompt.txt`: one invented but fully consistent run, with every file, app, tab and field named the way the brief demands.

> **Everything below is fictional.** The buyer, the tender, the reference, the filenames, the people and the Notion/Jira records are invented to illustrate the rules. A real run takes its reference character-for-character off the sheet.

**Run date for this story: Wednesday 2026-09-02, Asia/Kolkata.** Every date below is measured off it.

---

## Act 1 — Opening the tracker and picking exactly one row

You open **Google Sheets → Tender Tracker 2026**, which lives in **My Drive / Tender Management / 2026**, and go to the tab **Pending Tenders**. Row 1 is headers, so reading starts at row 2. Seven rows are sitting there:

| Row | Tender Name | Ref | Status | Deadline | Priority | Decision |
|---|---|---|---|---|---|---|
| 2 | City Bus Fleet Telematics | KMTC-TEL-2027-008 | Submitted | 2026-09-30 | High | Bid |
| 3 | Municipal Water SCADA Upgrade | NMWB-SCD-2027-014 | Pending Review | 2026-11-20 | Medium | *(empty)* |
| 4 | Statewide Health Records Portal | SHD-HRP-2027-003 | Pending Review | 2027-02-10 | High | *(empty)* |
| 5 | **Airport Baggage Handling Analytics** | **DAA-BHA-2027-052** | **Pending Review** | **2026-10-09** | **High** | *(empty)* |
| 6 | Highway Toll Audit Services | NHT-AUD-2027-019 | Pending Review | 2026-10-09 | High | No Bid |
| 7 | Port Cargo Weighbridge Integration | PCW-WBI-2026-044 | Pending Review | 2026-08-25 | Low | *(empty)* |
| 8 | Rail Yard Asset Tracking | IRY-AST-2027-027 | Pending Review | 2026-10-09 | Medium | *(empty)* |

The three filters knock rows out one at a time:

- **Row 2** — Status is `Submitted`, not `Pending Review`. Out.
- **Row 4** — deadline 2027-02-10 falls past 2026-12-31, outside the current calendar year. Out.
- **Row 6** — Decision cell already says `No Bid`, so it's already been worked. Out.
- **Row 7** — deadline 2026-08-25 is behind today. Out.

Three survive: rows 3, 5 and 8. Sort by deadline, earliest first → rows 5 and 8 tie at **2026-10-09**, with row 3 behind them at 2026-11-20. The tie breaks on Priority: row 5 is **High**, row 8 is **Medium**. Row 5 wins outright, so Tender Reference A-to-Z never gets used.

**You take row 5 and only row 5.** Row 8 is a different tender no matter how similar "asset tracking" and "baggage analytics" sound, and you do not stop to ask the bid owner which one to pick — the sort already decided.

From row 5 you carry forward: Buyer **Deccan Airports Authority**, Reference **DAA-BHA-2027-052**, Contract Start **2027-01-15**, Contract Duration **24 months**, Bid Owner **Anita Deshmukh**, Bid Owner Email **anita.deshmukh@empiricinfotech.com**, Drive Folder and Portal URL.

> *If all seven rows had been knocked out, the run would write nothing anywhere — no Notion page, no Jira issue, no calendar event, no draft — and the closing message would just say "read 7 rows, here is what disqualified each."*

---

## Act 2 — Finding the tender pack and proving it's the right one

The Drive Folder cell points at **My Drive / Tenders / 2027 / Deccan Airports Authority / DAA-BHA-2027-052 Baggage Handling Analytics**.

That folder tail gives you the **short tender name: `Baggage Handling Analytics`**. That exact string comes back in every Jira summary, Notion title, calendar event and email subject later — so getting it right here matters downstream.

**Before reading a single word**, you prove you're in the right folder: at least one document inside has to print `DAA-BHA-2027-052` character for character. You open `01_RFP_Main_Document.pdf` and page 1 carries the reference in the header. Proof passed.

> *If the folder had been the Deccan Airports Authority runway-lighting pack instead — right buyer, reference `DAA-RWY-2027-061` — that's the wrong folder. You'd write the mismatch down and stop work on this tender rather than dismantling somebody else's pack.*

Then you read **all of it**, not the first two files and a skim:

- `01_RFP_Main_Document.pdf` — issue date **2026-07-28**, printed on the cover
- `02_Eligibility_Criteria.pdf`
- `03_Scope_of_Work.pdf`
- `04_Technical_Specification.pdf`
- `05_Draft_Contract_Terms.pdf`
- `06_Annexure_C_Compliance_Matrix.xlsx` — **every tab**: `Eligibility`, `Technical`, `Legal`
- `07_Annexure_D_Pricing_Schedule.xlsx` — **every tab**: `BOQ`, `Rate Card`, `Summary`
- `08_Bid_Submission_Instructions.pdf`

The numbering *suggests* reading order, and here it holds. But it's a habit somebody has, not a guarantee — in this pack `05_Draft_Contract_Terms.pdf` turns out to carry an eligibility clause you'd have missed if you'd trusted the filename. You record the filename you actually opened for each, because those filenames are what the citations have to carry.

---

## Act 3 — The portal, where the pack goes out of date

The Portal URL cell points at `https://eprocure.deccanairports.gov.in/notices`. It opens with no login — good. You look at everything published between the RFP issue date **2026-07-28** and **today, 2026-09-02**, on the public notice page only.

Three notices are on that page. One is for `DAA-RWY-2027-061` — different reference, so it's invisible to this analysis however close the subject reads. The other two carry `DAA-BHA-2027-052` exactly:

- **Corrigendum-01, dated 2026-08-11** — moves the submission deadline from **2026-10-09 17:00 IST** to **2026-10-23 15:00 IST**.
- **Addendum-02, dated 2026-08-26** — amends `02_Eligibility_Criteria.pdf` clause 4.3: ISO/IEC 27001 certification must now be **valid through the entire contract term**, and raises the minimum similar-project value band.

Latest publication wins, so the **authoritative deadline is 2026-10-23**, set by Corrigendum-01. The RFP's 2026-10-09 gets recorded as **superseded**, with both dates spelled out on the Notion page. Note that the sheet still says 2026-10-09 — the sheet is stale and the portal is right. **Every backward-dated calendar milestone below hangs off 2026-10-23, not 2026-10-09.**

Two branches you didn't hit, but which change everything when you do:

- **Portal behind a login, or Portal URL empty and no public page findable** → mark the portal check *blocked*. Everything a notice could have moved becomes **Cannot Determine**, and the decision **caps at Conditional Bid** no matter how clean the pack looks. No exceptions.
- **Portal opens fine, nothing published for the reference in that window** → that is a *completed check with a nil result*. Record "checked, no notices found," carry on. Nothing becomes Cannot Determine, no cap fires.

And if Corrigendum-01 and Addendum-02 had carried the *same date* and contradicted each other, you would not pick the convenient reading — you'd record both, mark the requirement Cannot Determine, and push it onto the clarification list.

---

## Act 4 — Building the effective requirement set

From pack + portal together you assemble **28 requirements**: all **18 the pack marks mandatory**, plus the **10 non-mandatory** carrying the most delivery risk (ties there broken on lower document number, then lower page number).

Each one carries **11 fields**. Here's one, fully populated, so the shape is concrete:

| Field | Value |
|---|---|
| 1. Quote (buyer's words) | "The Bidder shall hold a valid ISO/IEC 27001 certification covering software development and data processing services, valid for the entire contract term." |
| 2. Mandatory? | Yes |
| 3. Source | `02_Eligibility_Criteria.pdf` page 7, clause 4.3 |
| 4. Version / amendment | RFP v1.0, amended by **Addendum-02 dated 2026-08-26** |
| 5. Status | **Partially Compliant** |
| 6. Company evidence | Notion → **Company Knowledge Base → Certifications** → record "ISO/IEC 27001:2022 — Information Security" |
| 7. Risk | Certificate expires 22 months before contract end; buyer can reject at evaluation or terminate mid-term. |
| 8. Action | Complete recertification with scope extended through 2029-01-14 |
| 9. Fatal / curable / neither | **Curable** |
| 10. Owner | Vikram Shah (Jira **BID-241**) |
| 11. Due by | **2026-10-15** (before the authoritative deadline 2026-10-23) |

Sources always look like `04_Technical_Specification.pdf page 14` or `06_Annexure_C_Compliance_Matrix.xlsx tab Eligibility row 22` — never "the technical document" or "the compliance sheet." Somebody has to be able to go and check.

---

## Act 5 — Notion, where the evidence actually lives

Two teamspaces, and the brief is fussy about which holds what:

- **Company Knowledge Base** → databases `Certifications`, `Project Experience`, `Client References`, `Technical Capabilities`
- **Bid Management** → `Historical Bid Outcomes` *(not in Company Knowledge Base)*, and `Tender Decisions`

**The certification test.** The `Certifications` record for ISO/IEC 27001:2022 shows Certificate Number `IS-7741-2024`, Issue Date `2024-03-01`, Expiry Date `2027-02-28`, Scope `Software development and managed IT services`. All four fields present → the record counts. Scope covers what the tender actually asks about → it's the right certificate, not a cousin sitting next door.

Now the arithmetic. Contract Start `2027-01-15` + Contract Duration `24 months` = **contract end 2029-01-14**. Expiry `2027-02-28` against that end date leaves **22 months of contract uncovered**. That makes it **Partially Compliant, not Compliant** — and the fact that somebody has a renewal pencilled in changes nothing about the status.

Contrast: the `Certifications` record for **CMMI Level 3** has a Certificate Number, an Issue Date and a Scope, but the **Expiry Date cell is empty**. One of the four missing means it doesn't count at all → that mandatory requirement lands at **Cannot Determine**, with "Expiry Date absent on the Notion Certifications record" written as exactly what's missing.

**The project reference test.** The tender wants a comparable project. The `Project Experience` record "Chennai Metro Passenger Flow Analytics" is checked on all four axes:

- Project Type — real-time passenger analytics platform ✓
- Contract Value Band — ₹5–10 Cr against a required ₹5 Cr+ ✓
- Completion Date — 2024-11-30, inside the required five years ✓
- Customer Type — **Metro Rail Corporation**, where the amended clause wants an **airport operator** ✗

Three of four clear → **Partially Compliant, with Customer Type named as the one that failed.**

`Historical Bid Outcomes` tells you Deccan Airports Authority has rejected two of your last three bids on documentation grounds. That's colour on the buyer and **nothing more** — it never decides the bid on its own.

---

## Act 6 — Jira, and whether anyone is actually free

Two projects. **Bid Management (key `BID`)** with components `Tender Pipeline`, `Active Bids`, `Bid Compliance`, `Bid Production`; and **Delivery (key `DEL`)** on component `Active Projects`, where the live client work sits.

You search both projects twice — once on `DAA-BHA-2027-052`, once on `Baggage Handling Analytics` word for word. Not "baggage analytics," not "the baggage tender."

The tender asks for **1 Project Manager, 3 Data Engineers, 1 Security Lead** from contract start **2027-01-15**. So you pull `DEL` / `Active Projects` issues whose **Due date runs past 2027-01-15** and whose status is **anything but Done**, and read the Assignee on each:

| Issue | Due | Assignee | Role | Status |
|---|---|---|---|---|
| DEL-482 | 2027-03-31 | Priya Menon | Data Engineer | In Progress |
| DEL-495 | 2027-06-30 | Rahul Iyer | Data Engineer | In Progress |
| DEL-501 | 2027-02-28 | Anand Krishnan | Security Lead | Blocked |

Three people already committed past contract start. That leaves one free Data Engineer and no Security Lead.

**Shortfall by role, with the date each clears:**

- Data Engineer — **short 2**; earliest clear **2027-04-01** (Priya) and **2027-07-01** (Rahul)
- Security Lead — **short 1**; earliest clear **2027-03-01** (Anand)

All three land *after* 2027-01-15, so this is a genuine staffing shortfall. The key move here: you are counting **people already committed to open work**, not people idle on 2026-09-02. Free today tells you nothing about free at contract start.

---

## Act 7 — The curable bar, which is deliberately high

"Curable" needs **three things on the record**: what closes it, who closes it, and a date on or before the **authoritative deadline (2026-10-23)** for submission-side issues, or on or before **Contract Start (2027-01-15)** for delivery-side ones. Anything short of all three is **fatal**, or it's **Cannot Determine**.

- **ISO 27001 gap** → `BID-241` "ISO 27001 recertification, scope extended through 2029-01-14", assignee **Vikram Shah**, due **2026-10-15**. What, who, date before 2026-10-23 → **curable**. ✓
- **Security Lead shortfall** → `BID-233` "Recruit second Security Lead", assignee **Meera Nair**, due **2026-12-15**, before contract start 2027-01-15 → **curable**. ✓
- **Data Engineer shortfall** → nothing in Jira. No hiring ticket, no named owner, no date. However fixable two engineers *feels*, with no plan on the record it is **fatal**. ✗
- **CMMI Level 3 expiry missing** → the pack, the portal and Notion between them don't settle it → **Cannot Determine**, and you say precisely what's missing rather than reading the silence as a pass *or* a fail.

---

## Act 8 — One decision

Counting the 28 requirements: **16 Compliant, 6 Partially Compliant, 2 Not Compliant, 4 Cannot Determine.** Of the 18 mandatory ones: 12 Compliant, 4 Partially, 2 Cannot Determine, **0 Not Compliant**.

Walk the three rules in order:

- **No Bid?** Needs a mandatory requirement that is Not Compliant *with a fatal issue behind it*. Both Not Compliant requirements are non-mandatory. Doesn't fire.
- **Bid?** Needs every mandatory Compliant, no staffing shortfall at contract start, and nothing Cannot Determine touching a mandatory requirement. Fails three ways over. Doesn't fire.
- **Everything in between** → **Conditional Bid**, and every condition gets an owner and a close-by date.

**Decision: Conditional Bid.**

And note the brief's warning applies right here: the fatal Data Engineer shortfall is exactly where you'd be tempted to argue "we'll find someone." You don't. A No Bid with evidence stacked behind it is a good result; getting to a bid is not the win condition.

---

## Act 9 — Three clarification questions, and not four

Five candidates qualified. Three is the hard ceiling, so you rank: mandatory first, then whichever blocks the larger share of priced scope, then lower document number.

**Kept:**

1. **Against clause 4.3 (`02_Eligibility_Criteria.pdf` p.7, as amended by Addendum-02)** — Does "valid for the entire contract term" require the certificate to be in force at bid submission, or is a dated recertification plan acceptable? *Moves eligibility, and moves the decision itself.*
2. **Against `04_Technical_Specification.pdf` p.14** — Does the 30-second baggage event latency ceiling apply at peak or as a daily average? *Moves technical scope and the sizing behind the price.*
3. **Against `07_Annexure_D_Pricing_Schedule.xlsx` tab `BOQ` row 41** — Is the optional analytics module priced inside the evaluated total? *Moves price.*

**Dropped, with reasons:** one asked about the preferred document font (moves nothing — not worth a question even though the buyer would take ten); one duplicated a point Addendum-02 already answered.

---

## Act 10 — What gets written, app by app

### Jira → project `BID`, component `Bid Compliance`

**One `Task` per mandatory requirement that came out Not Compliant, Partially Compliant or Cannot Determine.** That's 4 + 2 = **6 issues**, comfortably inside the cap of 12 (had it overflowed: fatal ranked ahead of curable, ties on lower document number then lower page number).

Format — summary is the bracketed reference then the check; the `Labels` field takes the **bare** reference with no brackets:

> **Summary:** `[DAA-BHA-2027-052] Verify ISO 27001 certification covers the contract period`
> **Labels:** `DAA-BHA-2027-052`
> **Due date:** `2026-10-15` (Asia/Kolkata, on or before 2026-10-23)
>
> Body carries the six required things: the quote from source, `02_Eligibility_Criteria.pdf page 7`, status Partially Compliant, curable, "complete recertification with extended scope," and the due date.

Then **3 more issues on the same component**, one per kept clarification question, same prefix and label, each carrying the question text and the requirement behind it. **`Bid Compliance` ends the run holding 9 issues.**

### Jira → project `BID`, component `Bid Production`

Exactly **6 issues**, same prefix and label, each taking the Due date of the calendar milestone it matches:

| Issue summary | Due |
|---|---|
| `[DAA-BHA-2027-052] Complete Technical Proposal` | 2026-10-13 |
| `[DAA-BHA-2027-052] Complete Commercial Proposal` | 2026-10-15 |
| `[DAA-BHA-2027-052] Complete Legal Review` | 2026-10-15 |
| `[DAA-BHA-2027-052] Complete Final Compliance Review` | 2026-10-09 |
| `[DAA-BHA-2027-052] Obtain Management Approval` | 2026-10-19 |
| `[DAA-BHA-2027-052] Final Tender Submission` | 2026-10-21 |

### Notion → `Bid Management` teamspace → `Tender Decisions` database

**One page**, titled `DAA-BHA-2027-052 Baggage Handling Analytics` — reference then short tender name. It carries: tender name, buyer, reference; original deadline 2026-10-09 and authoritative deadline 2026-10-23 *with Corrigendum-01 named as what set it*; contract dates 2027-01-15 to 2029-01-14; effective RFP version plus Corrigendum-01 and Addendum-02 with the wording each superseded; all 28 requirements at 11 fields apiece; the fatal issue (Data Engineer shortfall), the curable ones with owner and close date, the 4 Cannot Determine items with what's missing on each; the 3 clarification questions; the decision with reasoning **in 200 words or fewer**; and housekeeping — the 8 filenames read, the 15 Jira keys, the 6 event names, the draft subject.

### Google Calendar → `Bid Management`

Six events, all **1 hour, all starting 10:00 Asia/Kolkata, no guests on any of them**, dated backwards from **2026-10-23** in working days:

| Event name | Working days before deadline | Date |
|---|---|---|
| `[DAA-BHA-2027-052] Proposal Preparation` | 15 | Fri **2026-10-02** |
| `[DAA-BHA-2027-052] Compliance Review` | 10 | Fri **2026-10-09** |
| `[DAA-BHA-2027-052] Technical Review` | 8 | Tue **2026-10-13** |
| `[DAA-BHA-2027-052] Commercial Review` | 6 | Thu **2026-10-15** |
| `[DAA-BHA-2027-052] Management Approval` | 4 | Mon **2026-10-19** |
| `[DAA-BHA-2027-052] Final Tender Submission` | 2 | Wed **2026-10-21** |

There are **37 working days** between 2026-09-02 and 2026-10-23, so the full schedule fits and nothing gets squeezed. No weekend landings to fix.

> *Had the deadline been, say, 2026-09-18 — only 12 working days out — the earlier milestones would give way: Final Tender Submission keeps its 2 clear working days no matter what, nothing goes earlier than today 2026-09-02, and Proposal Preparation would compress from 15 to 12. The closing message would then have to say which ones were squeezed and by how much.*

### Gmail → Drafts, single signed-in account

**One unsent draft.**

> **To:** anita.deshmukh@empiricinfotech.com
> **Subject:** `[DAA-BHA-2027-052] Bid Decision Conditional Bid`
> **Body (180–260 words):** tender name and buyer; authoritative deadline 2026-10-23 set by Corrigendum-01 dated 2026-08-11; the decision and the one finding that drove it (mandatory ISO 27001 clause amended by Addendum-02 is only Partially Compliant, 22 months of contract uncovered); the fatal issue (Data Engineer shortfall of 2, no hiring plan on record); the curable ones with owner and close date each — Vikram Shah by 2026-10-15, Meera Nair by 2026-12-15; the 4 Cannot Determine items; the 3 clarification questions; and the one thing Anita has to do next, with its date.
> **No attachments. Not sent** — not through a connector, not through a browser.

> *If the Bid Owner Email cell had been empty: leave `To` empty, and open the body with the line `RECIPIENT NOT CONFIRMED`.*

### Back to the sheet

On **Tender Tracker 2026 → Pending Tenders → row 5**: `Decision` = `Conditional Bid`, `Decision Date` = `2026-09-02`. Two cells. Nothing else on that sheet is touched, and the row stays on the tab where you found it — it does not get moved to a "Decided" tab.

---

## Act 11 — Run it again the same day, and nothing new appears

This is the idempotency contract. **Look before creating anything:**

- Jira: `project = BID AND labels = "DAA-BHA-2027-052"` across `Bid Compliance` and `Bid Production`
- Notion: search the `Tender Decisions` database for the bracketed prefix
- Calendar: search `Bid Management` for `[DAA-BHA-2027-052]`
- Gmail: search Drafts for the same prefix

Anything already carrying it gets **updated where it stands**, never duplicated. However many times this runs: **1 reference = 1 decision page, 6 production issues, 6 calendar events, 1 draft.**

---

## Act 12 — When something breaks

**Two routes to every app**: the connected integration first, the **Chrome browser plugin** when that fails. And "fails" is broad — missing, erroring, timing out, refusing the call, reporting an unrecognised tool, returning nothing while the screen clearly shows something, or returning something the screen contradicts. All of those mean switch.

Say the Notion integration returns an empty result for `Certifications`. You don't write "Notion unavailable." You open **notion.so → Company Knowledge Base → Certifications** in Chrome, already signed in on this machine, and read it there. **Nothing is called missing, unauthorized, unavailable or blocked until Chrome has been pointed at it and failed too.** Transient-looking failure? Retry once. Rate limit? Wait it out rather than falling back. Integration and screen disagree? **Believe the screen** — the screen is what the workspace actually holds.

The login rule that blocks the buyer's portal (and Upwork, Freelancer, LinkedIn, Apollo) has nothing to say about these workspace apps. Going in through the browser is simply how the work gets done there.

**Only two things stop the run outright:** `Tender Tracker 2026` failing on both routes, or the tender folder failing on both routes. Either one is reported as blocked, quoting the exact error text from each route.

Everything else gets written down and worked around. If `07_Annexure_D_Pricing_Schedule.xlsx` refuses to open on both routes, you name it exactly as the brief names it, say what it cost the analysis, mark the requirements it left as **Cannot Determine**, and **finish every other part of the run**. You never invent a file, folder, tab, Notion page, Jira issue, calendar event, portal notice or certificate — and you never report something as opened or created when it wasn't.

---

## The closing message

The run is done when: row 5 carries `Conditional Bid` and `2026-09-02`; the Notion page has every field filled or marked Cannot Determine; `Bid Compliance` holds 6 compliance issues plus 3 clarification issues; `Bid Production` holds its 6; the 6 events sit on the `Bid Management` calendar with no guests and no weekend dates; one unsent draft sits in Gmail Drafts; and the closing message covers **all eleven items** — the tender taken and what ruled the other six rows out, the authoritative deadline and the notice that set it, requirement counts by status, the fatal issue, the curable ones, the Cannot Determine items, the 3 questions kept and the 2 dropped with reasons, every step that fell back to Chrome with the error that sent it there, and every step still blocked with the error from both routes.

---

**The shape of it, in one line:** *pick one row → prove the folder → read everything → check the portal for what moved → build 28 requirements at 11 fields each → test them against Notion evidence and Jira capacity → apply the curable bar honestly → land one decision → write it into Jira, Notion, Calendar, Gmail and back into the sheet, idempotently.*
