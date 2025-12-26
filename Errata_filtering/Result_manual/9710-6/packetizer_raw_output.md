# Errata Reports

Total reports: 2

---

## Report 1: 9710-6-1

**Label:** Stray closing parenthesis in Section 6.24.2 for NAT Threshold Event registry URL

**Bug Type:** Editorial punctuation error

**Explanation:**

A stray closing parenthesis appears after the NAT Threshold Event registry URL in Section 6.24.2, which is an editorial issue that does not affect field format or semantics.

**Justification:**

- The analysis notes a stray closing parenthesis after the NAT Threshold Event registry URL in Section 6.24.2, stating it is purely editorial punctuation without impact.

**Evidence Snippets:**

- **E1:**

  The only minor textual oddity is a stray closing parenthesis after the NAT Threshold Event registry URL in Section 6.24.2 (“ipfix]).”), but this is purely editorial punctuation and does not affect any field format, identifier, or registry structure.

**Evidence Summary:**

- (E1) The analysis highlights a stray closing parenthesis after the NAT Threshold Event registry URL in Section 6.24.2, noting it is solely an editorial issue.

**Fix Direction:**

Remove the stray closing parenthesis from the affected registry URL in Section 6.24.2.

**Severity:** Low
  *Basis:* This is a minor editorial issue affecting only punctuation, with no impact on technical functionality or interpretation.

**Confidence:** High

**Experts mentioning this issue:**

- Structural Expert: Issue-1

---

## Report 2: 9710-6-2

**Label:** Overly high-level reference for NAT46 using RFC6144 may cause ambiguity

**Bug Type:** Editorial/reference clarity issue

**Explanation:**

The text notes that RFC6144 is used as the reference for NAT46 in a high-level manner, which may benefit from further clarification despite not causing direct conflict.

**Justification:**

- The analysis comments that using RFC6144 as the reference for NAT46 is somewhat high‑level, suggesting that a more precise reference (such as RFC6145 for IP/ICMP translation) might improve clarity.

**Evidence Snippets:**

- **E2:**

  Using RFC6144 as the reference for NAT46 is somewhat high‑level (6144 is the framework for IPv4/IPv6 translation and terminology , while RFC6145 carries the IP/ICMP translation algorithm), but it is not contradictory and still points implementers at the correct family of specs.

**Evidence Summary:**

- (E2) The analysis observes that the use of RFC6144 as the reference for NAT46 is notably high-level, which could be perceived as less precise compared to referencing RFC6145.

**Fix Direction:**

Consider clarifying the rationale for using RFC6144 for NAT46 and, if appropriate, include additional or more specific references to provide clearer guidance.

**Severity:** Low
  *Basis:* This is an editorial observation that might lead to slight ambiguity, but it does not result in conflicting interpretations or technical errors.

**Confidence:** High

**Experts mentioning this issue:**

- CrossRFC Expert: NAT46 reference observation

---
