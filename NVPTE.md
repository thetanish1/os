Of course. Here are detailed answers to all your questions, structured for a 5-mark format, with types, real-life examples, and use cases.

---

### 1. Types of Vulnerabilities

**Answer:**
A vulnerability is a weakness in a system that can be exploited by a threat actor to perform unauthorized actions.

**Types with Examples:**
1.  **Injection Flaws:** An attacker sends untrusted data to an interpreter, tricking it into executing unintended commands.
    *   **Example:** SQL Injection, where an attacker inputs `' OR '1'='1` into a login form to bypass authentication.
    *   **Use Case:** Stealing, modifying, or deleting database records.
2.  **Broken Authentication:** Flaws in session management and credential verification allow attackers to compromise passwords or session tokens.
    *   **Example:** A website that does not invalidate a session ID after logout, allowing session hijacking.
    *   **Use Case:** Account takeover.
3.  **Sensitive Data Exposure:** When an application does not adequately protect sensitive data like passwords or credit card numbers.
    *   **Example:** Storing user passwords in plain text instead of hashing them. If the database is breached, all passwords are exposed.
    *   **Use Case:** Identity theft, financial fraud.
4.  **XML External Entities (XXE):** Poorly configured XML processors evaluate external entity references within XML documents.
    *   **Example:** An attacker uploads an XML file that, when processed, forces the application to send the server's `/etc/passwd` file to an external server.
    *   **Use Case:** Reading internal files, internal port scanning.
5.  **Security Misconfigurations:** This can happen at any level of the application stack, including the platform, web server, or application.
    *   **Example:** Leaving a cloud storage bucket (like AWS S3) publicly accessible, exposing sensitive files.
    *   **Use Case:** Unauthorized data access.

---

### 2. Web Server Features

**Answer:**
A web server is software and hardware that uses HTTP to serve files and content to clients upon request.

**Key Features:**
1.  **HTTP Request Handling:** Processes client requests (GET, POST) and delivers the corresponding web pages or resources.
2.  **Static Content Serving:** Efficiently delivers static files like HTML, CSS, JavaScript, and images.
3.  **Dynamic Content Support:** Can work with server-side technologies (like PHP, ASP.NET, Node.js) to generate dynamic content.
4.  **Virtual Hosting:** Allows a single server to host multiple websites with different domain names.
5.  **Logging:** Maintains access and error logs for monitoring, debugging, and security analysis.
6.  **Authentication & Access Control:** Restricts access to certain directories or resources based on credentials.
7.  **SSL/TLS Termination:** Manages HTTPS encryption and decryption to secure data in transit.

---

### 3. OWASP Principle Enlist and Explain in Details

**Answer:**
The OWASP Software Assurance Maturity Model (SAMM) provides principles for building secure software. Core principles include:

1.  **Secure by Design:** Security is considered from the very beginning of the development lifecycle, not as an afterthought.
    *   **Details:** This involves threat modeling, defining security requirements, and using secure architecture patterns.
2.  **Secure by Default:** The software ships in a secure state out-of-the-box.
    *   **Details:** Default accounts have strong passwords or are disabled, unnecessary features are turned off, and the principle of least privilege is applied.
3.  **Secure by Deployment:** The software can be deployed and maintained securely.
    *   **Details:** Provides clear documentation for secure configuration, patch management, and operational security for administrators.
4.  **Continuous Verification:** Security is continuously monitored and verified.
    *   **Details:** Implementing automated security testing (SAST, DAST), dependency scanning, and runtime application self-protection (RASP).
5.  **Defense in Depth:** Layering multiple security controls so that if one fails, others are in place to stop an attack.
    *   **Details:** Using a firewall, WAF, input validation, and prepared statements all together to protect against SQL injection.

---

### 4. TCP, UDP, HTTP, DHCP Protocols Details

**Answer:**
*   **TCP (Transmission Control Protocol):**
    *   **Details:** Connection-oriented, reliable. It establishes a connection (3-way handshake), guarantees delivery, orders packets, and provides error-checking.
    *   **Use Case:** Web browsing (HTTP/S), email (SMTP), file transfer (FTP). Used where data integrity is critical.
