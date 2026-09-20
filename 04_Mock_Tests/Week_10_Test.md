# Week 10 Question Bank — Web Technologies + Cloud + Cyber Security & Emerging Tech

**Syllabus §12 + §14 + §13** · 186 questions · Practice set · +1 / −0.33 marking

> These three sections are purely definitional and carry ~15 marks with almost no GATE overlap — the cheapest, highest-yield marks in Paper-II. Grouped by subtopic; attempt in blocks and check the key at the end.

---

## Part A — HTML5

**Q1.** Which of the following is a **semantic** element introduced in HTML5?
(A) `<div>`  (B) `<span>`  (C) `<article>`  (D) `<font>`

**Q2.** The elements `<div>` and `<span>` are best described as
(A) semantic elements  (B) deliberately non-semantic generic containers  (C) deprecated presentational tags  (D) metadata elements

**Q3.** Which element is a deprecated **presentational** tag whose styling role is now handled by CSS?
(A) `<article>`  (B) `<nav>`  (C) `<font>`  (D) `<main>`

**Q4.** Which HTML5 graphics element is **vector**-based, scalable without loss, and represents each shape as a DOM element?
(A) `<canvas>`  (B) `<svg>`  (C) `<img>`  (D) `<picture>`

**Q5.** Which HTML5 element provides a **bitmap** drawing surface scripted with JavaScript (used for games and charts)?
(A) `<svg>`  (B) `<canvas>`  (C) `<figure>`  (D) `<video>`

**Q6.** The HTML5 `<audio>` and `<video>` elements are significant because they
(A) require the Flash plugin  (B) provide native media playback with **no plugin needed**  (C) work only in Internet Explorer  (D) render vector graphics

**Q7.** Which of the following is a **new HTML5 input type** offering built-in browser validation?
(A) `email`  (B) `label`  (C) `textarea`  (D) `fieldset`

**Q8.** Which web-storage mechanism **persists until explicitly cleared**, surviving a browser restart?
(A) `sessionStorage`  (B) `localStorage`  (C) a session cookie  (D) the HTTP cache

**Q9.** Which client-side storage is **cleared when the tab/session closes**?
(A) `localStorage`  (B) `sessionStorage`  (C) a persistent cookie  (D) IndexedDB

**Q10.** Which storage mechanism is limited to about **4 KB** and is automatically **sent to the server with every HTTP request**?
(A) `localStorage`  (B) `sessionStorage`  (C) cookies  (D) Web SQL

**Q11.** Which statement about client-side storage is correct?
(A) `localStorage` is sent to the server on every request  (B) only cookies are automatically sent to the server with each request  (C) `sessionStorage` survives a browser restart  (D) cookies can hold ~10 MB

**Q12.** In an HTML form, which method places the data in the **request body** with no practical size limit and is used for logins and uploads?
(A) `GET`  (B) `POST`  (C) `HEAD`  (D) `TRACE`

---

## Part B — CSS3

**Q13.** The recommended **best practice** for applying CSS across many pages is
(A) inline styles  (B) an internal `<style>` block  (C) an external stylesheet linked with `<link>`  (D) the `style` attribute on every tag

**Q14.** Which represents the correct CSS **specificity** order, highest to lowest?
(A) element > class > ID > inline > !important
(B) !important > inline style > ID > class > element > universal
(C) universal > element > class > ID > inline
(D) inline > !important > class > ID > element

**Q15.** Ignoring `!important` and inline styles, which selector has the **highest** specificity?
(A) element selector (`p`)  (B) class selector (`.lead`)  (C) ID selector (`#intro`)  (D) universal selector (`*`)

**Q16.** In the CSS box model, the correct order of layers from the content **outwards** is
(A) content → border → padding → margin
(B) content → padding → border → margin
(C) margin → border → padding → content
(D) padding → content → border → margin

**Q17.** In the CSS box model, the **padding** is located
(A) outside the border, like the margin  (B) inside the border, between content and border  (C) in the same position as the margin  (D) outside the margin

**Q18.** With `box-sizing: content-box`, an element has `width:200px; padding:10px; border:5px`. Its **rendered element width** is
(A) 200 px  (B) 210 px  (C) 230 px  (D) 250 px

**Q19.** When two CSS rules have **equal specificity**, which one wins?
(A) the earlier rule in the source  (B) the rule appearing **later** in the source  (C) the one with the shorter selector  (D) it is chosen at random

**Q20.** Which CSS selector matches **only the direct children** of an element?
(A) `A B`  (B) `A > B`  (C) `A + B`  (D) `A ~ B`

**Q21.** The core mechanism that makes a responsive layout adapt to the viewport is the
(A) `<table>` element  (B) **media query**  (C) `<frame>` element  (D) inline style

**Q22.** "**Mobile-first**" responsive design means
(A) designing for desktop first, then stripping features away
(B) writing the smallest-screen styles first and adding complexity upward with `min-width` queries
(C) building a completely separate mobile website
(D) using fixed pixel widths everywhere

**Q23.** Which correctly states the dimensionality of Flexbox and CSS Grid?
(A) Flexbox is 2-D; Grid is 1-D  (B) Flexbox is 1-D (a row or column); Grid is 2-D (rows and columns)  (C) both are 1-D  (D) both are 2-D

**Q24.** Which `position` value **removes an element from the normal document flow** and positions it relative to the nearest positioned ancestor?
(A) `static`  (B) `relative`  (C) `absolute`  (D) `sticky`

---

## Part C — XML

**Q25.** An XML document that obeys XML's syntax rules but has **not** been checked against any DTD or schema is said to be
(A) valid  (B) well-formed  (C) normalised  (D) parsed

**Q26.** Which statement about XML is correct?
(A) every well-formed document is automatically valid
(B) every valid document is well-formed, but not every well-formed document is valid
(C) validity and well-formedness are identical
(D) a valid document need not be well-formed

**Q27.** Which is TRUE of **XSD** compared with **DTD**?
(A) XSD uses a non-XML syntax  (B) XSD is **written in XML** and supports rich data types  (C) DTD supports data types but XSD does not  (D) neither supports namespaces

**Q28.** Which supports **rich data types** such as integer, date and decimal?
(A) DTD  (B) XSD  (C) both equally  (D) neither

**Q29.** Which pairing is correct?
(A) XSLT navigates nodes; XPath transforms documents
(B) XSLT **transforms** XML into another format; XPath **navigates/queries** nodes
(C) both transform documents  (D) both only navigate

**Q30.** Which describes **SAX** parsing?
(A) builds the whole document tree in memory with random access
(B) event-driven, streaming, forward-only and low-memory
(C) writes new XML files  (D) validates only against an XSD

**Q31.** Which is TRUE of **JSON** compared with **XML**?
(A) JSON supports comments while XML does not
(B) JSON is more compact and native to JavaScript
(C) JSON requires matching closing tags
(D) XML is the usual format for modern REST APIs

**Q32.** A well-formed XML document must contain exactly
(A) one root element  (B) a DTD  (C) an XSD  (D) two root elements

---

## Part D — Client–Server Computing, Servers & Proxies

**Q33.** The three tiers of the standard **3-tier** web architecture are
(A) client, proxy, cache
(B) presentation, application (business logic), and data
(C) HTML, CSS, JavaScript
(D) web, mail, DNS

**Q34.** A browser-based **thin client** is characterised by
(A) heavy local processing and offline operation
(B) minimal local processing, reliance on the server, and a need for constant connectivity
(C) holding direct database credentials
(D) requiring no server at all

**Q35.** Which server primarily serves **static content** over HTTP (HTML, CSS, images)?
(A) application server  (B) web server (Apache, Nginx, IIS)  (C) database server  (D) mail server

**Q36.** Tomcat, JBoss/WildFly and WebLogic are examples of
(A) web servers  (B) application servers that run business logic  (C) proxy servers  (D) database servers

