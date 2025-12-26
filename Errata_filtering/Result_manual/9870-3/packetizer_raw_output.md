# Errata Reports

Total reports: 2

---

## Report 1: 9870-3-1

**Label:** Over‐generalized ExID size statement in RFC 9870 Section 3

**Bug Type:** Inconsistency

**Explanation:**

RFC 9870 states that only 16‑bit ExIDs are supported in [RFC9868], which may mislead readers into thinking that 32‑bit ExIDs are not supported at all, even though RFC 9868 allows 32‑bit ExIDs for TCP options.

**Justification:**

- RFC 9870 Section 3 includes the statement 'Only 16‑bit ExIDs are supported in [RFC9868]', which can be interpreted too broadly (E1).
- RFC 9868’s IANA considerations clarify that while UDP options use 16‑bit ExIDs, 32‑bit ExIDs are available for TCP, with UDP options constrained to 16‑bit values (E2).

**Evidence Snippets:**

- **E1:**

  Section 3 of RFC 9870:
“For both options, Experiment Identifiers (ExIDs) are used to differentiate concurrent use of these options. Known ExIDs are expected to be registered within IANA. … Also, Section 4.5 specifies a new IPFIX IE to export observed ExIDs in the UEXP Options. Only 16‑bit ExIDs are supported in [RFC9868].”

- **E2:**

  RFC 9868, Section 26 (IANA Considerations), as provided:
“16‑bit ExIDs can be used with either TCP or UDP; 32‑bit ExIDs can be used with TCP or their first 16 bits can be used with UDP. … TCP/UDP ExIDs used for UDP are always 16 bits because their use in EXP and UEXP Options is required …”

**Evidence Summary:**

- (E1) RFC 9870 Section 3 states the limitation to 16‑bit ExIDs.
- (E2) RFC 9868 clarifies that while UDP options are limited to 16‑bit ExIDs, 32‑bit ExIDs are supported for TCP.

**Fix Direction:**

In Section 3 of RFC 9870, rephrase the statement to clarify that only UDP Options use 16‑bit ExIDs. For example: 'For UDP Options, [RFC9868] defines the use of only 16‑bit ExIDs (even though the shared TCP/UDP ExID registry also supports 32‑bit ExIDs for TCP options).'

**Severity:** Low
  *Basis:* The issue is editorial; it may cause misinterpretation of ExID scope but does not affect the correct encoding or interoperability of UDP Options.

**Confidence:** High

**Experts mentioning this issue:**

- Terminology Expert: Issue-1

---

## Report 2: 9870-3-2

**Label:** UDP Option Numeric Encoding and SAFE/UNSAFE Ranges Consistent with RFC 9868

**Bug Type:** None

**Explanation:**

The document’s assignment of numeric ranges 0–191 for SAFE Options and 192–255 for UNSAFE Options, along with the use of a 16‑bit field for UDP ExIDs, is fully consistent with the normative definitions in RFC 9868.

**Justification:**

- RFC 9870 restates the numeric partitioning by mapping 192 distinct values to SAFE options and 64 values to UNSAFE options, which mirrors the IANA definitions in RFC 9868 (E1, E3).
- The basicList encoding example is arithmetically verified to sum to 9 bytes, confirming internal consistency (E2).

**Evidence Snippets:**

- **E1:**

  RFC 9868’s IANA section defines the “UDP Option Kind Numbers” table with SAFE options 0–191 and UNSAFE options 192–255; it then states explicitly: “Options indicated by Kind values in the range 0..191 are known as SAFE Options … Options indicated by Kind values in the range 192..255 are known as UNSAFE Options” . This matches RFC 9870’s Section 3 text.

- **E2:**

  In the example basicList encoding (Figure 5), the advertised “List Length = 9” matches the sum of the semantic (1 byte) + IE ID (2 bytes) + Field Length (2 bytes) + two ExID values at 2 bytes each = 1 + 2 + 2 + 4 = 9.

- **E3:**

  Options indicated by Kind values in the range 0-191 are called SAFE Options. … (Section 11 of [RFC9868]). Options indicated by Kind values in the range 192-255 are called UNSAFE Options. … (Section 12 of [RFC9868]).

**Evidence Summary:**

- (E1) The IANA table in RFC 9868 defines the SAFE/UNSAFE partition that RFC 9870 restates.
- (E2) The basicList encoding example correctly totals 9 bytes, confirming proper field sizing.
- (E3) The textual definitions for SAFE and UNSAFE Options align with the numeric ranges described.

**Severity:** Low
  *Basis:* The numerical assignments mirror the authoritative definitions in RFC 9868, presenting no risk to interoperability or implementation.

**Confidence:** High

**Experts mentioning this issue:**

- Quantitative Expert: Issue-1
- Terminology Expert: Issue-2

---
