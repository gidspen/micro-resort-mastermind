# Mastermind Landing Page Overhaul — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the incrediblehospitalityco.com landing page with proper technical SEO, AI-SEO/GEO optimization, and psychographically-aligned copy targeting both core personas (Generational Wealth Builder and W-2 Escapee).

**Architecture:** Single-file HTML landing page (index.html) with inline CSS. Changes span three layers: (1) `<head>` metadata and structured data, (2) body copy rewrite against psychographic research, (3) internal linking and content additions. No new files except a possible sitemap.xml.

**Tech Stack:** Static HTML/CSS on GitHub Pages. Facebook Pixel already integrated. Calendly for booking CTA. No JS framework.

---

## Context

### Source Documents
- **Current page:** `/Users/gideonspencer/micro-resort-mastermind/index.html`
- **Psychographic research:** `/Users/gideonspencer/Library/CloudStorage/GoogleDrive-gideon@stonemontcap.com/My Drive/Community/marketing/Avatar psychographic_report.docx`
- **Local preview:** `http://localhost:8000` (python3 http.server running)

### Two Core Personas
- **P1: Generational Wealth Builder** — Age 32-45, $200K-$500K+ HHI, 2-5 STRs. Driven by legacy, permanence, sophistication, control. Researcher. Needs evidence and frameworks. Slow decider.
- **P2: W-2 Escapee** — Age 28-42, $150K-$350K W-2, 2-3 STRs. Driven by freedom, urgency, cash flow, identity shift. Faster decider. Needs emotional permission and timeline proof.

### Owner Directives (Non-Negotiable)
- No $15k price references anywhere on the page
- De-emphasize Gideon personally; emphasize community, experts, and peer network
- "Micro resort" stays as lead positioning hook; include "boutique hotel" as scope expansion
- No double dashes (em dashes) in copy
- No use of word "honestly"
- "Student" language replaced with "Member" everywhere
- "Trained" replaced with "in the Network" or similar

### Key URLs
- Calendly CTA: `https://calendly.com/gideon-spencer/1-on-1-15-min-strategy-session-clone`
- Challenge page: `/challenge/`
- Webinar page: `/webinar/`
- Facebook Pixel ID: `1711035122902345`

---

## File Structure

All changes target a single file:
- **Modify:** `index.html` (all tasks)
- **Create:** `sitemap.xml` (Task 7)

---

## Task 1: Head Metadata — Meta Description, OG Tags, Canonical, Favicon

**Files:**
- Modify: `index.html:1-474` (the `<head>` section)

**Why:** Page has zero meta description, zero OG tags, no canonical tag. When shared via DM (the primary acquisition channel), it renders as a blank link. Google auto-generates a bad description.

- [ ] **Step 1: Add meta description after the viewport tag (line 5)**

```html
<meta name="description" content="The private mastermind for STR investors scaling into micro resorts and boutique hotels. Weekly expert calls, deal reviews, and $23M+ in member deal volume. Book a strategy call with Gideon Spencer." />
```

- [ ] **Step 2: Add canonical tag after meta description**

```html
<link rel="canonical" href="https://incrediblehospitalityco.com/" />
```

- [ ] **Step 3: Add Open Graph tags after canonical**

```html
<meta property="og:title" content="Micro Resort Mastermind for STR Investors | Gideon Spencer" />
<meta property="og:description" content="A private operator community for STR investors scaling into micro resorts and boutique hotels. Weekly expert calls, live deal reviews, and $23M+ in member deal volume." />
<meta property="og:image" content="https://incrediblehospitalityco.com/images/gideon-headshot.jpeg" />
<meta property="og:url" content="https://incrediblehospitalityco.com/" />
<meta property="og:type" content="website" />
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Micro Resort Mastermind for STR Investors | Gideon Spencer" />
<meta name="twitter:description" content="A private operator community for STR investors scaling into micro resorts and boutique hotels. Weekly expert calls, live deal reviews, and $23M+ in member deal volume." />
<meta name="twitter:image" content="https://incrediblehospitalityco.com/images/gideon-headshot.jpeg" />
```

Note: OG image should ideally be a 1200x630px branded image. Using headshot as placeholder. Gideon should create a proper social share image later.

- [ ] **Step 4: Add preconnect for Facebook pixel**

```html
<link rel="preconnect" href="https://connect.facebook.net" />
```

- [ ] **Step 5: Update title tag with target keywords**

Change from:
```html
<title>Incredible Hospitality Mastermind | Gideon Spencer</title>
```
To:
```html
<title>Micro Resort Mastermind for STR Investors | Gideon Spencer</title>
```

