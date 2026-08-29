# Fixpoint Studio — Agency Demo Library — Handoff

## What this is
Public demo gallery proving automation ideas to cold-email prospects, since past
outreach failed partly because links were untrustworthy/generic (claude.ai links,
no credibility). Repo: https://github.com/shloksarnayak/agency-demos
Live: https://shloksarnayak.github.io/agency-demos/
Local clone: `C:\Users\shlok\Documents\agency-demos` (paste this path to ChatGPT
or Claude to work on design/content directly; `git pull`/`git push` to sync).

## Structure
- `{function-name}/index.html` = generic template, fictional data, public-facing default.
- `{function-name}/examples/{client-slug}/index.html` = same template adapted with a
  real prospect's real, source-verified data. Linked from the generic page.
- `assets/theme.css` = single shared design system (fonts, colors, components) used
  by every page via relative `../assets/theme.css` (2 levels) or `../../../assets/theme.css`
  (3 levels, inside examples/).

## 7 templates built so far (all live, all verified working)
1. `product-finder-quiz/` — example: Ministry of Sight
2. `support-ticket-triage/` — examples: Jewelry Candles, Accurate Medical Billing, Simply Good Coffee, Thigpen Septic Tank Services, 512 Refrigeration Services
3. `instant-quote-calculator/` — example: Pool Table Guy
4. `review-showcase-widget/` — example: George's Concrete Pumping
5. `appointment-request-widget/` — examples: Wohl Optics, Independent Hearing
6. `order-status-lookup/` — examples: S&S Appliance, Wetworks Pool and Spa, Tow Pro Services, American Gutter Cleaning, iExpert Repairs, Modern Memory Design, The Cell Phone Guy, Music Corner, Process Server Associates, Beavers Bend Cabin Rentals, Water Well Services, Central Title & Escrow
7. `invoice-status-tracker/` — example: **AMR Janitorial Services** (newest, first of a new bucket, see below)

## Strategic pivot (2026-08-20): niche-first, agency-to-SaaS
Shlok decided to focus outreach on a specific underserved niche rather than staying
broad: **estimate/invoice reconciliation for multi-location field-service trades**
(scattered invoices, no cross-branch paid-status visibility, verbal estimates that
balloon into disputed final bills). Found by clustering the ~31 previously-
uncategorized prospects (out of 142 researched) that didn't fit the original 6
templates — this cluster had the most repeat businesses (~7) and, unlike generic
order-tracking, isn't already commoditized by cheap SaaS. Plan: land real paying
clients in this niche via the agency, learn the actual workflow deeply, then
productize into a SaaS once patterns are validated by real customers, not before.
`invoice-status-tracker/` is the first template built for this niche. A second
sub-pattern in the same cluster (consignment/estate-sale payout tracking) was
identified as low-competition but small-market, parked for now, not built.

**Separately, AfterShip/Track123 integration-as-a-service was scoped as a
DIFFERENT, cheaper offer** for the existing shipping/e-commerce-tracking leads
specifically (Modern Memory Design, Music Corner, etc.) — since that category IS
commoditized by $9-20/mo apps, the pitch there should flip to "I'll set that up
and configure it for you" (~$300-800 flat fee) rather than competing with a
custom build at $1,500-6,000. Not yet built into the site or reply-routine
copy — a decision, not an implementation, as of this handoff.

## Non-negotiable build standard (do this for every new example)
1. Read the real business's own live site yourself (WebFetch), never trust old
   archived research summaries without re-verifying.
2. Build using the matching template's structure/CSS classes, swap in real data.
3. Test every interactive path in the browser (click through all states, edge
   cases like empty input/unknown ticket), not just read the code.
4. Run a fresh-context subagent review (Agent tool) with no access to your own
   reasoning, ask it to independently re-fetch the real site and catch factual
   errors, overstated claims, or contradictions. This has caught real bugs every
   time (a false claim, a stale date, a wrong domain name, a stock-availability
   bug) — never skip it.