**Q37.** A **forward proxy**
(A) sits in front of the servers and provides load balancing
(B) sits in front of the clients and hides the client's identity from the server
(C) resolves domain names to IP addresses
(D) hosts the database

**Q38.** Which server type provides **load balancing**, SSL termination and caching while hiding the backend servers from clients?
(A) forward proxy  (B) reverse proxy  (C) DNS server  (D) file server

**Q39.** In a **2-tier** ("fat client") architecture, a key drawback is that
(A) the server holds all business logic
(B) the client holds business logic and needs direct database credentials, so changes require redeployment
(C) there is no database
(D) it cannot connect to a network

**Q40.** Which statement correctly separates the roles of a web server and an application server?
(A) both only serve static files
(B) a web server handles HTTP and serves files; an application server executes application code
(C) an application server serves only images
(D) a web server runs the business logic

---

## Part E — MVC Architecture

**Q41.** In MVC, the component that **handles user input**, invokes model operations and selects which view to render is the
(A) Model  (B) View  (C) Controller  (D) Router

**Q42.** Which MVC component holds the **data and business logic** and knows nothing about the UI?
(A) Model  (B) View  (C) Controller  (D) Template

**Q43.** In MVC, the component responsible for **presentation / rendering the UI** is the
(A) Model  (B) View  (C) Controller  (D) Service

---

## Part F — Web Services & APIs

**Q44.** Which statement correctly distinguishes **REST** from **SOAP**?
(A) REST is a protocol; SOAP is an architectural style
(B) REST is an architectural style (often JSON, stateless); SOAP is a protocol (XML messaging, WSDL)
(C) both are protocols using XML only
(D) REST mandates WSDL; SOAP does not

**Q45.** The SOAP message format is
(A) JSON only  (B) XML only, using an Envelope with Header and Body  (C) plain text  (D) HTML

**Q46.** In SOAP web services, **WSDL** is
(A) a registry used for discovery
(B) the machine-readable XML **contract** describing operations, messages and the endpoint
(C) the encrypted payload
(D) a transport protocol

**Q47.** **UDDI** is used for
(A) transforming XML  (B) discovering and registering web services  (C) encrypting SOAP messages  (D) styling web pages

**Q48.** A core REST constraint is that each request is
(A) stateful and tied to a server-side session
(B) **stateless** — it carries everything needed and the server keeps no session state
(C) always cached indefinitely
(D) always formatted as XML

**Q49.** Which statement about HTTP method **idempotency** is correct?
(A) POST is idempotent, PUT is not
(B) PUT is idempotent, POST is not
(C) both PUT and POST are idempotent
(D) neither PUT nor POST is idempotent

**Q50.** **CORS** (Cross-Origin Resource Sharing) is
(A) a database index type
(B) the browser rule governing whether a page from one origin may call another origin
(C) an encryption cipher
(D) a CSS layout module

**Q51.** The main advantage of **GraphQL** over a typical REST API is that
(A) it uses XML envelopes
(B) a single endpoint lets the client specify exactly which fields it wants, avoiding over-fetching
(C) it is always stateful
(D) it requires a WSDL contract

---

## Part G — Frontend Technologies

**Q52.** In JavaScript, the `===` operator
(A) performs type coercion before comparing
(B) compares both value and type, with no coercion
(C) assigns a value
(D) behaves identically to `==`

**Q53.** Which is TRUE of `let`/`const` versus `var` in JavaScript?
(A) `var` is block-scoped while `let` is function-scoped
(B) `let` and `const` are block-scoped, whereas `var` is function-scoped and hoisted
(C) all three are block-scoped
(D) `const` is function-scoped

**Q54.** The DOM (Document Object Model) is
(A) part of the JavaScript language core
(B) a W3C standard API provided by the **browser**, not part of the JavaScript language
(C) a CSS feature
(D) a server-side database engine

**Q55.** Despite its name, **AJAX** today usually exchanges data in
(A) XML  (B) JSON  (C) CSV  (D) raw binary

**Q56.** Which statement is correct?
(A) React is a full framework; Angular is a library
(B) React is a **library** using a virtual DOM; Angular is a **framework** with two-way data binding
(C) both are frameworks with two-way binding
(D) both are libraries with no data flow model

**Q57.** A **JWT** (JSON Web Token) enables
(A) stateful server-side sessions only
(B) **stateless authentication** via a self-contained, digitally signed token (header.payload.signature)
(C) encryption of the entire database
(D) client-side CSS styling

---

## Part H — Cloud Fundamentals & Service Models

**Q58.** Which of the following is **NOT** one of the NIST five essential characteristics of cloud computing?
(A) on-demand self-service  (B) rapid elasticity  (C) permanent local storage  (D) measured service

**Q59.** The NIST characteristic in which the provider's hardware is shared among many customers is called
(A) broad network access  (B) resource pooling (multi-tenancy)  (C) measured service  (D) on-demand self-service

**Q60.** A customer who rents virtual machines, storage and networking, and manages the operating system and applications themselves, is using
(A) SaaS  (B) PaaS  (C) IaaS  (D) FaaS

**Q61.** In the **IaaS** model, who is responsible for **patching the guest operating system**?
(A) the cloud provider  (B) the customer  (C) nobody — it is automatic  (D) the hardware vendor

**Q62.** In **PaaS**, the customer typically manages
(A) nothing at all  (B) only the applications and data  (C) the OS, runtime and applications  (D) the virtualisation layer

**Q63.** Gmail, Salesforce and Office 365 are examples of which cloud service model?
(A) IaaS  (B) PaaS  (C) SaaS  (D) DaaS

**Q64.** AWS EC2, Azure VMs and Google Compute Engine are examples of
(A) IaaS  (B) PaaS  (C) SaaS  (D) FaaS

**Q65.** Heroku, Google App Engine and AWS Elastic Beanstalk are examples of
(A) IaaS  (B) PaaS  (C) SaaS  (D) IaaS + SaaS

**Q66.** In the **SaaS** model, the customer manages
(A) the operating system and runtime
(B) essentially nothing beyond their own data and configuration
(C) the virtualisation layer
(D) the physical servers

**Q67.** The NIST characteristic of usage being **metered and billed** ("pay-per-use") is called
(A) rapid elasticity  (B) measured service  (C) resource pooling  (D) broad network access

**Q68.** "You provision computing resources yourself, instantly, with no human involvement on the provider's side" describes
(A) measured service  (B) on-demand self-service  (C) resource pooling  (D) broad network access

**Q69.** The NIST characteristic that allows resources to scale up and down quickly and automatically is
(A) resource pooling  (B) rapid elasticity  (C) measured service  (D) broad network access

---

## Part I — Cloud Deployment, Scaling & Economics

**Q70.** The four main cloud **deployment models** are
(A) IaaS, PaaS, SaaS, FaaS
(B) public, private, hybrid, community
(C) hot, cool, cold, archive
(D) block, file, object, tiered

**Q71.** Which deployment model gives an organisation **maximum control and security** but the highest cost and least elasticity benefit?
(A) public cloud  (B) private cloud  (C) hybrid cloud  (D) community cloud

**Q72.** A bank keeps customer records in a dedicated private cloud (for regulation) while running its public website in a public cloud. This is a
(A) public cloud  (B) private cloud  (C) hybrid cloud  (D) community cloud

**Q73.** Several state government departments share one cloud built to common government security standards. This is a
(A) public cloud  (B) private cloud  (C) hybrid cloud  (D) community cloud

**Q74.** **Vertical scaling** (scaling up) means
(A) adding more machines behind a load balancer
(B) making a single machine bigger (more CPU/RAM)
(C) moving to another provider
(D) deleting instances

**Q75.** **Horizontal scaling** (scaling out) — the practical meaning of cloud elasticity — means
(A) making one server more powerful
(B) adding more machines, usually behind a load balancer
(C) upgrading the operating system
(D) increasing disk size only