- [ ] **Step 6: Verify in browser**

Open `http://localhost:8000`, inspect `<head>` in DevTools, confirm all tags render correctly.

---

## Task 2: JSON-LD Structured Data — FAQPage, Organization, Person

**Files:**
- Modify: `index.html` — add `<script type="application/ld+json">` blocks before closing `</head>`

**Why:** Zero structured data on the page. FAQPage schema is the highest-ROI single addition for both Google rich snippets and AI-SEO citation. Organization and Person schema establish entity clarity for LLMs.

- [ ] **Step 1: Add FAQPage schema**

Insert before `</head>`, after the Facebook Pixel noscript tag. Use the actual FAQ content from the page. Schema should include all 7 FAQ items currently on the page plus the 2 new ones being added in Task 5.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is included in the Incredible Hospitality Mastermind?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Annual membership includes Tuesday live expert calls (operators, lenders, brokers), Thursday live deal review calls, private Skool community access, deal analysis model and LOI templates, all recorded call archives, direct messaging access to Gideon Spencer, and a ticket to Incredible Hospitality Live (the annual in-person event)."
      }
    },
    {
      "@type": "Question",
      "name": "Do I need to already own short-term rentals to join the Mastermind?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. The Mastermind is designed for operators who have proven the STR model and are ready to scale into micro resort or boutique hotel acquisition. If you own 1+ properties and are generating real cash flow, this is built for you."
      }
    },
    {
      "@type": "Question",
      "name": "How long is the Incredible Hospitality Mastermind membership?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Annual. You get 12 months of live calls, community access, deal reviews, and events. Most members close a deal within the first year. Renewal is available at the same rate for active members in good standing."
      }
    },
    {
      "@type": "Question",
      "name": "What if I'm not ready to buy a micro resort in the next 6 months?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "The strategy call will sort that out. If you need to build capital first, Gideon will tell you directly and point you to free resources to prepare. The Mastermind is for people actively working toward an acquisition."
      }
    },
    {
      "@type": "Question",
      "name": "What is Incredible Hospitality Live?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "The annual in-person event for the Mastermind community. Three days of deal talks, operator sessions, site tours, and networking. Mastermind membership includes your ticket. The 2026 event is April 24-26 at Lake Travis, TX."
      }
    },
    {
      "@type": "Question",
      "name": "Is the Mastermind the same as the Incredible Hospitality podcast or the free challenge?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "No. The podcast (86+ episodes) is free public content. The free 5-Day Challenge builds your buy box and deal framework. The Mastermind is the private, high-accountability tier with weekly live calls, deal reviews, and direct access to a network of operators, lenders, and brokers."
      }
    },
    {
      "@type": "Question",
      "name": "How do I apply to the Incredible Hospitality Mastermind?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Book a 15-minute strategy call. Gideon takes every application call personally. If it is the right fit, he will tell you how to get started. If it is not the right time, he will give you a clear path to get there."
      }
    },
    {
      "@type": "Question",
      "name": "Can I join the Mastermind while still working full-time?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Most members start while holding a W-2. The weekly calls are scheduled and recorded if you cannot attend live. Many members use the Mastermind as the bridge between their current income and their first fully operational micro resort or boutique hotel."
      }
    },
    {
      "@type": "Question",
      "name": "Is the Mastermind only for people buying their first micro resort?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "No. Members range from operators acquiring their first boutique property to portfolio builders on their third or fourth deal. The deal review calls handle any stage of acquisition complexity."
      }
    }
  ]
}
</script>
```

- [ ] **Step 2: Add Organization + Person schema**

Insert as a separate `<script type="application/ld+json">` block:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Incredible Hospitality Co",
  "url": "https://incrediblehospitalityco.com",
  "founder": {
    "@type": "Person",
    "name": "Gideon Spencer",
    "jobTitle": "Founder, Incredible Hospitality Mastermind",
    "url": "https://incrediblehospitalityco.com",
    "sameAs": [
      "https://www.instagram.com/gideonspencer_/"
    ]
  },
  "description": "A private mastermind community for short-term rental investors scaling into micro resorts and boutique hotels. Weekly expert calls, live deal reviews, and $23M+ in member deal volume.",
  "contactPoint": {
    "@type": "ContactPoint",
    "email": "gideon@stonemontcap.com",
    "contactType": "sales"
  }
}
</script>
```

- [ ] **Step 3: Verify structured data**

