---
layout: archive
title: "Zero-Knowledge Middleboxes — USENIX Security 2022"
permalink: /cryptostudies/zkmbs/
author_profile: true
---

{% include base_path %}

[← Back to CryptoStudies](/cryptostudies/)

Zero-Knowledge Middleboxes — USENIX Security 2022
===================================================

**Paper:** Paul Grubbs, Arasu Arun, Ye Zhang, Joseph Bonneau, and Michael Walfish, *Zero-Knowledge Middleboxes*, 31st USENIX Security Symposium (USENIX Security 2022), pp. 4255–4272  
**Official publication:** [USENIX Security 2022](https://www.usenix.org/conference/usenixsecurity22/presentation/grubbs)  
**Preprint:** [IACR ePrint 2021/1022](https://eprint.iacr.org/2021/1022)  
**Source code:** [https://github.com/pag-crypto/zkmbs](https://github.com/pag-crypto/zkmbs)  
**Category:** Zero-Knowledge Proofs; Network Security; TLS 1.3; Privacy-Preserving Middleboxes  
**Status:** Paper-and-code study  
**Summary note:** Generated with assistance from ChatGPT and curated as a working research note. Technical claims should be checked against the paper and implementation before citation.

Overview
--------

The paper studies how a network middlebox can enforce policies over encrypted traffic without learning the plaintext. Instead of giving the middlebox decryption capability, a client supplies a zero-knowledge proof that its encrypted communication satisfies the required policy.

The core architectural shift is:

1. The client retains the plaintext and cryptographic secrets.
2. The middlebox observes the encrypted flow and public protocol transcript.
3. The client proves that the encrypted traffic corresponds to a policy-compliant plaintext.
4. The proof should reveal no additional information beyond policy compliance.

This is a strong privacy goal, but it moves substantial work into the proof circuit. The practical question is therefore not only whether the construction is sound and zero knowledge, but whether TLS processing, parsing, policy evaluation, and channel binding can be represented efficiently enough in a SNARK circuit.

Core research questions
-----------------------

* How can a proof be cryptographically bound to a real encrypted channel rather than to an arbitrary plaintext chosen by the prover?
* Which parts of TLS 1.3 must be represented inside the circuit?
* How can expensive channel-opening work be reduced or amortized?
* Which middlebox policies are sufficiently structured to encode efficiently?
* What information is still leaked through metadata, traffic shape, timing, and the policy result itself?

Construction at a high level
----------------------------

A ZK middlebox proof generally needs to establish three linked facts:

**Channel consistency.** The prover knows the relevant TLS secrets or key-schedule inputs and derives the same traffic keys associated with the observed connection.

**Plaintext consistency.** The ciphertext decrypts under those keys to the witness plaintext supplied inside the circuit.

**Policy compliance.** The recovered application data satisfies the policy circuit, such as a firewall rule or a DNS blocklist condition.

The security argument relies on preserving this chain. If the proof checks the policy but is not correctly bound to the observed TLS channel, a malicious client could prove a benign statement about unrelated data while sending disallowed traffic.

Channel-opening strategies
--------------------------

The implementation exposes several channel-opening designs:

| Circuit | Paper label | Purpose |
|---|---|---|
| `ChannelBaseline` | BCO | Baseline channel opening with the largest circuit cost. |
| `ChannelShortcut` | SCO | Reduces channel-opening work using a more efficient proof path. |
| `Channel0RTT` | ECO | Uses an early/0-RTT-oriented opening strategy. |
| `ChannelAmortized` | ACO-AES | Amortizes expensive setup or channel validation across records using AES-based processing. |
| `ChannelAmortized_ChaCha` | ACO-ChaCha | Amortized design using ChaCha, with a smaller reported circuit than the AES version. |

The repository's sample reproduction results report a substantial reduction in circuit size and proving time from the baseline to the amortized constructions. These values are implementation measurements, not asymptotic security claims.

Case studies
------------

### Firewall enforcement

The firewall circuit demonstrates policy enforcement over encrypted traffic. The circuit must connect the encrypted record to the witness plaintext and then evaluate the relevant rule. The implementation includes an end-to-end firewall module and a `Firewall_HS` experiment target.

### Encrypted DNS filtering

The DNS case study checks encrypted DNS traffic carried over mechanisms such as DNS-over-TLS and DNS-over-HTTPS. The circuit parses the DNS request, extracts the queried label, and evaluates a Merkle-tree non-membership proof showing that the name is not in a blocklist.

The repository identifies the following important components:

* `e2eDNS/DNS_Shortcut_dot.java`: full encrypted DNS policy check using shortcut channel opening.
* `e2eDNS/LabelExtraction.java`: extracts a domain name from DoT, DoH POST, or DoH GET messages.
* `membership_merkle/non_membership`: verifies Merkle non-membership, including wildcard support.

### Oblivious DNS-over-HTTPS

The ODoH case study extends the approach to a setting with an additional privacy layer. Its circuit must preserve the relevant end-to-end bindings while proving compliance over data hidden from the enforcing middlebox.

Paper-to-code map
-----------------

| Paper concept | Repository location or target |
|---|---|
| TLS 1.3 channel opening | `TLSKeySchedule` and channel circuit programs |
| AES record processing | `aes_gcm` module |
| ECDHE operations | `ecdhe` module |
| Hashing and utility logic | `util_and_sha` |
| Merkle policy proofs | `membership_merkle` |
| DNS policy circuits | `e2eDNS` |
| Firewall policy circuits | `e2eFirewall` |
| ODoH circuits | `e2eODOH` |
| Human-readable DSL extraction | `readable_code` |
| Generated Java circuit code | `gen/src/xjsnark/` |
| Original MPS models | `xjsnark_zkmb/` |
| TLS transcript generation | `tls_testing/` |

Implementation architecture
---------------------------

The code is built around xJsnark, a Java-based circuit-generation DSL. The repository distinguishes between:

* **Programs**, which declare public inputs, witnesses, and the end-to-end circuit algorithm.
* **Classes**, which provide reusable circuit functionality such as cryptographic primitives, parsing, key derivation, and Merkle verification.

The `readable_code` directory contains extracted source-like files for inspection without JetBrains MPS. They use a `.java` extension for syntax highlighting but represent the xJsnark DSL rather than ordinary handwritten Java.

Build and reproduction workflow
-------------------------------

The repository's documented workflow is:

```bash
git clone https://github.com/pag-crypto/zkmbs.git
cd zkmbs
./install_deps_jsnark
cd gen
./compile_circuits
```

The authors recommend a machine with at least 32 GB RAM and 8 cores. The baseline channel-opening circuit can exceed the practical memory capacity of a 16 GB machine.

To reproduce aggregate circuit counts:

```bash
cd gen
./reproduce_total_counts
```

To reproduce proving time, SRS size, and verification time:

```bash
cd gen
./reproduce_times_srs
```

For an individual target:

```bash
./generate_circuit DNS_Amortized_ChaCha
./prove_and_verify DNS_Amortized_ChaCha
```

The generated `.arith` and `.in` files are then processed through jsnark/libsnark. The documented `gg` option selects Groth16.

Selected implementation observations
------------------------------------

* The repository reports verifier times in the low-millisecond range for its sample experiments, while proving takes seconds to tens of seconds depending on the circuit.
* The proving key or SRS footprint is significant, ranging from tens of megabytes to more than one gigabyte in the sample results.
* The baseline construction is much more expensive than the amortized designs.
* The ChaCha-based amortized circuit is reported as smaller and faster than the corresponding AES-based amortized circuit in the provided sample output.
* Proof generation is randomized, and the repository warns that single-run reproduction may differ from the paper's median-of-five measurements.

Security interpretation
-----------------------

The construction should be evaluated along several dimensions:

**Soundness.** A malicious client should not be able to convince the middlebox that disallowed traffic is compliant.

**Zero knowledge.** The proof should not reveal the plaintext, keys, or other witness information beyond the statement being proved.

**Channel binding.** The proof must refer to the actual encrypted connection accepted by the middlebox.

**Freshness and replay resistance.** A valid proof for one record or session should not be reusable for a different unauthorized flow.

**Policy correctness.** The circuit must encode the intended operational policy exactly; errors in parsing, wildcard handling, canonicalization, or blocklist representation can become security vulnerabilities even if the SNARK itself is sound.

Strengths
---------

* It presents a principled alternative to TLS interception and key-sharing middleboxes.
* It treats encrypted traffic policy enforcement as a verifiable-computation problem rather than weakening transport encryption.
* The paper is accompanied by substantial implementation artifacts and reproducibility scripts.
* The channel-opening variants make the main systems bottleneck explicit and measurable.
* The case studies cover distinct policy types rather than a single toy predicate.

Limitations and deployment concerns
----------------------------------

* Client-side proving cost is high for interactive or resource-constrained environments.
* Circuit-specific setup material can be large.
* Encoding TLS key schedules, parsing, and cryptographic primitives inside a circuit creates a large trusted implementation surface.
* The approach does not hide ordinary network metadata such as endpoint, timing, packet sizes, or connection frequency.
* Policy updates may require new circuits, keys, or setup material depending on how the policy is represented.
* A malicious endpoint can still transmit information through allowed channels or covert encodings unless the policy captures the full intended semantics.
* The repository reflects the cryptographic and tooling ecosystem available at the time; current proving systems may offer different trade-offs.

Questions for deeper study
--------------------------

1. Exactly which values are public inputs in each channel-opening construction?
2. How is the TLS transcript bound to the SNARK statement?
3. Which assumptions are required beyond the security of TLS 1.3 and the SNARK?
4. What changes when moving from AES-GCM to ChaCha20-Poly1305?
5. How are malformed DNS encodings, compression, capitalization, and wildcard rules handled?
6. Can lookup arguments, modern polynomial commitment schemes, or specialized hash functions reduce the circuit cost?
7. Could recursive proofs aggregate multiple records or policies?
8. How would the design behave on constrained gateways, mobile devices, or IoT endpoints?
9. Which parts of the implementation should be independently audited for soundness-critical bugs?

Study takeaway
--------------

The central contribution is not merely "use a SNARK for firewall rules." The difficult part is securely linking a private policy witness to a real TLS session while keeping the proof system practical. The paper's channel-opening constructions and code organization show that protocol binding, cryptographic circuit cost, and parsing correctness dominate the engineering problem.

For cryptographic systems research, this work is a useful case study in the gap between an elegant zero-knowledge statement and a deployable end-to-end system. The proof primitive is only one component; secure deployment depends equally on transcript binding, circuit correctness, policy semantics, setup management, and client-side performance.