**Q76.** A **99.9% ("three nines")** SLA corresponds to roughly how much downtime per year?
(A) ~5 minutes  (B) ~53 minutes  (C) ~8.8 hours  (D) ~3.65 days

**Q77.** Which is most often cited as a **drawback** of public cloud computing?
(A) unlimited free capacity  (B) vendor lock-in and data sovereignty concerns  (C) no need for internet  (D) permanent dedicated hardware

**Q78.** A major stated **benefit** of cloud computing over owning hardware is that
(A) capital expenditure (CapEx) is replaced by operating expenditure (OpEx)
(B) the network is no longer needed
(C) all data automatically stays within the country
(D) there is never any downtime

---

## Part J — Virtualisation, Containers & Orchestration

**Q79.** Virtualisation is best defined as
(A) deleting physical servers
(B) creating a software abstraction of physical resources so one machine appears as many
(C) a network routing protocol
(D) a type of database

**Q80.** A **type-1** hypervisor
(A) runs directly on the bare-metal hardware
(B) runs as an application on top of a host operating system
(C) is used only for containers
(D) cannot support multiple guest OSs

**Q81.** VirtualBox and VMware Workstation/Player are examples of
(A) type-1 (bare-metal) hypervisors  (B) type-2 (hosted) hypervisors  (C) container engines  (D) load balancers

**Q82.** Which are examples of **type-1 (bare-metal)** hypervisors?
(A) VirtualBox and Parallels  (B) VMware ESXi, Microsoft Hyper-V, Xen and KVM  (C) Docker and Podman  (D) Apache and Nginx

**Q83.** Compared with virtual machines, **containers**
(A) each include a full guest operating system
(B) share the host OS kernel and are therefore lighter and faster to start
(C) provide stronger hardware-level isolation
(D) cannot be orchestrated

**Q84.** Which provides **stronger, hardware-level isolation** between workloads?
(A) containers  (B) virtual machines  (C) both are identical  (D) neither isolates

**Q85.** A key difference of a virtual machine from a container is that a VM
(A) shares the host kernel  (B) runs its own full guest operating system  (C) is measured in megabytes  (D) boots in milliseconds

**Q86.** In Docker terminology, the relationship between an **image** and a **container** is that
(A) a container is an immutable template and an image is a running instance
(B) an image is an immutable template and a container is a running instance of it
(C) they are identical  (D) an image can only run on bare metal

**Q87.** **Kubernetes** is primarily a system for
(A) container orchestration — automated deployment, scaling and self-healing
(B) writing HTML  (C) relational database storage  (D) encrypting network traffic

**Q88.** The **smallest deployable unit** in Kubernetes, holding one or more containers, is a
(A) node  (B) cluster  (C) pod  (D) namespace

---

## Part K — Compute, Storage, Network & Edge

**Q89.** Which storage type presents fixed-size **blocks** as a raw volume and is best for **databases** and low-latency random I/O?
(A) file storage  (B) object storage  (C) block storage  (D) archive storage

**Q90.** Which storage type organises data as **files in a directory hierarchy**, accessed via NFS/SMB?
(A) block storage  (B) file storage  (C) object storage  (D) tape storage

**Q91.** AWS S3, Azure Blob and Google Cloud Storage are examples of
(A) block storage  (B) file storage  (C) object storage  (D) database storage

**Q92.** Which is TRUE of **object storage**?
(A) it has a deep directory hierarchy and is mounted as a filesystem
(B) it uses a flat namespace and is accessed over HTTP/REST
(C) it is best for high-frequency random database writes
(D) it must be attached as a raw volume

**Q93.** A relational database needs which storage type for its frequent small random reads and writes?
(A) object storage  (B) block storage  (C) archive storage  (D) CDN cache

**Q94.** **SDN (Software-Defined Networking)** is characterised by
(A) merging the control and data planes into hardware
(B) separating the control plane (decision-making) from the data plane (packet forwarding)
(C) eliminating all switches
(D) encrypting every packet twice

**Q95.** A **CDN (Content Delivery Network)** primarily
(A) runs the application's business logic
(B) caches static content at edge locations near users to reduce latency
(C) stores relational databases
(D) provides identity management

**Q96.** **Edge computing** primarily aims to
(A) centralise all processing in one large data centre
(B) process data close to where it is generated, reducing latency and bandwidth use
(C) eliminate the need for any network
(D) replace all cloud storage

**Q97.** Which correctly orders **latency** from highest to lowest?
(A) Edge > Fog > Cloud  (B) Cloud > Fog > Edge  (C) Fog > Cloud > Edge  (D) all equal

**Q98.** In the cloud–fog–edge hierarchy, the **fog** layer sits
(A) in centralised data centres
(B) at an intermediate level — gateways, local routers and the LAN
(C) on the device itself
(D) outside any network

**Q99.** **MeghRaj** is
(A) a private company's cloud
(B) the Government of India cloud initiative (with the NIC National Cloud) under MeitY
(C) a blockchain network
(D) an encryption standard

---

## Part L — Secure Programming Techniques

**Q100.** The root cause of most serious application vulnerabilities is
(A) using too much memory
(B) trusting input that should not be trusted, letting data be interpreted as code
(C) writing comments in code
(D) using open-source libraries

**Q101.** Input validation should primarily be performed
(A) only on the client side, since it is faster
(B) on the server side, because client-side checks are trivially bypassed
(C) never — it slows the app
(D) only in the database

**Q102.** Why is an **allow-list** generally safer than a **deny-list** for input validation?
(A) it is shorter to write
(B) it defines exactly what is acceptable and rejects everything else, including unknown attacks
(C) it never needs updating
(D) it runs faster on the GPU

**Q103.** A **buffer overflow** occurs when
(A) a program runs out of disk space
(B) data is written past the end of a buffer, overwriting adjacent memory such as the return address
(C) a password is too long to type
(D) the network drops packets

**Q104.** Which are mitigations against **buffer overflow** exploitation?
(A) longer passwords  (B) ASLR, DEP/NX and stack canaries  (C) more RAM  (D) disabling the firewall

**Q105.** **STRIDE** is a framework used for
(A) encryption key exchange  (B) threat modelling  (C) load balancing  (D) container orchestration

**Q106.** Which correctly distinguishes **SAST** from **DAST**?
(A) SAST tests the running application; DAST scans source code
(B) SAST scans source code statically; DAST tests the running application dynamically
(C) both only scan source code
(D) both only test running apps

**Q107.** The security principle **"shift left"** means
(A) moving servers to a left-hand data centre
(B) finding and fixing security defects early in the development lifecycle
(C) shifting all logic to the client
(D) left-aligning the user interface

**Q108.** The principle **"no security through obscurity"** (open design) states that
(A) all code must be public
(B) security must not depend on the design being kept secret
(C) passwords should be short
(D) encryption is unnecessary

---

## Part M — OWASP Top 10, SQL Injection, XSS & CSRF

**Q109.** In the **OWASP Top 10 (2021)** edition, the category ranked **A01** is
(A) Injection  (B) Broken Access Control  (C) Cryptographic Failures  (D) SSRF

**Q110.** In the OWASP Top 10 (2021), **Injection** (which includes SQL injection and XSS) is ranked
(A) A01  (B) A02  (C) A03  (D) A10

**Q111.** Injection was ranked **#1** in which OWASP editions before falling in 2021?
(A) 2013 and 2017  (B) 2021 only  (C) it has never been #1  (D) 2004 only

**Q112.** In the OWASP Top 10 (2021), **A10** is
(A) Broken Access Control  (B) Injection  (C) Server-Side Request Forgery (SSRF)  (D) Security Misconfiguration

**Q113.** The most effective defence against **SQL injection** is
(A) hiding error messages  (B) using parameterised queries / prepared statements  (C) using HTTPS  (D) increasing password length

**Q114.** Which of the following is **NOT** a genuine fix for SQL injection?
(A) parameterised queries  (B) hiding error messages from the user  (C) stored procedures written safely  (D) least-privilege database accounts