*   **UDP (User Datagram Protocol):**
    *   **Details:** Connectionless, unreliable. It sends datagrams without establishing a connection. It's faster but offers no delivery or order guarantees.
    *   **Use Case:** Video streaming, VoIP (like Skype), DNS lookups. Used where speed is more important than perfect accuracy.
*   **HTTP (Hypertext Transfer Protocol):**
    *   **Details:** An application-layer protocol for transmitting hypermedia documents. It is stateless and uses request-response methods (GET, POST).
    *   **Use Case:** Foundation of data communication on the World Wide Web.
*   **DHCP (Dynamic Host Configuration Protocol):**
    *   **Details:** A network management protocol used to automatically assign IP addresses and other communication parameters to devices on a network.
    *   **Use Case:** In your home Wi-Fi, your laptop automatically gets an IP address from the router via DHCP.

---

### 5. Wireshark Basic Commands

**Answer:**
Wireshark is a network protocol analyzer. It doesn't use "commands" in a CLI sense but uses display filters.

**Basic Filters with Explanation:**
1.  `ip.addr == 192.168.1.1`
    *   **Explanation:** Displays all packets to or from the IP address 192.168.1.1.
2.  `tcp.port == 80`
    *   **Explanation:** Shows all TCP traffic on port 80 (standard HTTP port).
3.  `http`
    *   **Explanation:** Filters to show only HTTP protocol traffic.
4.  `dns`
    *   **Explanation:** Filters to show only DNS query and response packets.
5.  `tcp.flags.syn == 1 and tcp.flags.ack == 0`
    *   **Explanation:** Shows only TCP SYN packets, useful for seeing new connection attempts (the first part of the 3-way handshake).

---

### 6. Nmap Basic Commands with Understanding

**Answer:**
Nmap (Network Mapper) is a network discovery and security auditing tool.

**Basic Commands:**
1.  `nmap 192.168.1.1`
    *   **Understanding:** A basic TCP SYN scan against a single target. It scans the 1000 most common ports.
2.  `nmap -sS -O 192.168.1.0/24`
    *   **Understanding:** `-sS` performs a Stealth SYN scan. `-O` enables OS detection. This scans an entire subnet and guesses the operating system of live hosts.
3.  `nmap -sV -p 22,80,443 example.com`
    *   **Understanding:** `-sV` probes open ports to determine service/version info. `-p` scans only specified ports (SSH, HTTP, HTTPS).
4.  `nmap -A -T4 target`
    *   **Understanding:** `-A` enables "Aggressive" mode (OS detection, version detection, script scanning, and traceroute). `-T4` sets the timing template for faster execution.
5.  `nmap --script vuln 192.168.1.1`
    *   **Understanding:** Uses Nmap Scripting Engine (NSE) to run scripts from the "vuln" category to check for known vulnerabilities.

---

### 7. Security Principles: What to Do, What Not to Do (OWASP)

**Answer:**
Based on OWASP's proactive controls and ASVS.

| What TO Do | What NOT To Do |
| :--- | :--- |
| **Implement Identity & Access Control** | **Use weak or no authentication** |
| **Validate All Input** | **Trust user input** |
| **Implement Logging & Monitoring** | **Ignore security logs** |
| **Use Cryptographic Controls (TLS, Hashing)** | **Store passwords in plaintext or use weak crypto** |
| **Handle Errors Gracefully** | **Show detailed error messages to users** |
| **Follow the Principle of Least Privilege** | **Run services with administrator/root privileges** |
| **Keep Dependencies Updated** | **Use libraries with known vulnerabilities** |
| **Secure the CI/CD Pipeline** | **Push untested code directly to production** |

---

### 8. All About Webserver

*   **Types:** Apache HTTP Server, Nginx, Microsoft IIS, LiteSpeed.
*   **Uses:** Hosting websites and web applications, serving static and dynamic content, acting as a reverse proxy or load balancer.
*   **Causes of Attacks:**
    *   Misconfigurations (default settings, open directories).
    *   Unpatched software (known vulnerabilities).
    *   Vulnerable web applications running on them (SQLi, XSS).