5. Fix what it finds, re-verify, then commit + push.
6. Zero em dashes anywhere in output (user's standing style rule). Check with:
   `grep -c $'\xe2\x80\x94' file.html` before every commit.

## Prospect research source
State repo (separate, private): `shloksarnayak/agency-prospecting-state`, branch
`master`. Local clone used this session:
`C:\Users\shlok\AppData\Local\Temp\claude\...\scratchpad\state` (session-temp,
re-clone with `gh repo clone shloksarnayak/agency-prospecting-state <path> -- -b master`
if starting fresh). Drafted prospects live in `prospects-outlook/2026-08-1*.md`.

## Categorization of the 142 fully-researched drafted prospects (done this session)
| Bucket | Count | Matches template |
|---|---|---|
| Unanswered contact / complaints / refunds / no-shows | 59 | support-ticket-triage OR order-status-lookup depending on whether it's an incoming-message-triage problem or a proactive-status-visibility problem — read each one, don't force-fit |
| No online booking / phone-only | 24 | appointment-request-widget |
| No online quote / "call for pricing" | 21 | instant-quote-calculator |
| Status/tracking gap | 6 | order-status-lookup |
| Empty reviews page | 1+ (undercounted by keyword search, needs manual read) | review-showcase-widget |
| Doesn't fit any of the 6 | ~31 | needs a new template design |

**Done:** Wetworks Pool and Spa LLC (order-status-lookup); Tow Pro Services
(order-status-lookup, dispatch-ETA-tracking variant); American Gutter Cleaning
& Installations (order-status-lookup, completion-confirmation variant);
iExpert Repairs (order-status-lookup, mail-in-repair-tracking variant,
UK, competitive-gap angle not complaint-based); Accurate Medical Billing
(support-ticket-triage, 2 tickets modeled closely on 2 real, independently
BBB-verified complaints rather than invented from scratch); Modern Memory
Design Picture Frames (order-status-lookup, custom-framing production
tracker, Trustpilot + BBB both independently verified); The Cell Phone Guy
(order-status-lookup, diagnostic-cost-estimate + repair-status variant,
Sioux Falls SD, deliberately excludes a separate rudeness/refund complaint
found in research, kept scoped to the cost-estimate/status gap only);
Music Corner (order-status-lookup, UK instrument-hire lifecycle tracker,
GoCardless+DPD stack, Trustpilot verification relied on search snippets
since Trustpilot itself blocks direct fetches); Simply Good Coffee
(support-ticket-triage, 2 tickets modeled on real BBB complaints about
their AI phone support; the draft's "AI chatbot" framing turned out to
be a phone-based AI voice system, not a website widget, live check
caught and corrected the mischaracterization before it shipped);
Process Server Associates (order-status-lookup, case-status/attempt
tracker; the draft claimed "zero proactive push" but a live check
found the opposite, they already email on attempted/complete, so the
demo was rebuilt around the real, narrower gap: silence between
multiple attempts); Beavers Bend Cabin Rentals (order-status-lookup,
guest-lifecycle messaging across 3 booking channels; deliberately
excludes real dispute/refund complaints per the source research's own
self-critique, and an overstated "over 50 properties" claim was caught
and corrected to the verified 49 before shipping); Thigpen Septic Tank
Services (support-ticket-triage, 3 tickets: 2 grounded in real dated
reviews about missed follow-up, 1 illustrative auto-send; explicitly
hedged as under 3% of ~440 reviews being negative, not a pattern);
Water Well Services (order-status-lookup, arrival-window texting on
top of their existing Jobber account; evidence is thin, single-platform
sourced, and the demo explicitly says so rather than overstating it);
512 Refrigeration Services (support-ticket-triage, structured-intake-
before-dispatch to protect a real 45-minute-response claim; zero
refund/money angle, an unverified "days later" detail from the source
review was softened before shipping); Central Title & Escrow
(order-status-lookup, closing-file status tracker for a licensed
title/escrow company; explicitly and repeatedly scoped away from the
actual title-examination/closing-disclosure work, status visibility
only, given regulatory sensitivity) — 15 of the 59-bucket.

**Then, a strategic pivot (see above):** rather than continuing the 59-bucket
one-at-a-time, built the first example in the new invoice/estimate-
reconciliation niche instead: AMR Janitorial Services (invoice-status-tracker,
new 7th template; sourced from the owner's own Make.com forum post plus an
independent live-site check; independent review caught a real misattribution,
the "3 branches, no cross-branch view" detail was written as if the owner said
it on the forum, when it actually came from the separate site check, corrected
before shipping to keep the two sources explicit and distinct).

**Skipped, not built:** Magic Moment Photography (magicmomentphotography.com)
— independently checked BBB directly and found 9 complaints over 3 years,
only 22% resolved, a recurring pattern of promised refunds never issued,
and language like "robbing us of the memory." That's a genuine
reliability/trust problem, not a fixable ops gap, the same category other
prospecting sessions explicitly excluded (e.g. the Sheamakery pattern:
money taken, nothing delivered). Do not build a demo for this business,
a friendly "just needs a status page" framing would understate real
financial harm to real customers. If this ever needs revisiting, it
would need a completely different, harm-aware approach, not this
template.

**Not yet done:** the other ~44 in that bucket, plus 24 booking, 21 quote, 6 status,
1+ reviews, ~31 uncategorized. Same one-at-a-time verified-build process for each.

## Recurring lesson across this session's 10 builds
The prospecting drafts (state repo) are a good starting point but not
gospel — three separate builds this session (American Gutter Cleaning,
Simply Good Coffee, Process Server Associates) needed the live-site
framing corrected because the draft's synthesis was stale, imprecise,
or characterized a real feature backwards. Always re-verify the
specific claim the demo's hero copy leans on against the live site
yourself, even when the draft cites it confidently with a "verified"
label.

## Important finding this session: outreach has outpaced demo-building
The Outlook send-drip routine sends on its own schedule regardless of whether a
demo exists yet — it does not wait for the demo library. As of 2026-08-19,
`replies-outlook/sent.json` in the state repo shows **171 emails already sent**,
against only 4 demos built total (Wetworks, S&S Appliance, Tow Pro Services,
American Gutter Cleaning). Both Tow Pro Services and American Gutter Cleaning
were already emailed (see `sent.json`) before their demos were built, so both
were built as reciprocity-for-a-follow-up, not a pre-outreach gift. The
"build before outreach" strategy from the prior session is not actually
enforced anywhere in the pipeline. Still undecided: whether to pause the
send-drip until the library catches up, or accept a two-speed system
(outreach on its own clock, demos built opportunistically for the strongest/
highest-value leads as follow-up ammo). Flag this back to the user before
assuming either direction.

## Caution from this session: don't trust the prospect draft's framing verbatim
Building the American Gutter Cleaning demo, the independent fresh-context
review (step 4 of the build standard) caught that the source prospect draft
in the state repo had mischaracterized one of two BBB complaints, calling it
"the same root problem" as the other when it was actually a different kind of
dispute (billing-without-authorization vs. no-completion-record), and got the
date gap wrong ("same week" vs. the actual 14 days). This got copied straight
into the first draft of the demo page and only caught by the independent
review. Lesson: re-verify BBB/complaint specifics against the primary source
when a page leans on more than one complaint, don't assume the prospecting
draft's synthesis is accurate just because the underlying fact-finding was
thorough. Never skip step 4.

## Sales strategy decided this session
Build the tool BEFORE outreach, not pitch-then-maybe-build. Reasoning: reciprocity
(a finished gift beats an ask), concreteness (a stranger's claims can't be
evaluated, a working demo can), and it directly answers the exact objection a real
lead gave ("I'm not going to open a link from a stranger, send me your full
profile"). Leverage: most new prospects reuse an existing template with their data
swapped in, cheap. Only genuinely novel problems (~31) need a new template built
from scratch — don't force everything into the existing 6.

## Standing rules from this session, still in force
- No em dashes anywhere in visible output.
- Never fabricate facts about a real business — verify live, cite what you found,
  say plainly if you couldn't access something (don't guess).
- Nothing gets sent/emailed without explicit approval — drafting/building is
  autonomous, sending to a real third party needs a clear yes first. (Update
  2026-08-20: Shlok gave blanket approval "all emails in drafts are approved
  to send" — 68 pre-existing Outlook drafts were queued and are being sent by
  the cloud send-drip routine at ~1/10min. That approval was for that specific
  batch, don't treat it as standing for future drafts without asking again.)
- Domain fixpointstudio.com previously got rate-blocked (550 5.7.708) — the
  cloud send-drip routine's global 10-minute pacing exists specifically to
  prevent a repeat, don't bypass it with a faster manual send.
- Agency target is back to $15,000/month (restored 2026-08-19 after UPSC prep
  was cancelled, see [[project_upsc_cancelled_aggressive_targets]] in Claude's
  memory) — the ~$500/month cost-coverage note from earlier is stale, both
  agency and SaaS ambition are aggressive again.
- Keep responses/chat terse when asked; the user directs everything and doesn't
  read code, so explain plainly and scope changes to exact files.

## Immediate next step
Strategic pivot as of 2026-08-20 (see above): focus is now the invoice/estimate-
reconciliation niche, not the broad 59-bucket sweep. Source more prospects
matching that pattern (multi-location field-service trades: scattered
invoices, no cross-branch paid-status view, or verbal-estimate-vs-final-bill
disputes) when prospecting research is turned back on, and build more
`invoice-status-tracker/` examples the same verified way as AMR Janitorial.
The broad 6-template/59-bucket sweep isn't abandoned, just deprioritized,
still fine to pick it back up between niche leads if one doesn't clear the
research gate. Also parked, not yet done: an AfterShip/Track123
setup-as-a-service offer for the shipping-tracking leads specifically (see
above), and a possible consignment/estate-sale payout-tracking template
(low competition, small addressable market, lower priority than #1).

## NOTE: this file was badly stale as of 2026-08-29 (see session below)
This handoff doc stopped being updated after 2026-08-20, but the repo kept
growing a lot: template count went from 7 to 33+ and example count from
~15 to 150+ via commits with messages like "Publish staged demos: X" and
"Add Y example to Z", evidently from other sessions/routines that never
wrote back here. The "7 templates" list and the 59-bucket categorization
above are stale, do not trust them, always `ls */examples` and `git log`
directly to see current real state before starting new work. This file's
narrative below picks up from the actual repo state as found 2026-08-29,
not from the stale "Immediate next step" above.

## 2026-08-29 session: sent-but-no-demo sweep (background run, Shlok asleep)
Task: Shlok asked to "ruthlessly build agency demos indefinitely" while he
sleeps, prioritizing businesses that already got cold outreach (tracked in
the private `agency-prospecting-state` repo's `replies-outlook/sent.json`,
230 unique sender emails / 228 unique domains) but have no demo built yet.

**Discovery:** local agency-demos clone was 58 commits behind origin
(another automated pipeline had been actively publishing demos all day,
last commit ~6 hours before this session started, alphabetically-ordered
commit messages suggesting a broad systematic sweep, not specifically a
sent-but-no-demo filter). Pulled to sync before starting, to avoid
duplicate work. Real state after pulling: 33 templates, 106+ examples
already live (see current `ls */examples` for the authoritative list, not
this file).

**Cross-referenced** all 228 unique domains from `sent.json` against every
built example (grepped every built .html file for each domain, not just
slug-name guessing, to avoid false negatives from name mismatches). Found
roughly 150 domains with outreach sent but genuinely no demo referencing
them anywhere in the repo. That backlog is large; this session worked
through a first slice of it, one at a time, full build standard, no
shortcuts, and is leaving the rest for continuation (see running list
below, kept updated after each commit this session).

**Built this session:**
1. **Prime Pest Control, LLC** (goprimepest.com, Huntsville AL + Greenville
   SC) — `billing-hold-tracker/examples/prime-pest-control/`. Two BBB
   complaints ~14 months apart (Sept 2024, Nov 2025) both describe billing
   continuing after service visits stopped or a cancellation request;
   verified the company's own BBB responses independently admit a "CRM
   billing system issue" and a scheduling "glitch," and confirmed
   GoHighLevel/LeadConnector on the live site plus no online
   portal/self-service cancellation. Independent fresh-context review
   re-fetched BBB and the live site separately, found no problems.
2. **The London Removal Company** (thelondonremovalcompany.co.uk, South
   London, family-run since 2000) — `follow-up-promise-tracker/examples/
   the-london-removal-company/`. Reviews found via web search (Trustpilot
   itself blocks direct fetch, disclosed explicitly on the page) describe
   damaged/missing items after a move followed by unanswered follow-up
   calls and emails, corroborated across at least two separate review
   texts. Verified live site runs WordPress with a bespoke quote tool, no
   post-booking claims/ticketing system. Independent review re-checked
   both independently, found no problems.

Both linked from their template's own index.html "How this gets built for
real" section (some existing examples, e.g. medcare-equipment, were
missing that link entirely before this session touched the file; only
fixed the ones edited this session, did not do a full audit of every
template for missing links).

**Backlog still remaining (sent but no demo, not yet built as of this
entry):** roughly 148 more domains, see the full list generation method
above (grep every domain from `agency-prospecting-state/replies-outlook/
sent.json` against `agency-demos/**/*.html`). Candidates already scoped
with research available in `agency-prospecting-state/prospects-outlook/
2026-08-11.md` and `2026-08-12.md` for a next batch include: Desert Rose
(desertroserv.com), Mission Pest Control (missionpestcontrol.com),
Cleveland Water and Fire (clevelandwaterandfire.com), Texas Fence
(texasfence.com), Classic Car Wash (classiccarwash.com), Superior
SoftWash (superiorsoftwash.com), Dallas Automatic Gate
(dallasautomaticgate.com), Eastern Locksmith Services
(easternlocksmithservices.com), Greenwich Locksmiths
(greenwichlocksmiths.com), Not Your Basic Locksmith
(notyourbasiclocksmith.com), RV Doctor Online (rvdoctoronline.com),
Garden State Gutter Cleaning (gardenstateguttercleaning.com), Crawl
Spaces NJ (crawlspacesnj.com), NW Fire Inc (nwfireinc.com), Quality
Brick & Stone (qualitybrickstone.com), Right Legal Solicitors
(rightlegalsolicitors.co.uk, mentioned as drafted same session as Prime
Pest Control and London Removal Co per the state repo's session summary).
Continue one at a time, same non-negotiable build standard, checkpoint
(commit+push+HANDOFF entry) after each one, do not batch multiple
uncommitted examples at once.

3. **Right Legal Solicitors Ltd** (rightlegalsolicitors.co.uk, Rotherham,
   UK) — `order-status-lookup/examples/right-legal-solicitors/`. Important
   nuance caught and verified before building: there are two SRA
   registrations tied to this business name, SRA 832861 shows CLOSED
   (01/05/2024) on the SRA register, while SRA 8007221 "Right Legal
   Solicitors Ltd" (Companies House 15196265, incorporated Oct 2023) is
   the currently ACTIVE, regulated successor firm at the same address and
   website, confirmed directly on both SRA register pages before writing
   anything. Built a status-visibility-only page (explicitly not legal
   advice or case management), sourced from reviews describing cases going
   quiet for months, including one file closed without notifying the
   client, alongside positive reviews of the same director, framed as
   "genuinely mixed," not a firm in trouble. Independent review confirmed
   the SRA distinction, the live site claims, and the review pattern
   separately, no problems found.

4. **Desert Rose RV Park** (desertroserv.com, Fernley, Nevada, family-owned
   since 1999) — `appointment-request-widget/examples/desert-rose-rv-park/`.
   Missed-call text-back angle (reused the American Asphalt
   Sealcoating/USA Pave template pattern). Verified phone-only booking
   and amenities directly on the live site, and independently re-fetched
   the specific guest review on The Dyrt (Reilly S., Oct 2025) describing
   an unreturned voicemail and 3 unanswered calls to the emergency line.
   Framed explicitly as one documented review, not a claimed pattern.
   Independent review confirmed both, no problems found.

5. **Mission Pest Control** (missionpestcontrol.com, San Diego, CA) —
   `billing-hold-tracker/examples/mission-pest-control/`. Same billing-hold
   pattern as Prime Pest Control (a different template reuse, both are
   pest control companies but unrelated businesses). Verified live site
   directly (San Diego, 6-city service area, FieldRoutes portal live at
   mission.pestportals.com) and independently re-fetched Mission's BBB
   complaint file, confirming three specific dated cases (Oct 2025, Dec
   2024-May 2025, Sept 2023-Jan 2024) of billing continuing after a
   cancellation request. Scoped narrowly to the acknowledgment gap, not
   the phone-based retention conversation. Independent review confirmed
   the live site, tech-stack claim, and each dated complaint separately,
   no problems found.

6. **Texas Fence** (texasfence.com, Houston, TX, family-owned since 2003)
   — `order-status-lookup/examples/texas-fence/`. Milestone status page
   with an escalation-flag stage (matches the draft's own proposed offer:
   "milestone-triggered status update... plus a simple unresolved-issue
   escalation flag"). Verified ProDBX embed via raw HTML fetch (WebFetch's
   markdown conversion silently strips iframes, had to curl the page
   directly, worth remembering for future builds), re-checked the July
   2024 BBB complaint, and confirmed recent (Aug 2025-Feb 2026) reviews
   are genuinely five-star so the "not a live fire" framing holds up.
   Independent review confirmed all three independently, no problems.

**Skipped, not built (found via the sent-but-no-demo cross-reference, but
already researched and explicitly dropped in the private state repo for
real trust/reliability reasons, not fixable ops gaps):**
- **Cleveland Water and Fire Restoration** (clevelandwaterandfire.com,
  Solon, OH) — dropped in state-repo research on both scale (~29-31
  employees, dedicated BD/sales team, owner runs ~100 employees across 3
  related companies, well above a solo-freelancer engagement) and trust
  grounds (BBB complaints describe quotes ballooning 2-3x with no advance
  notice, an insurer reportedly saying the company is "known for scamming
  seniors," an allegation of coercing a customer into believing salvageable
  items were unsalvageable, and the company asking a negative Google
  reviewer to revise their review). Same category as the Magic Moment
  Photography precedent, do not build a demo for this business.
- **Not Your Basic Locksmith** (notyourbasiclocksmith.com, Arlington, TX)
  — dropped in state-repo research: revoked BBB accreditation (D rating),
  genuinely ambiguous ownership across sources (tied to a differently-named
  sibling entity), and a complaint pattern (deposits taken via Zelle,
  technician no-shows, refunds promised and not delivered) that reads as a
  trust/fulfillment issue, not a fixable lead-routing gap. Do not build a
  demo for this business.
Both domains appear in `sent.json` (outreach already went out, likely
before or without cross-referencing the drop decision), but per the
project's own hard rule, a demo should not be built for a business with a
genuine reliability/trust problem rather than a fixable ops gap. Flagging
this discrepancy (outreach sent to businesses later flagged as trust
risks) as worth a look when send-drip/sourcing get reconciled again, not
something to silently fix by building a demo anyway.

7. **Superior SoftWash** (superiorsoftwash.com, Linthicum Heights, MD) —
   `qc-warranty-tracker/examples/superior-softwash/`. More sensitive than
   most builds in this library: references a real, disputed BBB complaint
   about conifer/tree damage allegedly from cleaning chemicals (14-day
   contract window vs an arborist's month-plus timeline for damage to
   show) and a second complaint about grass/bush damage the company
   declined responsibility for. Built to stay explicitly neutral, the
   page documents (before/after photos, a 30-day check-in), it does not
   adjudicate who was right. Independent review was specifically asked to
   lead with a sensitivity assessment given the subject matter and
   confirmed the framing is fair to both the business and the
   complainants, all facts verified against BBB and Checkbook.org.

8. **Dallas Automatic Gate, Inc.** (dallasautomaticgate.com, Mesquite/
   Dallas, TX, 31+ years) — `follow-up-promise-tracker/examples/
   dallas-automatic-gate/`. Verified live site (basic contact form only,
   no tracking/confirmation system) and a GuildQuality review (Oct 2025)
   plus Angi reviews describing the estimate/scheduling follow-through
   gap. Independent review caught one real discrepancy: the page cited
   145 GuildQuality reviews when the live count is 147, fixed before
   this was committed. Good example of the independent-review step
   catching something real, worth remembering it's not just a formality.

Remaining candidates for next batch (from the same 2026-08-11/12 research
files, not yet built): Cleveland Water and Fire
(clevelandwaterandfire.com, skip, see trust/reliability note above),
Classic Car Wash (classiccarwash.com), Not Your Basic Locksmith
(notyourbasiclocksmith.com, skip, see trust/reliability note above),
RV Doctor Online (rvdoctoronline.com), Garden State Gutter Cleaning
(gardenstateguttercleaning.com), Crawl Spaces NJ (crawlspacesnj.com,
not found in state-repo research as of this session, would need fresh
sourcing), NW Fire Inc (nwfireinc.com), Quality Brick & Stone
(qualitybrickstone.com), plus ~135 more domains from the same
sent-but-no-demo cross-reference not yet individually researched in
this file.

## 2026-08-29 session continued (new agent instance, Shlok still asleep)
Picked up the sent-but-no-demo sweep from the shortlist above. `git pull`
first (already up to date locally after the prior instance's pushes).
Re-cloned/pulled `agency-prospecting-state` too (62509e1, brought in
Tampa Well Drilling delivery notes and fresh prospecting logs, not
relevant to this repo). Continuing one-at-a-time, full build standard,
commit+push after each.

9. **Eastern Locksmith Service Inc.** (easternlocksmithservices.com,
   Goldsboro, NC) — `appointment-request-widget/examples/
   eastern-locksmith-service/`. Angle: the business's own drive-thru
   window already splits jobs into "quick" (key copies/pickup) vs
   "needs a full visit," but every inbound call, true lockout emergency
   or routine key/fob question, funnels through one phone line with no
   way to triage before pickup. Built a two-tap triage simulation
   (urgent lockout routes to "dispatch now," routine routes to
   "drive-thru/callback booking"). Verified phone number, hours,
   drive-thru window hours, and absence of any online booking directly
   against easternlocksmithservices.com and its /contact-us/ page.
   Independent fresh-context review re-fetched both pages separately,
   confirmed every factual claim, checked meta/disclaimer/em-dash
   requirements, and traced the JS triage logic branch by branch, found
   no problems.