**Q115.** **Cross-Site Scripting (XSS)** allows an attacker to
(A) inject and execute malicious script in another user's browser, in the trusted site's context
(B) read arbitrary files from the server's disk
(C) crash the database engine
(D) intercept traffic at the physical layer

**Q116.** Which is a correct list of the **three types of XSS**?
(A) local, remote, hybrid  (B) stored, reflected, DOM-based  (C) active, passive, inline  (D) symmetric, asymmetric, hashed

**Q117.** The primary defence against XSS is
(A) longer passwords
(B) output encoding for the correct context, supported by CSP and the HttpOnly cookie flag
(C) disabling cookies entirely
(D) using UDP instead of TCP

**Q118.** Which correctly contrasts **XSS** and **CSRF**?
(A) XSS exploits the site's trust in an authenticated browser; CSRF exploits trust in user input
(B) XSS exploits the site's trust in user input; CSRF exploits the site's trust in an authenticated user's browser
(C) both attack the database directly
(D) both are network-layer attacks

**Q119.** Standard defences against **CSRF** include
(A) anti-CSRF tokens and the SameSite cookie attribute
(B) parameterised queries
(C) stack canaries
(D) longer session timeouts only

---

## Part N — Cryptography & PKI

**Q120.** Which statement about symmetric and asymmetric cryptography is correct?
(A) symmetric uses two different keys; asymmetric uses one
(B) symmetric uses one shared key and is faster; asymmetric uses a public/private key pair and is slower
(C) both use the same single key
(D) asymmetric cannot be used for digital signatures

**Q121.** For **n users** who all need to communicate, **symmetric** cryptography requires how many keys?
(A) 2n  (B) n(n−1)/2  (C) n  (D) n²

**Q122.** For **n users**, **asymmetric** cryptography requires how many keys in total?
(A) n(n−1)/2  (B) 2n  (C) n  (D) n!

**Q123.** Which algorithm is a **symmetric** cipher?
(A) RSA  (B) AES  (C) ECC  (D) Diffie–Hellman

**Q124.** The security of **RSA** is based on the difficulty of
(A) computing discrete logarithms on elliptic curves
(B) factoring large integers
(C) reversing a hash function
(D) sorting large arrays

**Q125.** **Diffie–Hellman** is used for
(A) bulk data encryption  (B) key exchange only, not encryption  (C) hashing passwords  (D) digital certificate issuance

**Q126.** Why does TLS/HTTPS use **both** symmetric and asymmetric cryptography?
(A) asymmetric encrypts the bulk data, symmetric exchanges keys
(B) asymmetric is used to exchange a session key, then symmetric encrypts the bulk data (which is far faster)
(C) to double the key length
(D) it uses only one of them, never both

**Q127.** Which statement about cryptographic **hashing** is correct?
(A) it is reversible with the right key
(B) it is one-way; MD5 and SHA-1 are considered broken while SHA-256 is current
(C) MD5 is the current recommended standard
(D) hashing and encryption are the same thing

**Q128.** Adding a unique random **salt** to each password before hashing primarily
(A) speeds up the hash  (B) defeats precomputed rainbow-table attacks  (C) shortens the digest  (D) encrypts the password reversibly

**Q129.** The recommended way to store user passwords is
(A) plain text  (B) a fast hash such as SHA-256 alone  (C) a slow, salted key-derivation function such as bcrypt or Argon2  (D) Base64 encoding

**Q130.** A **digital signature** is created by encrypting the message hash with the
(A) sender's public key  (B) sender's private key  (C) receiver's public key  (D) receiver's private key

**Q131.** To encrypt a message for **confidentiality**, the sender uses the
(A) sender's private key  (B) sender's public key  (C) receiver's public key  (D) receiver's private key

**Q132.** A digital signature provides
(A) confidentiality only
(B) authentication, integrity and non-repudiation — but **not** confidentiality
(C) availability only
(D) encryption of the message body

**Q133.** Which correctly distinguishes hashing, encryption and encoding?
(A) all three are reversible security measures
(B) hashing is one-way, encryption is reversible with a key, and encoding (e.g. Base64) is not security at all
(C) encoding is the strongest of the three
(D) encryption is one-way and irreversible

**Q134.** In a **PKI**, a Certificate Authority (CA) issues
(A) symmetric session keys  (B) X.509 digital certificates binding an identity to a public key  (C) firewall rules  (D) DNS records

---

## Part O — Attacks, Security Controls & Cyber Law

**Q135.** The three objectives of the **CIA triad** are
(A) Control, Integrity, Access  (B) Confidentiality, Integrity, Availability  (C) Confidentiality, Identity, Authorisation  (D) Cryptography, Integrity, Auditing

**Q136.** A **DDoS** attack primarily targets which security objective, and typically uses what?
(A) confidentiality, using phishing  (B) availability, using a botnet of compromised machines  (C) integrity, using encryption  (D) non-repudiation, using a certificate

**Q137.** Which correctly distinguishes a **virus** from a **worm**?
(A) a worm needs a host file; a virus self-replicates
(B) a virus needs a host file and user action; a worm is self-replicating and spreads by itself
(C) both need a host file  (D) both are self-replicating without a host

**Q138.** **Phishing** is best described as
(A) flooding a server with traffic
(B) social engineering that targets the human to steal credentials
(C) intercepting packets on the wire
(D) encrypting a victim's files for ransom

**Q139.** Which correctly distinguishes an **IDS** from an **IPS**?
(A) IDS blocks traffic inline; IPS only alerts
(B) IDS detects and alerts (passive); IPS detects and blocks inline (active)
(C) both only alert  (D) both only block

**Q140.** A **WAF (Web Application Firewall)** is specifically designed to protect against
(A) power failures  (B) web attacks such as SQL injection and XSS  (C) hardware theft  (D) DNS outages

**Q141.** **Multi-factor authentication (MFA)** combines two or more of
(A) three passwords  (B) something you know, something you have, and something you are  (C) three biometrics  (D) three usernames

**Q142.** India's primary cyber law, which gave legal recognition to electronic records and signatures, is the
(A) DPDP Act 2023  (B) IT Act 2000 (amended 2008)  (C) RTI Act 2005  (D) Indian Telegraph Act 1885

**Q143.** Under the IT Act, **Section 66C** deals with
(A) cyber terrorism  (B) identity theft  (C) tampering with source documents  (D) publishing obscene material

**Q144.** **CERT-In** is
(A) a certificate authority
(B) India's national nodal agency for cyber-security incidents (with mandatory 6-hour reporting)
(C) a cloud provider
(D) an encryption algorithm

**Q145.** India's dedicated data-protection statute, introducing "data fiduciary" and "data principal", is the
(A) IT Act 2000  (B) Digital Personal Data Protection (DPDP) Act 2023  (C) Aadhaar Act 2016  (D) Consumer Protection Act 2019

---

## Part P — IoT (Internet of Things)

**Q146.** IoT is best defined as
(A) a programming language for the web
(B) a network of physical objects embedded with sensors, software and connectivity that collect and exchange data
(C) a type of relational database
(D) a cloud deployment model

**Q147.** Which correctly distinguishes a **sensor** from an **actuator**?
(A) a sensor is an output device; an actuator is an input device
(B) a sensor converts a physical quantity into a signal (input); an actuator converts a signal into physical action (output)
(C) both are input devices
(D) both are output devices

**Q148.** In the IoT architecture, the layer containing sensors and actuators is the
(A) application layer  (B) perception / sensing layer  (C) network layer  (D) business layer

**Q149.** **MQTT** is characterised as
(A) request/response over UDP  (B) publish/subscribe over TCP using a broker  (C) a file-transfer protocol  (D) an email protocol

**Q150.** **CoAP** is characterised as
(A) publish/subscribe over TCP  (B) a REST-like request/response protocol over UDP  (C) a routing protocol  (D) a symmetric cipher