*   **Prevention:**
    *   Regular patching and updates.
    *   Hardening (disable unnecessary modules, use secure configs).
    *   Use a Web Application Firewall (WAF).
    *   Segmented network architecture.
    *   Security headers (e.g., HSTS, CSP).

---

### 9. Explain Email Working Architecture

**Answer:**
**Single-Tier Architecture:**
*   All components (MTA, MDA, MUA) run on a single server.
*   **Example:** A small business running a mail server on one machine.
*   **Drawback:** Not scalable; single point of failure.

**Multi-Tier Architecture (with Load Balancer):**
*   Components are distributed across multiple servers for scalability and reliability.
    1.  **Front-End/Load Balancer:** Distributes incoming SMTP/HTTP requests across multiple Mail Transfer Agents (MTAs).
    2.  **MTA Tier (e.g., Postfix, Sendmail):** Routes emails between servers.
    3.  **MDA Tier (e.g., Dovecot, Cyrus):** Stores emails in user mailboxes and allows retrieval via IMAP/POP3.
    4.  **Database Tier:** Stores user accounts, passwords, and metadata.
*   **Use Case:** Large providers like Gmail or Outlook.com. The load balancer ensures no single MTA gets overwhelmed.

---

### 10. Application Server

**Answer:**
An application server is a software framework that provides an environment to run web applications. It sits between the web server and the backend database.

*   **Function:** Executes the business logic of an application, manages transactions, connection pooling, and provides services like messaging and security.
*   **Examples:** Apache Tomcat, JBoss/WildFly, IBM WebSphere, Oracle WebLogic.
*   **Use Case:** An e-commerce site uses a web server (Nginx) to serve product images (static content) and an application server (Tomcat) to run the Java servlets that handle "Add to Cart" and "Checkout" logic (dynamic content).

---

### 11. What are Cookies, Cache?

