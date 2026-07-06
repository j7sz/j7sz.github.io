---
layout: archive
title: "CryptoStudies"
permalink: /cryptostudies/
author_profile: true
---

{% include base_path %}

<style>
/* Category section */
details.cs-category {
  margin: 1.2em 0;
  border: 1px solid #d7e8ef;
  border-radius: 8px;
  overflow: hidden;
  background: #fff;
}
details.cs-category > summary {
  cursor: pointer;
  list-style: none;
  padding: 0.8em 1em;
  font-size: 1.15em;
  font-weight: 700;
  color: #2c3e50;
  background: linear-gradient(135deg, #f4fafd, #eaf4f9);
  border-left: 4px solid #52adc8;
  transition: background 0.2s ease;
}
details.cs-category > summary:hover {
  background: linear-gradient(135deg, #eaf6fb, #ddeef6);
}
details.cs-category[open] > summary {
  border-bottom: 1px solid #d7e8ef;
}
details.cs-category > .cs-category-body {
  padding: 0.9em 1em;
}

/* Paper note card */
details.cs-paper {
  margin: 0.8em 0;
  border: 1px solid #e3edf2;
  border-radius: 6px;
  background: #fcfeff;
}
details.cs-paper > summary {
  cursor: pointer;
  list-style: none;
  padding: 0.65em 0.9em;
  font-weight: 600;
  color: #34495e;
  transition: color 0.2s ease, background 0.2s ease;
}
details.cs-paper > summary:hover {
  color: #52adc8;
  background: #f4fafd;
}
details.cs-paper[open] > summary {
  color: #52adc8;
  border-bottom: 1px dashed #d7e8ef;
}
details.cs-paper > .cs-paper-body {
  padding: 0.9em 1.1em;
}
details.cs-paper .cs-paper-meta {
  font-size: 0.92em;
  color: #5d6d7e;
}

/* Arrow indicators */
details.cs-category > summary::before,
details.cs-paper > summary::before {
  content: '▸';
  display: inline-block;
  margin-right: 0.5em;
  color: #52adc8;
  transition: transform 0.2s ease;
}
details.cs-category[open] > summary::before,
details.cs-paper[open] > summary::before {
  transform: rotate(90deg);
}
details.cs-category > summary::-webkit-details-marker,
details.cs-paper > summary::-webkit-details-marker {
  display: none;
}

/* Small utility sections */
details.cs-aside {
  margin: 0.8em 0;
  border-left: 3px solid #d7e8ef;
  padding-left: 0.9em;
}
details.cs-aside > summary {
  cursor: pointer;
  list-style: none;
  font-weight: 600;
  color: #5d6d7e;
  padding: 0.3em 0;
}
details.cs-aside > summary:hover { color: #52adc8; }
details.cs-aside > summary::before {
  content: '▸';
  display: inline-block;
  margin-right: 0.45em;
  color: #52adc8;
  transition: transform 0.2s ease;
}
details.cs-aside[open] > summary::before { transform: rotate(90deg); }
details.cs-aside > summary::-webkit-details-marker { display: none; }
</style>

CryptoStudies is my living research notebook for reading, categorizing, and comparing cryptography papers. The goal is to keep short, structured notes that make it easier to revisit papers, compare arguments across papers, and connect them to ongoing research work.

Current focus areas include symmetric cryptography, post-quantum cryptography, security proofs, cryptanalysis, protocols, and implementation issues. Click a category below to expand it, then click a paper title to open its study note.

**Note on summaries:** The reading summaries on this page are generated with assistance from AI tools (ChatGPT and Claude Code) and then curated as part of my ongoing study process. They are intended as working notes, not authoritative paper reviews. If you notice any factual mistake, misinterpretation, missing context, or unclear phrasing, please let me know so I can correct and improve the notes.

Paper library
-------------

<details class="cs-category" open>
<summary>Authentication &amp; Passkeys</summary>
<div class="cs-category-body" markdown="1">

<details class="cs-paper">
<summary>CASPER: Detecting Compromise of Passkey Storage on the Cloud (USENIX Security 2025)</summary>
<div class="cs-paper-body" markdown="1">

<div class="cs-paper-meta" markdown="1">
**Paper:** Mazharul Islam, Sunpreet S. Arora, Rahul Chatterjee, Ke Coby Wang, *Detecting Compromise of Passkey Storage on the Cloud*, 34th USENIX Security Symposium, 2025  
**Link:** [https://www.usenix.org/conference/usenixsecurity25/presentation/islam](https://www.usenix.org/conference/usenixsecurity25/presentation/islam)  
**Category:** Authentication; FIDO2/Passkeys; Breach Detection; Decoy-Based Defences  
**Status:** Hands-on study — replicated and explored in my companion repo [Pollo — The CASPER Saver](https://github.com/j7sz/Pollo---The-CASPER-saver)  
**Summary note:** Generated with assistance from Claude Code; subject to revision after further reading.
</div>

**Core question:** When users back up their FIDO2 synced passkeys to the cloud storage of a passkey management service (PMS), how can a website detect that those passkeys have been stolen and are being abused for unauthorized logins?

**Main idea:** CASPER ("Capturing pASskey comPromise by attackER") is the first passkey breach detection framework that lets web service providers detect the abuse of passkeys leaked from a PMS. Synced passkeys solve the account-recovery problem of device-bound credentials, but they concentrate risk: a breach of the PMS cloud storage exposes users' private signing keys. Rather than trying to prevent theft, CASPER detects misuse — it adapts the classic *honeywords* idea (decoy passwords planted alongside real ones) from the password setting to the passkey setting, planting decoy passkeys in the PMS backup so that a login attempt using a decoy signals that the storage has been breached.

**Key concepts:**

* Synced passkeys trade device-bound security for recoverability, making the PMS cloud storage a high-value breach target.
* Decoy-based detection: an attacker who steals the backup cannot reliably distinguish real passkeys from planted decoys; using a decoy at login reveals the compromise.
* Detection as a complement to prevention — the framework assumes the breach can happen and focuses on catching exploitation.
* The design analyses detection effectiveness against strategic attackers who optimize which stolen credentials to try, and under partial marking of sites.
* Deployability: CASPER integrates into existing passkey backup, synchronization, and authentication flows with minimal user-experience impact and negligible performance overhead.

**Hands-on study:**

I explored CASPER beyond the paper in my repo [Pollo — The CASPER Saver](https://github.com/j7sz/Pollo---The-CASPER-saver), which includes an interactive Python notebook walking through the detection simulations (runnable via Binder), a Go proof-of-concept prototype of the login and detection flows, and PRISM model-checking scripts evaluating detection probability across parameters such as the number of snapshots, number of sites, and the fraction of unmarked sites. The official artifact from the authors is available at [islamazhar/CASPER](https://github.com/islamazhar/CASPER).

**Study takeaway:**

CASPER is a nice example of transplanting a mature defensive idea (honeywords) into a new authentication ecosystem (FIDO2 synced passkeys) while carefully respecting that ecosystem's constraints — no protocol changes for legitimate users, and a threat model where the attacker fully controls the stolen backup. It also connects naturally to my broader interest in deployment-oriented cryptographic engineering: the hard part is not the cryptographic trick itself, but making detection statistically meaningful against adaptive attackers at negligible deployment cost.

</div>
</details>

</div>
</details>

<details class="cs-category" open>
<summary>Symmetric Cryptography &amp; Cryptanalysis</summary>
<div class="cs-category-body" markdown="1">

<details class="cs-paper">
<summary>Too Much Crypto (IACR ePrint 2019/1492)</summary>
<div class="cs-paper-body" markdown="1">

<div class="cs-paper-meta" markdown="1">
**Paper:** Jean-Philippe Aumasson, *Too Much Crypto*, IACR ePrint 2019/1492  
**Link:** [https://eprint.iacr.org/2019/1492](https://eprint.iacr.org/2019/1492)  
**Category:** Symmetric Cryptography; Cryptanalysis; Security Margins  
**Status:** First-pass study note  
**Summary note:** Generated with assistance from ChatGPT; subject to revision after further reading.
</div>

**Core question:** Are some widely deployed symmetric primitives using more rounds than real-world security requires?

**Main idea:** The paper argues that many modern symmetric primitives were designed with conservative round counts, often under competition-era uncertainty. After years of cryptanalysis, the author suggests that some primitives may retain realistic security with fewer rounds, improving performance while preserving practical security.

**Key concepts:**

* Distinguishing academic attacks from practical attacks.
* Treating security as risk management rather than a binary broken/not-broken label.
* Evaluating how far the best known attacks are from full-round practical exploitation.
* Reconsidering security margins after years of public cryptanalysis.

**Attack-status taxonomy from the paper:**

* **Analyzed:** The primitive has been studied using its internal structure, but no meaningful attack beats generic expectations.
* **Attacked:** There is a technically better-than-generic attack, but it remains practically infeasible.
* **Wounded:** The attack is not practical yet, but it is close enough that improvements could matter.
* **Broken:** The attack is realistically exploitable now or in the near future.

**Reduced-round discussion:**

The paper discusses reduced-round variants of AES, BLAKE2, ChaCha, and SHA-3. Its central claim is not simply that fewer rounds are faster, but that the cost of extra rounds should be weighed against the actual security margin demonstrated by cryptanalysis.

**Study takeaway:**

This paper is useful as a risk-assessment reading. It challenges the habit of treating every non-generic cryptanalytic result as equally alarming, and it asks whether cryptographic engineering should distinguish more carefully between theoretical, impractical, near-practical, and practical attacks.

</div>
</details>

</div>
</details>

<details class="cs-aside">
<summary>Update log</summary>
<div markdown="1">

* **2026-07-07:** Reorganized the page into categorized, expandable sections for easier navigation.
* **2026-07-07:** Added a study note on *CASPER* (USENIX Security 2025) with links to my hands-on companion repo, Pollo — The CASPER Saver.
* **2026-07-07:** Added a disclosure note that the summaries are generated with assistance from AI tools (ChatGPT and Claude Code) and should be treated as working notes.
* **2026-07-07:** Added the initial CryptoStudies page with the first study note on *Too Much Crypto*.

</div>
</details>

<details class="cs-aside">
<summary>Planned additions</summary>
<div markdown="1">

* Add more papers by category.
* Add a reusable paper-note template.
* Add comparison tables for related papers.
* Track whether each note is a first-pass read, deep read, proof audit, or implementation-focused review.

</div>
</details>
