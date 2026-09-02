# Week 10 — Web Technologies + Cloud Technology + Cyber Security & Emerging Tech

**Syllabus §12:** HTML5, CSS3, XML, basic concept of client-server computing, web server, proxy server, web application development, MVC architecture, web services, frontend technologies.
**Syllabus §14:** Cloud computing, compute/network/storage management technologies, edge computing.
**Syllabus §13:** Secure programming techniques, OWASP top 10 vulnerabilities, concepts of IoT, blockchain, AI.

**Estimated marks: ~6 + ~4 + ~5 = ~15**

> ⭐⭐ **The most important week in this plan.** These three sections have **zero GATE coverage** and only ~139 PYQs across the whole state-PSC corpus, so most candidates arrive unprepared. Yet the questions are purely **definitional** — no numericals, no derivations — and directly relevant to the Directorate of IT's actual work. **These are the cheapest 15 marks in Paper-II.**

---

# PART A — WEB TECHNOLOGIES

## 1. ⭐ HTML5

**HTML** = HyperText Markup Language — structure, not styling. Current declaration: `<!DOCTYPE html>`.

### 1.1 ⭐ Semantic elements (new in HTML5)

📌 `<header>` `<footer>` `<nav>` `<section>` `<article>` `<aside>` `<main>` `<figure>` `<figcaption>` `<time>` `<mark>` `<details>` `<summary>`

⭐ **Semantic vs non-semantic:** `<div>` and `<span>` are deliberately **non-semantic** (generic containers). `<b>`, `<i>`, `<font>`, `<center>` are **presentational** (deprecated in favour of CSS). Semantic tags convey meaning to browsers, screen readers and search engines.

### 1.2 ⭐ Other HTML5 features

| Feature | Note |
|---|---|
| ⭐ **`<canvas>`** | Bitmap drawing surface, scripted with JavaScript |
| **`<svg>`** | Vector graphics (scalable, XML-based) |
| ⭐ **`<audio>` / `<video>`** | Native media without plugins |
| ⭐ **New input types** | `email`, `url`, `number`, `date`, `range`, `color`, `search`, `tel` — with built-in validation |
| **Form attributes** | `required`, `placeholder`, `pattern`, `autofocus`, `autocomplete` |
| ⭐ **Web Storage** | See below |
| **Geolocation API** | Location access |
| **Web Workers** | Background JavaScript threads |
| **WebSockets** | Full-duplex persistent connection |
| **Drag and drop, offline app cache** | |

⭐⭐ **Web Storage vs Cookies — a guaranteed comparison question:**

| | ⭐ **localStorage** | ⭐ **sessionStorage** | ⭐ **Cookies** |
|---|---|---|---|
| Lifetime | ⭐ **Persists until explicitly cleared** | ⭐ **Cleared when the tab/session closes** | Until expiry date |
| Capacity | ~5–10 MB | ~5–10 MB | ⭐ **~4 KB** |
| Sent to server | ⭐ **❌ No** | ❌ No | ⭐ **✅ With every HTTP request** |
| Scope | Origin | Origin + tab | Domain/path |

### 1.3 Structure and tags
`<html>` → `<head>` (metadata: `<title>`, `<meta>`, `<link>`, `<style>`, `<script>`) → `<body>` (content).
Tables: `<table>`, `<tr>`, `<th>`, `<td>`, `<thead>`, `<tbody>`, `colspan`, `rowspan`.
Lists: `<ul>`, `<ol>`, `<dl>`/`<dt>`/`<dd>`.
Links: `<a href>` with `target="_blank"`. Images: `<img src alt>` (`alt` is required for accessibility).
Forms: `<form action method>` with `method="GET"` (data in URL, limited length, cacheable, idempotent) vs `method="POST"` (data in body, no size limit, not cached).

---

## 2. ⭐ CSS3

**CSS** = Cascading Style Sheets — presentation. Syntax: `selector { property: value; }`

### 2.1 Ways to apply
**Inline** (`style=` attribute) · **Internal** (`<style>` in head) · ⭐ **External** (`<link rel="stylesheet">` — best practice, cacheable and reusable).

### 2.2 ⭐⭐ Specificity (the cascade order)