**Answer:**
*   **Cookies:**
    *   **What:** Small pieces of data stored on the *client-side* (user's browser) by the website.
    *   **Storage:** Browser's cookie storage.
    *   **Use:** Maintain state. Used for session management, personalization, and tracking.
    *   **Use Case:** A "Shopping Cart" on an e-commerce site. The cookie remembers the items you've added as you browse.
*   **Cache:**
    *   **What:** A temporary storage location for copies of files (like images, CSS, JS) to reduce server load and speed up page loads.
    *   **Storage:** Browser cache (on disk/memory) or intermediary caches (CDN, proxy servers).
    *   **Use:** Stores static resources so they don't need to be re-downloaded on subsequent visits.
    *   **Use Case:** When you revisit a news website, the logo and styles load instantly from your local cache.

---

### 12. Justify the Role of Servlet in Web Server

**Answer:**
A Servlet is a Java programming language class that dynamically processes requests and constructs responses. Its role is critical for enabling dynamic web content.

**Justification:**
1.  **Platform Independence:** "Write Once, Run Anywhere." Servlets run on any server with a Java Virtual Machine (JVM).
2.  **Performance:** Servlets remain in memory between requests, making them much faster than older CGI scripts which had to start a new process for each request.
3.  **Robustness:** Benefit from the strong typing, exception handling, and garbage collection of the Java language.
4.  **Security:** Inherits Java's strong security features, such as the lack of pointer memory manipulation.
5.  **Portfolio:** A web server like Apache serves static content, but it can delegate requests for dynamic content (e.g., JSP pages) to a servlet container like Apache Tomcat, which then uses Servlets to generate the HTML response.

---

### 13. Types of Cookies

**Answer:**
1.  **Session Cookies:**
    *   **Explanation:** Temporary cookies stored in browser memory. Deleted when the browser is closed.
    *   **Use Case:** Maintaining your login state during a single browsing session on a bank's website.
2.  **Persistent Cookies:**
    *   **Explanation:** Stored on the user's hard drive with an expiration date. Remain until they expire or are deleted.
    *   **Use Case:** A "Remember Me" login feature or language preference settings on a website.
3.  **First-Party Cookies:**
    *   **Explanation:** Set by the website the user is currently visiting.
    *   **Use Case:** Session management and user preferences for the current site.
4.  **Third-Party Cookies:**
    *   **Explanation:** Set by a domain other than the one the user is visiting. Often via embedded ads or trackers.
    *   **Use Case:** Tracking a user across multiple sites to build a profile for targeted advertising.

---

### 14. Explain Attack to Privacy Types

**Answer:**
1.  **Tracking:**
    *   **Explanation:** Monitoring a user's online activity across websites.
    *   **Method:** Third-party cookies, browser fingerprinting, tracking pixels.
2.  **Surveillance:**
    *   **Explanation:** Mass or targeted monitoring of communications and data by governments or corporations.
    *   **Method:** Deep Packet Inspection (DPI), mandatory data retention laws.
3.  **Data Aggregation & Profiling:**
    *   **Explanation:** Combining data from multiple sources to create a detailed profile of an individual.
    *   **Method:** Data brokers buying and selling user data from various online and offline sources.
4.  **Identity Theft:**
    *   **Explanation:** Stealing personal information to impersonate someone for financial gain.
    *   **Method:** Phishing attacks, data breaches.
5.  **Doxing:**
    *   **Explanation:** Publicly releasing a person's private identifying information without their consent.
    *   **Method:** Researching public databases and social media to find home addresses, phone numbers, etc.

---

### 15. What is CSP and Browser Fingerprinting

**Answer:**
*   **CSP (Content Security Policy):**
    *   **What:** A security standard that acts as an allowlist for resources that a browser is permitted to load. It is a primary method to prevent Cross-Site Scripting (XSS) attacks.
    *   **How:** The server sends a `Content-Security-Policy` HTTP header specifying which domains are approved sources for scripts, styles, images, etc. If an attacker injects a malicious script from an unapproved domain, the browser will block it.
*   **Browser Fingerprinting:**
    *   **What:** A technique to identify and track users by collecting unique characteristics of their browser and device.
    *   **How:** It gathers data like user agent, screen resolution, installed fonts, browser plugins, and timezone. This combination of attributes is often unique enough to identify a specific user, even with cookies disabled.

---

### 16. Phishing, Spamming & Spoofing

**Answer:**
*   **Phishing:**
    *   **What:** A social engineering attack to steal sensitive data like login credentials or credit card numbers.
    *   **Example:** An email pretending to be from "Netflix Security" claiming your account is on hold, with a link to a fake login page that harvests your password.
*   **Spamming:**
    *   **What:** The use of electronic messaging systems to send unsolicited bulk messages.
    *   **Example:** Bulk advertising emails for questionable products sent to millions of email addresses.
*   **Spoofing:**
    *   **What:** Faking the originating address (IP, email, SMS) to appear as a trusted source.
    *   **Example:**
        *   **Email Spoofing:** Forging the "From" address to make a phishing email look legitimate.
        *   **IP Spoofing:** Faking the source IP in a network packet to bypass IP-based access controls.

---

### 17. Five Stages of Hacking

**Answer:**
A structured methodology used by ethical hackers and malicious attackers.
1.  **Reconnaissance (Information Gathering):** Passive (searching public info) and active (scanning) gathering of target data.
2.  **Scanning:** Using tools to find open ports, services, and vulnerabilities (e.g., Nmap, Nessus).
3.  **Gaining Access (Exploitation):** Exploiting a vulnerability to enter the system (e.g., exploiting a buffer overflow, using a SQL injection).
4.  **Maintaining Access:** Installing backdoors, rootkits, or trojans to ensure persistent access for future visits.
5.  **Clearing Tracks (Covering Tracks):** Deleting logs, hiding files, and modifying registry entries to avoid detection.

---

### 18. Footprinting & Social Engineering

**Answer:**
*   **Footprinting:** The first stage of hacking. It is the process of collecting as much information as possible about a target network, system, or organization.
    *   **Methods:** WHOIS lookup, DNS enumeration, searching social media, Google Hacking (using advanced search operators), network scanning.
*   **Social Engineering:** The psychological manipulation of people into performing actions or divulging confidential information.
    *   **Types:**
        *   **Phishing:** Deceptive emails.
        *   **Vishing:** Voice phishing (phone calls).
        *   **Pretexting:** Creating a fabricated scenario (pretending to be from IT support).
        *   **Baiting:** Offering something enticing (a free USB drive) that contains malware.

---

### 19. Tools for Scanning

**Answer:**
1.  **Nmap:** Network discovery and security auditing. Finds open ports and services.
2.  **Nessus / OpenVAS:** Vulnerability scanners that identify known security flaws in systems and software.
3.  **Nikto:** A web server scanner that tests for dangerous files, outdated server software, and other problems.
4.  **Wireshark:** A network protocol analyzer for deep inspection of network traffic.
5.  **Burp Suite / OWASP ZAP:** Web application security scanners for finding vulnerabilities like SQLi and XSS.

---

### 20. Nmap Scanning Type

**Answer:**
1.  **TCP SYN Scan (`-sS`):** Default and most popular. Stealthy because it doesn't complete the TCP handshake. Sends a SYN packet; if a SYN/ACK is received, the port is open.
2.  **TCP Connect Scan (`-sT`):** Completes the full TCP 3-way handshake. Noisier but requires no special privileges.
3.  **UDP Scan (`-sU`):** Scans UDP ports. Much slower than TCP scans as UDP is stateless.
4.  **OS Detection (`-O`):** Uses TCP/IP stack fingerprinting to guess the remote operating system.
5.  **Version Detection (`-sV`):** Probes open ports to determine what application and version is running on them.

---

### 21. DNS Enumeration & Social Engineering Attack

**Answer:**
**DNS Enumeration Step-by-Step:**
1.  **Find Name Servers:** Use `nslookup -type=NS example.com` to find the authoritative name servers for the domain.
2.  **Zone Transfer Attempt:** Use `dig axfr @ns1.example.com example.com` to request a zone transfer. If misconfigured, this dumps all DNS records (hostnames, IPs) for the domain.
3.  **Brute-force Subdomains:** Use tools like `dnsrecon` or `sublist3r` to guess common subdomains (e.g., `mail.example.com`, `ftp.example.com`, `admin.example.com`).
4.  **DNS Lookups:** Perform standard `nslookup` or `dig` commands on discovered hosts to find their IP addresses.

**Social Engineering Attack (Linked):**
An attacker uses information from DNS enumeration (e.g., finding `mail.example.com`) to craft a targeted phishing email. The email appears to come from "IT Support <help@mail.example.com>" and tells the user to reset their password via a link to a fake login page on "admin-portal.example.com" (a subdomain the attacker might try to create or spoof).

---

### 22. Scanning & Enumeration: Port Scanning vs. Network Scanning

**Answer:**
*   **Network Scanning:** The process of discovering active devices on a network.
    *   **Purpose:** To create a map of the network.
    *   **Method:** Using ICMP ping sweeps (e.g., `nmap -sn 192.168.1.0/24`) to find which IP addresses are alive.
*   **Port Scanning:** The process of checking for open ports on a specific active host.
    *   **Purpose:** To identify available services (e.g., web server on port 80, SSH on port 22).
    *   **Method:** Using TCP/UDP scans (e.g., `nmap -sS 192.168.1.5`).
*   **Enumeration:** The process of extracting detailed information about the discovered services and hosts.
    *   **Purpose:** To gather usernames, machine names, network shares, and service banners.
    *   **Method:** Using tools like `enum4linux` for Windows/Samba systems or SNMP walk for network devices.

---

### 23. NMAP - OS Fingerprinting & Enumeration

**Answer:**
*   **OS Fingerprinting (`-O`):**
    *   **What:** Nmap sends a series of TCP, UDP, and ICMP probes to the target and analyzes the responses.
    *   **How:** It compares the unique quirks of the target's TCP/IP stack (like TCP window size, packet timing, and flag options) against a vast database of known OS signatures.
    *   **Use Case:** An attacker knows that a server is running an old, unpatched version of Windows Server, allowing them to use a specific exploit.
*   **System Hacking - Password (Post-Enumeration):**
    *   Once services are enumerated (e.g., finding SSH on port 22 or RDP on port 3389), an attacker may attempt to gain access.
    *   **Methods:**
        *   **Password Guessing/Cracking:** Using tools like `Hydra` or `John the Ripper` to perform brute-force or dictionary attacks.
        *   **Pass-the-Hash:** If NTLM hashes are enumerated from a Windows system, they can be reused for authentication without needing to crack the plaintext password.

---

### 24. ARP Poisoning, Session Hijacking, DNS Spoofing, SQL Injection

**Answer:**
1.  **ARP Poisoning:**
    *   **What:** Sending falsified ARP messages over a local network to link the attacker's MAC address with the IP address of a legitimate computer.
    *   **Use Case:** Man-in-the-Middle (MitM) attacks, allowing the attacker to intercept all traffic between two hosts.
2.  **Session Hijacking:**
    *   **What:** Exploiting a valid computer session to gain unauthorized access to information or services. Often involves stealing a session cookie.
    *   **Use Case:** Using an XSS attack to steal a user's session cookie and take over their logged-in account.
3.  **DNS Spoofing (DNS Cache Poisoning):**
    *   **What:** Corrupting the DNS cache of a server or resolver, causing it to return an incorrect IP address for a domain name.
    *   **Use Case:** Redirecting users from `mybank.com` to a fake, attacker-controlled website to steal login credentials.
4.  **SQL Injection:**
    *   **What:** Inserting or "injecting" a malicious SQL query via the input data from the client to the application.
    *   **Conducting the Attack:** Inputting `' OR '1'='1' -- ` into a login form. If vulnerable, this might log the attacker in as the first user in the database (often an administrator).

---

### 25. Key Loggers & Escalating Privileges

**Answer:**
*   **Key Loggers:**
    *   **What:** Software or hardware that records every keystroke made on a computer.
    *   **Types:**
        *   **Software-based:** A stealthy program running in the background.
        *   **Hardware-based:** A physical device plugged between the keyboard and computer.
    *   **Use Case:** Stealing passwords, credit card numbers, and other sensitive data typed by the user.
*   **Escalating Privileges:**
    *   **What:** The act of exploiting a bug, design flaw, or configuration oversight to gain elevated access to resources that are normally protected.
    *   **Types:**
        *   **Vertical (Privilege Escalation):** Gaining higher-level privileges (e.g., from a standard user to an administrator/root).
        *   **Horizontal:** Gaining access to the privileges of a different user of the same level (e.g., accessing another user's files).

---

### 26. SQL Injection

**Answer:**
*   **What:** A web security vulnerability that allows an attacker to interfere with the queries an application makes to its database.
*   **Why it's done:** To view, modify, or delete data they shouldn't have access to (user data, passwords), and sometimes to issue commands to the operating system.
*   **Why we need to understand it:** It's one of the most prevalent and dangerous web vulnerabilities. Understanding it is crucial for both developers (to prevent it) and security professionals (to test for it).
*   **Types:**
    1.  **In-band SQLi (Classic):** Using the same channel to launch the attack and gather results (e.g., Union-based, Error-based).
    2.  **Blind SQLi:** The database does not output data to the web page. The attacker asks the database true/false questions or triggers time delays to infer information.
    3.  **Out-of-band SQLi:** The attacker forces the database to send data to a remote endpoint they control (rare).
*   **Use Case:** An attacker inputs `'; DROP TABLE Users; --` into a search field. If the application is vulnerable, it could delete the entire "Users" table from the database.

---

### 27. Cookie Syncing

**Answer:**
*   **What:** A technique used in online advertising where multiple tracking companies (ad exchanges, data brokers) share anonymous user identifiers with each other.
*   **How it Works:**
    1.  You visit **Website A**, which has an ad from **Company X**. Company X places its cookie (ID: 123) in your browser.
    2.  **Website A** redirects your browser through **Company Y** (an ad exchange). Company Y doesn't know who you are yet, so it creates its own ID for you (ID: 456) and stores it in a cookie.
    3.  A pixel or script then allows **Company X** and **Company Y** to communicate. Company X tells Company Y: "The user with my ID 123 is the same as your ID 456."
    4.  Now, both companies have synced their cookies and can combine their separate profiles of you into a larger, more detailed one.
*   **Use Case:** Building comprehensive user profiles for highly targeted advertising across the web, even when third-party cookies are blocked or limited.