**Q151.** The **Mirai** botnet (2016) built a massive DDoS army mainly by exploiting
(A) a zero-day in TLS  (B) default/weak credentials on IoT devices  (C) SQL injection  (D) buffer overflows in routers

---

## Part Q — Blockchain

**Q152.** A blockchain is best described as
(A) a centralised relational database
(B) a distributed, append-only ledger replicated across nodes with cryptographically chained blocks
(C) a single encrypted file on one server
(D) a symmetric encryption scheme

**Q153.** In a blockchain, immutability of past records is primarily achieved because
(A) records are encrypted with AES
(B) each block stores the cryptographic hash of the previous block, so altering one block invalidates all later blocks
(C) only administrators may write to the ledger
(D) blocks are stored on a single trusted server

**Q154.** The single hash summarising all transactions in a block, stored in its header for efficient inclusion proofs, is the
(A) nonce  (B) Merkle root  (C) difficulty target  (D) genesis hash

**Q155.** Which correctly contrasts **PoW** and **PoS** consensus?
(A) PoW is energy-efficient; PoS is energy-intensive
(B) PoW (Bitcoin) is enormously energy-intensive; PoS (Ethereum) is far more energy-efficient
(C) both use the same energy  (D) neither reaches consensus

**Q156.** A **smart contract** is
(A) a paper contract stored as a PDF
(B) self-executing code stored on the blockchain that runs automatically when predefined conditions are met
(C) a legal firm's software
(D) a type of cryptocurrency wallet

**Q157.** Ethereum smart contracts are typically written in
(A) Python, run on the JVM  (B) Solidity, executed by the EVM  (C) C++, run on bare metal  (D) SQL, run on a database

**Q158.** In a **public (permissionless)** blockchain such as Bitcoin
(A) only invited, known participants may validate
(B) anyone can read, write and validate
(C) a single company governs it
(D) it requires a central bank

---

## Part R — Artificial Intelligence & Machine Learning

**Q159.** The relationship between AI, Machine Learning and Deep Learning is
(A) three unrelated fields
(B) three nested subsets: AI ⊃ Machine Learning ⊃ Deep Learning
(C) Deep Learning ⊃ Machine Learning ⊃ AI
(D) they are synonyms

**Q160.** Which statement is correct?
(A) all AI is machine learning
(B) AI is broader than ML — rule-based expert systems and search are AI with no learning
(C) ML never uses data
(D) deep learning contains all of AI

**Q161.** Which pairing of historical facts is correct?
(A) Turing Test 1956; term "AI" coined at Dartmouth 1950
(B) Turing Test 1950; term "AI" coined at the Dartmouth Conference 1956
(C) both events occurred in 1960
(D) both occurred in 1943

**Q162.** **Supervised** learning is trained on
(A) unlabelled data  (B) labelled data  (C) a reward signal only  (D) no data

**Q163.** k-means clustering and PCA are examples of
(A) supervised learning  (B) unsupervised learning on unlabelled data  (C) reinforcement learning  (D) deep reinforcement learning

**Q164.** **Reinforcement** learning is driven by
(A) labelled examples  (B) a reward/penalty signal from an environment  (C) unlabelled clustering  (D) fixed if-else rules

**Q165.** Within supervised learning, which correctly distinguishes classification from regression?
(A) classification predicts a continuous value; regression predicts a class
(B) classification predicts a discrete class; regression predicts a continuous value
(C) both predict continuous values  (D) both predict discrete classes

**Q166.** Which neural-network architecture is designed primarily for **images / computer vision**?
(A) RNN  (B) CNN (Convolutional Neural Network)  (C) Transformer  (D) autoencoder

**Q167.** Which architecture underlies modern **large language models** such as GPT and BERT?
(A) CNN  (B) plain RNN  (C) the Transformer (attention-based)  (D) a decision tree

**Q168.** **Precision** is defined as
(A) TP / (TP + FN)  (B) TP / (TP + FP)  (C) (TP + TN) / Total  (D) TN / (TN + FP)

**Q169.** **Overfitting** is characterised by
(A) high training error and high test error
(B) low training error but high test error (the model memorises noise)
(C) low training and low test error
(D) high training error but low test error

**Q170.** Which set of techniques helps combat **overfitting**?
(A) fewer data and a more complex model
(B) regularisation, dropout, more data, early stopping and cross-validation
(C) removing the test set  (D) increasing the learning rate only

**Q171.** Why can **accuracy** be a misleading metric?
(A) it is always zero on real data
(B) on imbalanced datasets a trivial model can score very high while being useless — precision, recall or F1 should be used
(C) it cannot be computed  (D) it only applies to regression

---

## Part S — Paper-I (English, Reasoning, GK)

**Q172.** Choose the word most nearly **opposite** in meaning to **AMBIGUOUS**.
(A) Vague  (B) Unclear  (C) Explicit  (D) Puzzling

**Q173.** Identify the part containing the error: *"One of my friends (A)/ who lives in Agartala (B)/ have invited me (C)/ for dinner. (D)"*
(A) A  (B) B  (C) C  (D) D

**Q174.** Find the **odd one out**: 8, 27, 64, 100, 125
(A) 27  (B) 64  (C) 100  (D) 125

**Q175.** A shopkeeper sells an article at a loss of 10%. Had he sold it for ₹90 more, he would have made a profit of 20%. The cost price is
(A) ₹250  (B) ₹300  (C) ₹350  (D) ₹400

**Q176.** The **Agartala–Akhaura** rail link connects Tripura with
(A) Myanmar  (B) Bangladesh  (C) Nepal  (D) Bhutan

**Q177.** Choose the correctly spelt word.
(A) Occurrence  (B) Occurence  (C) Ocurrence  (D) Occurrance

**Q178.** Fill in the blank: *If he ___ harder, he would have passed.*
(A) works  (B) worked  (C) had worked  (D) has worked

**Q179.** Find the next term in the series: 2, 6, 12, 20, 30, ___
(A) 40  (B) 42  (C) 36  (D) 44

**Q180.** 'Pointing to a man, a woman said, "His mother is the only daughter of my mother." How is the woman related to the man?
(A) Mother  (B) Aunt  (C) Sister  (D) Grandmother

**Q181.** If in a certain code **LAMP** is written as **MBNQ**, then **BULB** is written as
(A) CVMC  (B) CWMC  (C) CVMD  (D) DVMC

**Q182.** Which is the **capital** of Tripura?
(A) Aizawl  (B) Agartala  (C) Imphal  (D) Kohima

**Q183.** The **Tripura Sundari Temple**, one of the 51 Shakti Peethas, is located at
(A) Udaipur (Gomati district)  (B) Agartala  (C) Dharmanagar  (D) Kailashahar

**Q184.** Who is the constitutional head of a **State** in India?
(A) the Chief Minister  (B) the Governor  (C) the Chief Justice  (D) the Speaker

**Q185.** The **UNESCO World Heritage** status question: which river forms a major part of Tripura's boundary and drainage, flowing through Agartala?
(A) Gomati  (B) Haora  (C) Manu  (D) Feni

**Q186.** Choose the synonym of **METICULOUS**.
(A) Careless  (B) Thorough and precise  (C) Lazy  (D) Hasty

---
---

