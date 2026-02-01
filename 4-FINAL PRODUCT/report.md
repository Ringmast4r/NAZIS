# Gravatar Hash Recovery Report

## Summary

| Metric | Value |
|--------|-------|
| Target sites scanned | 627 |
| WordPress confirmed | 213 |
| Not WordPress | 414 |
| Gravatar hashes collected | 1,997 |
| Emails recovered | 378 |
| Uncracked hashes | 1,619 |
| Domains with hashes | 69 |
| Domains with cracked emails | 17 |

---

## Stage 1: Site Scanning

627 known neo-Nazi, white supremacist, and hate group websites were checked for WordPress. 213 (34%) were confirmed running WordPress and passed to Stage 2.

## Stage 2: Hash Collection

1,997 Gravatar email hashes were extracted from 69 domains using REST API, sitemap parsing, author page scraping, and deep page scraping.

## Stage 3: Hash Cracking

378 email addresses were recovered from 17 domains using pattern-based cracking against the collected hashes. 1,619 hashes remain uncracked.

### Cracked by Domain

| Domain | Emails Recovered | Description |
|--------|-----------------|-------------|
| amren.com | 257 | American Renaissance - white supremacist publication |
| altright.com | 64 | Alt-right movement hub |
| veteranstoday.com | 25 | Conspiracy / antisemitic content |
| attackthesystem.com | 8 | National-anarchist / far-right |
| faithandheritage.com | 4 | Christian Identity / white nationalist |
| therightstuff.biz | 4 | Neo-Nazi podcast network (TDS) |
| eurofolkradio.com | 3 | White supremacist radio |
| karpatskasich.com | 2 | Ukrainian far-right |
| svoboda.org.ua | 2 | Svoboda party (Ukrainian nationalist) |
| americannaziparty.com | 1 | American Nazi Party |
| bloccostudentesco.org | 1 | Italian far-right student bloc |
| bnp.org.uk | 1 | British National Party |
| codoh.com | 1 | Committee for Open Debate on the Holocaust (denial) |
| forbritain.uk | 1 | For Britain (anti-Islam party) |
| fpp.co.uk | 1 | David Irving (Holocaust denier) |
| nipponkaigi.org | 1 | Nippon Kaigi (Japanese ultranationalist) |
| proudboysusa.com | 1 | Proud Boys |

---

## Methodology

1. **Target identification** - Compiled list of 627 known extremist websites
2. **WordPress detection** - Identified 213 WordPress sites via REST API probing and signature detection
3. **Hash collection** - Extracted 1,997 Gravatar hashes via REST API, sitemaps, author pages, and deep scraping
4. **Pattern-based cracking** - Recovered 378 emails using contextual pattern generation

All data obtained from publicly accessible sources. No authentication bypassed.
