# proxy for web scraping: real plan prices, per-site credit costs, and how to pick the right setup without overpaying

Most people searching for a proxy for web scraping are really choosing between two different products: a raw proxy pool you configure yourself, or a managed scraping API that handles proxies, CAPTCHAs, and retries for you. Raw residential proxies typically run $1.75–$8.40 per GB depending on the vendor and volume, while managed APIs charge per request. If you'd rather send one API call and get clean HTML back, ScraperAPI is the managed route: a free plan with 1,000 credits a month, a 7-day trial with 5,000 credits and no credit card, and paid plans from $49/month.

This guide walks through the full plan lineup, the credit costs most articles skip, and the small print that changes what you'll actually pay.

> **Quick picks**
> - Just testing an idea? Start on the free plan (1,000 credits/month) or the 7-day trial (5,000 credits, no card).
> - Running a small-to-medium scraper? Hobby at **$49/month** (100,000 credits) covers most single-project workloads.
> - Scraping Google, Bing, or LinkedIn heavily? Price those domains first — they cost 25–30 credits per request, not 1. The math is in the section below.
>
> 👉 [See all ScraperAPI plans and current prices](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## First, figure out which kind of proxy you actually need

"Proxy for web scraping" covers three products with very different price tags, and picking the wrong category is the most common way people overspend.

Datacenter proxies are the cheapest ($0.50–$2/GB in most lineups) but in 2026 mainstream sites detect and block them almost immediately. They're fine for targets with no anti-bot protection and useless for Amazon or Google. Residential proxies come from real ISP connections, cost roughly 5–10x more, and are the baseline for scraping protected sites. Mobile proxies ($15–$30/GB) are nearly undetectable and mostly reserved for social platforms like Instagram and TikTok when residential IPs fail.

On top of that, the industry has split into two billing models. Proxy pools bill per GB of bandwidth. Managed scraping APIs bill per request or per credit — you send a URL, the provider rotates IPs, solves CAPTCHAs, renders JavaScript, and returns the page. A 2026 hands-on comparison of six proxy services summed up the choice plainly: pick the model that mirrors your traffic shape, not the vendor's preferred SKU. If your projects are request-heavy but bandwidth-light (most HTML scraping is), per-request pricing usually wins.

ScraperAPI sits in the managed camp. You never see the underlying proxies — you call the API with a target URL and get back rendered, unblocked HTML or JSON. One 2026 comparison ranked it first among managed options for exactly this reason: you write less code and skip proxy infrastructure entirely.

## ScraperAPI plans and pricing: the full lineup

ScraperAPI bills by monthly API credits, and every paid plan includes the same core features: JS rendering, premium residential and mobile IPs, CAPTCHA and anti-bot handling, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee. The plans differ in credits, concurrency, and geo-targeting. Annual billing knocks 10% off every tier.

| Plan | Credits/month | Concurrent threads | Monthly price | Annual (per month) | Get it |
| --- | --- | --- | --- | --- | --- |
| Free | 1,000 | 5 connections | $0 | $0 | [Get free credits](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Hobby | 100,000 | 20 | $49 | $44.10 | [Get Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Startup | 1,000,000 | 50 | $149 | $134.10 | [Get Startup](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | 3,000,000 | 100 | $299 | $269.10 | [Get Business](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling | 5,000,000 | 200 | $475 | $427.50 | [Get Scaling](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Professional | 10,500,000 | 300 | $975 | $877.50 | [Get Professional](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Advanced | 21,500,000 | 500 | $1,975 | $1,777.50 | [Get Advanced](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | 22,000,000+ | 500+ | Custom | Custom | [Contact sales via pricing page](https://www.scraperapi.com/pricing/?fp_ref=coupons) |

Two things worth doing before you commit to a tier. First, divide credits by your real request volume — a plan's headline credit number means nothing until you know what your target sites charge per request (next section). Second, compare the annual column: Hobby drops from $49 to $44.10, Advanced from $1,975 to $1,777.50, and those savings compound across a year of scraping.

A student plan also exists in the official billing docs, though its pricing isn't published on the public pricing page — worth asking support about if that's you.

## What one credit actually buys

One credit equals one standard page request — but "standard" excludes a lot of the sites people actually scrape. ScraperAPI prices known-difficult domains separately, and the official list looks like this:

- Standard page: **1 credit**
- Amazon: **5 credits**
- Google and Bing (including subdomains): **25 credits**
- LinkedIn: **30 credits**
- Sites behind Cloudflare, Datadome, or PerimeterX: **+10 credits per request** when the bypass fires

This is the single most useful piece of information for budgeting, and it's missing from most comparison articles. If your project scrapes Google search results, 100,000 credits gets you roughly 4,000 pages on Hobby, not 100,000. A third-party review did similar math for rendered protected pages at 75 credits apiece: the free plan's 1,000 monthly credits cover about 13 such pages. The free tier is for testing, not running.

Two dashboard tools keep these costs under control. The Domain Cost Estimator shows the exact credit cost for any URL before you scrape it, and the `max_cost` parameter caps what a single request can consume. Between the two, you can price out an entire project before spending a dime beyond the trial.

👉 [Check current plan prices against your target sites](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## The fine print that changes the math

The billing FAQ answers several questions the marketing page doesn't, and each one affects real spending.

**Running out of credits behaves differently by plan.** By default, scraping pauses until credits renew. On Hobby through Professional (monthly), you can opt into auto-upgrade, which bumps you to the next tier automatically when credits hit zero — usually at a better price per credit. Pay-as-you-go, where you keep scraping past your limit at a fixed per-credit rate with a monthly spending cap you set, is only available on Scaling, Professional, Advanced, and Enterprise. Here's a trap worth flagging: the feature list on every plan's pricing card says "Pay as you go," but the official FAQ is explicit that it's a Scaling-and-up option. If PAYG flexibility matters to you, Hobby and Startup don't have it.

**Exceeding concurrency costs nothing.** Go over your thread limit and you get a 429 response telling you to throttle — the request is turned away rather than queued, with no extra charge. Compare that to services that bill overage requests silently; this one at least fails loudly and free.

**Geo-targeting has a floor.** Hobby and Startup are limited to US and EU targeting. Country-level targeting elsewhere requires Business ($299) or higher. If your targets sit outside the US and EU, budget for Business from the start — the cheaper tiers won't do the job, and the official docs and reviews agree on this limit.

**Annual plans have their own refill rule.** If you burn through an annual plan's credits before the 12 months are up, your options are re-subscribing on the next billing date for a fresh batch or moving to a higher monthly plan. There's no mid-year credit top-up for annual tiers.

## Free trial, refund policy, and how to test cheaply

ScraperAPI gives you two no-cost ways in. The free plan runs permanently: 1,000 credits a month, up to 5 concurrent connections, no credit card required. On top of that, the first 7 days after signup include 5,000 free requests for larger-scale testing. If you need more trial volume, support can grant additional testing credits on request.

The refund policy is unusually clean: a 7-day, no-questions-asked refund if you're unhappy for any reason — you contact support and they process it. Cancellation is self-serve from the dashboard at any time, with no cancellation fee. Combined with the trial, this means you can validate ScraperAPI against your actual target sites before any money is genuinely at stake, which is exactly how you should evaluate any scraping proxy.

👉 [Start the 7-day trial with 5,000 free credits](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## How ScraperAPI stacks up against raw proxy providers

If you're comparing a proxy for web scraping across the market, the honest picture looks like this. Figures come from a 2026 hands-on comparison of six services plus vendor-published rate cards; residential per-GB prices vary a lot with volume, so treat them as ranges.

| Provider | Model | Entry price point | Free trial | Notable strength |
| --- | --- | --- | --- | --- |
| ScraperAPI | Managed API, per-credit | $49/mo, 100K credits | 5,000 credits / 7 days | Handles proxies, CAPTCHAs, JS rendering in one call |
| Bright Data | Raw proxies + APIs | Residential from $2.50/GB (vendor rate card; one comparison lists $8.40/GB) | $5 credit | Largest pool, 400M+ IPs claimed, enterprise tooling |
| Oxylabs | Raw proxies + APIs | $8/GB in the same comparison; vendor lists from $2.50/GB at volume | 7-day trial | City-level geo-targeting, strong SERP API |
| Smartproxy / Decodo | Raw proxies | $7/GB (comparison) / from $2/GB (vendor) | 3-day trial | Clean dashboard, mid-range |
| IPRoyal | Raw proxies | From $1.75/GB bulk, $7/GB pay-as-you-go | None | Unused bandwidth never expires |
| ThorData | Raw proxies | $3/GB | Trial credits | Cheapest residential in the comparison |
| Webshare | Raw proxies | From $1.40/GB bulk | Free plan (10 proxies, 1GB/mo) | Self-serve free tier |

Reading that table honestly: raw residential proxies are cheaper per unit of data if you're willing to build and maintain the rotation, retry, and unblocking logic yourself. Bright Data and Oxylabs are built for dedicated scraping teams with serious budgets — one comparison called Bright Data outright "overkill for indie developers." ThorData wins on raw GB price for straightforward needs. And per-request managed APIs like ScraperAPI win on time-to-first-data: the same comparison's advice to beginners was to start there precisely because you write less code.

One more structural difference: ScraperAPI doesn't sell individual proxies from its pool at all, and bills nothing by bandwidth. If your project specifically needs a stash of raw IPs to plug into your own infrastructure, this is the wrong product category, full stop.

## When ScraperAPI is the wrong choice

No tool fits everyone, and the cases where ScraperAPI loses are easy to spell out.

- **You need raw IP pools.** Own scraper infrastructure with your own rotation logic? A residential proxy vendor selling per-GB will cost less at scale than per-credit pricing.
- **Your volume is enormous and price-sensitive.** At tens of millions of requests a month, enterprise proxy contracts negotiated per GB routinely beat per-credit rates. ScraperAPI's Enterprise tier exists for this, but the pricing is custom, so there's no published guarantee.
- **Your targets are trivially easy to scrape.** If you're pulling from sites with no anti-bot protection, paying managed-API premiums to bypass defenses you never encounter is waste. Datacenter proxies at $0.50–$2/GB handle those fine.
- **You need credit flexibility on a budget.** Pay-as-you-go starts at Scaling ($475/month). On Hobby or Startup, running dry means pausing or auto-upgrading.

## FAQ

**Is there a free plan?**
Yes. 1,000 API credits per month with up to 5 concurrent connections, free indefinitely, no credit card required. The first 7 days after signup add 5,000 free requests for bigger tests.

**What happens when I run out of credits mid-month?**
Scraping pauses until renewal by default. Depending on your plan, you can enable auto-upgrade (Hobby through Professional), use pay-as-you-go at a fixed per-credit rate with a spending cap (Scaling and above), or ask support for a custom plan. Annual plans can re-subscribe on the next billing date for fresh credits.

**Do I pay extra if I exceed my concurrency limit?**
No. Requests beyond your plan's thread limit return a 429 and are turned away rather than queued, with no charge.

**Can I get a refund?**
Yes — 7 days, no questions asked, handled through support. You can also cancel anytime from the dashboard at no charge.

**How much does scraping Google or Amazon cost?**
Amazon costs 5 credits per request, Google and Bing cost 25 (subdomains included), and LinkedIn costs 30. Sites behind Cloudflare, Datadome, or PerimeterX add 10 credits per bypassed request. Check any URL's exact cost with the Domain Cost Estimator in your dashboard.

**Does annual billing save money?**
Yes, 10% across every tier — Hobby drops to $44.10/month, Startup to $134.10, Business to $269.10, Scaling to $427.50, Professional to $877.50, and Advanced to $1,777.50.

## Before you click buy

Match the plan to your situation rather than to the "most popular" badge. Hobby at $49 is the right call for one or two projects under ~100,000 standard requests a month. If your credits will be spent mostly on Google, Bing, or LinkedIn, multiply your page volume by 25–30 first — you may land on Startup or Business faster than you expect. Need country-level targeting outside the US and EU? That's Business minimum. And if pay-as-you-go headroom matters, Scaling is where it starts.

Last practical step: run two or three of your real target URLs through the Domain Cost Estimator during the free trial, multiply by your monthly volume, and buy the tier that number points to — not the one that sounds impressive.

👉 [Pick your plan and start the free trial on ScraperAPI](https://www.scraperapi.com/pricing/?fp_ref=coupons)