# ✅ Answer Key

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 40 | B | 79 | B | 118 | B | 157 | B |
| 2 | B | 41 | C | 80 | A | 119 | A | 158 | B |
| 3 | C | 42 | A | 81 | B | 120 | B | 159 | B |
| 4 | B | 43 | B | 82 | B | 121 | B | 160 | B |
| 5 | B | 44 | B | 83 | B | 122 | B | 161 | B |
| 6 | B | 45 | B | 84 | B | 123 | B | 162 | B |
| 7 | A | 46 | B | 85 | B | 124 | B | 163 | B |
| 8 | B | 47 | B | 86 | B | 125 | B | 164 | B |
| 9 | B | 48 | B | 87 | A | 126 | B | 165 | B |
| 10 | C | 49 | B | 88 | C | 127 | B | 166 | B |
| 11 | B | 50 | B | 89 | C | 128 | B | 167 | C |
| 12 | B | 51 | B | 90 | B | 129 | C | 168 | B |
| 13 | C | 52 | B | 91 | C | 130 | B | 169 | B |
| 14 | B | 53 | B | 92 | B | 131 | C | 170 | B |
| 15 | C | 54 | B | 93 | B | 132 | B | 171 | B |
| 16 | B | 55 | B | 94 | B | 133 | B | 172 | C |
| 17 | B | 56 | B | 95 | B | 134 | B | 173 | C |
| 18 | C | 57 | B | 96 | B | 135 | B | 174 | C |
| 19 | B | 58 | C | 97 | B | 136 | B | 175 | B |
| 20 | B | 59 | B | 98 | B | 137 | B | 176 | B |
| 21 | B | 60 | C | 99 | B | 138 | B | 177 | A |
| 22 | B | 61 | B | 100 | B | 139 | B | 178 | C |
| 23 | B | 62 | B | 101 | B | 140 | B | 179 | B |
| 24 | C | 63 | C | 102 | B | 141 | B | 180 | A |
| 25 | B | 64 | A | 103 | B | 142 | B | 181 | A |
| 26 | B | 65 | B | 104 | B | 143 | B | 182 | B |
| 27 | B | 66 | B | 105 | B | 144 | B | 183 | A |
| 28 | B | 67 | B | 106 | B | 145 | B | 184 | B |
| 29 | B | 68 | B | 107 | B | 146 | B | 185 | B |
| 30 | B | 69 | B | 108 | B | 147 | B | 186 | B |
| 31 | B | 70 | B | 109 | B | 148 | B | | |
| 32 | A | 71 | B | 110 | C | 149 | B | | |
| 33 | B | 72 | C | 111 | A | 150 | B | | |
| 34 | B | 73 | D | 112 | C | 151 | B | | |
| 35 | B | 74 | B | 113 | B | 152 | B | | |
| 36 | B | 75 | B | 114 | B | 153 | B | | |
| 37 | B | 76 | C | 115 | A | 154 | B | | |
| 38 | B | 77 | B | 116 | B | 155 | B | | |
| 39 | B | 78 | A | 117 | B | 156 | B | | |

---

# 📝 Detailed Solutions

**Q1. (C)** `<article>` (like `<header>`, `<footer>`, `<nav>`, `<section>`, `<aside>`, `<main>`) carries meaning about its content. `<div>`/`<span>` are non-semantic and `<font>` is deprecated presentational.

**Q2. (B)** `<div>` and `<span>` are deliberately meaning-free generic containers — the non-semantic category, used only for grouping and styling.

**Q3. (C)** `<font>` (with `<b>`, `<i>`, `<center>`, `<big>`) describes appearance and is deprecated; styling is now CSS's job. `<article>`, `<nav>`, `<main>` are semantic.

**Q4. (B)** SVG is vector-based, scalable without loss, XML-based, and each shape is a DOM element. Canvas is a pixel/bitmap surface.

**Q5. (B)** `<canvas>` is a scripted bitmap drawing surface used for games and charts; SVG is vector.

**Q6. (B)** HTML5 `<audio>`/`<video>` give native media playback with no plugin — this is what displaced Flash.

**Q7. (A)** `email` is a new HTML5 input type (with `url`, `number`, `date`, `range`, `color`) offering built-in browser validation. `label`, `textarea`, `fieldset` are older form elements, not input types.

**Q8. (B)** `localStorage` persists until explicitly cleared and survives a browser restart; `sessionStorage` is per-tab.

**Q9. (B)** `sessionStorage` is cleared when the tab/session closes.

**Q10. (C)** Cookies are limited to ~4 KB and are automatically sent to the server with every HTTP request — which is why session tokens live there.

**Q11. (B)** Only cookies are automatically transmitted to the server on each request; `localStorage`/`sessionStorage` are never sent, and `sessionStorage` does not survive a restart.

**Q12. (B)** POST places data in the request body with no practical size limit and is used for logins, uploads and state-changing actions; GET puts data in the URL.

**Q13. (C)** An external stylesheet (via `<link>`) is best practice — cacheable and reusable across many pages.

**Q14. (B)** The cascade order is `!important` > inline style > ID > class/attribute/pseudo-class > element > universal, then inherited.

**Q15. (C)** Among plain selectors, an ID selector (`#intro`) beats any number of class or element selectors.

**Q16. (B)** From the content outwards: content → padding → border → margin.

**Q17. (B)** Padding is inside the border (between content and border); margin is outside the border. Reversing these is the classic error.

**Q18. (C)** With content-box, rendered width = 200 + 2×10 + 2×5 = 230 px (margin adds spacing but not element width).

**Q19. (B)** On a specificity tie, the rule that appears later in the source order wins.

**Q20. (B)** `A > B` selects only the direct (immediate) children; `A B` matches descendants at any depth.

**Q21. (B)** Media queries are the core mechanism of responsive design, applying different styles at different viewport sizes.

**Q22. (B)** Mobile-first writes the smallest-screen styles first and layers on complexity upward with `min-width` queries — simpler CSS and better performance on constrained devices.

**Q23. (B)** Flexbox is one-dimensional (a single row or column); Grid is two-dimensional (rows and columns together).

**Q24. (C)** `absolute` removes the element from normal flow and positions it relative to the nearest positioned ancestor. `relative` keeps its space; `fixed` is relative to the viewport.

**Q25. (B)** Obeying syntax rules but not checked against a grammar = well-formed. Valid additionally conforms to a DTD/XSD.

**Q26. (B)** Every valid document is well-formed, but not every well-formed document is valid — a one-way implication.

**Q27. (B)** XSD is itself written in XML and supports rich data types (integer, date, decimal); DTD uses a non-XML syntax and has no data types.

**Q28. (B)** XSD supports rich data types; DTD treats everything as text.

**Q29. (B)** XSLT transforms XML into another format (HTML, text, other XML); XPath navigates/queries nodes within a document.

**Q30. (B)** SAX is an event-driven, streaming, forward-only, low-memory parser. DOM builds the whole tree in memory with random access.

**Q31. (B)** JSON is more compact and native to JavaScript (`JSON.parse`). It does not support comments, and XML — not JSON — needs closing tags; REST APIs favour JSON.

**Q32. (A)** A well-formed XML document must have exactly one root element (plus proper nesting, closed tags and quoted attributes). A DTD/XSD is only needed for validity.

**Q33. (B)** The 3-tier architecture separates presentation, application (business logic) and data layers.

**Q34. (B)** A thin client does minimal local processing, relies on the server, and therefore needs constant connectivity (e.g. a browser app).

**Q35. (B)** A web server (Apache, Nginx, IIS) serves static content over HTTP; an application server runs business logic.

**Q36. (B)** Tomcat, JBoss/WildFly and WebLogic are application servers that execute business logic.

**Q37. (B)** A forward proxy sits in front of the clients and hides the client's identity from the server. A reverse proxy fronts the servers.

**Q38. (B)** A reverse proxy sits in front of the servers, providing load balancing, SSL termination and caching, and hiding the backend.

**Q39. (B)** In a 2-tier "fat client", business logic lives on the client, which needs direct DB credentials, so changes require redeploying every client — the reasons 3-tier replaced it.

**Q40. (B)** A web server handles HTTP and serves files; an application server executes the application code. In practice Nginx/Apache front Tomcat.

**Q41. (C)** The Controller receives user input, invokes model operations and selects the view. The Model holds data/logic; the View renders.

**Q42. (A)** The Model holds data and business logic and knows nothing about the UI.

**Q43. (B)** The View is responsible for presentation and rendering the UI from the model.

**Q44. (B)** REST is an architectural style (often JSON, stateless, HTTP verbs); SOAP is a protocol (rigid XML envelope, WSDL). Option B states this correctly; option A reverses the two.