📌 ⭐ **`!important` > Inline style > ID (#) > Class (.) / attribute / pseudo-class > Element (tag) > Universal (\*) > inherited**

Specificity is often scored as (inline, ID, class, element): an ID selector `#header` beats any number of class selectors.
⭐ When specificity ties, the **later** rule wins (that is the "cascading" part).

### 2.3 ⭐ Selectors

| Selector | Matches |
|---|---|
| `*` | Everything (universal) |
| `p` | All `<p>` elements (type) |
| `.cls` | Elements with class `cls` |
| `#id` | The element with that id |
| `A B` | Descendant |
| `A > B` | ⭐ **Direct child** |
| `A + B` | Adjacent sibling |
| `A ~ B` | General sibling |
| `[attr=val]` | Attribute |
| `:hover`, `:focus`, `:nth-child(n)`, `:first-child` | Pseudo-classes |
| `::before`, `::after`, `::first-line` | Pseudo-elements |

### 2.4 ⭐⭐ The box model

📌 ⭐ **From the content outwards: CONTENT → PADDING → BORDER → MARGIN**

⚠ **Padding is inside the border; margin is outside.** Reversing these is the single most common CSS error in exams.

📌 Default (`box-sizing: content-box`): **total width = width + 2×padding + 2×border + 2×margin**
📌 With `box-sizing: border-box`: the declared `width` **includes** padding and border.

🔢 `width: 200px; padding: 10px; border: 5px; margin: 20px;` (content-box) → rendered element width = 200 + 20 + 10 = **230 px**; total space occupied = 270 px.

### 2.5 Positioning and layout

| `position` | Behaviour |
|---|---|
| `static` | Default; normal flow |
| `relative` | Offset from its normal position; still occupies space |
| ⭐ `absolute` | Removed from flow; positioned relative to the nearest **positioned** ancestor |
| `fixed` | Relative to the **viewport**; does not scroll |
| `sticky` | Relative until a threshold, then fixed |

`display`: `block` · `inline` · `inline-block` · `none` · `flex` · `grid`
⭐ **Flexbox** — one-dimensional layout (`justify-content`, `align-items`, `flex-direction`).
⭐ **CSS Grid** — two-dimensional layout (`grid-template-columns`, `grid-gap`).
**Float** and `clear` — the legacy layout mechanism.

### 2.6 ⭐ Responsive design
📌 ⭐ **Media queries:** `@media screen and (max-width: 768px) { ... }`
Concepts: fluid grids (percentages), flexible images, the **viewport meta tag**, ⭐ **mobile-first** design (start with the smallest breakpoint and add complexity upward), breakpoints.
**CSS3 additions:** border-radius, box-shadow, gradients, transitions, transforms, animations, web fonts, opacity, RGBA/HSL colours, multiple columns.

---

## 3. ⭐ XML

**XML** = eXtensible Markup Language — for **describing and transporting data** (unlike HTML, which displays it). Tags are user-defined; XML is case-sensitive.

### 3.1 ⭐⭐ Well-formed vs valid

| | ⭐ **Well-formed** | ⭐ **Valid** |
|---|---|---|
| Requirement | Obeys XML **syntax** rules | Well-formed **AND** conforms to a DTD or XML Schema |
| Checked by | Any XML parser | A **validating** parser |

⭐ **Every valid document is well-formed, but not every well-formed document is valid.** This one-way implication is the standard question.

⭐ **Rules for well-formedness:** exactly one **root element** · every tag closed · tags properly **nested** · attribute values **quoted** · case-sensitive matching · reserved characters escaped (`&lt;` `&gt;` `&amp;` `&quot;` `&apos;`).

### 3.2 ⭐ DTD vs XSD (XML Schema)

| | **DTD** | ⭐ **XSD (XML Schema)** |
|---|---|---|
| Written in | Its own non-XML syntax | ⭐ **XML itself** |
| Data types | ❌ No support | ⭐ **✅ Rich data types** |
| Namespace support | ❌ | ✅ |
| Extensible | Limited | ✅ |

### 3.3 Related technologies

| Technology | Purpose |
|---|---|
| ⭐ **XSLT** | **Transforms** XML into another format (HTML, text, other XML) |
| ⭐ **XPath** | **Navigates/queries** nodes in an XML document |
| **XQuery** | Queries XML data (like SQL for XML) |
| **XSL-FO** | Formatting for print |
| **DOM / SAX** | Parsing APIs — DOM builds the whole tree in memory (random access, memory-heavy); **SAX** is event-driven and streaming (memory-light, forward-only) |
| **Namespaces** | Avoid element-name collisions (`xmlns`) |

### 3.4 ⭐ XML vs JSON

| | **XML** | ⭐ **JSON** |
|---|---|---|
| Verbosity | Verbose (closing tags) | ⭐ **Compact** |
| Data types | Text (typed via XSD) | Native: string, number, boolean, array, object, null |
| Parsing | Needs an XML parser | ⭐ **Native to JavaScript** |
| Comments | ✅ | ❌ |
| Attributes / namespaces | ✅ | ❌ |
| Typical use | Enterprise, SOAP, config | ⭐ **REST APIs, web/mobile** |

---

## 4. ⭐ Client–server computing and servers

### 4.1 Architecture tiers

| Architecture | Layers |
|---|---|
| **1-tier** | Everything on one machine |
| **2-tier** | Client + database server (client holds business logic — "fat client") |
| ⭐ **3-tier** | ⭐ **Presentation + Application/Business logic + Data** |
| **n-tier** | Further decomposition (web, app, service, data) |

⭐ **3-tier advantages:** scalability, maintainability, security (the client never touches the database directly), and independent layer evolution.

⭐ **Thin vs thick (fat) client:** a thin client does minimal processing and relies on the server (browser-based, easy to maintain, needs connectivity); a thick client does substantial local processing (responsive, offline-capable, harder to deploy/update).

**Other models:** peer-to-peer (no central server) · **microservices** (small independently deployable services vs a **monolith**) · serverless.
**Stateful vs stateless:** HTTP is stateless; state is layered on with cookies, sessions or tokens.

### 4.2 ⭐⭐ Server types

| Server | Role |
|---|---|
| ⭐ **Web server** | Serves **static** content over HTTP (HTML, CSS, JS, images). Examples: **Apache HTTP Server, Nginx, IIS** |
| ⭐ **Application server** | Executes **business logic / dynamic** content, provides transactions, security, connection pooling. Examples: **Tomcat, JBoss/WildFly, WebLogic, WebSphere** |
| ⭐ **Proxy server** | An intermediary between client and server |
| **Database server** | Hosts the DBMS |
| **Mail / DNS / File server** | Named by function |

⚠ **Web server vs application server** is a favourite: a web server handles HTTP and static files; an application server runs the application code. Nginx/Apache are often placed *in front of* Tomcat.

### 4.3 ⭐⭐ Forward vs reverse proxy

| | ⭐ **Forward proxy** | ⭐ **Reverse proxy** |
|---|---|---|
| Sits in front of | ⭐ **The clients** | ⭐ **The servers** |
| Hides | ⭐ **The client's identity** from the server | ⭐ **The backend servers** from the client |
| Typical uses | Content filtering, anonymity, caching for a LAN, bypassing restrictions | ⭐ **Load balancing, SSL termination, caching, compression, security/WAF** |
| Example | Corporate/school web proxy | Nginx in front of app servers; a CDN edge |

⚠ Learn this pairing precisely — "which proxy provides load balancing?" is a common one-mark question. Answer: **reverse proxy**.

**Proxy benefits generally:** caching (reduced latency and bandwidth), anonymity, access control, logging.

---

## 5. ⭐ MVC architecture

⭐ **Separation of concerns into three components:**

| Component | Responsibility |
|---|---|
| ⭐ **Model** | ⭐ **Data + business logic**; database interaction. Knows nothing about the UI |
| ⭐ **View** | ⭐ **Presentation / UI** — renders the model to the user |
| ⭐ **Controller** | ⭐ **Handles user input**, invokes model operations, and selects the view to render |

⭐ **Flow:** user → **Controller** → updates **Model** → **View** reads the model → response to user.

⭐ **Advantages:** separation of concerns, parallel development, testability, reusable views, easier maintenance.

**Variants:**
- **MVP (Model-View-Presenter):** the presenter handles all UI logic; the view is passive.
- **MVVM (Model-View-ViewModel):** the ViewModel exposes bindable state; used in Angular, WPF, Vue.

**MVC frameworks:** Spring MVC, ASP.NET MVC, Django (MTV), Ruby on Rails, Laravel, Struts, CodeIgniter.

---

## 6. ⭐ Web services and APIs

📌 A **web service** is a software system supporting machine-to-machine interaction over a network.

### 6.1 ⭐⭐ SOAP vs REST

| | ⭐ **SOAP** | ⭐ **REST** |
|---|---|---|
| Nature | ⭐ **A protocol** (strict standard) | ⭐ **An architectural style** |
| Message format | ⭐ **XML only** (Envelope/Header/Body) | JSON, XML, HTML, plain text |
| Transport | HTTP, SMTP, TCP, JMS | ⭐ **HTTP only** |
| Contract | ⭐ **WSDL** | OpenAPI/Swagger (optional) |
| State | Can be stateful | ⭐ **Stateless** |
| Overhead | Heavy | ⭐ **Lightweight** |
| Built-in standards | WS-Security, WS-AtomicTransaction, reliability | Relies on HTTPS, OAuth |
| Caching | Difficult | ⭐ **HTTP caching works** |
| Best for | Enterprise, banking, high-security transactions | ⭐ **Web/mobile APIs, public APIs** |

⚠ ⭐ **REST is a style, SOAP is a protocol.** Reversing this is the single most common error in this section.

### 6.2 SOAP-related standards
⭐ **WSDL** (Web Services Description Language) — an XML document describing the service's operations, messages and endpoints (the machine-readable contract).
⭐ **UDDI** (Universal Description, Discovery and Integration) — a registry for **discovering** web services.
⭐ **SOAP envelope structure:** `Envelope` → `Header` (optional metadata) + `Body` (payload, or `Fault` on error).

### 6.3 ⭐ REST constraints and conventions

⭐ **Six REST constraints:** client–server · ⭐ **stateless** · cacheable · uniform interface · layered system · code-on-demand (optional).

⭐ **HTTP verbs mapped to CRUD:**

| Verb | CRUD | Idempotent? | Safe? |
|---|---|---|---|
| **GET** | Read | ✅ | ✅ |
| **POST** | Create | ⭐ **❌ No** | ❌ |
| **PUT** | Create/Replace | ⭐ **✅ Yes** | ❌ |
| **PATCH** | Partial update | ❌ (generally) | ❌ |
| **DELETE** | Delete | ✅ | ❌ |

⚠ **POST is not idempotent; PUT is.** Repeating a PUT leaves the same final state; repeating a POST creates duplicates.

**Richardson maturity model:** level 0 (single endpoint) → 1 (resources) → 2 (HTTP verbs) → 3 (HATEOAS).
**API concepts:** endpoints, versioning, rate limiting, pagination, API gateway, **CORS**, **GraphQL** (client specifies exactly the data it wants, single endpoint).

---

## 7. ⭐ Frontend technologies

### 7.1 JavaScript
Client-side (and, via Node.js, server-side) scripting. **Interpreted**, dynamically typed, single-threaded with an **event loop**.
- **Types:** number, string, boolean, null, undefined, symbol, bigint, object.
- ⚠ `==` performs type coercion; ⭐ **`===` compares value *and* type** — always prefer `===`.
- `var` (function-scoped, hoisted) vs ⭐ **`let`/`const` (block-scoped)**.
- Concepts: closures · hoisting · `this` · prototypes and prototypal inheritance · callbacks → **Promises** → `async`/`await` · arrow functions · **event bubbling and capturing** · JSON (`JSON.parse`, `JSON.stringify`).

### 7.2 ⭐ DOM (Document Object Model)
A **tree** representation of the document that scripts can read and modify.
Methods: `getElementById`, `querySelector`, `createElement`, `appendChild`, `addEventListener`, `innerHTML`.
⚠ The **DOM is a W3C standard API, not part of JavaScript itself** — it is provided by the browser.

### 7.3 ⭐ AJAX
📌 **Asynchronous JavaScript And XML** — exchanges data with the server **without reloading the page**, enabling single-page applications.
Implemented with `XMLHttpRequest` or the modern ⭐ **`fetch()` API**. Despite the name, it usually carries **JSON**, not XML.

### 7.4 Frameworks and libraries (awareness)

| Tool | Note |
|---|---|
| **jQuery** | Legacy DOM/AJAX library; simplified cross-browser scripting |
| ⭐ **React** | Facebook/Meta; component-based, **virtual DOM**, JSX; a library |
| ⭐ **Angular** | Google; full **framework**, TypeScript, two-way data binding, MVVM |
| ⭐ **Vue.js** | Progressive framework, gentle learning curve |
| **Bootstrap / Tailwind** | CSS frameworks; responsive grid systems |
| **Node.js** | JavaScript runtime (V8) for server-side; **npm** package manager |
| **Webpack / Vite / Babel** | Bundlers and transpilers |

⚠ **React is a library; Angular is a full framework.** Also: React uses one-way data flow with a virtual DOM; Angular offers two-way binding.

**Session management:** cookies · server-side sessions · ⭐ **JWT (JSON Web Token)** — a self-contained, signed token with **header.payload.signature**, enabling stateless authentication.

---

# PART B — CLOUD TECHNOLOGY

## 8. ⭐⭐ Cloud computing fundamentals

📌 **NIST definition:** on-demand network access to a shared pool of configurable computing resources, rapidly provisioned with minimal management effort.

### 8.1 ⭐⭐ Five essential characteristics (NIST)

📌 ⭐ **1. On-demand self-service · 2. Broad network access · 3. Resource pooling (multi-tenancy) · 4. Rapid elasticity · 5. Measured service (pay-per-use)**

⚠ "Permanent local storage", "dedicated hardware per customer" and "unlimited free capacity" are **not** cloud characteristics — a common distractor pattern.

### 8.2 ⭐⭐ Service models — the guaranteed question

| Model | Customer manages | Provider manages | Examples |
|---|---|---|---|
| ⭐ **IaaS** | ⭐ **OS, runtime, middleware, applications, data** | Virtualisation, servers, storage, networking, physical | **AWS EC2, Azure VMs, Google Compute Engine** |
| ⭐ **PaaS** | ⭐ **Applications and data only** | + OS, runtime, middleware | **Heroku, Google App Engine, AWS Elastic Beanstalk, Azure App Service** |
| ⭐ **SaaS** | ⭐ **Nothing — just use it** (data/config) | Everything | ⭐ **Gmail, Salesforce, Office 365, Dropbox, Zoom** |
| **FaaS / Serverless** | Individual functions | Everything else, including scaling | AWS Lambda, Azure Functions |

⭐ **Mnemonic for the responsibility gradient:** as you move IaaS → PaaS → SaaS, **customer control decreases and provider responsibility increases.**

⭐ **"Who patches the guest OS?"** — IaaS: the **customer**. PaaS/SaaS: the **provider**. This exact question appears frequently.

Also: **DaaS** (Desktop/Data as a Service), **STaaS** (Storage), **NaaS** (Network), **DBaaS**, **XaaS** (anything).

### 8.3 ⭐ Deployment models

| Model | Description |
|---|---|
| ⭐ **Public cloud** | Shared infrastructure owned by a provider; cheapest, most scalable, least control |
| ⭐ **Private cloud** | Dedicated to one organisation (on- or off-premises); ⭐ **most control and security**, higher cost |
| ⭐ **Hybrid cloud** | Public + private with orchestration between them; ⭐ **keeps sensitive data private while bursting to public capacity** |
| ⭐ **Community cloud** | Shared by several organisations with common concerns (e.g. government departments, healthcare consortia) |
| **Multi-cloud** | Multiple public providers (avoids vendor lock-in) |

### 8.4 ⭐ Benefits and drawbacks

**Benefits:** no capital expenditure (CapEx → OpEx) · elasticity and scalability · global reach · high availability and disaster recovery · automatic updates · pay-per-use.

**Drawbacks:** ⚠ **dependence on internet connectivity** · ⭐ **vendor lock-in** · **data security, privacy and sovereignty** concerns · limited control and customisation · unpredictable cost at scale · downtime is outside your control · compliance/regulatory complexity.

📌 ⭐ **Scaling:** **vertical scaling (scale up)** = a bigger machine; **horizontal scaling (scale out)** = more machines. ⭐ Cloud elasticity primarily means **horizontal auto-scaling**.
📌 ⭐ **SLA (Service Level Agreement):** the contractual uptime/performance guarantee. "Three nines" (99.9%) ≈ 8.77 hours downtime/year; "five nines" (99.999%) ≈ 5.26 minutes/year.

---

## 9. ⭐ Virtualisation

📌 **Virtualisation** creates a software abstraction of physical resources — the enabling technology for cloud computing.

### 9.1 ⭐ Hypervisors

| | ⭐ **Type-1 (bare-metal / native)** | ⭐ **Type-2 (hosted)** |
|---|---|---|
| Runs on | ⭐ **The hardware directly** | ⭐ **On top of a host OS** |
| Performance | Better | Lower (extra layer) |
| Use | ⭐ **Data centres, production** | Desktop testing/development |
| Examples | ⭐ **VMware ESXi, Microsoft Hyper-V, Xen, KVM** | ⭐ **VirtualBox, VMware Workstation/Player, Parallels** |

**Types of virtualisation:** server · storage · network (**SDN**, **NFV**) · desktop (VDI) · application · data.

### 9.2 ⭐⭐ Virtual machines vs containers

| | ⭐ **Virtual Machine** | ⭐ **Container** |
|---|---|---|
| Virtualises | Hardware | ⭐ **The operating system** |
| Guest OS | ⭐ **Each VM has its own full guest OS** | ⭐ **Shares the host kernel** |
| Size | GB | ⭐ **MB** |
| Boot time | Minutes | ⭐ **Seconds/milliseconds** |
| Isolation | ⭐ **Stronger (hardware-level)** | Weaker (process-level, shared kernel) |
| Density per host | Lower | ⭐ **Much higher** |
| Portability | Heavier images | ⭐ **Highly portable** |
| Technology | ESXi, KVM, Hyper-V | ⭐ **Docker**, containerd, LXC, Podman |

⚠ ⭐ **Containers are lighter and faster; VMs give stronger isolation.** Both halves of that sentence get asked.

⭐ **Docker:** image (immutable template) → container (running instance) · Dockerfile · Docker Hub (registry) · layered filesystem.
⭐ **Kubernetes (K8s):** container **orchestration** — automated deployment, scaling, self-healing and load balancing. Objects: **pod** (smallest deployable unit) · node · cluster · service · deployment · ReplicaSet · namespace.

---

## 10. ⭐ Compute, network and storage management

### 10.1 Compute
Virtual machines/instances (sizing, families) · **auto-scaling groups** · ⭐ **load balancing** (round robin, least connections, IP hash; layer-4 vs layer-7) · containers and orchestration · serverless functions · GPU/HPC instances · spot/reserved/on-demand pricing.

### 10.2 ⭐⭐ Storage types — a very common question

| Type | Unit | Access | Best for | Examples |
|---|---|---|---|---|
| ⭐ **Block storage** | Fixed-size blocks | Attached as a raw volume; the OS puts a filesystem on it | ⭐ **Databases, boot volumes, low-latency I/O** | AWS EBS, SAN, iSCSI |
| ⭐ **File storage** | Files in a hierarchy | Network file protocols (NFS, SMB) | ⭐ **Shared file access, home directories** | AWS EFS, NAS |
| ⭐ **Object storage** | ⭐ **Objects (data + metadata + unique ID) in a flat namespace** | ⭐ **HTTP/REST API** | ⭐ **Unstructured data, backups, media, static websites, data lakes** | ⭐ **AWS S3**, Azure Blob, Google Cloud Storage |

⭐ **Object storage is flat (no true directory hierarchy — "folders" are name prefixes), infinitely scalable, and accessed over HTTP.** These three properties are the exam answers.

**Storage concepts:** ⭐ **storage tiers** (hot / cool / cold / archive — cheaper storage, higher retrieval cost/latency) · replication and durability ("eleven nines") · snapshots · **lifecycle policies** · deduplication and compression · encryption at rest and in transit · **CDN** (edge caching of static content).

### 10.3 Network
Virtual private cloud (**VPC**) · subnets · security groups and network ACLs · route tables · internet/NAT gateways · VPN and dedicated interconnects (Direct Connect/ExpressRoute) · elastic/floating IPs · DNS services · ⭐ **SDN (Software-Defined Networking)** — separates the **control plane** from the **data plane** for centralised, programmable control · **NFV** (Network Function Virtualisation).

### 10.4 Cloud migration and management
**Migration strategies (the 6 R's):** Rehost ("lift and shift") · Replatform · Refactor/Re-architect · Repurchase · Retire · Retain.
**Management:** monitoring and logging · cost management/FinOps · **IaC (Infrastructure as Code** — Terraform, CloudFormation) · **DevOps** and CI/CD.

### 10.5 ⭐⭐ Edge computing

📌 ⭐ **Edge computing processes data close to where it is generated**, rather than sending everything to a central cloud.

⭐ **Motivations:** ⭐ **reduced latency** · reduced backhaul **bandwidth** cost · data privacy/sovereignty (data stays local) · offline/intermittent-connectivity resilience · real-time response.

⭐ **Cloud vs Fog vs Edge:**

| | ⭐ **Cloud** | ⭐ **Fog** | ⭐ **Edge** |
|---|---|---|---|
| Location | Centralised data centres | ⭐ **Intermediate layer — LAN, gateways, routers** | ⭐ **On or next to the device itself** |
| Latency | Highest | Medium | ⭐ **Lowest** |
| Compute power | Highest | Medium | Limited |
| Data retained | Long-term | Short-term | Transient |

**Use cases:** autonomous vehicles · industrial IoT and predictive maintenance · smart cities and traffic systems · AR/VR · video analytics/CCTV · healthcare monitoring · retail. Related: **MEC (Multi-access Edge Computing)** in 5G.

### 10.6 Government/Indian cloud context ⭐
⭐ **MeghRaj** — the Government of India (MeitY) Cloud initiative; **NIC National Cloud** provides GI Cloud services to government departments.
**Empanelled cloud service providers** under MeitY; **data localisation** requirements; **State Data Centres (SDC)** and **SWAN (State Wide Area Network)** under the National e-Governance Plan. Relevant to the Directorate of Information Technology's own work.

---

# PART C — CYBER SECURITY & EMERGING TECHNOLOGIES

## 11. ⭐ Secure programming techniques

⭐ **Core principles:**

| Principle | Meaning |
|---|---|
| ⭐ **Input validation** | Never trust user input; validate on the **server side**; prefer **allow-lists** over deny-lists |
| ⭐ **Output encoding** | Encode data for its destination context (HTML, JS, SQL, URL) — the defence against XSS |
| ⭐ **Least privilege** | Every component gets the minimum rights it needs |
| ⭐ **Defence in depth** | Multiple independent layers of control |
| ⭐ **Fail securely / secure defaults** | On error, deny; ship with security switched **on** |
| **Complete mediation** | Check authorisation on **every** access, not just the first |
| **Open design** | Security must not depend on secrecy of the design (⚠ **no security through obscurity**) |
| **Separation of duties** | Split critical actions between actors |
| **Economy of mechanism** | Keep security logic simple and auditable |

⭐ **Common vulnerability classes:**
- ⭐ **Buffer overflow** — writing past a buffer's bounds, potentially overwriting the return address and executing attacker code. *Mitigations:* bounds checking, safe functions (`strncpy` over `strcpy`), **ASLR**, **DEP/NX**, stack canaries.
- ⭐ **Integer overflow / underflow**
- ⭐ **Race conditions / TOCTOU** (time-of-check to time-of-use)
- **Format string vulnerabilities** (`printf(user_input)`)
- **Hardcoded credentials**, verbose error messages, insecure deserialisation
- **Use-after-free, dangling pointers, memory leaks**

⭐ **Secure SDLC:** threat modelling (**STRIDE**) · secure design review · **SAST** (static analysis) and **DAST** (dynamic analysis) · dependency/SCA scanning · code review · penetration testing · **shift left** (find defects early — cheapest to fix).

---

## 12. ⭐⭐ OWASP Top 10

📌 **OWASP** = Open Worldwide Application Security Project — a non-profit publishing the most widely cited list of web application security risks, revised every few years.

⭐ **The OWASP Top 10 (2021 edition) — learn all ten by name:**

| Rank | Category | One-line meaning |
|---|---|---|
| ⭐ **A01** | ⭐ **Broken Access Control** | Users can act outside their permissions (IDOR, privilege escalation, missing function-level checks) |
| **A02** | **Cryptographic Failures** | Sensitive data exposed through weak/absent encryption (formerly "Sensitive Data Exposure") |
| ⭐ **A03** | ⭐ **Injection** | Untrusted input interpreted as code/query — ⭐ **SQL injection, XSS, command injection, LDAP injection** |
| **A04** | **Insecure Design** | Missing or ineffective security controls by design (new in 2021) |
| **A05** | **Security Misconfiguration** | Default credentials, unnecessary features, verbose errors, missing hardening (includes XXE) |
| **A06** | **Vulnerable and Outdated Components** | Unpatched libraries and dependencies |
| **A07** | **Identification and Authentication Failures** | Weak passwords, broken session management, credential stuffing |
| **A08** | **Software and Data Integrity Failures** | Unverified updates, insecure deserialisation, CI/CD pipeline compromise |
| **A09** | **Security Logging and Monitoring Failures** | Breaches go undetected |
| **A10** | **Server-Side Request Forgery (SSRF)** | The server is tricked into making requests to unintended internal destinations |

⭐ **Key changes in 2021:** Broken Access Control rose to **#1**; **Injection dropped from #1 to #3** and absorbed XSS; three new categories appeared (Insecure Design, Software & Data Integrity Failures, SSRF).

⚠ **OWASP revises this list periodically.** If a question names an edition, answer for that edition; otherwise learn the most recent list you can confirm and be aware that Injection was #1 in the 2013/2017 editions and Broken Access Control was #1 in 2021.

### 12.1 ⭐⭐ The two vulnerabilities you must understand properly

⭐ **SQL Injection**
Untrusted input is concatenated into a SQL query, letting the attacker alter its logic.
```
Vulnerable:  "SELECT * FROM users WHERE name='" + input + "'"
Attack:      input = ' OR '1'='1
Result:      SELECT * FROM users WHERE name='' OR '1'='1'   → returns all rows
```
| Defence | Effectiveness |
|---|---|
| ⭐ **Parameterised queries / prepared statements** | ⭐ **THE fix** — separates code from data so input can never be parsed as SQL |
| Stored procedures (written safely) | Good |
| Input validation / allow-listing | Useful defence in depth |
| Least-privilege DB accounts | Limits damage |
| Escaping input | Fragile; last resort |
| Hiding error messages | ⚠ **Not a fix** — only hides the symptom |

⭐ **Cross-Site Scripting (XSS)**
The attacker injects script that executes **in another user's browser**, in the trusted site's context — enabling session-cookie theft, keylogging and defacement.

| Type | Description |
|---|---|
| ⭐ **Stored (persistent)** | Payload saved on the server (e.g. a comment) and served to every viewer — most damaging |
| ⭐ **Reflected** | Payload comes in the request and is echoed straight back (typically via a crafted link) |
| ⭐ **DOM-based** | Client-side script writes untrusted data into the DOM |

**Defences:** ⭐ **output encoding for the correct context** · input validation · ⭐ **Content Security Policy (CSP)** · `HttpOnly` and `Secure` cookie flags · sanitisation libraries · avoiding `innerHTML`/`eval`.

⚠ **XSS attacks the user's browser; SQL injection attacks the database.** Do not confuse them.

⭐ **CSRF (Cross-Site Request Forgery):** tricks an authenticated user's browser into submitting an unwanted request. **Defences:** anti-CSRF tokens, `SameSite` cookies, checking Origin/Referer.
⚠ **XSS vs CSRF:** XSS exploits the site's trust in **user input**; CSRF exploits the site's trust in an **authenticated user's browser**.

---

## 13. ⭐ Cryptography and security controls

### 13.1 ⭐⭐ Symmetric vs asymmetric

| | ⭐ **Symmetric** | ⭐ **Asymmetric (public key)** |
|---|---|---|
| Keys | ⭐ **One shared secret key** | ⭐ **Public/private key pair** |
| Speed | ⭐ **Fast** | ⭐ **Slow** (~1000×) |
| Key distribution | ⭐ **The hard problem** | ⭐ **Solved** |
| Keys for n users | ⭐ **n(n−1)/2** | ⭐ **2n** |
| Algorithms | ⭐ **AES, DES, 3DES, Blowfish, RC4, ChaCha20** | ⭐ **RSA, ECC, Diffie–Hellman, DSA, ElGamal** |
| Provides | Confidentiality | Confidentiality, ⭐ **digital signatures, non-repudiation** |

⭐ **Hybrid cryptosystems (TLS) use both:** asymmetric to exchange a symmetric **session key**, then symmetric for the bulk data. This gets asked as "why does HTTPS use both?"

**DES:** 64-bit block, **56-bit effective key** (broken by brute force). **3DES:** 168-bit. ⭐ **AES:** 128-bit block with 128/192/256-bit keys — the current standard.
**RSA:** based on the difficulty of **factoring large integers**. **ECC:** based on the elliptic-curve discrete logarithm problem — equivalent security with much smaller keys. **Diffie–Hellman:** key *exchange* only, not encryption.

### 13.2 ⭐ Hashing

📌 A **cryptographic hash** is a one-way function producing a fixed-size digest.
⭐ **Required properties:** deterministic · fast · ⭐ **pre-image resistance** (cannot invert) · ⭐ **collision resistance** · ⭐ **avalanche effect** (a 1-bit input change flips ~half the output bits).

| Algorithm | Digest | Status |
|---|---|---|
| **MD5** | 128 bits | ⭐ **Broken** (collisions) |
| **SHA-1** | 160 bits | ⭐ **Broken/deprecated** |
| ⭐ **SHA-256 / SHA-2 family** | 256+ bits | ⭐ **Current standard** |
| **SHA-3** | variable | Standard |
| **bcrypt, scrypt, Argon2, PBKDF2** | — | ⭐ **For password storage** (deliberately slow, salted) |

⚠ ⭐ **Never store passwords with a plain fast hash.** Use a **salt** (unique random value per password, defeats rainbow tables) with a slow **key-derivation function**. **Pepper** is a secret site-wide value.
⚠ **Hashing ≠ encryption** — hashing is one-way and irreversible; encryption is reversible with a key. **Encoding** (Base64) is neither.

### 13.3 ⭐ Digital signatures and PKI

⭐ **To sign:** hash the message, then **encrypt the hash with the SENDER'S PRIVATE key**.
⭐ **To verify:** decrypt the signature with the **sender's PUBLIC key** and compare with a freshly computed hash.

📌 ⭐ **Provides: authentication + integrity + non-repudiation.** ⚠ **It does NOT provide confidentiality** (the message itself is not encrypted).

⚠ ⭐ **Signing uses the sender's private key; encrypting for confidentiality uses the receiver's public key.** This direction is asked constantly.

**PKI (Public Key Infrastructure):** ⭐ **Certificate Authority (CA)** issues **X.509 digital certificates** binding an identity to a public key; RA, CRL/OCSP for revocation, chain of trust to a root CA.
⭐ **SSL/TLS:** the TLS handshake authenticates the server via its certificate, negotiates a cipher suite, and establishes a symmetric session key. **HTTPS = HTTP over TLS, port 443.**

### 13.4 ⭐ CIA triad and attacks

📌 ⭐ **Confidentiality · Integrity · Availability** (extended: Authentication, Authorisation, Non-repudiation, Accountability).

| Attack | Description | Targets |
|---|---|---|
| ⭐ **DoS / DDoS** | Flood a target to exhaust resources; DDoS uses a **botnet** of compromised hosts | ⭐ **Availability** |
| ⭐ **Phishing / spear phishing / vishing** | Social engineering to steal credentials | Confidentiality |
| ⭐ **Man-in-the-Middle (MITM)** | Intercept/alter traffic between two parties | Confidentiality, integrity |
| ⭐ **Ransomware** | Encrypts victim data and demands payment | Availability |
| **Malware** | Virus (needs a host, needs a trigger) · **worm** (⭐ **self-replicating, spreads by itself**) · trojan · spyware · rootkit · **logic bomb** · botnet | Various |
| **Password attacks** | Brute force · dictionary · ⭐ **rainbow tables** (defeated by salting) · credential stuffing | |
| **Privilege escalation** | Vertical (gain higher rights) / horizontal (access a peer's data) | |
| **Zero-day** | Exploits an unpatched, undisclosed vulnerability | |
| **Replay attack** | Re-sends captured valid data (defence: nonces, timestamps) | |
| **Insider threat** | | |

⚠ **Virus vs worm:** a virus needs a host file and user action; a **worm self-propagates** across networks.

**Defensive controls:**

| Control | Function |
|---|---|
| ⭐ **Firewall** | Filters traffic by rules. **Packet filter** (stateless, L3/L4) · ⭐ **stateful inspection** · **application/proxy** · **NGFW**. ⭐ **WAF** protects web apps specifically (SQLi/XSS) |
| ⭐ **IDS vs IPS** | ⭐ **IDS detects and alerts (passive); IPS detects and BLOCKS (inline, active)** |
| **VPN** | Encrypted tunnel over a public network (IPsec, SSL/TLS) |
| **Antivirus / EDR** | Signature and behaviour-based malware defence |
| **DMZ** | A screened subnet for public-facing servers |
| ⭐ **MFA / 2FA** | Two or more of: something you **know**, **have**, **are** |
| **SIEM, honeypot, sandboxing, air gap, RBAC, DLP** | |

⚠ **IDS alerts, IPS blocks.** A one-word difference that is worth a mark.

### 13.5 Indian cyber law and institutions ⭐
⭐ **IT Act, 2000** (amended 2008) — India's primary cyber law. Key sections: **43** (damage to computer systems, civil) · **65** (tampering with source code) · **66** (computer-related offences) · **66C** (identity theft) · **66D** (cheating by personation) · **66E** (violation of privacy) · **66F** (cyber terrorism) · **67** (obscene material) · **69** (interception/decryption powers) · **70** (protected systems) · **72** (breach of confidentiality) · **43A** (compensation for failure to protect data). Recognises **digital/electronic signatures** and electronic records.
⭐ **DPDP Act, 2023** — Digital Personal Data Protection Act; data fiduciary/principal, consent, purpose limitation, Data Protection Board.
⭐ **CERT-In** — Indian Computer Emergency Response Team (national nodal agency for cyber incidents; mandatory 6-hour incident reporting).
Also: **NCIIPC** (critical information infrastructure) · **Cyber Swachhta Kendra** · **I4C** (Indian Cyber Crime Coordination Centre) · **National Cyber Security Policy 2013**.

---

## 14. ⭐ IoT (Internet of Things)

📌 **IoT** = a network of physical objects embedded with sensors, software and connectivity that collect and exchange data.

### 14.1 ⭐ Architecture layers

| Layer | Function |
|---|---|
| ⭐ **1. Perception / Sensing** | Sensors and actuators — collect physical data, act on the environment |
| ⭐ **2. Network / Transport** | Connectivity — gateways, WiFi, cellular, LPWAN |
| **3. Processing / Middleware** | Data storage, analytics, edge/fog processing, device management |
| ⭐ **4. Application** | End-user services and interfaces |
| (5. Business) | Business models, dashboards |

⚠ **Sensor vs actuator:** a **sensor** converts a physical quantity into a signal (input); an **actuator** converts a signal into physical action (output).

### 14.2 ⭐⭐ Protocols

| Protocol | Model | Transport | Note |
|---|---|---|---|
| ⭐ **MQTT** | ⭐ **Publish/Subscribe** (via a **broker**) | TCP | ⭐ **The most-cited IoT protocol** — lightweight, designed for constrained devices and unreliable networks; QoS levels 0/1/2 |
| ⭐ **CoAP** | ⭐ **Request/Response (REST-like)** | ⭐ **UDP** | Constrained Application Protocol; HTTP-like for tiny devices |
| **AMQP** | Message queuing | TCP | Enterprise messaging, reliable |
| **HTTP/HTTPS** | Request/Response | TCP | Heavy for constrained devices |
| **XMPP** | Messaging | TCP | |

⭐ **MQTT is publish/subscribe over TCP with a broker; CoAP is request/response over UDP.** That contrast is the standard question.

**Connectivity technologies:** ⭐ **Zigbee** (802.15.4, low-power mesh) · ⭐ **BLE** (Bluetooth Low Energy) · Z-Wave · WiFi · **LoRaWAN** and **NB-IoT** / LTE-M (LPWAN — long range, very low power, low data rate) · RFID · NFC · 5G (mMTC).
**Hardware:** Arduino (microcontroller) · Raspberry Pi (single-board computer) · ESP32/ESP8266.

### 14.3 ⭐ IoT security concerns
⭐ **Weak/default credentials** (the Mirai botnet exploited exactly this) · unencrypted communication · no secure firmware update mechanism · huge attack surface and device count · physical accessibility · limited compute for cryptography · privacy of continuously collected data · botnet recruitment for DDoS · long device lifecycles with no vendor patching.

**Applications:** smart home · smart city (traffic, lighting, waste) · industrial IoT / Industry 4.0 · precision agriculture · healthcare/wearables · smart grid and metering · logistics and asset tracking · connected vehicles.
⭐ **Digital twin:** a live virtual replica of a physical asset, fed by IoT data.

---

## 15. ⭐ Blockchain

📌 ⭐ **A blockchain is a distributed, append-only ledger of transactions, replicated across nodes, in which blocks are cryptographically chained together.**

### 15.1 ⭐⭐ Structure and immutability

⭐ **Each block contains:** a **block header** with the ⭐ **hash of the previous block**, a **timestamp**, a **Merkle root** of the transactions, a **nonce** and difficulty target — plus the transaction list.

⭐⭐ **Why it is immutable:** each block stores the **cryptographic hash of its predecessor**. Altering any past block changes its hash, which invalidates the "previous hash" stored in the next block, and so on — **breaking the entire chain from that point forward**. The distributed network detects the mismatch immediately, and an attacker would have to redo the proof-of-work for every subsequent block **faster than the honest majority**.

⭐ **Merkle tree (hash tree):** transactions are hashed in pairs up to a single **Merkle root**, allowing efficient verification that a transaction is included without downloading the whole block.

### 15.2 ⭐ Key properties
⭐ **Decentralisation** (no single trusted authority) · ⭐ **immutability / tamper-evidence** · **transparency** · **distributed consensus** · **provenance/auditability** · pseudonymity · availability.

### 15.3 ⭐⭐ Consensus mechanisms

| Mechanism | How | Notes |
|---|---|---|
| ⭐ **PoW (Proof of Work)** | Miners race to find a nonce making the block hash below a target | ⭐ **Bitcoin**; secure but ⭐ **enormously energy-intensive**; vulnerable in theory to a **51% attack** |
| ⭐ **PoS (Proof of Stake)** | Validators are chosen in proportion to the stake they lock up | ⭐ **Ethereum (post-Merge)**; ⭐ **far more energy-efficient** |
| **DPoS** | Stakeholders elect delegates | Faster |
| **PBFT** | Byzantine fault-tolerant voting | Permissioned; tolerates <1/3 faulty nodes |
| **PoA / PoET / PoB** | Authority / elapsed time / burn | Various |

⭐ **PoW vs PoS:** the standard contrast is **energy consumption** — PoS eliminates the computational race.

### 15.4 ⭐ Types of blockchain

| Type | Access |
|---|---|
| ⭐ **Public / permissionless** | Anyone can read, write and validate (Bitcoin, Ethereum) |
| ⭐ **Private / permissioned** | Restricted participants, known identities (Hyperledger Fabric) |
| **Consortium / federated** | Governed by a group of organisations |
| **Hybrid** | Mixed |

### 15.5 ⭐ Smart contracts
📌 ⭐ **Self-executing code stored on the blockchain that runs automatically when predefined conditions are met** — "code is law", no intermediary needed.
Platform: ⭐ **Ethereum**, written in **Solidity**, executed by the **EVM**; gas fees meter computation.
⚠ Bugs are permanent because the code is immutable (the DAO hack).
**Applications:** supply-chain traceability · land records · digital identity · trade finance · voting · healthcare records · **DeFi** · NFTs.
**Trade-offs:** ⭐ **the scalability trilemma** (decentralisation vs security vs scalability) · low throughput · storage growth · regulatory uncertainty · energy (PoW).
Related terms: cryptocurrency · wallet (public/private keys) · **51% attack** · fork (soft/hard) · **DLT** (distributed ledger technology — the broader category) · layer-2 solutions.

---

## 16. ⭐ Artificial Intelligence

### 16.1 ⭐⭐ AI vs ML vs Deep Learning

📌 ⭐ **AI ⊃ Machine Learning ⊃ Deep Learning** — nested subsets.

| Term | Definition |
|---|---|
| ⭐ **AI** | The broad field of making machines exhibit intelligent behaviour (includes rule-based/expert systems, search, planning, logic — **not only learning**) |
| ⭐ **ML** | Systems that ⭐ **learn patterns from data** rather than being explicitly programmed |
| ⭐ **Deep Learning** | ML using ⭐ **multi-layer (deep) neural networks**; learns features automatically |

⭐ **Narrow (weak) AI** — task-specific, everything in use today. **General AI (AGI)** — human-level breadth, hypothetical. **Super AI** — beyond human, hypothetical.
⭐ **Turing Test** (1950) — a behavioural test of machine intelligence. The term "artificial intelligence" was coined at the **Dartmouth Conference, 1956** (John McCarthy).

### 16.2 ⭐⭐ Types of machine learning

| Type | Data | Goal | Algorithms | Examples |
|---|---|---|---|---|
| ⭐ **Supervised** | ⭐ **Labelled** | Predict a label/value | Linear & logistic regression, decision trees, random forest, SVM, k-NN, naïve Bayes, neural networks | Spam detection, price prediction, image classification |
| ⭐ **Unsupervised** | ⭐ **Unlabelled** | Find structure | ⭐ **k-means**, hierarchical clustering, DBSCAN, **PCA**, apriori | Customer segmentation, anomaly detection, market-basket analysis |
| **Semi-supervised** | Mixed | Use unlabelled data to help | | |
| ⭐ **Reinforcement learning** | ⭐ **Reward signal from an environment** | Learn a policy maximising cumulative reward | Q-learning, SARSA, deep Q-networks, policy gradients | Game playing (AlphaGo), robotics, control |

⭐ **Supervised = labelled data; unsupervised = unlabelled; reinforcement = reward/penalty feedback.** This three-way split is the most-asked AI question.
⭐ **Classification** predicts a **discrete** class; ⭐ **regression** predicts a **continuous** value. **Clustering** is the unsupervised analogue of classification.

### 16.3 ⭐ Neural networks
**Structure:** input layer → hidden layer(s) → output layer, connected by **weighted** edges with **biases**.
**Neuron/perceptron:** computes a weighted sum then applies an **activation function**.
⭐ **Activation functions:** **sigmoid** (0–1) · **tanh** (−1 to 1) · ⭐ **ReLU** (max(0,x) — the modern default, avoids vanishing gradients) · **softmax** (multi-class output probabilities).
⭐ **Training:** **forward propagation** → compute a **loss** → ⭐ **backpropagation** (compute gradients by the chain rule) → **gradient descent** updates the weights. Hyperparameters: learning rate, epochs, batch size.

**Architectures:**
- ⭐ **CNN (Convolutional NN)** — ⭐ **images/vision**; convolution + pooling layers exploit spatial locality
- ⭐ **RNN / LSTM / GRU** — ⭐ **sequences** (text, speech, time series); LSTM addresses the vanishing-gradient problem
- ⭐ **Transformer** — attention-based; the basis of modern **LLMs** (BERT, GPT); parallelisable, handles long-range dependencies
- **GAN** — generator vs discriminator, for synthesis
- Autoencoder — dimensionality reduction, denoising

### 16.4 ⭐ Model evaluation

📌 **Confusion matrix:** TP, TN, FP (Type I error), FN (Type II error)
📌 ⭐ **Accuracy = (TP + TN)/Total**
📌 ⭐ **Precision = TP/(TP + FP)** — of those predicted positive, how many really were
📌 ⭐ **Recall (sensitivity) = TP/(TP + FN)** — of the actual positives, how many were found
📌 ⭐ **F1 score = 2·(Precision × Recall)/(Precision + Recall)** — the harmonic mean

⚠ ⭐ **Accuracy is misleading on imbalanced data** (99% accuracy is trivial if 99% of cases are negative) — use precision, recall, F1 or AUC-ROC.

⭐ **Overfitting vs underfitting:**

| | ⭐ **Overfitting** | ⭐ **Underfitting** |
|---|---|---|
| Training error | ⭐ **Low** | High |
| Test error | ⭐ **High** | High |
| Cause | Model too complex; memorises noise | Model too simple |
| Fixes | ⭐ **More data, regularisation (L1/L2), dropout, early stopping, cross-validation, simpler model** | More complex model, better features, train longer |

📌 ⭐ **Bias–variance trade-off:** underfitting = high bias; overfitting = high variance.
**Data splits:** training / validation / test; **k-fold cross-validation**.

### 16.5 ⭐ Applications and subfields
⭐ **NLP** (translation, sentiment analysis, chatbots, LLMs) · ⭐ **Computer vision** (object detection, face recognition, OCR) · speech recognition and synthesis · recommender systems · robotics · expert systems · **generative AI** · autonomous vehicles · fraud detection · medical diagnosis · predictive maintenance.

⭐ **AI ethics and governance:** algorithmic **bias and fairness** · **explainability/XAI** (the "black box" problem) · privacy · accountability · job displacement · deepfakes and misinformation · **hallucination** in generative models.

⭐ **Indian AI/digital policy context** (worth knowing for both Paper-II §13 and Paper-I current affairs):
**IndiaAI Mission** · **NITI Aayog's National Strategy for AI (#AIforAll)** and **Responsible AI** principles · **Digital India** · **Digital Personal Data Protection Act 2023** · **India Semiconductor Mission** · **ONDC**, **UPI**, **Aadhaar**, **DigiLocker**, **UMANG** (India Stack) · **BharatNet** · **National Supercomputing Mission (PARAM)** · **MeitY** as the nodal ministry.

---

## 17. Rapid-fire facts ⭐

### Web

| Fact | Value |
|---|---|
| HTML5 semantic tags | article, section, header, footer, nav, aside |
| Non-semantic | div, span |
| Box model order | content → padding → border → margin |
| Highest CSS specificity | !important > inline > ID > class > element |
| Direct child selector | `A > B` |
| Responsive design uses | Media queries |
| localStorage vs sessionStorage | Persistent vs per-tab |
| Cookie size limit | ~4 KB, sent with every request |
| Well-formed vs valid XML | Syntax vs conforms to DTD/XSD |
| XSD written in | XML |
| Transforms XML | XSLT |
| Navigates XML | XPath |
| Load balancing proxy | **Reverse** proxy |
| Hides client | **Forward** proxy |
| Static content server | Web server |
| Business logic server | Application server |
| MVC: handles input | Controller |
| REST vs SOAP | Style vs protocol |
| SOAP contract | WSDL |
| SOAP discovery | UDDI |
| Idempotent: PUT / POST | Yes / No |
| AJAX | Async requests without page reload |
| React vs Angular | Library vs framework |

### Cloud

| Fact | Value |
|---|---|
| NIST essential characteristics | 5 (on-demand, broad access, pooling, elasticity, measured) |
| Customer manages OS in | IaaS |
| Gmail / Salesforce | SaaS |
| Heroku / App Engine | PaaS |
| Type-1 hypervisor | Bare metal (ESXi, Hyper-V, Xen, KVM) |
| Type-2 hypervisor | Hosted (VirtualBox, VMware Workstation) |
| Containers share | Host OS kernel |
| Stronger isolation | VMs |
| Container orchestration | Kubernetes |
| Smallest K8s unit | Pod |
| Databases need | Block storage |
| S3 / Azure Blob | Object storage (flat, HTTP) |
| Scale out | Horizontal |
| Edge computing motive | Reduce latency and bandwidth |
| Fog layer | Between edge and cloud (gateways) |
| Govt of India cloud | MeghRaj |

### Security & Emerging

| Fact | Value |
|---|---|
| OWASP A01 (2021) | Broken Access Control |
| OWASP A03 (2021) | Injection |
| SQL injection fix | Parameterised queries |
| XSS executes in | The victim's browser |
| XSS defence | Output encoding + CSP |
| CSRF defence | Anti-CSRF tokens, SameSite |
| Symmetric keys for n users | n(n−1)/2 |
| Asymmetric keys for n users | 2n |
| Current symmetric standard | AES |
| RSA is based on | Integer factorisation |
| Digital signature uses | Sender's **private** key |
| Signature provides | Authentication, integrity, non-repudiation (**not** confidentiality) |
| Broken hashes | MD5, SHA-1 |
| Password storage | bcrypt/Argon2 + salt |
| CIA triad | Confidentiality, Integrity, Availability |
| DDoS targets | Availability |
| Self-replicating malware | Worm |
| IDS vs IPS | Detects/alerts vs blocks |
| India's cyber law | IT Act 2000 |
| National CERT | CERT-In |
| MQTT | Pub/sub, TCP, broker |
| CoAP | Request/response, UDP |
| IoT layer 1 | Perception/sensing |
| Blockchain immutability from | Previous-block hash chaining |
| Bitcoin consensus | PoW |
| Energy-efficient consensus | PoS |
| Self-executing blockchain code | Smart contract |
| Ethereum contract language | Solidity |
| Supervised learning needs | Labelled data |
| Clustering (k-means) | Unsupervised |
| Learns from rewards | Reinforcement learning |
| CNN for | Images |
| RNN/LSTM for | Sequences |
| LLMs built on | Transformers |
| Precision | TP/(TP+FP) |
| Recall | TP/(TP+FN) |
| Low train error, high test error | Overfitting |
| Overfitting fix | Regularisation, dropout, more data |

---

## 18. Common traps ⚠

1. ⭐ **REST is an architectural style; SOAP is a protocol.**
2. ⭐ **Reverse proxy = in front of servers (load balancing); forward proxy = in front of clients (anonymity).**
3. ⭐ **Box model: padding is inside the border, margin outside.**
4. **Every valid XML document is well-formed, but not vice versa.**
5. **PUT is idempotent; POST is not.**
6. **localStorage persists; sessionStorage dies with the tab.**
7. ⭐ **In IaaS the customer patches the guest OS**, not the provider.
8. ⭐ **Containers are lighter; VMs isolate better.**
9. **Object storage is flat and HTTP-accessed; block storage is for databases.**
10. **Edge < Fog < Cloud** in both latency and compute power.
11. ⭐ **Broken Access Control is A01 in OWASP 2021; Injection dropped to A03.**
12. ⭐ **Digital signatures use the sender's PRIVATE key** — and give no confidentiality.
13. ⭐ **Hashing is one-way; encryption is reversible; encoding is neither.**
14. **IDS alerts; IPS blocks.**
15. **A worm self-replicates; a virus needs a host.**
16. **MQTT is pub/sub over TCP; CoAP is request/response over UDP.**
17. ⭐ **Blockchain immutability comes from hash chaining**, not from encryption.
18. **PoS saves energy; PoW consumes it.**
19. ⭐ **AI ⊃ ML ⊃ Deep Learning** — not the reverse, and AI is not only ML.
20. **k-means is unsupervised**, not supervised.
21. **Overfitting = low training error but high test error.**
22. **Accuracy is a poor metric on imbalanced datasets.**

---

## 19. Practice

- Web: [`Paper2_S12_Web_Technologies/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S12_Web_Technologies/) — 65 questions
- Cloud: [`Paper2_S14_Cloud_Technology/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S14_Cloud_Technology/) — only 8 questions
- Security/Emerging: [`Paper2_S13_Cyber_Security_and_Emerging_Tech/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S13_Cyber_Security_and_Emerging_Tech/) — 66 questions
- ⭐ Also: `02_State_PSC_PYQs/Papers/Other_State_PSCs/Arunachal_Pradesh_PSC/APPSC_2021_AssistantSystemManager_PracticalProgramming_and_WebDesign.pdf` — a full paper on web design
- ⚠ **No GATE coverage exists for any of these three sections.**
- Test: [`Week_10_Test.md`](../04_Mock_Tests/Week_10_Test.md)

**Because the PYQ pool is thin here, these notes are your primary source.** Read them twice rather than hunting for more questions.

**Priority order if short on time:** IaaS/PaaS/SaaS responsibility split → OWASP Top 10 by name → SQL injection & XSS defences → symmetric vs asymmetric + digital signatures → MVC → REST vs SOAP → forward vs reverse proxy → CSS box model & specificity → VMs vs containers → storage types → edge computing → supervised/unsupervised/reinforcement → blockchain immutability & PoW/PoS → MQTT/CoAP.