Open `http://localhost:8000`, view page source, confirm both JSON-LD blocks parse correctly (no trailing commas, valid JSON).

---

## Task 3: Copy Rewrite — Hero, Top Bar, Proof Bar (Psychographic Alignment)

**Files:**
- Modify: `index.html:477-521`

**Why:** Top bar is dead real estate. Hero subtitle describes category, not transformation. Proof bar uses "Student" and "Trained" language that both personas reject.

- [ ] **Step 1: Rewrite top bar (line 479)**

Change from:
```
Incredible Hospitality Mastermind | Applications Open
```
To:
```
38 Properties. $304M+ AUM. The Mastermind Where STR Operators Build Resort Portfolios.
```

Rationale: Leads with community proof (P1 sophistication + P2 peer validation). "Resort Portfolios" signals scale.

- [ ] **Step 2: Rewrite hero subtitle (line 488)**

Change from:
```
A private mastermind for STR operators who are done scaling horizontally and ready to acquire their first (or next) micro resort.
```
To:
```
A private operator community for STR investors ready to acquire their first (or next) micro resort, boutique hotel, or small hospitality property. Weekly expert calls. Live deal reviews. $23M+ in member deal volume.
```

Rationale: Adds "boutique hotel" scope expansion per positioning decision. Adds concrete proof points. "Operator community" not "mastermind" in subtitle avoids course framing. Serves P1 (sophistication of "hospitality property") and P2 (specificity of weekly calls).

- [ ] **Step 3: Add secondary CTA below hero primary CTA (after line 494)**

Add after the `<p class="cta-note">` line:
```html
<p class="cta-note" style="margin-top:20px;"><a href="/challenge/" style="color:var(--gold); text-decoration:underline;">Not ready for a call? Start with the free 5-Day Challenge.</a></p>
```

Rationale: P1 (Generational Wealth Builder) will not book a call cold. They need a lower-friction research path. This reduces bounce without diluting the primary CTA.

- [ ] **Step 4: Rewrite proof bar labels (lines 513, 517)**

Change:
```
STR Investors Trained
```
To:
```
Operators in the Network
```

Change:
```
Student Deal Volume
```
To:
```
Member Deal Volume
```

- [ ] **Step 5: Verify in browser**

Refresh `http://localhost:8000`, check hero, proof bar, and secondary CTA render correctly.

---

## Task 4: Copy Rewrite — Feature Cards, Results Band, Qualifier Section

**Files:**
- Modify: `index.html:523-618`

**Why:** Feature Card 2 is Gideon-centric. Results band is thin (one stat). Qualifier section has generic language that doesn't hit persona triggers and still references "Gideon in your corner."

- [ ] **Step 1: Rewrite Feature Card 2 headline and copy (lines 543-550)**

Change headline from:
```
Private Skool Community &amp; Direct Access to Gideon
```
To:
```
Active Operator Network + Direct Access
```

Change card body from:
```
A private operator community (not a Facebook group) with direct access to Gideon, peer accountability, and deal collaboration from investors actively in the market.
```
To:
```
A private community of STR operators who are actively in the market, not just consuming content. Peer deal collaboration, co-investment threads, and direct access to Gideon and the expert network when you need it.
```

Change bullets:
- "Private Skool community with 200+ STR investors" → "200+ active operators sharing deal flow, not just asking questions"
- "Direct messaging access to Gideon" → "Direct access to Gideon, member operators, and weekly expert guests"
- "Member deal sharing and co-investment threads" → keep as-is

- [ ] **Step 2: Rewrite Feature section header H2 (line 528)**

Change from:
```
Everything You Need to Close Your First Micro Resort Deal
```
To:
```
Everything You Need to Close Your Next Hospitality Deal
```

Rationale: "Next" instead of "First" serves both first-timers (P2) and portfolio builders (P1). "Hospitality Deal" covers micro resorts + hotels.

- [ ] **Step 3: Rewrite Feature Card 3 body (line 555)**

Change from:
```
The actual tools Gideon uses to analyze, underwrite, and close micro resort acquisitions, plus in-person access at the annual live event.
```
To:
```
The deal frameworks, templates, and tools the community uses to underwrite and close hospitality acquisitions, plus in-person access at the annual live event.
```

- [ ] **Step 4: Expand Results Band (lines 572-581)**

