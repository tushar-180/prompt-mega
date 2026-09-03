# The Prospect Research Workflow, Told as a Story

A plain-language walkthrough of `finalPrompt.txt`, using a worked example.

> Company names below are invented for illustration. `dummy_setup.txt` only says "Company A...E".

---

## The Cast

**The agency:** a small digital marketing shop in Ahmedabad. Sells exactly 4 things, SEO, Paid Advertising, Social Media Marketing, Website Optimization.

**The people:** Rahul and Priya, two BDEs.

**The date:** everything is frozen at **2026-09-01, Asia/Kolkata**. Every "last 90 days" means back to **2026-06-03**.

**The apps:**

| App | What lives there |
|---|---|
| **Jira Cloud** | Project *Sales Prospecting* (key `SP`), board *Prospect Pipeline* |
| **Google Drive** | Folder *Sales Prospect Research* |
| **Google Docs** | *Agency Services and Ideal Customer* + one report per prospect |
| **Google Sheets** | *Sales Prospect Research Tracker*, tab **Prospects** |
| **Gmail** | One signed-in account (search + Drafts) |
| **google.com** | Public search results only |
| **pagespeed.web.dev** | PageSpeed Insights |
| **Chrome browser plugin** | The universal fallback when any connector fails |

---

## Act 1, Monday morning, opening the board

The agent opens the *Prospect Pipeline* board and finds 5 cards:

| Key | Company | Status | Priority | Company Website |
|---|---|---|---|---|
| SP-1 | Shreeji Interiors | Pending | High | *(empty)* |
| SP-2 | Aarav Plumbing Services | Pending | Medium | aaravplumbing.in |
| SP-3 | Nova Dental Clinic | Pending | Low | novadentalcare.in |
| SP-4 | Ridham Electricals | Pending | High | ridhamelectricals.in |
| SP-5 | Kiran Tutorials | Research Complete | Medium | kirantutorials.in |

The filter is: **Status = Pending, type = Task, Company Website filled.**

- **SP-1 is the trap.** It is the oldest and it is High priority, the tempting one. But its Company Website is empty, so it is **out**. The rule says an empty field stays empty; you do not go Google "Shreeji Interiors" and paste in whatever site looks close.
- **SP-5 is out**, already Research Complete. Finished work, do not touch it.
- That leaves SP-2, SP-3, SP-4. Sorted by **Created date, oldest first** gives SP-2, SP-3, SP-4.
- **Take the top 2. Never a 3rd.** SP-4 qualifies on every rule and still does not get worked, because it is third in the queue. Processing it means a failed run.

> Priority High over Medium over Low, and then the lower issue number, are only tie-breakers on Created date. Here nothing ties, so High-priority SP-4 still loses to Low-priority SP-3.

**Selected: SP-2 Aarav Plumbing Services (Rahul) and SP-3 Nova Dental Clinic (Priya).**

---

## Act 2, Reading the prospect's own house

Starting from `aaravplumbing.in`, the address on the Jira card and not a search result for a similarly-named firm, the agent reads the home page, service pages, about, contact, and the blog. **Ceiling: 15 pages.**

What it comes back with for Aarav Plumbing:

- Sells emergency plumbing, bathroom fitting, water tank cleaning; serves Satellite, Bopal, Maninagar
- CTA is a "Get a Quote" form **that throws an error on submit**, and the phone number is baked into an image, not a `tel:` link
- Trust signals: 4 client logos, no reviews, no case studies
- Newest blog article: **2024-11-02**
- Gap: a visitor on a phone has no working way to contact them

---

## Act 3, What Google actually shows

Five searches on **google.com**, 2 pages of results each, public results only:

1. `Aarav Plumbing Services`
2. `Aarav Plumbing Services Ahmedabad`
3. `emergency plumber Ahmedabad` (a real buyer search, not "plumbing")
4. `bathroom fitting service Ahmedabad`
5. `water tank cleaning Ahmedabad`

The record is not "they rank badly". It is **absent from 2 pages on searches 3 and 5; page 2 position 14 on search 4; and here is who sits above them.**

**Hard boundary:** Search Console, Analytics and paid keyword tools are out of bounds. So no search volumes, no traffic estimates, no keyword difficulty. Anything you cannot see in public results is written as **Not Verified** with a line on what would settle it.

---

## Act 4, Picking exactly 3 competitors

Only from companies that **turned up in those same searches**, sell the same main service, serve the same area. Six qualified, so:

