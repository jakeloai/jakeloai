# Jake Lo

## Exploit-driven offensive security focused on initial access and real exposure, not compliance checklists or Nessus-monkey button-pushing.

Offensive Security Operator specializing in reconnaissance automation, external attack surface analysis, and infrastructure discovery.

Focused on scalable asset discovery workflows, exposure analysis, reconnaissance pipelines, and operational mapping across modern external environments.

Research interests include adversary reconnaissance methodology, exposed infrastructure analysis, attack surface expansion, and discovery automation.

<img width="3440" height="1440" alt="Initial Access" src="https://github.com/user-attachments/assets/25558ad6-cc2b-42ac-bbef-059cd075c88e" />

---

## Featured Methodology: 2026 Red Team Initial Access Workflow

A highly efficient, automation-friendly, and pure technical reconnaissance pipeline designed for modern penetration testing and red teaming engagements. This workflow focuses entirely on technical infrastructure, cloud environments, application logic, and supply chain vulnerabilities, bypassing traditional social engineering vectors.

### Workflow Architecture

```text
[Target: Company Name]
   │
   ├── Phase 1: OSINT & Architectural Reconnaissance (Passive)
   │     ├── EP1: Employee Reviews & Culture Analysis
   │     ├── EP2: Job Posts & Technical Stack Disclosure
   │     └── EP3: Certificate Transparency (CT) Logs Mining
   │
   ├── Phase 2: Asset & Service Enumeration (Active)
   │     ├── EP4: Multi-Layer Recursive Subdomains Enumeration
   │     ├── EP5: Hosting Server Open Ports & Censys/Shodan Mapping
   │     └── EP6: Cloud Resources & Storage Bucket Enumeration
   │
   ├── Phase 3: Web Application & API Deep Dive (Exploitation)
   │     ├── EP7: Web Path & Parameter Fuzzing
   │     ├── EP8: API Spec & Endpoint Leakage (Swagger/GraphQL)
   │     ├── EP9: Shadow AI & Chatbot Endpoints Exploitation
   │     ├── EP10: Web JS Crawling & Static Code Analysis (SAST)
   │     └── EP11: APK Decompilation & Client-Side Reverse Engineering
   │
   └── Phase 4: Code & Supply Chain Penetration (Persistence & High-Privilege Keys)
         ├── EP12: GitHub Public Repos & Commit History Leaks
         ├── EP13: Shadow Apps & Third-Party OAuth Integration Review
         └── EP14: Internal Dependency Confusion & Public Registry Exploitation

```

---

### Phase-by-Phase Technical Breakdown & Tool Mapping

#### Phase 1: OSINT & Architectural Reconnaissance (Passive)

*Objective: Build an operational model of the target's internal technologies, defense policies, and historical footprint without sending a single packet to their servers.*

##### EP1: Employee Reviews & Culture Analysis

