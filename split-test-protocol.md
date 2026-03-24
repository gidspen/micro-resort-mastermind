# Split Test Protocol: Brayv AI vs Claude Ad Copy

## Objective
Determine which ad creation approach (Brayv's automated AI or Claude-written copy) drives lower cost-per-lead for the Micro Resort Buyer Challenge.

---

## Test Setup

| | Campaign A (Brayv) | Campaign B (Meta) |
|--|--|--|
| **Ad creation** | Brayv AI auto-generated | Claude-written copy |
| **Platform** | Brayv → Meta | Meta Ads Manager directly |
| **Pixel** | 1711035122902345 | 1711035122902345 |
| **Destination URL** | incrediblehospitalityco.com | incrediblehospitalityco.com |
| **Daily budget** | $10/day | $10/day |
| **Audience** | Match as closely as possible | Match as closely as possible |
| **Campaign objective** | Lead / Conversion | Lead / Conversion |
| **Conversion event** | Lead | Lead |

**Rule:** Keep everything identical except the ad creative. Same audience, same budget, same destination.

---

## Timeline

| Day | Action |
|-----|--------|
| Day 0 | Launch both campaigns simultaneously |
| Day 3 | Sanity check — confirm both ads are active and pixel is firing |
| Day 7 | First review — note early trends, do not make decisions yet |
| Day 14 | Decision point — evaluate results and determine winner |
| Day 30 | Brayv subscription renewal decision due |

**Minimum run time: 7 days.** Meta's algorithm needs time to exit the learning phase (~50 optimization events). Do not pause or adjust either campaign before Day 7.

---

## Metrics to Track (pull from Meta Ads Manager)

| Metric | What It Tells You |
|--------|------------------|
| **Cost per Lead (CPL)** | Primary decision metric — lower is better |
| **Click-through rate (CTR)** | How compelling the ad copy is |
| **Cost per click (CPC)** | How efficiently you're buying attention |
| **Landing page conversion rate** | Leads ÷ Link clicks — isolates landing page performance |
| **Reach & frequency** | Are you hitting new people or burning out the same audience |
| **Ad relevance score** | Meta's quality signal — higher = better targeting fit |

---

## Decision Criteria (Day 14)

**Declare Campaign B (Claude) the winner if:**
- CPL is ≥15% lower than Campaign A, OR
- CTR is ≥20% higher with comparable CPL

**Declare Campaign A (Brayv) the winner if:**
- CPL is ≥15% lower than Campaign B, OR
- Results are within 15% and Brayv saves meaningful time

**No clear winner if:**
- Results within 15% either direction — extend test to Day 21 or increase budget to get more data

---

## Brayv Renewal Decision (Day 30)

Renew if either:
- Brayv's CPL is competitive (within 20% of Meta direct)
- The multi-platform distribution (Google, TikTok, LinkedIn) is worth testing next

Cancel if:
- Claude + Meta Ads Manager clearly wins on CPL
- Brayv's CRM/follow-up features are already covered by GHL

---

## Notes
- Both campaigns use Pixel ID `1711035122902345` — attribution is handled automatically by Meta's backend via `fbclid`
- No separate pixels needed — Meta reports results per campaign in Ads Manager
- Screenshot both campaigns' stats on Day 7 and Day 14 for records