**Q45. (B)** SOAP messages are XML only, structured as an Envelope containing a Header and Body.

**Q46. (B)** WSDL is the machine-readable XML contract describing operations, messages and the endpoint; tools can generate client code from it.

**Q47. (B)** UDDI is a registry for discovering and registering web services. Memory aid: SOAP = message, WSDL = contract, UDDI = directory.

**Q48. (B)** REST requires statelessness: each request carries everything needed, and the server holds no session state — enabling easy horizontal scaling.

**Q49. (B)** PUT is idempotent (repeating it leaves the same state); POST is not (each call creates a new resource).

**Q50. (B)** CORS is the browser rule controlling whether a page from one origin may call another origin.

**Q51. (B)** GraphQL exposes a single endpoint where the client specifies exactly which fields it wants, avoiding over-fetching and multiple round trips.

**Q52. (B)** `===` compares both value and type with no coercion; `==` performs type coercion.

**Q53. (B)** `let` and `const` are block-scoped; `var` is function-scoped and hoisted.

**Q54. (B)** The DOM is a W3C standard API provided by the browser, not part of the JavaScript language — which is why Node.js has no DOM.

**Q55. (B)** Despite the name (Asynchronous JavaScript And XML), AJAX today usually carries JSON.

**Q56. (B)** React is a library using a virtual DOM with one-way data flow; Angular is a full framework with two-way data binding.

**Q57. (B)** A JWT is a self-contained, digitally signed token (header.payload.signature) that the server can verify without stored session state — enabling stateless authentication.

**Q58. (C)** NIST's five characteristics are on-demand self-service, broad network access, resource pooling, rapid elasticity and measured service. "Permanent local storage" contradicts the cloud model.

**Q59. (B)** Resource pooling (multi-tenancy) means the provider's hardware is shared among many customers.

**Q60. (C)** IaaS delivers raw compute, storage and networking; the customer manages the OS upward.

**Q61. (B)** In IaaS the customer patches the guest OS. In PaaS and SaaS the provider handles it.

**Q62. (B)** In PaaS the customer manages only the applications and data; the provider handles the OS, runtime and below.

**Q63. (C)** Ready-to-use applications delivered over the web (Gmail, Salesforce, Office 365) are SaaS.

**Q64. (A)** EC2, Azure VMs and Google Compute Engine are IaaS.

**Q65. (B)** Heroku, App Engine and Elastic Beanstalk are PaaS platforms.

**Q66. (B)** In SaaS the customer manages essentially nothing beyond their own data and configuration.

**Q67. (B)** Measured service means usage is metered and billed (pay-per-use).

**Q68. (B)** On-demand self-service means you provision resources yourself, instantly, with no human on the provider's side.

**Q69. (B)** Rapid elasticity means resources scale up and down quickly and automatically.

**Q70. (B)** The four deployment models are public, private, hybrid and community.

**Q71. (B)** Private cloud gives maximum control and security but at the highest cost and with little elasticity benefit.

**Q72. (C)** Keeping sensitive data in a private cloud while bursting the public website to a public cloud is a hybrid deployment.

**Q73. (D)** Several organisations with common concerns (government departments) sharing one cloud is a community cloud.

**Q74. (B)** Vertical scaling (scale up) makes one machine bigger; it hits a hardware ceiling.

**Q75. (B)** Horizontal scaling (scale out) adds more machines behind a load balancer — the practical meaning of cloud elasticity.

**Q76. (C)** 99.9% ("three nines") allows about 8.77 hours of downtime per year.

**Q77. (B)** Vendor lock-in and data sovereignty (plus connectivity dependence) are the most commonly cited cloud drawbacks.

**Q78. (A)** A core benefit is converting capital expenditure into operating expenditure — renting instead of buying hardware.

**Q79. (B)** Virtualisation creates a software abstraction of physical resources, so one machine can appear as many independent ones.

**Q80. (A)** A type-1 (bare-metal) hypervisor runs directly on the hardware; type-2 runs on a host OS.

**Q81. (B)** VirtualBox and VMware Workstation/Player are type-2 (hosted) hypervisors.

**Q82. (B)** VMware ESXi, Hyper-V, Xen and KVM are type-1 (bare-metal) hypervisors used in data centres.

**Q83. (B)** Containers share the host OS kernel, so they are megabytes not gigabytes and start in milliseconds. VMs each run a full guest OS.

**Q84. (B)** VMs provide stronger, hardware-level isolation; a container escape only has to break a kernel namespace.

**Q85. (B)** Each VM runs its own full guest OS (gigabytes, minutes to boot); a container shares the host kernel.

**Q86. (B)** A Docker image is an immutable template; a container is a running instance of that image.

**Q87. (A)** Kubernetes is a container orchestration system: automated deployment, scaling, self-healing and load balancing.

**Q88. (C)** The pod is the smallest deployable Kubernetes unit, wrapping one or more containers.

**Q89. (C)** Block storage presents fixed-size blocks as a raw volume — ideal for databases and low-latency random I/O.

**Q90. (B)** File storage organises data as files in a directory hierarchy, accessed over NFS/SMB.

**Q91. (C)** S3, Azure Blob and Google Cloud Storage are object storage.

**Q92. (B)** Object storage uses a flat namespace ("folders" are just name prefixes) and is accessed over HTTP/REST, not mounted as a filesystem.

**Q93. (B)** Databases need block storage for their frequent small random reads and writes and control over layout.

**Q94. (B)** SDN separates the control plane (decision-making) from the data plane (packet forwarding), centralising control in software.

**Q95. (B)** A CDN caches static content at edge locations near users to cut latency and origin load.

**Q96. (B)** Edge computing processes data close to where it is generated, reducing latency and backhaul bandwidth.

**Q97. (B)** Latency ordering is Cloud > Fog > Edge (edge is lowest); compute power is also Cloud > Fog > Edge.

**Q98. (B)** The fog layer is intermediate — gateways, local routers and the LAN — between edge devices and the central cloud.

**Q99. (B)** MeghRaj is the Government of India cloud initiative (with the NIC National Cloud) under MeitY.

**Q100. (B)** Almost every serious vulnerability stems from trusting untrusted input and letting data be interpreted as code.

**Q101. (B)** Input validation must be done server-side; client-side checks are trivially bypassed.

**Q102. (B)** An allow-list defines exactly what is acceptable and rejects everything else — including attacks nobody has anticipated. A deny-list must enumerate every bad input.

**Q103. (B)** A buffer overflow writes past a buffer's end, overwriting adjacent memory such as the return address, so attacker data can become executed code.

**Q104. (B)** ASLR, DEP/NX and stack canaries (plus bounds checking and safe functions) mitigate buffer-overflow exploitation.

**Q105. (B)** STRIDE (Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege) is a threat-modelling framework.

**Q106. (B)** SAST scans source code statically; DAST tests the running application dynamically.

**Q107. (B)** "Shift left" means finding and fixing security defects early, because fixing them late is far costlier.

**Q108. (B)** Open design / "no security through obscurity" states that security must not rely on the design being secret.

**Q109. (B)** A01 in OWASP 2021 is Broken Access Control, which rose from #5 to #1.

**Q110. (C)** Injection fell to A03 in 2021 and absorbed XSS as a subcategory.

**Q111. (A)** Injection was #1 in the 2013 and 2017 editions before dropping to A03 in 2021.

**Q112. (C)** A10 in OWASP 2021 is Server-Side Request Forgery (SSRF), a new entry.

**Q113. (B)** Parameterised queries / prepared statements are the actual fix: the query structure is compiled first, and input is supplied separately as pure data.

**Q114. (B)** Hiding error messages only masks the symptom; it is not a fix. The others genuinely help.

**Q115. (A)** XSS injects script that executes in another user's browser in the trusted site's context, enabling cookie theft and defacement.

**Q116. (B)** The three XSS types are stored (persistent), reflected and DOM-based.