Replace entire results band inner content:
```html
<h2>Members Don't Study Deals. They Close Them.</h2>
<p>This is not a course. It is an operator environment with weekly deal reviews, real expert access, and a peer group that holds you accountable to execution.</p>
<div class="results-stats">
  <div class="results-stat">
    <span class="rs-number">$23M+</span>
    <span class="rs-label">Member Deal Volume</span>
  </div>
  <div class="results-stat">
    <span class="rs-number">38</span>
    <span class="rs-label">Properties in Community</span>
  </div>
  <div class="results-stat">
    <span class="rs-number">12 mo</span>
    <span class="rs-label">Avg Time to First Deal</span>
  </div>
</div>
```

Rationale: Pulls "members close their first deal within the first year" out of the FAQ (where it was buried) and into the results band. Adds a second community stat. The "12 mo" stat directly serves P2's need for a timeline. H2 now has operator-level language instead of generic "Members Are Closing Deals."

**Note to Gideon:** Confirm the "12 months" claim is defensible before launch. If not, remove that stat and keep the other two.

- [ ] **Step 5: Rewrite qualifier section "Yes" bullets (lines 597-604)**

Replace all six bullets:
```html
<li>You own 1+ short-term rentals and have proven the model. Now you want to own the whole property.</li>
<li>You want to acquire a boutique hotel or micro resort and need the deal framework, the network, and the accountability to make it happen</li>
<li>You're past the research phase. You're ready to put a deal on the table.</li>
<li>You want peer-level access to operators who are actively in the market, not just talking about it</li>
<li>You want access to a network of operators, lenders, and brokers who are actively working deals, not just teaching about them</li>
<li>You want out of the W-2, or you're already out, and a micro resort is the vehicle you're building toward</li>
```

Rationale: Bullet 3 replaces generic "invest in your growth" with P1-resonant action language. Bullet 5 replaces "Gideon in your corner" with network framing. Bullet 6 directly addresses P2's W-2 escape drive.

- [ ] **Step 6: Verify in browser**

Refresh, check all four sections render correctly.

---

## Task 5: Copy Rewrite — About Section, CTA, FAQ, Bottom Hero

**Files:**
- Modify: `index.html:622-760`

**Why:** About section frames Gideon as instructor ("Who You're Learning From"). CTA is generic. FAQ is missing two key objection-handling questions. Bottom hero buries network proof and uses "student" language.

- [ ] **Step 1: Rewrite About section eyebrow (line 626)**

Change from:
```
Who You're Learning From
```
To:
```
Who Built This
```

- [ ] **Step 2: Rewrite About section body copy (lines 634-636)**

Replace three paragraphs with two:

```html
<p>Gideon Spencer has personally acquired $6.5M in hospitality assets across 6 hotels and 30 units, starting from the same position most Mastermind members start: a handful of STRs and the conviction there was a bigger play. He hosts the Incredible Hospitality podcast (86+ episodes, 5 stars, 98 ratings) and takes every application call personally.</p>
<p>The Mastermind is not his coaching program. It is the high-accountability environment he built because the peer group he wanted did not exist. Every Tuesday, a different expert joins the call: operators, lenders, lawyers, brokers. Every Thursday, members put their live deals on the table for group feedback. The community collectively spans 38 properties and $304M+ in assets under management.</p>
```

Rationale: Paragraph 1 is a tight founder bio. Paragraph 2 pivots immediately to the community and expert network. De-centers Gideon per his directive.

- [ ] **Step 3: Reorder About section badges (lines 637-642)**

Change from: `$6.5M Personal Portfolio | 6 Hotels, 30 Units | 38 Hotels in Community | $304M+ AUM`

To: `38 Properties in Community | $304M+ AUM | 86+ Podcast Episodes | $23M+ Member Deal Volume`

Rationale: Lead with community stats, not personal stats. Personal acquisition numbers are in the body copy already.

- [ ] **Step 4: Update image alt tag (line 630)**

Change from:
```
alt="Gideon Spencer"
```
To:
```
alt="Gideon Spencer, micro resort investor and founder of Incredible Hospitality Mastermind"
```

- [ ] **Step 5: Rewrite CTA section H2 and subtitle (lines 697-698)**

Change H2 from:
```
Ready to Build Your Micro Resort?
```
To:
```
The Next Deal Starts with One Conversation.
```

Change subtitle from:
```
Book a 15-minute strategy call. We'll talk about where you are, where you want to go, and whether the Mastermind is the right fit.
```
To:
```
Book a 15-minute call. We'll look at your current portfolio, your buy box, and whether the Mastermind is the right environment for where you're headed.
```

- [ ] **Step 6: Add two new FAQ items (after line 743, before closing faq-list div)**

