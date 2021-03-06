---
layout: notes
title: Traffic Shaping for Electronic Surveillance
author: Kristel Tan
---

## Presentation: Cloudbleed

* What is Cloudflare? They are a content distribution network (CDN) 
  * HTML parser created by Cloudflare had a memory leak bug and leaked data was cached by search engines automatically 

* How the Bug Works
  * Malformed HTML tags like this would trigger the bug (i.e. <script type= )
  * This would trigger the buffer overrun and returns raw server memory that is displayed on the page
  * Well-formed HTML tags wouldn’t trigger the bug
  
* Single Point of Failure
  * TSL/SSL were not broken or misused
  * Authentication was not compromised
  * The problem was not with the security of client-server communications, but rather the single point of failure was Cloudflare 

* Prevention
  * Tagged memory
  * Sandbox their servers
  * Evaluate legacy code thoroughly

## Traffic Shaping for Electronic Surveillance

* Talk Overview
  1. The “collection abroad” loophole in US surveillance law
  2. Using port mirroring to “shape” US traffic
  3. Using routing hijacks to “shape” US traffic abroad
  4. Recommendations for surveillance policy
  5. Recommendations for securing routing

* Primary Argument: Collection in the US vs. collection abroad does not sufficiently distinguish US and foreigners

### “Collection Abroad” Loophole in US Surveillance Law

* Foreign Intelligence Surveillance Act (FISA) — a lot more oversight
  * FISA is the “exclusive means” on “electronic surveillance”
  * Electronic surveillance under FISA is defined as (roughly)
  * Surveillance operations conducted on US soil, OR
  * Surveillance operations that “intentionally target a US person”
  * Programs must be authorized by the secret FISA court (regular judges, not NSA employees)
  * Criminal liabilities for violations
  * If you do collection outside of the US, you are subject to less stringent rules than doing it inside the US
  * Surveillance of Internet traffic that is collected abroad, AND does not “intentionally target a US person” is exclusively under Executive 12333
  * What does “intentional targeting” mean? 
    * If in the process of intentionally targeting someone, you also receive information about other related parties, this is called “incidental collection”

* Executive Order 12333 — a lot less oversight
  * Order signed by Regan in 1981
  * Self-imposed rules Executive follows when conducting intelligence activities beyond those regulated by Congress
  * The NSA stated that it “conducts the majority of its SIGINT activities solely pursuant to the authority”
  * No court oversight (Just AG-approved procedures)

* US persons’ communications can naturally flow abroad

- ["NSA Presentation on Google Cloud Exploitation"](https://www.washingtonpost.com/world/national-security/nsa-infiltrates-links-to-yahoo-google-data-centers-worldwide-snowden-documents-say/2013/10/30/e51d661e-4166-11e3-8b74-d89d714ca4dd_story.html?utm_term=.133bd4f77383)

* What if the same info is collected under FISA & EO 12333?
  * If I could have collected this data in the US, but collected it outside, what laws apply?
  * If you query something outside you the US, you can collect it under EO 12333 (less strict rule)

* Why the domestic email metadata program (PRTT) was shut down
  * PRTT = domestic email collection program
  * Allows NSA to call-chain from, to, or through US person selectors

### Using Port Mirroring to “Shape” US Traffic Abroad

* To use port mirroring to shape US traffic abroad:
  * A router on US soil must be hacked and instructed to shape traffic to a tapped cable abroad where traffic will be collected under EO 12333
* Key question: does hacking into a US router & instructing it to port mirror traffic constitute “electronic surveillance” under FISA?
  * “Electronic surveillance” = wire or radio communication

* Is hacking a US router covered by the 4th Amendment?
  * Bottom line: we don’t know the government’s interpretation, but they might not consider hacking a US router as covered by the 4th Amendment
  * We can do traffic shaping without hacking on US soil

### Using Routing Hijacks to “Shape” US Traffic Abroad

* Internet routing with BGP
  * 206.51.64.0/19 — the first 19 bits of this IP address is the same as the other IP address 206.51.69.20
  
* Surveillance policy recommendations
  * Update FISA so that it covers all types of “electronic surveillance”
  * FISA Amendments Act up for renewal in December 2017

* The RPKI stops all subprefix hijacks
  * The forged-origin hijack circumvents the RPKI!
  * Choose the cheaper route


