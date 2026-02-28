# 📖 DNS: The Internet's Phone Book

> *"The Domain Name System is, by far, the largest distributed database on Earth."* — Paul Mockapetris, DNS Inventor

![DNS Domain Name System](../images/Internet/dns-domain-system.jpg)

---

## 📚 Table of Contents
- [What is DNS?](#what-is-dns)
- [Why Do We Need DNS?](#why-do-we-need-dns)
- [How DNS Works](#how-dns-works)
- [DNS Hierarchy](#dns-hierarchy)
- [Types of DNS Servers](#types-of-dns-servers)
- [DNS Records Explained](#dns-records-explained)
- [DNS Resolution Step by Step](#dns-resolution-step-by-step)
- [DNS Caching](#dns-caching)
- [DNS Security](#dns-security)
- [Changing Your DNS Server](#changing-your-dns-server)

---

## 🤔 What is DNS?

**DNS (Domain Name System)** is the system that converts human-readable domain names into IP addresses that computers use.

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS IS A TRANSLATOR                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   😊 What YOU type:                                             │
│   ┌─────────────────────────────────────┐                       │
│   │        www.google.com               │                       │
│   └─────────────────────────────────────┘                       │
│                      │                                           │
│                      │  DNS Translation                         │
│                      ▼                                           │
│   💻 What COMPUTERS use:                                        │
│   ┌─────────────────────────────────────┐                       │
│   │        142.250.195.46               │                       │
│   └─────────────────────────────────────┘                       │
│                                                                  │
│   Think of DNS as the internet's phone book!                    │
│   You look up a name → You get a number                         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Phone Book Analogy

| Phone Book | DNS |
|------------|-----|
| Person's Name | Domain Name (google.com) |
| Phone Number | IP Address (142.250.195.46) |
| Yellow Pages Categories | DNS Record Types |
| Directory Assistance | DNS Server |
| Local Phone Book | DNS Cache |

---

## ❓ Why Do We Need DNS?

### The Problem Without DNS

```
    Imagine having to remember:
    
    ❌ Google:    142.250.195.46
    ❌ Facebook:  157.240.241.35
    ❌ Amazon:    52.94.236.248
    ❌ Netflix:   54.74.73.31
    ❌ Twitter:   104.244.42.193
    
    And these IPs can CHANGE at any time! 😱
```

### The Solution With DNS

```
    Much easier to remember:
    
    ✅ google.com
    ✅ facebook.com
    ✅ amazon.com
    ✅ netflix.com
    ✅ twitter.com
    
    DNS handles the IP lookup automatically! 🎉
```

### Benefits of DNS

| Benefit | Explanation |
|---------|-------------|
| **Human-Friendly** | Names are easier than numbers |
| **Flexibility** | IP can change, domain stays same |
| **Load Balancing** | One domain → multiple IPs |
| **Geographic Routing** | Different IPs for different regions |
| **Redundancy** | Multiple servers, no single failure point |

---

## ⚙️ How DNS Works

### The Big Picture

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS RESOLUTION OVERVIEW                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   👤 You                   🌐 DNS System              🖥️ Website │
│                                                                  │
│   ┌──────┐    "google.com?"    ┌──────────┐                     │
│   │  💻  │ ──────────────────► │   DNS    │                     │
│   │      │                     │  Server  │                     │
│   │      │ ◄────────────────── │          │                     │
│   └──────┘   "142.250.195.46"  └──────────┘                     │
│       │                                                          │
│       │  Now connect to 142.250.195.46                          │
│       │                                                          │
│       └─────────────────────────────────────────► ┌──────────┐  │
│                                                   │  Google  │  │
│                                                   │  Server  │  │
│                                                   └──────────┘  │
│                                                                  │
│   Total time: Usually under 100 milliseconds!                   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### 🎬 Watch: DNS Explained

[![DNS Explained](https://img.youtube.com/vi/72snZctFFtA/maxresdefault.jpg)](https://www.youtube.com/watch?v=72snZctFFtA)

> 🔗 **Video**: [DNS Explained in 100 Seconds](https://www.youtube.com/watch?v=uvr9lhugayu)

---

## 🏛️ DNS Hierarchy

DNS is organized like an upside-down tree!

### The DNS Tree Structure

```
                            ┌───────┐
                            │   .   │  ◄── ROOT (unnamed)
                            │ (root)│
                            └───┬───┘
                                │
        ┌───────────────────────┼───────────────────────┐
        │                       │                       │
        ▼                       ▼                       ▼
    ┌───────┐              ┌────────┐             ┌────────┐
    │ .com  │              │  .org  │             │  .net  │
    │ (TLD) │              │ (TLD)  │             │ (TLD)  │
    └───┬───┘              └────┬───┘             └────┬───┘
        │                       │                      │
    ┌───┴───┐              ┌────┴────┐            ┌────┴────┐
    │       │              │         │            │         │
    ▼       ▼              ▼         ▼            ▼         ▼
 google  facebook      wikipedia   mozilla     cloudflare  nginx
    │                      │
    │                      │
    ▼                      ▼
   www                    www
   mail                   en
   drive                  de
```

### Domain Name Structure

```
    https://www.example.com/page
    └─┬─┘   └┬┘ └──┬───┘└┬┘ └─┬─┘
      │      │     │     │    │
      │      │     │     │    └── Path (handled by web server)
      │      │     │     │
      │      │     │     └── TLD (Top-Level Domain)
      │      │     │
      │      │     └── Second-Level Domain (SLD)
      │      │
      │      └── Subdomain
      │
      └── Protocol (not part of DNS)
    
    
    DNS processes from RIGHT to LEFT:
    . → com → example → www
```

### Types of Top-Level Domains (TLDs)

```
┌─────────────────────────────────────────────────────────────────┐
│                    TYPES OF TLDs                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📋 Generic TLDs (gTLDs):                                       │
│  ┌─────────┬──────────────────────────────────────────────┐     │
│  │ .com    │ Commercial (most popular!)                   │     │
│  │ .org    │ Organizations                                │     │
│  │ .net    │ Network services                             │     │
│  │ .edu    │ Educational institutions (US)                │     │
│  │ .gov    │ US Government                                │     │
│  │ .info   │ Information                                  │     │
│  │ .biz    │ Business                                     │     │
│  └─────────┴──────────────────────────────────────────────┘     │
│                                                                  │
│  🌍 Country Code TLDs (ccTLDs):                                 │
│  ┌─────────┬──────────────────────────────────────────────┐     │
│  │ .us     │ United States                                │     │
│  │ .uk     │ United Kingdom                               │     │
│  │ .in     │ India                                        │     │
│  │ .de     │ Germany                                      │     │
│  │ .jp     │ Japan                                        │     │
│  │ .cn     │ China                                        │     │
│  │ .io     │ British Indian Ocean (popular for tech!)    │     │
│  └─────────┴──────────────────────────────────────────────┘     │
│                                                                  │
│  🆕 New gTLDs (since 2012):                                     │
│  .app, .dev, .cloud, .ai, .tech, .xyz, .online, etc.           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🖥️ Types of DNS Servers

### The Players in DNS

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS SERVER TYPES                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1️⃣ DNS RESOLVER (Recursive Resolver)                          │
│     ┌──────────────────────────────────────────────────────┐    │
│     │ • First point of contact for your device             │    │
│     │ • Does the heavy lifting of querying other servers   │    │
│     │ • Usually run by your ISP or Google/Cloudflare      │    │
│     │ • Caches results for speed                           │    │
│     └──────────────────────────────────────────────────────┘    │
│                                                                  │
│  2️⃣ ROOT NAME SERVERS (13 worldwide)                           │
│     ┌──────────────────────────────────────────────────────┐    │
│     │ • Top of the DNS hierarchy                           │    │
│     │ • Know where to find TLD servers                     │    │
│     │ • Named A through M (a.root-servers.net, etc.)      │    │
│     │ • Actually 1000+ physical servers (anycast)         │    │
│     └──────────────────────────────────────────────────────┘    │
│                                                                  │
│  3️⃣ TLD NAME SERVERS                                           │
│     ┌──────────────────────────────────────────────────────┐    │
│     │ • One for each TLD (.com, .org, .net, etc.)         │    │
│     │ • Know all domains under that TLD                    │    │
│     │ • Managed by registry operators                      │    │
│     └──────────────────────────────────────────────────────┘    │
│                                                                  │
│  4️⃣ AUTHORITATIVE NAME SERVERS                                 │
│     ┌──────────────────────────────────────────────────────┐    │
│     │ • Has the actual DNS records for a domain            │    │
│     │ • The "source of truth"                              │    │
│     │ • Managed by domain owner or hosting provider       │    │
│     └──────────────────────────────────────────────────────┘    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Root Servers Map

```
    13 Root Server Identities (A-M)
    Over 1,500 physical instances worldwide!
    
    ┌────────────────────────────────────────────────────────────┐
    │                                                             │
    │   A - Verisign (US)          H - US Army Research Lab      │
    │   B - USC-ISI (US)           I - Netnod (Sweden)           │
    │   C - Cogent (US)            J - Verisign (US)             │
    │   D - University of Maryland K - RIPE NCC (Netherlands)    │
    │   E - NASA (US)              L - ICANN (US)                │
    │   F - Internet Systems       M - WIDE Project (Japan)      │
    │       Consortium                                            │
    │   G - US DOD                                               │
    │                                                             │
    └────────────────────────────────────────────────────────────┘
```

---

## 📋 DNS Records Explained

DNS records are instructions stored in authoritative DNS servers.

### Common DNS Record Types

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS RECORD TYPES                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📍 A RECORD (Address)                                          │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Maps domain to IPv4 address                              │   │
│  │  example.com → 93.184.216.34                             │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  📍 AAAA RECORD (IPv6 Address)                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Maps domain to IPv6 address                              │   │
│  │  example.com → 2606:2800:220:1:248:1893:25c8:1946        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🔗 CNAME RECORD (Canonical Name / Alias)                       │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Points one domain to another domain                      │   │
│  │  www.example.com → example.com                           │   │
│  │  blog.example.com → myblog.wordpress.com                 │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  📧 MX RECORD (Mail Exchange)                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Directs email to mail servers                            │   │
│  │  example.com → mail.example.com (priority: 10)           │   │
│  │            → backup.example.com (priority: 20)           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  📝 TXT RECORD (Text)                                           │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Stores text information                                  │   │
│  │  Used for: SPF, DKIM, domain verification                │   │
│  │  example.com → "v=spf1 include:_spf.google.com ~all"    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🔑 NS RECORD (Name Server)                                     │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Delegates domain to authoritative name servers          │   │
│  │  example.com → ns1.examplehost.com                       │   │
│  │             → ns2.examplehost.com                        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Quick Reference Table

| Record | Purpose | Example |
|--------|---------|---------|
| **A** | Domain → IPv4 | `google.com → 142.250.195.46` |
| **AAAA** | Domain → IPv6 | `google.com → 2607:f8b0:4004:800::200e` |
| **CNAME** | Alias → Domain | `www → example.com` |
| **MX** | Mail servers | `→ mail.google.com` |
| **TXT** | Text data | SPF, DKIM, verification |
| **NS** | Name servers | `ns1.provider.com` |
| **SOA** | Zone authority | Start of authority info |
| **PTR** | IP → Domain (reverse) | `142.250.195.46 → google.com` |
| **SRV** | Service location | VoIP, game servers |
| **CAA** | Certificate authority | Which CAs can issue certs |

### Real Example: Google's DNS Records

```bash
# Check DNS records yourself:
$ dig google.com A +short
142.250.195.46

$ dig google.com MX +short
10 smtp.google.com.

$ dig google.com NS +short
ns1.google.com.
ns2.google.com.
ns3.google.com.
ns4.google.com.

$ dig google.com TXT +short
"v=spf1 include:_spf.google.com ~all"
```

---

## 🔄 DNS Resolution Step by Step

Let's trace exactly what happens when you visit **www.example.com**:

### The Complete Journey

```
┌─────────────────────────────────────────────────────────────────┐
│            DNS RESOLUTION: www.example.com                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  STEP 1: Check Browser Cache                                    │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Browser: "Did I look this up recently?"                  │   │
│  │  Cache: ❌ Not found (or expired)                        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 2: Check OS Cache (hosts file)                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OS: "Is it in my hosts file or DNS cache?"              │   │
│  │  Cache: ❌ Not found                                     │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 3: Query DNS Resolver (ISP or Public DNS)                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  💻 → 🖥️ Resolver: "What's the IP for www.example.com?" │   │
│  │  Resolver checks its cache...                             │   │
│  │  Cache: ❌ Not found                                     │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 4: Resolver Queries Root Server                           │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Resolver → Root: "Where can I find .com?"               │   │
│  │  Root: "Try the .com TLD servers at 192.5.6.30"         │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 5: Resolver Queries TLD Server                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Resolver → .com TLD: "Where's example.com?"             │   │
│  │  TLD: "Try ns1.example.com at 93.184.216.40"            │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 6: Resolver Queries Authoritative Server                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Resolver → Authoritative: "IP for www.example.com?"     │   │
│  │  Authoritative: "93.184.216.34 (TTL: 3600 seconds)"     │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 7: Resolver Returns Answer                                │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Resolver → 💻: "93.184.216.34"                          │   │
│  │  (Also caches the result for future queries)             │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  STEP 8: Browser Connects to IP                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  💻 → 93.184.216.34: "GET /index.html"                   │   │
│  │  Server: Returns the webpage! 🎉                         │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ⏱️ Total time: ~50-200 milliseconds                           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Visualized Flow

```
        💻                🖥️              🌐            🌐           🖥️
       Your              DNS           Root         TLD        Authoritative
      Device           Resolver       Server       Server        Server
        │                 │              │            │             │
        │  1. Query       │              │            │             │
        │────────────────►│              │            │             │
        │                 │  2. Query    │            │             │
        │                 │─────────────►│            │             │
        │                 │  3. Referral │            │             │
        │                 │◄─────────────│            │             │
        │                 │  4. Query    │            │             │
        │                 │──────────────────────────►│             │
        │                 │  5. Referral │            │             │
        │                 │◄──────────────────────────│             │
        │                 │  6. Query    │            │             │
        │                 │─────────────────────────────────────────►│
        │                 │  7. Answer   │            │             │
        │                 │◄─────────────────────────────────────────│
        │  8. Answer      │              │            │             │
        │◄────────────────│              │            │             │
        │                 │              │            │             │
```

---

## 💾 DNS Caching

Caching makes DNS much faster by storing previous lookups.

### Cache Levels

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS CACHE LAYERS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Level 1: BROWSER CACHE                                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Fastest lookup                                         │   │
│  │  • Chrome: chrome://net-internals/#dns                   │   │
│  │  • Usually caches for a few minutes                       │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          ↓                                       │
│  Level 2: OS CACHE                                              │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Shared by all applications                             │   │
│  │  • Windows: ipconfig /displaydns                         │   │
│  │  • Mac/Linux: varies by OS                               │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          ↓                                       │
│  Level 3: ROUTER CACHE                                          │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Shared by all devices on network                       │   │
│  │  • Usually a few hours                                    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          ↓                                       │
│  Level 4: ISP/RESOLVER CACHE                                    │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Shared by many users                                   │   │
│  │  • Can cache for hours to days                           │   │
│  │  • Based on TTL (Time To Live)                           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### TTL (Time To Live)

```
    TTL tells caches how long to remember an answer.
    
    High TTL (86400 = 24 hours):
    ✅ Faster lookups (more cache hits)
    ✅ Less load on DNS servers
    ❌ Slow to update if IP changes
    
    Low TTL (60 = 1 minute):
    ✅ Quick updates when IP changes
    ✅ Better for load balancing
    ❌ More DNS lookups
    ❌ Slightly slower for users
```

### Clear DNS Cache

```bash
# Windows
ipconfig /flushdns

# macOS
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder

# Linux (systemd)
sudo systemd-resolve --flush-caches

# Chrome browser
# Visit: chrome://net-internals/#dns
# Click "Clear host cache"
```

---

## 🔒 DNS Security

DNS was designed in 1983 without security in mind. Here are modern protections:

### DNS Threats

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS SECURITY THREATS                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🦠 DNS SPOOFING / CACHE POISONING                              │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Attacker injects fake DNS records into cache             │   │
│  │  You think you're at bank.com, but you're at evil.com    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  👀 DNS SNOOPING                                                │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Your DNS queries are visible to ISP, network admins     │   │
│  │  They can see every website you visit!                   │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🔒 DNS HIJACKING                                               │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Malware changes your DNS settings                        │   │
│  │  All queries go to attacker's server                      │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  💥 DDoS ON DNS                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Overwhelm DNS servers with requests                      │   │
│  │  2016 Dyn attack took down Twitter, Netflix, etc.        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### DNS Security Solutions

```
┌─────────────────────────────────────────────────────────────────┐
│                    DNS SECURITY SOLUTIONS                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🔐 DNSSEC (DNS Security Extensions)                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Adds digital signatures to DNS records                 │   │
│  │  • Proves records haven't been tampered with              │   │
│  │  • Doesn't encrypt, just authenticates                    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🔒 DoH (DNS over HTTPS)                                        │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Encrypts DNS queries using HTTPS                       │   │
│  │  • ISP can't see your DNS queries                         │   │
│  │  • Used by Firefox, Chrome, etc.                          │   │
│  │  • Providers: Cloudflare, Google, NextDNS               │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🔒 DoT (DNS over TLS)                                          │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Encrypts DNS using TLS                                 │   │
│  │  • Dedicated port (853)                                   │   │
│  │  • Easier to block than DoH                               │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ Changing Your DNS Server

### Why Change DNS?

| Reason | Benefit |
|--------|---------|
| **Speed** | Public DNS may be faster than ISP |
| **Privacy** | Some DNS providers don't log queries |
| **Security** | Better malware/phishing blocking |
| **Reliability** | Major providers have better uptime |
| **Bypass Censorship** | Avoid ISP-level blocking |

### Popular Public DNS Servers

```
┌─────────────────────────────────────────────────────────────────┐
│                    PUBLIC DNS SERVERS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ☁️ CLOUDFLARE (Privacy-focused)                                │
│     Primary:   1.1.1.1                                          │
│     Secondary: 1.0.0.1                                          │
│     DoH: https://cloudflare-dns.com/dns-query                   │
│                                                                  │
│  🔍 GOOGLE (Reliable, fast)                                     │
│     Primary:   8.8.8.8                                          │
│     Secondary: 8.8.4.4                                          │
│     DoH: https://dns.google/dns-query                           │
│                                                                  │
│  🔒 QUAD9 (Security-focused)                                    │
│     Primary:   9.9.9.9                                          │
│     Secondary: 149.112.112.112                                  │
│     Blocks malicious domains                                    │
│                                                                  │
│  🛡️ OPENDNS (Cisco - Filtering options)                        │
│     Primary:   208.67.222.222                                   │
│     Secondary: 208.67.220.220                                   │
│     Family Shield: 208.67.222.123                               │
│                                                                  │
│  🔐 NEXTDNS (Customizable)                                      │
│     Custom per-account addresses                                │
│     Highly configurable blocking                                │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### How to Change DNS

**Windows:**
```
1. Control Panel → Network and Internet → Network Connections
2. Right-click your connection → Properties
3. Select "Internet Protocol Version 4 (TCP/IPv4)"
4. Properties → "Use the following DNS server addresses"
5. Enter: 1.1.1.1 and 1.0.0.1
```

**Mac:**
```
1. System Preferences → Network
2. Select your connection → Advanced
3. DNS tab → Add with "+"
4. Enter: 1.1.1.1 and 1.0.0.1
```

**Linux:**
```bash
# Edit /etc/resolv.conf
sudo nano /etc/resolv.conf

# Add:
nameserver 1.1.1.1
nameserver 1.0.0.1
```

**Router (affects all devices):**
```
1. Access router admin (usually 192.168.1.1)
2. Find DNS settings (often under DHCP or Internet)
3. Change DNS servers
4. Save and reboot router
```

---

## 🧪 Hands-On Exercises

### Exercise 1: Look Up DNS Records

```bash
# Using dig (Linux/Mac)
dig google.com A
dig google.com MX
dig google.com NS

# Using nslookup (Windows/all)
nslookup google.com
nslookup -type=MX google.com
nslookup -type=NS google.com

# Online tools
# Visit: https://toolbox.googleapps.com/apps/dig/
```

### Exercise 2: Trace DNS Resolution

```bash
# See the full resolution path
dig +trace google.com
```

### Exercise 3: Check Your DNS Server

```bash
# Windows
nslookup google.com

# Look at the "Server" line - that's your DNS resolver!
```

### Exercise 4: Measure DNS Speed

```bash
# Time a DNS lookup
time nslookup google.com

# Compare different DNS servers
time nslookup google.com 1.1.1.1
time nslookup google.com 8.8.8.8
```

---

## 📖 Key Takeaways

```
┌──────────────────────────────────────────────────────────────┐
│                    KEY TAKEAWAYS                              │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  ✅ DNS converts domain names to IP addresses               │
│                                                               │
│  ✅ DNS is hierarchical: Root → TLD → Authoritative         │
│                                                               │
│  ✅ Multiple DNS record types exist (A, AAAA, CNAME, MX...) │
│                                                               │
│  ✅ Caching at multiple levels makes DNS fast               │
│                                                               │
│  ✅ DNSSEC adds authentication; DoH/DoT add encryption      │
│                                                               │
│  ✅ Public DNS servers can improve speed and privacy        │
│                                                               │
│  ✅ DNS resolution typically takes <100ms                   │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## 🔗 Additional Resources

### 📹 Videos
- [DNS Explained - PowerCert](https://www.youtube.com/watch?v=mpQZVYPuDGU)
- [How DNS Works - Computerphile](https://www.youtube.com/watch?v=uOfonONtIuk)
- [DNS Records Explained - ByteByteGo](https://www.youtube.com/watch?v=HnUDtycXSNE)

### 📚 Interactive
- [How DNS Works - Comic](https://howdns.works/)
- [DNS Checker](https://dnschecker.org/)
- [Google Admin Toolbox Dig](https://toolbox.googleapps.com/apps/dig/)

### 🛠️ Tools
- [MXToolbox](https://mxtoolbox.com/)
- [DNS Propagation Checker](https://www.whatsmydns.net/)
- [DNS Benchmark (Windows)](https://www.grc.com/dns/benchmark.htm)

---

## ⏭️ What's Next?

Now that you understand DNS, let's explore:

**[➡️ 04 - HTTP/HTTPS: The Language of the Web](./04-http-https-protocols.md)**

We'll learn:
- How web pages are requested and delivered
- HTTP methods (GET, POST, PUT, DELETE)
- How HTTPS keeps your data secure
- SSL/TLS certificates

---

<div align="center">

**🎓 Elite Ball Knowledge - Internet Fundamentals**

[← Previous: IP Addresses](./02-ip-addresses.md) | [Home](./README.md) | [Next: HTTP/HTTPS →](./04-http-https-protocols.md)

</div>
