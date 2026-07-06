---
layout: archive
title: "CryptoStudies"
permalink: /cryptostudies/
author_profile: true
---

{% include base_path %}

CryptoStudies
=============

CryptoStudies is my living research notebook for reading, categorizing, and comparing cryptography papers. The goal is to keep short, structured notes that make it easier to revisit papers, compare arguments across papers, and connect them to ongoing research work.

Current focus areas include symmetric cryptography, post-quantum cryptography, security proofs, cryptanalysis, protocols, and implementation issues.

Note on summaries
-----------------

The reading summaries on this page are generated with assistance from ChatGPT and then curated as part of my ongoing study process. They are intended as working notes, not authoritative paper reviews. If you notice any factual mistake, misinterpretation, missing context, or unclear phrasing, please let me know so I can correct and improve the notes.

Paper library
-------------

### Too Much Crypto

**Paper:** Jean-Philippe Aumasson, *Too Much Crypto*, IACR ePrint 2019/1492  
**Link:** [https://eprint.iacr.org/2019/1492](https://eprint.iacr.org/2019/1492)  
**Category:** Symmetric Cryptography; Cryptanalysis; Security Margins  
**Status:** First-pass study note  
**Summary note:** Generated with assistance from ChatGPT; subject to revision after further reading.

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

Update log
----------

* **2026-07-07:** Added a disclosure note that the summaries are generated with assistance from ChatGPT and should be treated as working notes.
* **2026-07-07:** Added the initial CryptoStudies page with the first study note on *Too Much Crypto*.

Planned additions
-----------------

* Add more papers by category.
* Add a reusable paper-note template.
* Add comparison tables for related papers.
* Track whether each note is a first-pass read, deep read, proof audit, or implementation-focused review.