1. Keep the ones appearing in the most of the 3 commercial searches: *Rapid Plumb Care* (3/3), *Shakti Plumbers* (3/3), *Ahmedabad Pipe Works* (2/3), *Metro Plumbing* (2/3)
2. Tie broken on higher position: Ahmedabad Pipe Works sat at #3, Metro at #9
3. Final three: **Rapid Plumb Care, Shakti Plumbers, Ahmedabad Pipe Works**

If only 2 had qualified, the comparison runs on 2 and the shortfall is named in the document *and* in the closing message.

---

## Act 5, PageSpeed, 8 sites, 16 runs

For the prospect **and all 3 competitors**, on the home page **and** the single most important service page:

| | Mobile | Desktop | LCP | CLS | INP |
|---|---|---|---|---|---|
| aaravplumbing.in (home) | **38** | 71 | **5.8 s** | 0.21 | 340 ms |
| Rapid Plumb Care | 74 | 93 | 2.1 s | 0.02 | 180 ms |

Plus the top 3 opportunities from each report. Shakti Plumbers' service page times out, so that is written as **Not Verified** with the exact error text pasted in. Never a guessed score.

---

## Act 6, The social read

Only pages the prospect links from its own site, plus anything public that opens without an account. Three readings each: platform, newest public post date, and post count from **2026-06-03 to 2026-09-01**.

- Aarav Plumbing Facebook: newest post **2025-12-19**, 0 posts in window
- Aarav Plumbing Instagram: exists but private, so **Not Verified**, not "absent"
- LinkedIn, Upwork, Freelancer, Apollo: **out of bounds** this run

---

## Act 7, Gmail memory, and the plot twist

Search the signed-in account across **all mail, Sent, Archive, Spam included**, for `aaravplumbing.in` and "Aarav Plumbing", over 2024-09-01 to 2026-09-01.

A thread comes back: **"Website enquiry Aarav Plumbing"**, newest message **2026-09-01**.

That is inside the 90-day window, so it is a **live conversation someone already owns**. Consequences:

- **No draft is written for Aarav Plumbing at all**
- Tracker Outreach Status becomes `Active Thread Do Not Draft`
- The Jira comment names who sent that newest message and when

For Nova Dental: nothing found, so **No Previous Contact**, and a draft *does* get written.

> One subtlety that saves the run from itself: **Drafts do not count.** A "Prospect Outreach" draft left by yesterday's run of this same workflow must never be misread as a live conversation.

---

## Act 8, Scoring, and the cap that bites

100 points: **30** competitor gap + **25** how squarely the gap sits in one of the 4 services + **20** business fit (Industry and Location against *Agency Services and Ideal Customer*) + **15** verified rather than inferred + **10** decision-maker reachability.

**Aarav Plumbing:** 24 + 23 + 18 + 11 + 6 = **82**, which looks High.

But the team page names an owner and no second public source agrees, so decision maker is **Not Verified** and the cap fires at **69 maximum**. Final score **69, band Medium**. The whole point of the caps is that a strong-looking pitch cannot outrun weak evidence.

**Nova Dental:** 22 + 20 + 17 + 12 + 8 = **79, High**. The owner is confirmed by the clinic's team page *and* a signed byline in a public health column, 2 independent sources, so no cap.

---

## Act 9, Which one service to lead with

Four tests, and more than one fires.

**Aarav Plumbing**

- Website Optimization FIRES (mobile 38 under 50, LCP 5.8 s over 4 s, no working contact route)
- SEO FIRES (absent from 2 pages on 2 of 3 commercial searches; 3 competitors on page 1)
- Paid Advertising does NOT fire. Same absence, but Paid only fires where the site *converts cleanly*, and mobile 38 with a broken form does not
- Social Media Marketing FIRES (newest post 2025-12-19, 2 competitors posted in window)

Precedence is **Website Optimization > SEO > Paid Advertising > Social Media Marketing**, so **Primary: Website Optimization.** SEO and Social Media Marketing become **secondary services**, each written down with the evidence that fired it.

**Nova Dental:** Website Optimization does not fire (mobile 63, contact works). SEO fires. Paid fires too. Social Media Marketing fires. So **Primary: SEO**, secondaries Paid Advertising and Social Media Marketing.

---

## Act 10, Four things get written

**1. A Google Doc, in Drive folder *Sales Prospect Research*:**

`Prospect_Analysis_Aarav_Plumbing_Services_2026-09-01`

Carrying 15 required things: findings with the page each came from, all PageSpeed numbers, per-search visibility, social readings, the 3 competitors, the strongest gap, all 5 score components spelled out, band, primary service *with the test that fired it*, secondaries, decision maker or "Not Verified", Gmail result, an 80-word-or-fewer sales angle, and every Not Verified item with what would settle it. Sharing untouched.

**2. A row on the *Prospects* tab**, columns A to Q, matched on column A:

