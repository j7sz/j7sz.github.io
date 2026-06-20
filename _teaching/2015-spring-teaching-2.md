---
title: "How DPI Can Inspect Encrypted Traffic over TLS in a Privacy-Preserving Manner"
collection: teaching
type: "Research Seminar / Tutorial"
permalink: /teaching/privacy-preserving-dpi-tls
venue: "National University of Singapore"
date: 2020-01-01
location: "Singapore"
---

## Overview

The widespread adoption of TLS encryption has rendered traditional **deep packet inspection (DPI)** — used by network middleboxes to detect anomalies and security threats — largely ineffective. This tutorial explores how DPI can be performed **directly over encrypted TLS traffic** without exposing users' plaintext data or an enterprise's proprietary inspection rule set, drawing on techniques from applied cryptography.

## What You Will Learn

- Why TLS encryption challenges conventional network security inspection, and what the threat model looks like
- What must remain private: user traffic (from the middlebox) and enterprise rules (from the middlebox provider)
- How BlindBox (SIGCOMM 2015) enables encrypted traffic inspection using **garbled circuits**, and the high setup latency this incurs
- How **PrivDPI** overcomes this with a new rule encryption technique and **reusable obfuscated rules**, reducing setup overhead by orders of magnitude
- How **Pine** extends privacy guarantees with **rule-hiding** and faster TLS connection establishment

## Related Publications

- [PrivDPI: Privacy-Preserving Encrypted Traffic Inspection with Reusable Obfuscated Rules](/publication/NPL+19) — CCS 2019 &nbsp;&nbsp; [[Slides]](https://j7sz.github.io/files/PrivDPI_slide.pdf)
- [Pine: Enabling Privacy-Preserving Deep Packet Inspection on TLS with Rule-Hiding and Fast Connection Establishment](/publication/NHP+20) — ESORICS 2020 *(Best Paper Award)*