* **Description:** Analyzing anonymous employee reviews to gauge internal IT policies, security friction, corporate structures, and infrastructure blind spots.
* **Primary Vectors:** Glassdoor, Indeed, local workplace forums.
* **Kali Linux Pre-installed:** firefox-esr (Manual reconnaissance via private browsing).
* **GitHub/External Tools:** [Google-Dorks Wordlists](https://www.google.com/search?q=https://github.com/theMiddleBlue/unofficial-google-dorks) for dorking corporate complaints.

##### EP2: Job Posts & Technical Stack Disclosure

* **Description:** Inspecting current and historical job vacancies. Engineering and DevOps postings often explicitly list exact versions of firewalls, SIEMs, databases, and cloud providers in use.
* **Primary Vectors:** LinkedIn, JobsDB, Indeed, company career pages.
* **Kali Linux Pre-installed:** Custom bash/python web scrapers.
* **GitHub/External Tools:** Browser extensions for profiling technology stacks (e.g., Wappalyzer API).

##### EP3: Certificate Transparency (CT) Logs Mining

* **Description:** Extracting all historical SSL/TLS certificates issued to the target organization to reveal forgotten or unmapped staging, UAT, or dev environments.
* **Primary Vectors:** [crt.sh](https://crt.sh/)
* **Kali Linux Pre-installed:** curl, jq (Parsing crt.sh JSON output directly via CLI).
* **GitHub/External Tools:** [ctfr](https://github.com/UnaPibaGeek/ctfr) (Instant subdomain pulling via CT logs).

---

#### Phase 2: Asset & Service Enumeration (Active)

*Objective: Map the external technical attack surface and isolate exposed assets that bypass enterprise firewalls or lack Multi-Factor Authentication (MFA).*

##### EP4: Multi-Layer Recursive Subdomains Enumeration

* **Description:** A deep-scanning redirection pipeline that utilizes initial findings to seed deeper dictionary attacks and multi-tiered domain discoveries.
* **Kali Linux Pre-installed:** dnsrecon, puredns.
* **GitHub/External Tools:** [subfinder](https://github.com/projectdiscovery/subfinder), [amass](https://github.com/owasp-amass/amass).
* > **Red Team Pro-Tip:** Run subfinder with -all -recursive flags. If the target asset footprint is massive, save the initial run to deep1.txt. Then, feed deep1.txt back into the scanner as a seed list to perform a secondary deep scan, outputting to deep2.txt to uncover multi-level internal routing domains.



##### EP5: Hosting Server Open Ports

* **Description:** Ultra-fast, low-noise port discovery combined with global internet scanning engines to identify exposed management panels, VPN gateways, or unauthenticated database nodes.
* **Kali Linux Pre-installed:** nmap (Crucial for fingerprinting via -sV and standard vulnerability scripts via -sC).
* **GitHub/External Tools:** [naabu](https://github.com/projectdiscovery/naabu) (Highly recommended for high-speed stateless scanning), [shodan-cli](https://github.com/achillean/shodan-python) (Querying Shodan Membership Accounts to view assets without direct interaction).

##### EP6: Cloud Resources & Storage Bucket Enumeration

* **Description:** Brute-forcing cloud asset naming conventions using subdomain assets as keywords to identify exposed storage containers across AWS, Azure, and GCP.
* **Kali Linux Pre-installed:** None (Requires external installation).
* **GitHub/External Tools:** [cloud_enum](https://github.com/initstring/cloud_enum) (The industry standard for multi-cloud discovery), [S3Scanner](https://github.com/sa7mon/S3Scanner).

---

#### Phase 3: Web Application & API Deep Dive (Exploitation)

*Objective: Analyze application-level logic, frontend code artifacts, and modern endpoints (including AI features) to capture backend keys and uncover unauthenticated routes.*

##### EP7: Web Path & Parameter Fuzzing

* **Description:** High-velocity directory, file, and HTTP parameter discovery using context-specific wordlists based on target technology profiling.
* **Kali Linux Pre-installed:** ffuf (The fastest engine for web fuzzing), gobuster, dirb.
* **GitHub/External Tools:** [Arjun](https://github.com/s0md3v/Arjun) (Discovers hidden HTTP query parameters frequently tied to debug modes or SSRF entry points).

##### EP8: API Spec & Endpoint Leakage (Swagger/GraphQL)

* **Description:** Parsing client-side routing logic and crawling web trees to locate exposed API documentation sheets or interactive query consoles.
* **Kali Linux Pre-installed:** burpsuite (Target SiteMap tree analysis).
* **GitHub/External Tools:** [katana](https://github.com/projectdiscovery/katana) (Crawling using the -js and -jc flags to aggressively pull API endpoints from minified scripts).

##### EP9: Shadow AI & Chatbot Endpoints Exploitation

* **Description:** Locating integrated conversational AI instances or embedded LLM web wrappers. Intercepting underlying API and WebSocket parameters to check for unauthenticated communication or susceptibility to prompt injection data leakage.
* **Kali Linux Pre-installed:** burpsuite (For intercepting, modification, and replaying WebSocket/HTTP requests directly via the Proxy and Repeater).
* **GitHub/External Tools:** [garak](https://github.com/leondz/garak) (Automated LLM vulnerability scanner).

##### EP10: Web JS Crawling & Static Code Analysis (SAST)

* **Description:** Downloading all client-side JavaScript components crawled by mapping tools, performing local secrets extraction, and running pattern matching to isolate logic flaws.
* **Kali Linux Pre-installed:** wget, curl, semgrep (Installable natively via apt install semgrep).
* **GitHub/External Tools:** [trufflehog](https://github.com/trufflesecurity/trufflehog) (Local filesystem secret hunting), [SecretFinder](https://github.com/m4ll0k/SecretFinder) (Regex mapping optimized specifically for JS files).
* > **Red Team Pro-Tip:** Pass your crawled URLs from katana into wget -i to pull all frontend source scripts locally. Then, construct customized local rules in semgrep to analyze code structures and expose logic vulnerabilities.



##### EP11: APK Decompilation & Client-Side Reverse Engineering

* **Description:** Extracting production or staging Android Application Packages (APKs) tied to the organization, deconstructing the code to source text, and auditing it for hardcoded infrastructure keys.
* **Kali Linux Pre-installed:** apktool (Package disassembly/reassembly).
* **GitHub/External Tools:** [jadx](https://github.com/skylot/jadx) (JADX-GUI is unbeatable for code tracking), [apkleaks](https://github.com/dwisiswant0/apkleaks).
* > **Red Team Pro-Tip:** When using JADX-GUI, search explicitly for "api key", "http://", and "https://". These queries return distinctly different asset structures. Filter down using high-value infrastructure keywords like internal, ip, server, and dev to track testing environments.



---

#### Phase 4: Code & Supply Chain Penetration (Persistence & High-Privilege Keys)

*Objective: Compromise development pipelines and code lineage histories to secure production-grade keys, third-party access, or code execution properties.*

##### EP12: GitHub Public Repos & Commit History Leaks

* **Description:** Auditing public enterprise repositories alongside the personal public repositories of identified developers for exposed secrets, checking the entire git commit history timeline.
* **Kali Linux Pre-installed:** git.
* **GitHub/External Tools:** [gitleaks](https://github.com/gitleaks/gitleaks) (Best-in-class commit history tracking), [GitHound](https://www.google.com/search?q=https://github.com/tillson/githound) (Utilizes GitHub search APIs to locate leaks across GitHub at scale).

##### EP13: Shadow Apps & Third-Party OAuth Integration Review

* **Description:** Researching third-party integration points (e.g., historical Slack bots, Vercel deployments, unmanaged SaaS apps linked via OAuth) to uncover dangling access chains.
* **Kali Linux Pre-installed:** Manual intelligence gathering.
* **GitHub/External Tools:** Custom integration mapping scripts.

##### EP14: Internal Dependency Confusion & Public Registry Exploitation

* **Description:** Inspecting application configurations (such as package.json, requirements.txt, or pom.xml mapped in Phase 3) for references to proprietary internal packages. If these internal naming conventions are unregistered on public package management registries, the namespace can be registered to induce package substitution attacks during build sequences.
* **Kali Linux Pre-installed:** None.
* **GitHub/External Tools:** [packj](https://www.google.com/search?q=https://github.com/ossilluminate/packj) (Audits software supply chains and detects package registry vulnerabilities).
* > **Red Team Pro-Tip:** This entry vector cannot be fully automated; it requires an in-depth understanding of the target system's build architecture and dependency paths. Look for uniquely named corporate internal namespaces.



---

### Execution Strategy Summary

To maximize speed and maintain structural clarity during a red team engagement, run the workflow sequentially: Use the intelligence gained in Phase 1 to inform the asset lists in Phase 2, feed the discovered web perimeters into Phase 3 for deep exploit analysis, and leverage all leaked code configurations to check for supply chain pivots in Phase 4.

---

## Contact

* Email: hello@jakelo.ai
