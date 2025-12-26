# Errata Reports

Total reports: 2

---

## Report 1: 9868-18-1

**Label:** Ambiguity in UDP Length Permissibility Wording (Section 18 vs ROHC Requirements)

**Bug Type:** Underspecification

**Explanation:**

Section 18’s statement that it has 'always been permissible' for the UDP Length to be inconsistent with the IP payload length may mislead implementers by implying universal permissiveness, which contrasts with the ROHC profile’s 'MUST match' requirement.

**Justification:**

- Section 18 explicitly states 'It has always been permissible for the UDP Length to be inconsistent with the IP transport payload length [RFC0768].' (E1)
- The RouterSketch assessment notes that the hypothesis focused on whether 'always been permissible' is too strong given ROHC’s 'MUST match' wording. (E2)

**Evidence Snippets:**

- **E1:**

  RFC 9868 Section 18 states, “It has always been permissible for the UDP Length to be inconsistent with the IP transport payload length [RFC0768].” There is no text in the base UDP spec (RFC 768) or the host requirements (RFC 1122) that requires the UDP Length to equal the IP payload length; RFC 1122 even explicitly notes there are “no known errors in the specification of UDP” .

- **E2:**

  RouterSketch assessment: The router’s hypothesis focused on whether “always been permissible” is too strong given ROHC’s “MUST match” wording, and whether the embedded device comment is fully supported.

**Evidence Summary:**

- (E1) RFC 9868 Section 18 permissiveness clause regarding UDP Length.
- (E2) RouterSketch assessment questioning the strength of the 'always been permissible' wording relative to ROHC requirements.

**Fix Direction:**

Revise the wording in Section 18 to clarify that the permissibility of a UDP Length and IP payload length mismatch is context-specific and does not override specific requirements such as those in ROHC profiles.





---
