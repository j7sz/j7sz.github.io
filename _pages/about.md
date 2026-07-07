---
permalink: /
title: "About"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<div class="toolbar">
  <button onclick="document.querySelectorAll('.page__content details').forEach(function(d){d.open=true})">Expand all</button>
  <span>·</span>
  <button onclick="document.querySelectorAll('.page__content details').forEach(function(d){d.open=false})">Collapse all</button>
</div>

<details class="sec" open>
<summary><span class="eyebrow">About</span><span class="sec-title">Applied cryptography, from proofs to deployment</span></summary>
<div class="sec-body" markdown="1">

I am a Research Fellow at [Singapore Institute of Technology (SIT)](https://www.singaporetech.edu.sg/), Singapore, specialising in **applied cryptography** and **information security**. My research spans identity-based cryptography, digital signature security, secure multiparty computation, and privacy-preserving protocols. My current work investigates **post-quantum cryptography (PQC)** with a focus on deployment optimisation for resource-constrained IoT systems, particularly over the MQTTs protocol.

I received my Ph.D. from the University of Wollongong, Australia (2025), where my doctoral research centred on tightening security reductions for identity-based signatures using the Algebraic Group Model (AGM). Prior to my current appointment, I served as a Research Fellow (2025–2026) and previously as a Research Assistant (2019–2021) at the same laboratory at the National University of Singapore — known as NUS-Singtel Cyber Security Laboratory during my earlier tenure, and subsequently renamed NUS-NCS.

<div class="chips">
  <span class="chip">Identity-based cryptography</span>
  <span class="chip">Digital signatures</span>
  <span class="chip">Post-quantum crypto for IoT (MQTTs)</span>
  <span class="chip">Secure multiparty computation</span>
  <span class="chip">Privacy-preserving inspection</span>
  <span class="chip">AGM &amp; ROM proof techniques</span>
</div>

</div>
</details>

<details class="sec" open>
<summary><span class="eyebrow">Recognition</span><span class="sec-title">Awards</span></summary>
<div class="sec-body">

<div class="award-strip">
  <div class="award">
    <p class="what">Best Paper Award</p>
    <p class="where">ACISP 2024 · Australasian Conference on Information Security and Privacy</p>
  </div>
  <div class="award">
    <p class="what">Best Paper Award</p>
    <p class="where">ESORICS 2020 · European Symposium on Research in Computer Security</p>
  </div>
</div>

</div>
</details>

<details class="sec" open>
<summary><span class="eyebrow">Research output</span><span class="sec-title">Publications, by research theme</span></summary>
<div class="sec-body">

<details class="pub-group" open>
<summary>Identity-based signatures &amp; tight security proofs <span class="count">2 papers</span></summary>
<div class="pubs">
  <div class="pub">
    <div class="year">2024</div>
    <div>
      <p class="title"><a href="/publication/LGW24">Pairing-Free ID-Based Signatures as Secure as Discrete Logarithm in AGM</a><span class="badge-award">Best Paper</span></p>
      <p class="meta"><span class="venue">ACISP</span> · Loh, Guo, Susilo</p>
      <p class="links"><a href="https://j7sz.github.io/files/LGW24.pdf">Paper</a><a href="https://j7sz.github.io/files/Jason_ACISP24.pdf">Slides</a></p>
    </div>
  </div>
  <div class="pub">
    <div class="year">2023</div>
    <div>
      <p class="title"><a href="/publication/LGWY23">A Tightly Secure ID-Based Signature Scheme Under DL Assumption in AGM</a></p>
      <p class="meta"><span class="venue">ACISP</span> · Loh, Guo, Susilo, Yang</p>
      <p class="links"><a href="https://j7sz.github.io/files/LGWY23.pdf">Paper</a><a href="https://j7sz.github.io/files/Jason_ACISP23.pdf">Slides</a></p>
    </div>
  </div>
</div>
</details>

<details class="pub-group">
<summary>Anonymous credentials <span class="count">1 paper</span></summary>
<div class="pubs">
  <div class="pub">
    <div class="year">2024</div>
    <div>
      <p class="title"><a href="/publication/LGW24b">Improving Efficiency and Security of Camenisch–Lysyanskaya Signatures for Anonymous Credential Systems</a></p>
      <p class="meta"><span class="venue">Computer Standards &amp; Interfaces</span> · Loh, Guo, Susilo</p>
      <p class="links"><a href="https://j7sz.github.io/files/LGW24b.pdf">Paper</a></p>
    </div>
  </div>
</div>
</details>

<details class="pub-group">
<summary>Privacy-preserving traffic inspection <span class="count">2 papers</span></summary>
<div class="pubs">
  <div class="pub">
    <div class="year">2020</div>
    <div>
      <p class="title"><a href="/publication/NHP+20">Pine: Enabling Privacy-Preserving Deep Packet Inspection on TLS with Rule-Hiding and Fast Connection Establishment</a><span class="badge-award">Best Paper</span></p>
      <p class="meta"><span class="venue">ESORICS</span> · Ning, Huang, Poh, Xu, Loh, Weng, Deng</p>
      <p class="links"><a href="https://j7sz.github.io/files/NHP+20.pdf">Paper</a></p>
    </div>
  </div>
  <div class="pub">
    <div class="year">2019</div>
    <div>
      <p class="title"><a href="/publication/NPL+19">PrivDPI: Privacy-Preserving Encrypted Traffic Inspection with Reusable Obfuscated Rules</a></p>
      <p class="meta"><span class="venue">CCS</span> · Ning, Poh, Loh, Chia, Chang</p>
      <p class="links"><a href="https://j7sz.github.io/files/NPL+19.pdf">Paper</a><a href="https://j7sz.github.io/files/PrivDPI_slide.pdf">Slides</a></p>
    </div>
  </div>
</div>
</details>

<p style="margin-top: 12px"><a href="/publications/">All publications →</a></p>

</div>
</details>

<details class="sec" open>
<summary><span class="eyebrow">Research notebook</span><span class="sec-title">CryptoStudies</span></summary>
<div class="sec-body" markdown="1">

Structured study notes on cryptography papers I am reading — categorized by topic, with expandable notes for each paper. Recent additions include *CASPER* (USENIX Security 2025), a decoy-passkey breach detection framework for FIDO2 synced passkeys, and *Too Much Crypto* (IACR ePrint 2019/1492) on security margins of symmetric primitives.

[Browse all study notes →](/cryptostudies/)

</div>
</details>

---

<small>I would like to acknowledge that this web profile is managed with the assistance of [Claude Code](https://claude.ai/code) by Anthropic. Some content, including research summaries and descriptions, has been drafted or paraphrased by Claude Code; I may not be fully aware of every summarised statement, and errors or inaccuracies may be present. Should you notice any mistakes, please do not hesitate to contact me at [jason.loh@singaporetech.edu.sg](mailto:jason.loh@singaporetech.edu.sg).</small>