Add before the "How do I apply?" FAQ item:

```html
<div class="faq-item">
  <h3>Can I join the Mastermind while still working full-time?</h3>
  <p>Most members start while holding a W-2. The weekly calls are scheduled and recorded if you can't attend live. Many members use the Mastermind as the bridge between their current income and their first fully operational micro resort or boutique hotel.</p>
</div>
<div class="faq-item">
  <h3>Is this only for people buying their first micro resort?</h3>
  <p>No. Members range from operators acquiring their first boutique property to portfolio builders on their third or fourth deal. The deal review calls handle any stage of acquisition complexity.</p>
</div>
```

Rationale: First question directly addresses P2's biggest blocker (W-2 constraint). Second question serves P1 who may already have properties and wonders if this is too junior.

- [ ] **Step 7: Rewrite FAQ question wording for AI query matching**

Change "What exactly is included?" to:
```
What is included in the Incredible Hospitality Mastermind?
```

Change "Do I need to already own short-term rentals?" to:
```
Do I need to own short-term rentals to join the Mastermind?
```

Rationale: FAQ questions should match natural language queries that users type into AI tools.

- [ ] **Step 8: Rewrite bottom hero body copy (line 754)**

Change from:
```
The Mastermind is where STR operators become micro resort owners. Two calls per week. A community of 200+ active investors. Direct access to Gideon. $23M in student deal volume and counting.
```
To:
```
The Mastermind is where STR operators become micro resort and boutique hotel owners. Two calls per week. A community of 200+ active operators. Direct access to lenders, brokers, and peers who are actively closing deals. $23M in member deal volume and counting.
```

Rationale: Adds "boutique hotel" scope. Replaces "Direct access to Gideon" with network framing. Replaces "student" with "member." Replaces "investors" with "operators."

- [ ] **Step 9: Verify in browser**

Refresh, review all modified sections.

---

## Task 6: Internal Links — Challenge, Podcast, Webinar

**Files:**
- Modify: `index.html` — multiple locations

**Why:** The challenge page is mentioned once (in FAQ body text) but never linked. The podcast is mentioned but not linked to any platform. This hurts both SEO (PageRank distribution) and conversion (giving non-ready visitors a next step).

- [ ] **Step 1: Link the challenge page in FAQ "Do I need to own short-term rentals?" answer**

Change:
```
start with the free 5-Day Micro Resort Buyer Challenge first at incrediblehospitalityco.com/challenge.
```
To:
```
start with the free <a href="/challenge/" style="color:var(--gold);">5-Day Micro Resort Buyer Challenge</a> first.
```

- [ ] **Step 2: Link the challenge page in qualifier "Not for you" section**

Change:
```
You're not ready to invest in yourself yet. Join the free challenge first and come back when you are.
```
To:
```
You're not ready to invest in yourself yet. <a href="/challenge/" style="color:#e74c3c;">Join the free challenge first</a> and come back when you are.
```

- [ ] **Step 3: Link to podcast in the "Is this the same as the podcast?" FAQ answer**

Change:
```
The podcast (86+ episodes, available everywhere) is public content
```
To:
```
The <a href="https://podcasts.apple.com/us/podcast/incredible-hospitality/id1234567890" target="_blank" rel="noopener" style="color:var(--gold);">Incredible Hospitality podcast</a> (86+ episodes, available everywhere) is public content
```

**Note to Gideon:** Replace the Apple Podcasts URL placeholder above with the actual podcast URL before launch.

- [ ] **Step 4: Verify all links work**

Click each link in the browser. Confirm /challenge/ loads, secondary CTA link works, podcast link opens in new tab.

---

## Task 7: Create sitemap.xml

**Files:**
- Create: `sitemap.xml` in project root

**Why:** New domain with no link equity. Sitemap accelerates Google indexing for all three pages.

- [ ] **Step 1: Create sitemap.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://incrediblehospitalityco.com/</loc>
    <lastmod>2026-03-23</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://incrediblehospitalityco.com/challenge/</loc>
    <lastmod>2026-03-18</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://incrediblehospitalityco.com/webinar/</loc>
    <lastmod>2026-03-18</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.6</priority>
  </url>
</urlset>
```

- [ ] **Step 2: Verify sitemap loads**

Open `http://localhost:8000/sitemap.xml` in browser. Confirm valid XML renders.

---

## Task 8: Add "What Is a Micro Resort?" Definitional Section

**Files:**
- Modify: `index.html` — add new section after the social proof bar and before "What's Included"

