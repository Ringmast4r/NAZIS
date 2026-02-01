# Gravatar Hash Recovery Report

## Summary

| Metric | Value |
|--------|-------|
| Target sites scanned | 627 |
| WordPress confirmed | 213 |
| Not WordPress | 414 |
| Gravatar hashes collected | 1,997 |
| **Emails recovered** | **378** |
| **Uncracked hashes** | **1,619** |
| Domains with hashes | 69 |
| Domains with cracked emails | 17 |

---

## Stage 1: Site Scanning

627 known neo-Nazi, white supremacist, and hate group websites were checked for WordPress. 213 (34%) were confirmed running WordPress and passed to Stage 2.

## Stage 2: Hash Collection

1,997 Gravatar email hashes were extracted from 69 domains using REST API, sitemap parsing, author page scraping, and deep page scraping.

## Stage 3: Hash Cracking

378 email addresses were recovered from 17 domains using pattern-based cracking against the collected hashes. 1,619 hashes remain uncracked across 68 domains.

---

## Cracked Emails by Domain

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
| codoh.com | 1 | Holocaust denial |
| forbritain.uk | 1 | For Britain (anti-Islam party) |
| fpp.co.uk | 1 | David Irving (Holocaust denier) |
| nipponkaigi.org | 1 | Nippon Kaigi (Japanese ultranationalist) |
| proudboysusa.com | 1 | Proud Boys |

---

## Uncracked Hashes by Domain

1,619 hashes remain uncracked. These users have Gravatar hashes publicly exposed but their email addresses have not yet been recovered.

| Domain | Uncracked | Description |
|--------|-----------|-------------|
| theoccidentalobserver.net | 336 | Occidental Observer - antisemitic publication |
| amren.com | 267 | American Renaissance |
| renegadetribune.com | 185 | Renegade Tribune - neo-Nazi media |
| arktos.com | 107 | Arktos Media - far-right publishing house |
| therightstuff.biz | 104 | The Right Stuff - neo-Nazi podcast network |
| freewestmedia.com | 59 | Free West Media - far-right news |
| nationalvanguard.org | 58 | National Vanguard - neo-Nazi organization |
| occidentaldissent.com | 45 | Occidental Dissent - white nationalist blog |
| frihetskamp.net | 45 | Nordic far-right |
| veteranstoday.com | 44 | Veterans Today |
| compact-online.de | 44 | COMPACT Magazine - German far-right |
| whiterabbitradio.net | 36 | White genocide conspiracy media |
| altright.com | 32 | Alt-right hub |
| faithandheritage.com | 31 | Christian Identity / white nationalist |
| vnnforum.com | 26 | Vanguard News Network - neo-Nazi forum |
| attackthesystem.com | 21 | National-anarchist / far-right |
| azov.org.ua | 20 | Azov movement (Ukrainian far-right) |
| white-history.com | 15 | White supremacist revisionism |
| eurofolkradio.com | 14 | White supremacist radio |
| bnp.org.uk | 13 | British National Party |
| jewworldorder.org | 10 | Antisemitic conspiracy site |
| davidduke.com | 7 | David Duke - former KKK Grand Wizard |
| frankspeech.com | 7 | Mike Lindell - far-right media |
| americanfreepress.net | 6 | American Free Press - antisemitic newspaper |
| americannaziparty.com | 5 | American Nazi Party |
| nipponkaigi.org | 5 | Nippon Kaigi (Japanese ultranationalist) |
| onr.com.pl | 5 | National Radical Camp (Polish far-right) |
| falange.es | 4 | Falange (Spanish fascist party) |
| nordfront.dk | 4 | Nordic Resistance Movement (Denmark) |
| codoh.com | 3 | Holocaust denial |
| heritageanddestiny.com | 3 | British far-right magazine |
| dieheimat.de | 3 | Die Heimat (German far-right) |
| awb.co.za | 3 | Afrikaner Weerstandsbeweging (South African neo-Nazi) |
| castaliapub.com | 3 | Castalia House - far-right publishing |
| imperiumpress.org | 3 | Far-right publishing |
| Others (33 domains) | 38 | Various extremist sites with 1-2 uncracked each |

---

## Methodology

1. **Target identification** - Compiled list of 627 known extremist websites
2. **WordPress detection** - Identified 213 WordPress sites via REST API probing and signature detection
3. **Hash collection** - Extracted 1,997 Gravatar hashes via REST API, sitemaps, author pages, and deep scraping
4. **Pattern-based cracking** - Recovered 378 emails using contextual pattern generation

All data obtained from publicly accessible sources. No authentication bypassed.

---

## Viewing the Data

Open `viewer.html` in any browser to interactively browse all data across four tabs:

1. **Sites** - All 627 scanned domains with WordPress status
2. **Hashes** - All 1,997 collected hashes with cracked/uncracked status
3. **Cracked** - 378 recovered email addresses
4. **Uncracked** - 1,619 remaining hashes awaiting cracking

Each tab supports search, domain filtering, column sorting, and CSV export.
