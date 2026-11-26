# Los Angeles Residential Proxy Pricing: What Per-GB Pools Cost, When a $25/Month LA Residential-IP VPS Wins, and Whether You Need ZIP or ASN Targeting

Oxylabs publishes **from $8/GB** for Los Angeles residential traffic. SixtyNet, a VPS host with a single Los Angeles data center, rents a server carrying a residential IP **from $25/month** with 5 TB of transfer included, which works out to roughly $0.005 per gigabyte if that allowance gets used.

The two figures describe different products. One is metered access to a rotating pool with city, ZIP and ASN targeting. The other is a fixed Los Angeles residential address on a machine you administer. Which one you want comes down to request volume, how many distinct LA locations you need to appear from, and what happens when a target site blocks you.

Below: what SixtyNet's LA residential plans actually are, the per-gigabyte math at realistic volumes, what the closed ports mean for a do-it-yourself proxy, and where the metered providers sit for comparison.

> **Quick pick.** For scraping, account work or ad checks that need a stable Los Angeles residential IP and run past a few hundred gigabytes a month, SixtyNet's **Residential-STARTER** (2 vCPU, 2 GB RAM, 40 GB NVMe, 5 TB traffic, **$25/month**) is the cheapest verified entry point in this article. Ports 80 and 443 stay closed on it, so treat it as an outbound endpoint rather than a web host.
>
> 👉 [See SixtyNet's current LA residential-IP plans and monthly prices](https://sixtynet.net/aff.php?aff=39)

## What SixtyNet actually sells in Los Angeles

Los Angeles is the company's only location, and the catalogue splits into two lines. The residential line is four monthly VPS tiers. The LAX line is four annual DDoS-protected servers without residential IPs, meant for people who need open ports and public hosting.

One detail worth checking before you buy: the order links for the residential tiers are filed under a store path named `at-and-t-mobility-residential`, which points to AT&T Mobility carrier addresses rather than home fiber. Mobile and fixed-line residential IPs get treated differently by some targets, so if carrier type matters to your project, ask before paying.

| Plan | vCPU / RAM / NVMe | Network / traffic | Price | Billing | Order |
| --- | --- | --- | --- | --- | --- |
| Residential-STARTER | 2 / 2 GB / 40 GB | 2G port / 5 TB | **$25.00/mo** | Monthly | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| Residential-MICRO | 4 / 4 GB / 80 GB | 4G port / 10 TB | $45.00/mo | Monthly | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| Residential-MEDIUM | 8 / 8 GB / 160 GB | 10G port / 20 TB | $85.00/mo | Monthly | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| Residential-LARGE | 16 / 16 GB / 320 GB | 10G port / 40 TB | $165.00/mo | Monthly | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| LAX-STARTER (no residential IP) | 2 / 2 GB / 40 GB | 2G port / 5 TB | $200.00/yr (list $240) | Annual | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| LAX-MICRO (no residential IP) | 4 / 4 GB / 80 GB | 4G port / 10 TB | $400.00/yr (list $480) | Annual | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| LAX-MEDIUM (no residential IP) | 8 / 8 GB / 160 GB | 10G port / 20 TB | $800.00/yr (list $960) | Annual | [ View plan](https://sixtynet.net/aff.php?aff=39) |
| LAX-LARGE (no residential IP) | 8 / 16 GB / 320 GB | 10G port / 40 TB | $1,600.00/yr (list $1,920) | Annual | [ View plan](https://sixtynet.net/aff.php?aff=39) |

Every residential tier carries the same line in its spec sheet: ports 80 and 443 are closed "due to IP risk control reasons." The LAX plans keep the ports open and add DDoS protection, but the IP is a datacenter address. The cart also listed **0 available** across all four residential tiers at the time of checking, so availability is worth confirming before you put a deadline against it.

SixtyNet also lists a China Unicom Premium line on its VPS hosting page with AS9929 routing and residential IPs, quoted at $2,500/year for the 2-core tier. That route exists for latency into mainland China; if your targets are in Los Angeles, the standard residential tiers are the ones that matter.

## Do the per-gigabyte math before you pick a tier

Unit cost barely moves as you go up the residential line. STARTER is $5.00 per TB of included traffic, MICRO $4.50, MEDIUM $4.25, LARGE $4.13. Moving from the $25 tier to the $165 tier buys eight times the traffic for about 18% less per terabyte. What it does not buy is a second IP. Each VPS is one address.

That changes how you scale. Four STARTER instances cost $100 and give 20 TB of traffic across four separate Los Angeles addresses. One MEDIUM costs $85 and gives the same 20 TB through a single address. If blocking is your problem, the extra $15 buys three more exit IPs, which is usually worth more than the CPU upgrade. If throughput through one IP is your problem, the bigger tier is the right buy.

Now put those numbers against metered pricing at a realistic monthly volume. Say 500 GB:

- At Oxylabs' $8/GB headline, 500 GB costs **$4,000**.
- At Rayobyte's self-serve band of $0.70 to $3.50/GB, it costs **$350 to $1,750**. That page is dated December 2022, so treat it as an indicator of how wide the band runs, not as today's quote.
- Inside a $25 STARTER, it costs nothing extra. The 5 TB allowance covers it ten times over.

The metered price pays for rotation, targeting and someone else absorbing the block rate on hard targets. The VPS price pays for bandwidth and one address. Both are fair prices for different things, which is why comparing the two per gigabyte produces silly conclusions in either direction.

👉 [Check the $25/month Residential-STARTER specification](https://sixtynet.net/aff.php?aff=39)

## What the closed ports change

Ports 80 and 443 being shut rules out two things. You cannot host a public-facing site on the machine, and you cannot run a proxy listener on 443, which is the port most clients and corporate networks assume. Your proxy daemon has to sit on a non-standard port, and you should test from the actual network your team connects from, because some workplaces only allow outbound traffic on 443.

Outbound requests from the box are unaffected. Scrapers, browser automation and API calls leave the machine on the IP that SixtyNet assigned, and that is the part that matters for data collection.

If you need a server you can point a browser at over HTTPS, or you want to host anything public, the LAX line is the version with open ports. The trade is that you lose the residential IP, which defeats the purpose if looking residential is the whole requirement.

## City, ZIP or ASN: which targeting you are paying for

Country and city targeting is table stakes. Every provider in this space offers Los Angeles. The differentiation sits one level down, at ZIP code and ASN.

Rayobyte states that ZIP code and ASN targeting are available at no extra cost on Premium Residential. Decodo lists continent, country, state, city, ZIP code and ASN targeting as part of every residential plan. A fixed VPS gives you exactly one point in the LA metro, and no way to move it.

ZIP-level targeting earns its price when the answer genuinely changes by neighborhood:

- **Local pack and Maps positions.** Rankings for "personal injury lawyer" in Beverly Hills and in Long Beach are different results pages.
- **California tax and shipping quotes.** Sales tax rates, shipping zones and delivery estimates vary by ZIP within LA County.
- **In-store availability.** Whether a specific Target or Best Buy has an item on the shelf is a store-level question.
- **Delivery ETAs and surge fees.** DoorDash and Uber Eats pricing differs across neighborhoods at the same moment.

It is wasted money when the target doesn't vary at that granularity. Netflix, Hulu, Disney+ and Max libraries are licensed by market, not by ZIP. A single storefront's price page returns the same number whether your IP resolves to Hollywood or Santa Monica. Most ad verification work needs an impression from Los Angeles, not from 90028 specifically.

One caution on ZIP targeting in general: IP-to-ZIP geolocation is approximate. Treat a ZIP-targeted request as sampling a neighborhood, not as proof of what a specific household sees.

ASN targeting matters only if you need to look like a particular carrier type, for example cable versus fiber versus mobile. It is a niche requirement and worth paying for only when a target treats carrier classes differently.

## What people do with a Los Angeles residential IP, and whether rotation earns its cost

The workload decides the product. These six come up most often:

1. **Streaming catalog comparison.** Netflix, Hulu, Disney+, Max libraries as LA viewers see them. Dozens of requests per service, not millions. One fixed LA IP handles it.
2. **California price and stock checks.** Amazon, Target, Best Buy and DTC brands, checked across a handful of ZIPs for tax, shipping and promotions. A pool with ZIP targeting is the right tool once you go past a few locations.
3. **Local SEO and SERP tracking.** Google local pack, Maps listings and organic rankings as seen from LA. Low volume per query, high location count, which is exactly the shape a rotating pool serves.
4. **Ad verification.** Confirming that geo-targeted display, video and social campaigns serve correctly across Meta, YouTube, TikTok and publisher networks. This one needs volume and multiple IPs; a single address gets rate-limited or remembered fast.
5. **Real estate data.** Listings, rents and trends from Zillow, Redfin, Realtor.com and Apartments.com across LA and Orange County submarkets. Page counts run high against a small set of domains, so expect blocks either way.
6. **Food delivery monitoring.** Menus, surge pricing and ETAs on DoorDash, Uber Eats, Postmates and Grubhub. Location-specific, changes hourly, and the request volume is repetitive.

Items 1 and 2 at small scale fit comfortably on a $25 VPS with your own rate limiting. Items 3, 4 and 6 are where per-GB billing starts to look reasonable, because the alternative is managing dozens of individual addresses yourself.

👉 [Compare all four LA residential tiers](https://sixtynet.net/aff.php?aff=39)

## Where the per-GB providers sit

If rotation and targeting are requirements, these are the names that come up, with the figures their own pages publish.

| Provider | Verified LA figure | Billing model | Notable terms |
| --- | --- | --- | --- |
| Oxylabs | from $8/GB residential; 99.2% average residential success rate; datacenter uptime up to 99.9% | Per GB | Free replacement of malfunctioning proxies; HTTP(S), SOCKS5, ISP proxies |
| Rayobyte | from $0.50/GB via sales; $0.70–$3.50/GB self-serve (page dated December 2022) | Per GB; static IPs per IP/month | ZIP and ASN targeting at no extra cost; sticky sessions up to 120 minutes; free trial on self-serve, no credit card |
| Decodo | 7,940 residential IPs in Los Angeles; 99.92% success rate; under 0.5s average response | Per GB | City, ZIP and ASN targeting; rotating and sticky sessions; 14-day money-back with terms |
| Shifter | 266K+ LA IPs sourced from Spectrum, AT&T Fiber, Frontier FiOS, Cox and major mobile carriers | Per GB | City-level targeting set directly in credentials |

Entry prices across this group disagree by a factor of sixteen, and third-party comparison charts make it worse. One vendor's own chart prices a competitor at $2.50/GB while that competitor's page advertises from $8/GB. Neither number is a lie; "from" prices assume committed volume, and quota, targeting and target difficulty all move the effective rate. Ask for a quote at your actual monthly gigabytes before you build a budget on a headline.

What none of them sell is a single fixed Los Angeles residential address for $25 a month, which is the gap SixtyNet fills.

## Before you order

Four things to confirm, in this order:

1. **Stock.** The residential tiers showed 0 available when checked. Ask when the next allocation lands if you have a launch date.
2. **Carrier type.** The AT&T Mobility store path suggests mobile addresses. Confirm if your targets distinguish mobile from fixed-line residential.
3. **Refund window.** The residential product pages do not state one. Get it in writing before paying, since hosting refund policies range widely.
4. **Ports.** If anything inbound on 80 or 443 is part of the plan, the residential tiers are the wrong line.

## The decision rule

A few thousand requests a month from one LA vantage point, or a scraping stack you already run yourself: take Residential-STARTER at $25 and put the savings into more instances when you need more IPs. Tens of thousands of requests spread across dozens of ZIPs, or a target that blocks aggressively: you need a metered pool with rotation, and SixtyNet is not that product.

The middle case is the common one. Start with one STARTER, log how often you get blocked over two weeks, and only move to per-gigabyte billing when blocks rather than bandwidth are what costs you money.

👉 [Start with SixtyNet's $25/month LA residential-IP plan](https://sixtynet.net/aff.php?aff=39)