**Why:** AI tools answering "what is a micro resort" or "how to buy a micro resort" will cite pages that define the term. This page assumes the reader already knows. Adding a short definitional section captures top-of-funnel AI queries and serves both personas (P1 wants sophistication framing, P2 wants the opportunity sized).

- [ ] **Step 1: Add new section HTML after proof bar (after line 521, before "WHAT YOU GET" section)**

```html
<hr class="divider" />

<!-- WHAT IS A MICRO RESORT -->
<section class="section-sm">
  <div class="container">
    <div class="section-header">
      <span class="eyebrow">The Opportunity</span>
      <h2>What Is a Micro Resort?</h2>
      <p style="max-width:680px;">A micro resort is a small-scale hospitality property, typically 4-20 units, that combines the operational model of short-term rentals with the asset value of a commercial hotel. Think boutique cabins, glamping sites, container hotels, or small lodge properties in high-demand leisure markets.</p>
      <p style="max-width:680px; margin-top:16px;">Unlike adding another Airbnb to your portfolio, a micro resort is a branded, appreciating commercial asset. You own the land, the brand, and the guest experience. It can be acquired as an existing property or developed from raw land. The financing structures (DSCR, SBA 7(a), seller carry) are different from residential STR loans, and the returns profile is fundamentally different: forced appreciation, higher ADR, and an asset you can sell as a going concern.</p>
      <p style="max-width:680px; margin-top:16px;">The Mastermind exists because this transition, from STR investor to hospitality operator, requires a deal framework, a financing strategy, and a network of people who have done it. That is what we built.</p>
    </div>
  </div>
</section>
```

Rationale: Three short paragraphs. First defines the asset class (citeable by AI). Second explains why it's different from STRs (hits P1's sophistication driver and P2's "what's the bigger play" question). Third bridges to the Mastermind as the mechanism.

- [ ] **Step 2: Verify in browser**

Refresh, confirm new section appears between proof bar and feature cards. Check mobile rendering.

---

## Task 9: Final Cleanup and Consistency Pass

**Files:**
- Modify: `index.html` — full document

**Why:** Multiple rounds of editing have introduced some inconsistencies. This task is a single pass to catch remaining issues.

- [ ] **Step 1: Search for remaining "student" references**

Grep the file for "student" (case-insensitive). Replace any remaining instances with "member."

- [ ] **Step 2: Search for remaining "trained" references**

Grep for "trained" (case-insensitive). Replace with "in the network" or similar.

- [ ] **Step 3: Search for remaining double dashes**

Grep for ` — ` (em dash with spaces). Replace with commas, colons, periods, or parentheses depending on context.

- [ ] **Step 4: Search for any remaining "$15" references**

Grep for `$15` to catch any $15k or $15,000 references. Remove.

- [ ] **Step 5: Confirm "Micro-Resort" vs "micro resort" consistency**

The H1 uses "Micro-Resort" (hyphenated, capitalized) for stylistic emphasis. All other body copy should use "micro resort" (unhyphenated, lowercase) for SEO consistency with search patterns.

- [ ] **Step 6: Remove unused CSS**

The `.price-callout` CSS class (lines 376-405) is no longer used since we removed the price display. Remove the entire block.

- [ ] **Step 7: Full browser review**

Open `http://localhost:8000`. Scroll the entire page top to bottom. Check:
- All links work (Calendly, /challenge/, podcast placeholder)
- No broken layout on desktop
- Resize to mobile width, confirm responsive behavior
- No placeholder text visible ([STUDENT NAME] section still hidden)
- No "student," "trained," em dashes, or $15k references visible

- [ ] **Step 8: Commit**

```bash
cd /Users/gideonspencer/micro-resort-mastermind
git add index.html sitemap.xml
git commit -m "Overhaul mastermind landing page: SEO metadata, JSON-LD schema, psychographic copy rewrite, internal linking, sitemap

- Add meta description, OG tags, canonical, Twitter cards
- Add FAQPage + Organization + Person JSON-LD structured data
- Rewrite copy against psychographic research (P1: Generational Wealth Builder, P2: W-2 Escapee)
- De-emphasize Gideon personally, emphasize community/expert network
- Add 'What Is a Micro Resort?' definitional section for AI-SEO
- Add secondary CTA to free challenge for non-ready visitors
- Add 2 new FAQ items (working full-time, portfolio stage)
- Internal link challenge page, podcast
- Create sitemap.xml
- Replace 'student' with 'member', 'trained' with 'in the network'
- Remove price references, unused CSS"
```
