# Errata Reports

Total reports: 2

---

## Report 1: 9762-3-1

**Label:** PIO reference misdirect: RFC9762 cites RFC4862 instead of RFC4861 for Prefix Information Option

**Bug Type:** Inconsistency

**Explanation:**

RFC9762 incorrectly points to RFC4862 for the definition of the Prefix Information Option, while the on‐wire format is truly specified in RFC4861, which may mislead implementers.

**Justification:**

- RFC9762’s terminology defines PIO as "Prefix Information Option [RFC4862]", yet the actual on‐wire format is defined in RFC4861 Section 4.6.2 (E1).
- The Terminology analysis confirms that RFC4862 only describes SLAAC processing, requiring a reference to RFC4861 for the normative definition (E2, E3).

**Evidence Snippets:**

- **E1:**

  RFC 9762’s terminology defines “PIO:  Prefix Information Option [RFC4862]”. However, the on‑the‑wire definition of the Prefix Information Option (type, length, Prefix Length, L and A flags, Reserved1/2, and Prefix field) is specified in RFC 4861 Section 4.6.2, not in RFC 4862. RFC 4862 merely describes how hosts process “Prefix Information options in the Router Advertisement” for SLAAC, and itself relies on RFC 4861 for the option format and flag semantics. RFC 9762 later extends that same ND option by adding the P flag in the PIO (Section 5 and the IANA allocation in the “IPv6 Neighbor Discovery Prefix Information Option Flags” registry), which is conceptually and normatively tied to RFC 4861’s definition. Pointing implementers to RFC 4862 as the defining document for “Prefix Information Option” is therefore inaccurate and may cause confusion when they look for the actual option format and existing flag positions. An erratum would ideally change this to reference RFC 4861 (or both RFC 4861 for the format and RFC 4862 for SLAAC processing).

- **E2:**

  Section 3 of RFC 9762:  PIO:  Prefix Information Option [RFC4862]

- **E3:**

  RFC 4861, Section 4.6.2 (provided in the context):  Heading: 4.6.2. Prefix Information followed by the full on‑the‑wire format of the Prefix Information option, including Type, Length, Prefix Length, L, A, and Reserved1/Reserved2, and the field semantics.

**Evidence Summary:**

- (E1) Indicates that the PIO is defined on-wire in RFC4861 rather than in RFC4862.
- (E2) Shows the verbatim entry from RFC9762 that erroneously cites RFC4862.
- (E3) Provides the normative context from RFC4861 for the Prefix Information option.

**Fix Direction:**

In Section 3 of RFC9762, update the PIO entry to reference RFC4861 (or both RFC4861 and RFC4862) to clearly delineate the definition of the on‐wire format.


---

## Report 2: 9762-3-2

**Label:** On-link/off-link terminology abbreviated but consistent with RFC4861

**Bug Type:** None

**Explanation:**

The document uses shortened definitions for on-link and off-link addresses that refer back to RFC4861 and are consistent with the full definitions, though the brevity might be seen as overly simplified.

**Justification:**

- RFC9762’s Section 3 provides abbreviated definitions for on-link addresses and off-link terms with explicit reference to RFC4861 (E1).
- Context from RFC4861 Section 2.1 confirms that the abbreviated versions in RFC9762 accurately reflect the full semantics without contradiction (E2).

**Evidence Snippets:**

- **E1:**

  Section 3 of RFC 9762:
        On-link address:  an address that is assigned to an interface on a specified link [RFC4861]
        On-link prefix:  a prefix that is assigned to a specified link
        Off-link:  the opposite of "on-link" (see [RFC4861])

- **E2:**

  RFC 4861, Section 2.1:
        on-link  - an address that is assigned to an interface on a specified link.  A node considers an address to be on-link if: ...
        off-link    - the opposite of "on-link"; an address that is not assigned to any interfaces on the specified link.

**Evidence Summary:**

- (E1) Presents the abbreviated on-link and off-link definitions as given in RFC9762.
- (E2) Provides contextual full definitions from RFC4861, confirming consistency.


---
