# NAZIS

![NAZIS](inglorious%20basterds.PNG)

**Exposing white supremacists through Gravatar email hash recovery.**

Gravatar publicly exposes unsalted MD5/SHA256 hashes of user email addresses on every WordPress site. This project uses a three-stage OSINT pipeline to recover the real email addresses of contributors, authors, and commenters on known neo-Nazi and white supremacist websites.

---

## The Gravatar Problem

Every WordPress site leaks Gravatar hashes through its REST API (`/wp-json/wp/v2/users`). These hashes are derived from email addresses with no salt, no key stretching, and no rate limiting. Anyone with an account on a WordPress site has their email hash publicly visible.

```
email: john.smith@gmail.com
  MD5: 271b8427864f0c82acf2a7fde5c6e8e6
SHA256: 8e4d25e0587baa8edeba3bce2fd93d83e3d5e21f8...

These hashes are PUBLIC on every WordPress site the user has an account on.
```

This project exploits that design flaw specifically against hate sites to identify the people behind anonymous accounts.

---

## Pipeline

```
 [1] WP Determiner          [2] Hash Hunter            [3] Hash Cracker
 ==================         ===============            ================
 Input: hate site list      Input: WP sites            Input: hash database
 Check for WordPress   -->  Extract Gravatar      -->  Pattern-based email
 Output: confirmed WP       hashes via REST API        recovery
                            + sitemaps + scraping
                            Output: hashes.db          Output: cracked.db

 627 sites checked          1,997 hashes collected     377 emails recovered
 213 confirmed WP           69 domains with data       17 domains cracked
```

---

## Stage 1: WordPress Determiner

Identifies which target sites run WordPress by checking for known WordPress signatures (REST API endpoints, `wp-content` paths, meta tags, etc.).

### Usage
```
wp-determiner.exe
```

| Feature | Description |
|---------|-------------|
| Bulk scan | Load a list of domains from file |
| Single scan | Check one domain |
| Recheck | Re-check previously scanned sites |
| Database | SQLite storage with scan history |
| Detection methods | REST API probe, HTML signatures, header analysis |

### Target Lists

Lists of known extremist websites organized by category are in `lists/`:

- `Nazis.txt` - Neo-Nazi, white supremacist, and hate group websites
- Additional lists for cross-referencing

---

## Stage 2: Hash Hunter

Aggressively collects Gravatar email hashes from confirmed WordPress sites using four methods:

1. **REST API** - Full pagination of `/wp-json/wp/v2/users` with retry logic
2. **Sitemap parsing** - `/sitemap.xml`, `/wp-sitemap-users-1.xml`
3. **Author page scraping** - `/author/`, `/team/`, `/about/`, `/staff/` pages
4. **Deep scraping** - Comment sections, internal pages, RSS feeds

### Usage
```
hash-hunter.exe
```

| Key | Command | Description |
|-----|---------|-------------|
| 1 | Scan | Single target scan |
| 2 | Bulk | Bulk scan from target file |
| 3 | Rescan | Retry incomplete sites |
| 4 | Stats | Database statistics |
| 5 | Export | Export hashes to CSV |

### Database

Stores results in `hashes.db`:

| Table | Purpose |
|-------|---------|
| `domains` | Scanned sites with completion status |
| `hashes` | Collected Gravatar hashes with metadata |
| `hash_history` | Change tracking |

Each hash record includes: domain, user ID, username, display name, hash, hash type (MD5/SHA256), avatar URL, source method, and timestamps.

---

## Stage 3: Hash Cracker

Pattern-based email recovery tool. Unlike traditional wordlist crackers (Hashcat, John the Ripper), this generates candidate emails dynamically from metadata already collected by Hash Hunter.

### Why Pattern-Based?

| | Traditional (Hashcat) | Hash Cracker |
|---|---|---|
| Input | Massive wordlists (GB+) | Username + display name + domain |
| Approach | Brute force | Contextual pattern generation |
| Email-aware | No | Yes - 772+ email providers |
| Name-aware | No | Yes - cultural patterns, nicknames, corporate formats |

### Pattern Categories

- **Username match** (54% of cracks) - `username@sitedomain.com`
- **Corporate patterns** - `first.last@`, `flast@`, `firstl@`
- **Scandinavian short codes** - `first2+last2` format
- **International patterns** - Hispanic, Asian, German, Celtic naming conventions
- **Nickname/diminutive** - william -> bill, robert -> bob, etc.
- **Numeric suffixes** - birth years, common sequences

### Usage
```
hashcracker.exe
```

| Key | Command | Description |
|-----|---------|-------------|
| 1 | Load DB | Import hashes from Hash Hunter |
| 2 | Wordlist | Load additional patterns |
| 3 | Crack | Start cracking |
| 4 | View | View cracked results |
| 5 | Export | Export to CSV |

---

## Results

### Current Statistics

| Metric | Count |
|--------|-------|
| Sites checked | 627 |
| WordPress confirmed | 213 |
| Gravatar hashes collected | 1,997 |
| Emails recovered | 377 |
| Domains with cracked emails | 17 |

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
| americannaziparty.com | 1 | American Nazi Party |
| bnp.org.uk | 1 | British National Party |
| codoh.com | 1 | Holocaust denial |
| proudboysusa.com | 1 | Proud Boys |
| Others | 8 | Various extremist sites |

---

## Building from Source

All tools are written in Go.

### Prerequisites
- Go 1.21+

### Build
```bash
# Stage 1
cd "1 - Wordpress Determiner Nazis"
go build -o wp-determiner.exe .

# Stage 2
cd "2 - Hash Hunter Nazis"
go build -o hash-hunter.exe main.go

# Stage 3
cd "3 - Hash Cracker Master"
go build -o hashcracker.exe main.go
```

---

## Database Viewers

Each stage includes a `db-viewer.html` file that can be opened in any browser to inspect the SQLite database contents locally. No server required.

---

## How Gravatar Hashes Work

```
1. User signs up on wordpress-site.com with email "name@gmail.com"
2. WordPress computes: MD5("name@gmail.com") = abc123...
3. WordPress REST API exposes this hash publicly at:
   GET /wp-json/wp/v2/users → avatar_urls → gravatar hash
4. Anyone can see the hash. No authentication required.
5. Hash Cracker reverses it: abc123... → name@gmail.com
```

Gravatar hashes are unsalted and use fast algorithms (MD5/SHA256). Combined with the fact that email addresses follow predictable patterns, recovery rates are high when you have metadata like usernames and display names.

---

## Legal & Ethics

**What this accesses:** Only publicly available data. WordPress REST APIs are public by default. Gravatar hashes are exposed by design. No authentication is bypassed. No private systems are accessed. No vulnerabilities are exploited.

**Why this matters:** Anonymous participation on hate sites enables radicalization without accountability. Gravatar's design decision to use unsalted hashes of email addresses creates a deanonymization vector that applies to every WordPress site on the internet. This project demonstrates that vulnerability against sites that promote hate.

**Responsible use:** This toolkit is designed for OSINT research, journalism, and counter-extremism work. The email recovery techniques documented here apply to ALL WordPress sites, not just hate sites. If you run a WordPress site, consider disabling Gravatar or the REST API user endpoint to protect your users.

---

## Protecting Yourself

If you run a WordPress site and want to protect your users:

```php
// Disable REST API user enumeration
add_filter('rest_endpoints', function($endpoints) {
    unset($endpoints['/wp/v2/users']);
    return $endpoints;
});

// Or disable Gravatar entirely
add_filter('option_show_avatars', '__return_false');
```

---

## Author

**Ringmast4r**

## License

MIT
