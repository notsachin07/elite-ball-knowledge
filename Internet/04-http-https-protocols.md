# 🌐 HTTP & HTTPS: The Language of the Web

> *"HTTP is the foundation of any data exchange on the Web, and it is a client-server protocol."* — MDN Web Docs

![HTTP HTTPS Protocols](../images/Internet/http-https-protocols.jpg)

---

## 📚 Table of Contents
- [What is HTTP?](#what-is-http)
- [How HTTP Works](#how-http-works)
- [HTTP Request Methods](#http-request-methods)
- [HTTP Status Codes](#http-status-codes)
- [HTTP Headers](#http-headers)
- [What is HTTPS?](#what-is-https)
- [SSL/TLS Explained](#ssltls-explained)
- [The HTTPS Handshake](#the-https-handshake)
- [HTTP/1.1 vs HTTP/2 vs HTTP/3](#http11-vs-http2-vs-http3)
- [Cookies and Sessions](#cookies-and-sessions)

---

## 🤔 What is HTTP?

**HTTP (Hypertext Transfer Protocol)** is the foundation of data communication on the World Wide Web. It's the language browsers and servers use to talk to each other.

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP IN A NUTSHELL                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   👤 You click a link                                           │
│         │                                                        │
│         ▼                                                        │
│   🌐 Browser: "GET /page.html please"  ─────────►  🖥️ Server   │
│                                                                  │
│   🖥️ Server: "200 OK, here's the page" ◄─────────  🌐 Browser  │
│         │                                                        │
│         ▼                                                        │
│   📄 You see the webpage!                                       │
│                                                                  │
│   That's HTTP - a REQUEST and RESPONSE system!                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Key Characteristics

| Property | Description |
|----------|-------------|
| **Stateless** | Each request is independent; server doesn't remember you |
| **Text-based** | Human-readable messages (in HTTP/1.x) |
| **Client-Server** | Browser requests, server responds |
| **Extensible** | Headers can add new features |
| **Application Layer** | Sits on top of TCP/IP |

### Restaurant Analogy 🍽️

| Restaurant | HTTP |
|------------|------|
| Customer | Client (Browser) |
| Waiter | HTTP Protocol |
| Kitchen | Web Server |
| Menu | Available URLs/Resources |
| Order | HTTP Request |
| Food delivered | HTTP Response |
| Bill | Status Code |

---

## ⚙️ How HTTP Works

### The Request-Response Cycle

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP REQUEST/RESPONSE                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ╔═══════════════════════════════════════════════════════════╗  │
│  ║                      HTTP REQUEST                          ║  │
│  ╠═══════════════════════════════════════════════════════════╣  │
│  ║  GET /products/laptop HTTP/1.1                            ║  │
│  ║  Host: www.store.com                                       ║  │
│  ║  User-Agent: Chrome/120.0                                  ║  │
│  ║  Accept: text/html                                         ║  │
│  ║  Accept-Language: en-US                                    ║  │
│  ║  Cookie: session=abc123                                    ║  │
│  ╚═══════════════════════════════════════════════════════════╝  │
│                          │                                       │
│                          ▼                                       │
│                    🖥️ SERVER                                    │
│              (Processes the request)                            │
│                          │                                       │
│                          ▼                                       │
│  ╔═══════════════════════════════════════════════════════════╗  │
│  ║                      HTTP RESPONSE                         ║  │
│  ╠═══════════════════════════════════════════════════════════╣  │
│  ║  HTTP/1.1 200 OK                                          ║  │
│  ║  Content-Type: text/html; charset=utf-8                   ║  │
│  ║  Content-Length: 3420                                      ║  │
│  ║  Date: Mon, 24 Feb 2026 10:30:00 GMT                      ║  │
│  ║  Server: nginx/1.24.0                                      ║  │
│  ║                                                            ║  │
│  ║  <!DOCTYPE html>                                           ║  │
│  ║  <html>                                                    ║  │
│  ║  <body>Welcome to our store!</body>                       ║  │
│  ║  </html>                                                   ║  │
│  ╚═══════════════════════════════════════════════════════════╝  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Anatomy of a URL

```
  https://www.example.com:443/path/to/page?name=value&foo=bar#section
  └─┬──┘   └──────┬──────┘└┬┘└─────┬─────┘└────────┬────────┘└───┬──┘
    │             │        │       │                │             │
  Protocol      Host     Port    Path            Query        Fragment
                                                 String
    
  Protocol: https (secure) or http
  Host: Domain name or IP address
  Port: 443 (HTTPS default) or 80 (HTTP default)
  Path: Location of resource on server
  Query String: Parameters sent to server
  Fragment: Section on the page (handled by browser)
```

---

## 📨 HTTP Request Methods

HTTP defines different methods for different actions.

### The Main Methods

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP METHODS (VERBS)                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📥 GET                                                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Retrieve data                                          │   │
│  │  • Should not change server state                         │   │
│  │  • Parameters in URL                                      │   │
│  │  • Example: View a webpage, fetch user profile            │   │
│  │  GET /users/123                                           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  📤 POST                                                        │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Submit data to server                                  │   │
│  │  • Creates new resources                                  │   │
│  │  • Data in request body                                   │   │
│  │  • Example: Submit form, create account                   │   │
│  │  POST /users  {"name": "John", "email": "john@mail.com"} │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ✏️ PUT                                                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Update existing resource (full replacement)            │   │
│  │  • Idempotent (same result if repeated)                   │   │
│  │  • Example: Update entire user profile                    │   │
│  │  PUT /users/123  {"name": "John Doe", "email": "..."}    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🔧 PATCH                                                       │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Partial update of resource                             │   │
│  │  • Only sends changed fields                              │   │
│  │  • Example: Change just the email                         │   │
│  │  PATCH /users/123  {"email": "newemail@mail.com"}        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🗑️ DELETE                                                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Remove a resource                                      │   │
│  │  • Should be idempotent                                   │   │
│  │  • Example: Delete a user                                 │   │
│  │  DELETE /users/123                                        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Other Methods

| Method | Purpose |
|--------|---------|
| **HEAD** | Like GET, but only returns headers (no body) |
| **OPTIONS** | Get allowed methods for a resource |
| **CONNECT** | Establish tunnel (used for HTTPS proxies) |
| **TRACE** | Debug - echoes received request |

### CRUD Operations Mapped to HTTP

```
    CRUD         HTTP        Example
    ────         ────        ───────
    Create   →   POST        POST /articles (create new article)
    Read     →   GET         GET /articles/1 (get article)
    Update   →   PUT/PATCH   PUT /articles/1 (update article)
    Delete   →   DELETE      DELETE /articles/1 (remove article)
```

### 🎬 Watch: HTTP Methods Explained

[![HTTP Methods](https://img.youtube.com/vi/guYMSP7JVTA/maxresdefault.jpg)](https://www.youtube.com/watch?v=guYMSP7JVTA)

> 🔗 **Video**: [HTTP Request Methods Explained](https://www.youtube.com/watch?v=guYMSP7JVTA)

---

## 📊 HTTP Status Codes

Status codes tell you what happened with your request.

### Status Code Categories

```
┌─────────────────────────────────────────────────────────────────┐
│                    STATUS CODE FAMILIES                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1️⃣ xx - INFORMATIONAL                                         │
│     "Hang on, still processing..."                              │
│     100 Continue, 101 Switching Protocols                       │
│                                                                  │
│  2️⃣ xx - SUCCESS ✅                                            │
│     "Everything worked!"                                        │
│     200 OK, 201 Created, 204 No Content                        │
│                                                                  │
│  3️⃣ xx - REDIRECTION ↪️                                        │
│     "Go look somewhere else"                                    │
│     301 Moved Permanently, 302 Found, 304 Not Modified         │
│                                                                  │
│  4️⃣ xx - CLIENT ERROR ❌                                       │
│     "You did something wrong"                                   │
│     400 Bad Request, 401 Unauthorized, 404 Not Found           │
│                                                                  │
│  5️⃣ xx - SERVER ERROR 💥                                       │
│     "We messed up"                                              │
│     500 Internal Error, 502 Bad Gateway, 503 Unavailable       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Common Status Codes Explained

```
┌────────┬──────────────────────────┬────────────────────────────────┐
│ Code   │ Status                   │ Meaning                        │
├────────┼──────────────────────────┼────────────────────────────────┤
│ 200    │ OK                       │ Success! Here's your data      │
│ 201    │ Created                  │ Resource created successfully  │
│ 204    │ No Content               │ Success, but nothing to return │
├────────┼──────────────────────────┼────────────────────────────────┤
│ 301    │ Moved Permanently        │ URL changed forever            │
│ 302    │ Found (Temporary)        │ Temporary redirect             │
│ 304    │ Not Modified             │ Use your cached version        │
├────────┼──────────────────────────┼────────────────────────────────┤
│ 400    │ Bad Request              │ Malformed request syntax       │
│ 401    │ Unauthorized             │ Authentication required        │
│ 403    │ Forbidden                │ You don't have permission      │
│ 404    │ Not Found                │ Resource doesn't exist         │
│ 405    │ Method Not Allowed       │ Wrong HTTP method used         │
│ 408    │ Request Timeout          │ Request took too long          │
│ 429    │ Too Many Requests        │ Rate limit exceeded            │
├────────┼──────────────────────────┼────────────────────────────────┤
│ 500    │ Internal Server Error    │ Generic server error           │
│ 502    │ Bad Gateway              │ Upstream server failed         │
│ 503    │ Service Unavailable      │ Server overloaded/maintenance  │
│ 504    │ Gateway Timeout          │ Upstream server timeout        │
└────────┴──────────────────────────┴────────────────────────────────┘
```

### Status Code Visual

```
    200 OK 🎉
    ┌────────────────────────────────┐
    │  Server: "Here's your page!"  │
    └────────────────────────────────┘

    404 Not Found 😕
    ┌────────────────────────────────┐
    │  Server: "What? Never heard   │
    │           of that page..."    │
    └────────────────────────────────┘

    500 Internal Server Error 😰
    ┌────────────────────────────────┐
    │  Server: "I'm broken, sorry!" │
    └────────────────────────────────┘

    503 Service Unavailable 🔧
    ┌────────────────────────────────┐
    │  Server: "I'm taking a break" │
    └────────────────────────────────┘
```

---

## 📋 HTTP Headers

Headers carry metadata about the request/response.

### Common Request Headers

```
┌─────────────────────────────────────────────────────────────────┐
│                    REQUEST HEADERS                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Host: www.example.com                                          │
│  └── Required! Which website you're requesting                  │
│                                                                  │
│  User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64) Chrome/120    │
│  └── Your browser/device info                                   │
│                                                                  │
│  Accept: text/html, application/json                            │
│  └── What content types you can handle                          │
│                                                                  │
│  Accept-Language: en-US, en;q=0.9                               │
│  └── Preferred languages                                        │
│                                                                  │
│  Accept-Encoding: gzip, deflate, br                             │
│  └── Compression formats supported                              │
│                                                                  │
│  Authorization: Bearer eyJhbGciOiJIUzI1NiIs...                  │
│  └── Authentication token                                       │
│                                                                  │
│  Cookie: session=abc123; user_id=456                            │
│  └── Stored data from previous visits                           │
│                                                                  │
│  Content-Type: application/json                                 │
│  └── Format of data you're sending                              │
│                                                                  │
│  Cache-Control: no-cache                                        │
│  └── Caching preferences                                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Common Response Headers

```
┌─────────────────────────────────────────────────────────────────┐
│                    RESPONSE HEADERS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Content-Type: text/html; charset=utf-8                         │
│  └── What kind of content is being sent                         │
│                                                                  │
│  Content-Length: 3420                                           │
│  └── Size in bytes                                              │
│                                                                  │
│  Content-Encoding: gzip                                         │
│  └── Compression used                                           │
│                                                                  │
│  Set-Cookie: session=xyz789; HttpOnly; Secure                   │
│  └── Store this cookie in browser                               │
│                                                                  │
│  Cache-Control: max-age=3600                                    │
│  └── Cache this for 1 hour                                      │
│                                                                  │
│  ETag: "abc123"                                                 │
│  └── Version identifier for caching                             │
│                                                                  │
│  Location: https://new-url.com                                  │
│  └── Where to redirect (with 3xx codes)                         │
│                                                                  │
│  Access-Control-Allow-Origin: *                                 │
│  └── CORS - who can access this                                 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔒 What is HTTPS?

**HTTPS (HTTP Secure)** is HTTP with encryption. It protects data in transit.

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP vs HTTPS                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  HTTP (Insecure) 😰                                             │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                                                           │   │
│  │  💻 ────── "password123" ────── 🖥️                       │   │
│  │              ▲                                            │   │
│  │              │                                            │   │
│  │           👀 🦹 Hacker can see everything!               │   │
│  │                                                           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  HTTPS (Secure) 🔒                                              │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                                                           │   │
│  │  💻 ════ "7&$jK#2@pL9!" ════ 🖥️                         │   │
│  │           ▲                                               │   │
│  │           │    Encrypted - looks like gibberish!         │   │
│  │        😕 🦹  Hacker can't read it                       │   │
│  │                                                           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### What HTTPS Protects

| Protection | Description |
|------------|-------------|
| **Confidentiality** | Data is encrypted; eavesdroppers can't read it |
| **Integrity** | Data can't be modified in transit |
| **Authentication** | You're talking to the real server, not an imposter |

### When You NEED HTTPS

```
    ✅ ALWAYS use HTTPS for:
    
    • Login pages (passwords!)
    • Payment processing (credit cards!)
    • Personal information (addresses, SSN)
    • Any form submission
    • Actually... just use it everywhere!
    
    Modern browsers mark HTTP sites as "Not Secure" ⚠️
```

---

## 🔐 SSL/TLS Explained

**SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)** are the encryption protocols behind HTTPS.

### The Evolution

```
    SSL 1.0 (1994) - Never released (security flaws)
         │
    SSL 2.0 (1995) - Deprecated (insecure)
         │
    SSL 3.0 (1996) - Deprecated (POODLE attack)
         │
    TLS 1.0 (1999) - Deprecated
         │
    TLS 1.1 (2006) - Deprecated
         │
    TLS 1.2 (2008) - Still widely used ✅
         │
    TLS 1.3 (2018) - Current standard ✅✅
    
    People still say "SSL" but mean "TLS"!
```

### How TLS Works (Simplified)

```
┌─────────────────────────────────────────────────────────────────┐
│                    TLS ENCRYPTION                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Two types of encryption are used:                              │
│                                                                  │
│  1️⃣ ASYMMETRIC (Public/Private Key)                            │
│     ┌──────────────────────────────────────────────────────┐    │
│     │                                                       │    │
│     │    🔑 Public Key    🔐 Private Key                   │    │
│     │    (Everyone has)   (Only server has)                │    │
│     │                                                       │    │
│     │    Used to securely exchange symmetric key           │    │
│     │    Slow, but very secure for key exchange            │    │
│     │                                                       │    │
│     └──────────────────────────────────────────────────────┘    │
│                                                                  │
│  2️⃣ SYMMETRIC (Shared Secret)                                  │
│     ┌──────────────────────────────────────────────────────┐    │
│     │                                                       │    │
│     │    🔑 Same key for encrypt & decrypt                 │    │
│     │                                                       │    │
│     │    Fast! Used for all actual data transfer          │    │
│     │    The "session key" created during handshake       │    │
│     │                                                       │    │
│     └──────────────────────────────────────────────────────┘    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### SSL/TLS Certificates

```
┌─────────────────────────────────────────────────────────────────┐
│                    SSL CERTIFICATE                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  A certificate is like a digital passport for websites:        │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  📜 CERTIFICATE FOR: www.google.com                       │   │
│  │                                                           │   │
│  │  Issued By: Google Trust Services                        │   │
│  │  Valid From: Jan 1, 2026                                  │   │
│  │  Valid Until: Apr 1, 2026                                 │   │
│  │  Public Key: MIIBIjANBgkqhki...                          │   │
│  │  Signature: SHA256 RSA                                    │   │
│  │                                                           │   │
│  │  ✅ Verified by Certificate Authority (CA)               │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  Certificate Authorities (CAs):                                 │
│  • Let's Encrypt (Free!)                                        │
│  • DigiCert                                                     │
│  • Comodo                                                       │
│  • GlobalSign                                                   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🤝 The HTTPS Handshake

The TLS handshake establishes a secure connection.

### TLS 1.2 Handshake

```
┌─────────────────────────────────────────────────────────────────┐
│                    TLS 1.2 HANDSHAKE                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  💻 Client                                    🖥️ Server        │
│      │                                            │              │
│      │  1. ClientHello                           │              │
│      │     "Hi! I support TLS 1.2, these        │              │
│      │      ciphers, here's a random number"    │              │
│      │─────────────────────────────────────────►│              │
│      │                                            │              │
│      │  2. ServerHello                           │              │
│      │     "Hi! Let's use TLS 1.2, this cipher, │              │
│      │      here's MY random number"            │              │
│      │◄─────────────────────────────────────────│              │
│      │                                            │              │
│      │  3. Certificate                           │              │
│      │     "Here's my certificate + public key" │              │
│      │◄─────────────────────────────────────────│              │
│      │                                            │              │
│      │  4. Client verifies certificate           │              │
│      │     (Is it valid? Trusted CA? Right domain?)            │
│      │                                            │              │
│      │  5. Key Exchange                          │              │
│      │     "Here's encrypted pre-master secret" │              │
│      │─────────────────────────────────────────►│              │
│      │                                            │              │
│      │  6. Both derive session keys              │              │
│      │     (From random numbers + pre-master)    │              │
│      │                                            │              │
│      │  7. Finished                              │              │
│      │◄────────────────────────────────────────►│              │
│      │                                            │              │
│      │  🔐 Secure connection established!        │              │
│      │  Now all data is encrypted                │              │
│                                                                  │
│  Total: 2 round trips ⏱️                                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### TLS 1.3 Handshake (Faster!)

```
┌─────────────────────────────────────────────────────────────────┐
│                    TLS 1.3 HANDSHAKE                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  💻 Client                                    🖥️ Server        │
│      │                                            │              │
│      │  1. ClientHello + Key Share               │              │
│      │     "Hi! Here's my key share upfront"     │              │
│      │─────────────────────────────────────────►│              │
│      │                                            │              │
│      │  2. ServerHello + Key Share + Cert        │              │
│      │     "Great! Here's mine + certificate"   │              │
│      │◄─────────────────────────────────────────│              │
│      │                                            │              │
│      │  3. Finished                              │              │
│      │─────────────────────────────────────────►│              │
│      │                                            │              │
│      │  🔐 Secure! Start sending data!           │              │
│                                                                  │
│  Total: 1 round trip! ⚡                                        │
│                                                                  │
│  + 0-RTT resumption for returning visitors!                    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### 🎬 Watch: TLS Handshake Explained

[![TLS Handshake](https://img.youtube.com/vi/86cQJ0MMses/maxresdefault.jpg)](https://www.youtube.com/watch?v=86cQJ0MMses)

> 🔗 **Video**: [TLS Handshake Explained](https://www.youtube.com/watch?v=86cQJ0MMses)

---

## 🚀 HTTP/1.1 vs HTTP/2 vs HTTP/3

### Evolution of HTTP

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP VERSION EVOLUTION                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  HTTP/1.0 (1996)                                                │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • One request per connection                             │   │
│  │  • Connection closed after each request                   │   │
│  │  • Very inefficient! ❌                                   │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  HTTP/1.1 (1997)                                                │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Keep-alive connections (reuse connection)             │   │
│  │  • Pipelining (send multiple requests)                   │   │
│  │  • But still: head-of-line blocking 😕                   │   │
│  │  • Text-based protocol                                    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  HTTP/2 (2015)                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Binary protocol (not text)                             │   │
│  │  • Multiplexing (many requests on one connection)        │   │
│  │  • Header compression                                     │   │
│  │  • Server push                                            │   │
│  │  • Still uses TCP ✅                                      │   │
│  └──────────────────────────────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  HTTP/3 (2022)                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Uses QUIC instead of TCP                               │   │
│  │  • Built-in encryption                                    │   │
│  │  • Even faster connection setup                           │   │
│  │  • Better for mobile (handles network changes)           │   │
│  │  • No head-of-line blocking at all! ⚡                   │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Visual Comparison

```
    HTTP/1.1 (Sequential)
    ┌─────────────────────────────────────────────┐
    │  Req1 ──────► Res1 ──────►                 │
    │                          Req2 ──────► Res2 │
    │                                            │
    │  One at a time, waiting for each response  │
    └─────────────────────────────────────────────┘

    HTTP/2 (Multiplexed)
    ┌─────────────────────────────────────────────┐
    │  Req1 ────►  Req2 ────►  Req3 ────►        │
    │       ◄──── Res2 ◄──── Res1 ◄──── Res3    │
    │                                            │
    │  All at once, interleaved on one connection│
    └─────────────────────────────────────────────┘

    HTTP/3 (QUIC)
    ┌─────────────────────────────────────────────┐
    │  Even faster! No TCP overhead              │
    │  0-RTT connection resumption               │
    │  Built-in encryption                       │
    │  No head-of-line blocking                  │
    └─────────────────────────────────────────────┘
```

### Quick Comparison Table

| Feature | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---------|----------|--------|--------|
| **Protocol** | Text | Binary | Binary |
| **Transport** | TCP | TCP | QUIC (UDP) |
| **Multiplexing** | No | Yes | Yes |
| **Header Compression** | No | HPACK | QPACK |
| **Server Push** | No | Yes | Yes |
| **Encryption** | Optional | Optional* | Required |
| **Connection Setup** | 1-3 RTT | 1-3 RTT | 0-1 RTT |

*HTTP/2 browsers require HTTPS

---

## 🍪 Cookies and Sessions

### What Are Cookies?

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP COOKIES                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Cookies are small pieces of data stored in your browser.       │
│                                                                  │
│  💻 Browser                           🖥️ Server                │
│      │                                     │                     │
│      │  1. First visit                    │                     │
│      │─────────────────────────────────►  │                     │
│      │                                     │                     │
│      │  2. Set-Cookie: user_id=abc123     │                     │
│      │◄─────────────────────────────────  │                     │
│      │                                     │                     │
│      │  (Browser stores the cookie)        │                     │
│      │                                     │                     │
│      │  3. Next request                   │                     │
│      │     Cookie: user_id=abc123         │                     │
│      │─────────────────────────────────►  │                     │
│      │                                     │                     │
│      │  Server recognizes you!            │                     │
│                                                                  │
│  This is how websites "remember" you!                           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Cookie Attributes

```
Set-Cookie: session_id=xyz789; 
            Expires=Wed, 09 Jun 2026 10:18:14 GMT;
            Path=/;
            Domain=example.com;
            Secure;
            HttpOnly;
            SameSite=Strict

┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│  Expires/Max-Age: When cookie dies                              │
│  Path: Which paths can access it                                │
│  Domain: Which domains can access it                            │
│  Secure: Only send over HTTPS                                   │
│  HttpOnly: JavaScript can't access it (security!)               │
│  SameSite: CSRF protection                                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Sessions

```
┌─────────────────────────────────────────────────────────────────┐
│                    SESSIONS VS COOKIES                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  COOKIES                           SESSIONS                     │
│  • Stored in browser               • Stored on server           │
│  • Limited size (4KB)              • Can be larger              │
│  • Sent with every request         • Only session ID sent       │
│  • Less secure                     • More secure                │
│                                                                  │
│  How Sessions Work:                                             │
│                                                                  │
│  💻 ──────────────────────────────────────── 🖥️                │
│       │                                  │                      │
│       │  Cookie: session_id=abc123      │                      │
│       │                                  │                      │
│       └──────────────────────────────────┘                      │
│                                          │                      │
│                        ┌─────────────────▼──────────────────┐   │
│                        │         SESSION STORE              │   │
│                        │ ┌────────────────────────────────┐ │   │
│                        │ │ abc123: {                      │ │   │
│                        │ │   user_id: 42,                 │ │   │
│                        │ │   name: "Alice",               │ │   │
│                        │ │   cart: [...],                 │ │   │
│                        │ │   logged_in: true              │ │   │
│                        │ │ }                              │ │   │
│                        │ └────────────────────────────────┘ │   │
│                        └────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🧪 Hands-On Exercises

### Exercise 1: Inspect HTTP in Browser

1. Open Chrome/Firefox Developer Tools (F12)
2. Go to the "Network" tab
3. Visit any website
4. Click on any request to see:
   - Request headers
   - Response headers
   - Status code
   - Timing information

### Exercise 2: Make HTTP Requests with curl

```bash
# GET request
curl -v https://httpbin.org/get

# POST request
curl -X POST https://httpbin.org/post \
  -H "Content-Type: application/json" \
  -d '{"name": "John"}'

# See headers only
curl -I https://google.com

# Follow redirects
curl -L http://google.com
```

### Exercise 3: Check HTTPS Certificate

```bash
# View certificate details
openssl s_client -connect google.com:443 -servername google.com

# Or in browser:
# Click the padlock icon → Certificate
```

### Exercise 4: Compare HTTP Versions

```bash
# Check HTTP version used
curl -I --http1.1 https://google.com
curl -I --http2 https://google.com
```

---

## 📖 Key Takeaways

```
┌──────────────────────────────────────────────────────────────┐
│                    KEY TAKEAWAYS                              │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  ✅ HTTP is request-response protocol for the web           │
│                                                               │
│  ✅ Methods: GET (read), POST (create), PUT (update),       │
│     DELETE (remove)                                          │
│                                                               │
│  ✅ Status codes: 2xx (success), 3xx (redirect),            │
│     4xx (client error), 5xx (server error)                  │
│                                                               │
│  ✅ HTTPS = HTTP + TLS encryption                           │
│                                                               │
│  ✅ TLS protects confidentiality, integrity, authentication │
│                                                               │
│  ✅ HTTP/2 adds multiplexing; HTTP/3 uses QUIC              │
│                                                               │
│  ✅ Cookies enable stateful sessions on stateless HTTP      │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## 🔗 Additional Resources

### 📹 Videos
- [HTTP Crash Course - Traversy Media](https://www.youtube.com/watch?v=iYM2zFP3Zn0)
- [HTTPS Explained - Computerphile](https://www.youtube.com/watch?v=T4Df5_cojAs)
- [HTTP/2 and HTTP/3 - Fireship](https://www.youtube.com/watch?v=a-sBfyiXysI)

### 📚 Documentation
- [MDN: HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [HTTP Status Codes](https://httpstatuses.com/)
- [RFC 2616 - HTTP/1.1](https://tools.ietf.org/html/rfc2616)

### 🛠️ Tools
- [httpbin.org](https://httpbin.org/) - Test HTTP requests
- [curl](https://curl.se/) - Command-line HTTP client
- [Postman](https://www.postman.com/) - API testing tool

---

## ⏭️ What's Next?

Now that you understand HTTP/HTTPS, let's explore:

**[➡️ 05 - TCP/IP: The Internet Protocol Suite](./05-tcp-ip-model.md)**

We'll learn:
- The 4-layer TCP/IP model
- How TCP ensures reliable delivery
- UDP for fast, unreliable transport
- Ports and sockets

---

<div align="center">

**🎓 Elite Ball Knowledge - Internet Fundamentals**

[← Previous: DNS](./03-dns-domain-name-system.md) | [Home](./README.md) | [Next: TCP/IP →](./05-tcp-ip-model.md)

</div>
