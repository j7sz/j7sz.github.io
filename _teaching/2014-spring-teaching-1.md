---
title: "Achieving Tight Security for Signatures under (EC)DL with the AGM and ROM"
collection: teaching
type: "Research Seminar / Tutorial"
permalink: /teaching/tight-reduction-signatures-agm
venue: "University of Wollongong"
date: 2024-01-01
location: "Wollongong, Australia"
---

## Overview

Classical security proofs for digital signature schemes often suffer from a large **reduction loss** — meaning the security guarantee weakens significantly when reducing the scheme's security to an underlying hard problem such as the discrete logarithm (DL). This tutorial explores how the **Algebraic Group Model (AGM)**, combined with the **Random Oracle Model (ROM)**, enables the construction of signature schemes with **tight security reductions** under the (EC)DL assumption.

## What You Will Learn

- What a security reduction is, and why tightness matters in practical parameter selection
- How the AGM idealises adversarial computation (every group element output includes its algebraic representation) to unlock tighter proofs
- How to extend the AGM framework to **identity-based signatures (IBS)** — where the signer's identity serves directly as the public key
- The OR-proof technique for achieving tight EUF-CMA security against chosen identity-and-message attacks in the IBS setting

## Related Publications

- [A Tightly Secure ID-Based Signature Scheme Under DL Assumption in AGM](/publication/LGWY23) — ACISP 2023 &nbsp;&nbsp; [[Slides]](https://j7sz.github.io/files/Jason_ACISP23.pdf)
- [Pairing-Free ID-Based Signatures as Secure as Discrete Logarithm in AGM](/publication/LGW24) — ACISP 2024 &nbsp;&nbsp; [[Slides]](https://j7sz.github.io/files/Jason_ACISP24.pdf)