**Q117. (B)** The primary XSS defence is context-correct output encoding, backed by CSP and the HttpOnly cookie flag.

**Q118. (B)** XSS exploits the site's trust in user input; CSRF exploits the site's trust in an authenticated user's browser (which auto-sends its cookies).

**Q119. (A)** Anti-CSRF tokens (a secret the attacker's page cannot know) and the SameSite cookie attribute defend against CSRF.

**Q120. (B)** Symmetric uses one shared key and is fast; asymmetric uses a public/private key pair and is slow but solves key distribution.

**Q121. (B)** Symmetric needs n(n−1)/2 keys for n users, all of which must be distributed secretly.

**Q122. (B)** Asymmetric needs 2n keys (a key pair per user), half of them public.

**Q123. (B)** AES is symmetric; RSA, ECC and Diffie–Hellman are asymmetric.

**Q124. (B)** RSA's security rests on the difficulty of factoring large integers.

**Q125. (B)** Diffie–Hellman performs key exchange only; it does not encrypt data itself.

**Q126. (B)** TLS uses asymmetric crypto to exchange a random session key, then symmetric crypto for the bulk data because asymmetric is far too slow for large volumes.

**Q127. (B)** Hashing is one-way; MD5 and SHA-1 are broken while SHA-256 is the current standard.

**Q128. (B)** A unique random salt per password defeats precomputed rainbow tables by forcing the attacker to attack each password separately.

**Q129. (C)** Passwords should be stored with a slow, salted key-derivation function such as bcrypt, scrypt, Argon2 or PBKDF2 — never plain text, a fast hash alone, or Base64.

**Q130. (B)** A digital signature is the message hash encrypted with the sender's private key; anyone verifies it with the sender's public key.

**Q131. (C)** To encrypt for confidentiality, use the receiver's public key so only the receiver's private key can decrypt.

**Q132. (B)** A digital signature provides authentication, integrity and non-repudiation — but not confidentiality (the message is sent in the clear unless also encrypted).

**Q133. (B)** Hashing is one-way, encryption is reversible with a key, and encoding (Base64) is not security at all — just a representation change.

**Q134. (B)** A Certificate Authority issues X.509 digital certificates binding an identity to a public key within a PKI.

**Q135. (B)** The CIA triad is Confidentiality, Integrity and Availability.

**Q136. (B)** DDoS targets availability and typically uses a botnet of compromised machines to flood the target.

**Q137. (B)** A virus needs a host file and usually a user action; a worm is self-replicating and spreads across networks by itself.

**Q138. (B)** Phishing is social engineering that targets the human to steal credentials, not the software.

**Q139. (B)** An IDS detects and alerts (passive, out-of-band); an IPS detects and blocks inline (active).

**Q140. (B)** A WAF specifically protects web applications against attacks such as SQL injection and XSS.

**Q141. (B)** MFA combines two or more of: something you know, something you have, and something you are.

**Q142. (B)** The IT Act 2000 (amended 2008) is India's primary cyber law, recognising electronic records and digital signatures.

**Q143. (B)** Section 66C of the IT Act deals with identity theft; 66D is cheating by personation and 66F is cyber terrorism.

**Q144. (B)** CERT-In is India's national nodal agency for cyber-security incidents, with mandatory 6-hour incident reporting.

**Q145. (B)** The DPDP Act 2023 is India's data-protection law, introducing "data fiduciary" and "data principal" and a Data Protection Board.

**Q146. (B)** IoT is a network of physical objects embedded with sensors, software and connectivity that collect and exchange data.

**Q147. (B)** A sensor converts a physical quantity into a signal (input); an actuator converts a signal into physical action (output).

**Q148. (B)** Sensors and actuators live in the perception / sensing layer (layer 1) of IoT architecture.

**Q149. (B)** MQTT is a lightweight publish/subscribe protocol over TCP that uses a broker — the most-cited IoT protocol.

**Q150. (B)** CoAP is a REST-like request/response protocol over UDP — "HTTP for tiny devices".

**Q151. (B)** The Mirai botnet built its DDoS army mainly by trying default/weak credentials on IoT devices.

**Q152. (B)** A blockchain is a distributed, append-only ledger replicated across nodes with blocks cryptographically chained together.

**Q153. (B)** Immutability comes from each block storing the previous block's hash: altering one block breaks every subsequent link — not from encryption.

**Q154. (B)** The Merkle root is the single hash summarising all transactions, enabling efficient inclusion proofs.

**Q155. (B)** PoW (Bitcoin) is enormously energy-intensive; PoS (Ethereum after the Merge) is far more energy-efficient.

**Q156. (B)** A smart contract is self-executing code stored on the blockchain that runs automatically when conditions are met.

**Q157. (B)** Ethereum smart contracts are written in Solidity and executed by the EVM.

**Q158. (B)** In a public (permissionless) blockchain such as Bitcoin, anyone can read, write and validate.

**Q159. (B)** AI ⊃ Machine Learning ⊃ Deep Learning — three nested subsets.

**Q160. (B)** AI is broader than ML: rule-based expert systems and search algorithms are AI with no learning at all.

**Q161. (B)** The Turing Test was proposed by Turing in 1950; the term "artificial intelligence" was coined at the Dartmouth Conference in 1956.

**Q162. (B)** Supervised learning trains on labelled data.

**Q163. (B)** k-means and PCA are unsupervised techniques operating on unlabelled data.

**Q164. (B)** Reinforcement learning learns a policy from a reward/penalty signal supplied by an environment.

**Q165. (B)** Classification predicts a discrete class; regression predicts a continuous value.

**Q166. (B)** CNNs use convolution and pooling to exploit spatial locality — designed for images/vision.

**Q167. (C)** Modern LLMs (GPT, BERT) are built on the Transformer architecture, which uses attention instead of recurrence.

**Q168. (B)** Precision = TP / (TP + FP): of everything flagged positive, how much really was.

**Q169. (B)** Overfitting shows low training error but high test error — the model memorises noise rather than generalising.

**Q170. (B)** Regularisation, dropout, more data, early stopping and cross-validation combat overfitting.

**Q171. (B)** On imbalanced data a trivial model can score high accuracy while being useless; precision, recall, F1 or AUC-ROC are better metrics.

**Q172. (C)** *Ambiguous* means open to more than one interpretation; its opposite is **explicit**. The others are synonyms.

**Q173. (C)** The subject *One* is singular, so it must be "**has** invited me", not "have invited me". The error is in part C.

**Q174. (C)** 8, 27, 64 and 125 are perfect cubes (2³, 3³, 4³, 5³); **100** is not (it is a perfect square).

**Q175. (B)** Let CP = x. 1.2x − 0.9x = 90 → 0.3x = 90 → x = ₹300.

**Q176. (B)** The Agartala–Akhaura rail link connects Tripura with Akhaura in **Bangladesh** (inaugurated November 2023).

**Q177. (A)** The correct spelling is **Occurrence** (double c, double r).

**Q178. (C)** The third conditional needs the past perfect: "If he **had worked** harder, he would have passed."

**Q179. (B)** Differences are 4, 6, 8, 10, so the next difference is 12: 30 + 12 = **42** (pattern n(n+1): 2,6,12,20,30,42).

**Q180. (A)** "The only daughter of my mother" is the woman herself; so his mother is the woman — she is his **mother**.

**Q181. (A)** Each letter shifts +1: B→C, U→V, L→M, B→C, giving **CVMC** (same rule that turns LAMP into MBNQ).

**Q182. (B)** The capital of Tripura is **Agartala**.

**Q183. (A)** The Tripura Sundari Temple, one of the 51 Shakti Peethas, is at **Udaipur** in Gomati district.

**Q184. (B)** The **Governor** is the constitutional head of a State in India.

**Q185. (B)** The **Haora** river flows through Agartala and is central to the city's drainage.

**Q186. (B)** *Meticulous* means **thorough and precise** (showing great attention to detail).
