# Errata Reports

Total reports: 2

---

## Report 1: 9761-10-1

**Label:** Over‑broad and Underspecified ‘MUD URL MUST be encrypted’ Requirement Conflicts with RFC 8520 Emission Mechanisms

**Bug Type:** Both

**Explanation:**

Section 10 mandates that the MUD URL MUST be encrypted and shared only with authorized components without defining the encryption mechanism, applicable emission methods, or responsible entity, causing a conflict with RFC 8520’s clear yet unencrypted emission methods.

**Justification:**

- RFC 9761 Section 10 applies a blanket MUST for encrypting the MUD URL without qualification, which is not supported by the emission methods defined in RFC 8520. (E1)
- RFC 8520 Section 1.5 permits the MUD URL to be emitted via DHCP, LLDP, or X.509 without requiring on‐wire encryption. (E2)
- The text fails to specify which encryption techniques (e.g., TEAP/EAP-TLS, MACsec, WPA2, IPsec) or network segments must be protected, creating ambiguous implementation guidance. (E3)

**Evidence Snippets:**

- **E1:**

  RFC 9761 Section 10: “The MUD URL MUST be encrypted and shared only with the authorized components in the network (see Sections 1.5 and 1.8 of [RFC8520]) so that an on-path attacker cannot read the MUD URL and identify the IoT device.”

- **E2:**

  RFC 8520 Section 1.5: defines three ways for a device to *emit* the MUD URL: DHCP option, LLDP frame, or X.509 certificate extension, and notes “Implementors are encouraged to allow for the flexibility of how MUD URLs may be learned.” There is no requirement that these emissions are encrypted on the wire.

- **E3:**

  Without specifying the relevant layer and threat model, the scope of “MUST be encrypted” is unclear and not interoperable.

**Evidence Summary:**

- (E1) shows that RFC 9761 imposes an unconditional encryption mandate.
- (E2) demonstrates that RFC 8520 allows for unencrypted emission methods.
- (E3) highlights the lack of clarity on which encryption mechanisms and network segments must be protected.

**Fix Direction:**

Clarify the requirement by explicitly stating which emission methods are subject to encryption and specifying acceptable encryption mechanisms (e.g., TEAP/EAP-TLS, MACsec) and the responsible network component, or limit the mandate to new TEE storage contexts.


---

## Report 2: 9761-10-2

**Label:** Awkward Phrasing of (D)TLS Proxies Recommendation in Section 10

**Bug Type:** None

**Explanation:**

The statement ‘The use of (D)TLS proxies is NOT RECOMMENDED whenever possible’ is stylistically awkward and could be clarified, though it does not create a normative inconsistency.

**Justification:**

- The phrasing ‘NOT RECOMMENDED whenever possible’ is non-standard and may be misinterpreted compared to typical BCP 14 language. (E1)
- Despite the awkward wording, the specification still provides a normative framework for proxy behavior, ensuring compliant operation if used. (E2)

**Evidence Snippets:**

- **E1:**

  The use of (D)TLS proxies is NOT RECOMMENDED whenever possible.

- **E2:**

  To obtain more visibility into negotiated TLS 1.3 parameters, a middlebox can act as a (D)TLS 1.3 proxy. The middlebox MUST adhere to the invariants discussed in Section 9.3 of [RFC8446] to act as a compliant proxy.

**Evidence Summary:**

- (E1) provides the exact wording that is awkwardly phrased.
- (E2) indicates that although (D)TLS proxies are discouraged, their use is still normatively defined if deployed.

**Fix Direction:**

Rephrase the sentence to align with standard BCP 14 language, for example: 'The use of (D)TLS proxies SHOULD be avoided whenever possible.'


---