- Aarav Plumbing already had row 2 (seeded 2026-08-18), so it is **updated in place**
- Nova Dental had no row, so one is **appended at the bottom**
- Row 3 (Kiran Tutorials, finished last week) and Row 4 (*Nova Dental Solutions*, the near-miss name trap) are left **completely alone**

**3. One unsent Gmail draft, for Nova Dental only.**

Subject `Prospect Outreach Nova Dental Clinic`, To is the Contact Email on SP-3. Body 120 to 180 words: 2 findings with evidence, 1 thing a named competitor does better, the single primary service and what it fixes, 1 question answerable in a line. **No attachments, no external links, no promise about rankings, traffic, leads or revenue.** Nothing sent, scheduled or queued. It sits in Drafts for Priya to send by hand.

**4. Both Jira issues** get a comment (score and band, primary and secondaries, strongest gap with evidence, the competitor that beat them, doc name and link, decision maker status, Gmail result, next action with a date) and move **Pending to Research Complete**. Nothing moves to a status meaning *contacted*, because nothing was sent.

---

## About that draft

Yes, a **draft**, never a send. The workflow itself sends, schedules and queues nothing, not through the Gmail connector and not through Chrome.

| Field | Value |
|---|---|
| To | the **Contact Email** on that prospect's Jira issue, not a person found on Google |
| Subject | `Prospect Outreach ` + company name, so `Prospect Outreach Nova Dental Clinic` |
| Body | 120 to 180 words: 2 findings + evidence, 1 competitor advantage, the single primary service and what it fixes, 1 question answerable in a line |
| Forbidden | attachments, links outside the prospect's own site, any promise about rankings, traffic, leads or revenue |

Four ways it can go:

1. **Normal**, draft written. *Nova Dental Clinic* came back "No Previous Contact", so the draft opens cold. Column O reads `Draft Ready Not Sent`.
2. **Old thread found**, draft still written, but it opens by naming the last thing discussed and its date rather than introducing the agency cold.
3. **Blocked by a live thread**, so **no draft at all**. *Aarav Plumbing* had a thread whose newest message was dated 2026-09-01. Somebody already owns that conversation. Column O reads `Active Thread Do Not Draft`, and the Jira comment names who sent that last message and when.
4. **Gmail refuses to save**, so the full email text goes into that prospect's Google Doc under the label **Draft Email Not Saved** with the exact error text beside it, and no attempt is made to send it another way. Column O reads `Draft Blocked`.

So in this walkthrough: 2 prospects worked, 2 docs, 2 tracker rows, 2 Jira comments, but only **1 draft** in the Drafts folder.

---

## The two rules that run underneath everything

**Run it twice, nothing doubles.** Before writing anything: check the Drive folder for that filename, the Prospects tab for that company name, Gmail Drafts for that subject, and the Jira issue for a comment already dated 2026-09-01, then **update in place**. One doc, one row, one draft, one comment per company, however many times it runs.

**Chrome is the second route, always.** Connector missing? Times out? "No tool for that"? Permission refused? **That is not blocked, that is a reason to open the app in Chrome and carry on.** Nothing may be reported as unavailable until the Chrome browser plugin has been pointed at it and failed too, with both error texts quoted. A step called blocked without trying Chrome is a failed run.

Only **two** things stop anything:

- **Jira dead on both routes**, which stops the whole run
- **A prospect's own site dead on both routes**, which stops that one prospect and nothing else

Everything else, a PageSpeed run that will not finish, a competitor site that will not open, a sheet row that will not save, gets named, its cost to the analysis stated, marked Not Verified, and the run finishes around it.

---

## The closing message Rahul reads

> Took SP-2 and SP-3. SP-1 skipped, Company Website empty. SP-4 qualified but was 3rd on Created date. SP-5 already Research Complete.
>
> **Aarav Plumbing 69 Medium** (24/23/18/11/6, capped from 82, decision maker unverified), Website Optimization, fired by mobile 38 and LCP 5.8 s. No draft, live Gmail thread dated 2026-09-01.
>
> **Nova Dental 79 High** (22/20/17/12/8), SEO, fired by absence on 2 of 3 commercial searches with 3 competitors on page 1. Draft ready, not sent.
>
> Not Verified: Aarav Instagram (private), Shakti Plumbers service-page PageSpeed (timeout, error text below), Aarav decision maker (1 source).
>
> Fell back to Chrome plugin: Google Sheets write (connector 403). Still blocked: none.

---

## The design idea in one line

Every number in that message has to trace back to a page a skeptical person could open and check, and where it cannot, the workflow would rather say *Not Verified* and score the prospect Low than write something that sells well.
