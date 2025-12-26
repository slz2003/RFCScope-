# Errata Reports

Total reports: 2

---

## Report 1: 9740-2-1

**Label:** Consistent Use of 'Flow' and 'Extension header chain' Terminology in Section 2

**Bug Type:** None

**Explanation:**

The document’s Section 2 terminology—including terms such as 'Flow' and 'Extension header chain'—is used consistently and aligns with the referenced RFCs (RFC7011, RFC8200, and RFC9293).

**Justification:**

- The BCP 14 boilerplate and the explicit import of IPFIX terminology establish that key terms are used in a standard, unambiguous fashion (E1).
- Local definitions in Section 2 clearly define 'Extension header chain' and 'Flow with varying extension header chains', and subsequent use in normative sections confirms internal coherence (E2).

**Evidence Snippets:**

- **E1:**

  BCP 14 boilerplate in RFC 9740 Section 2:

  The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
  "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
  "OPTIONAL" in this document are to be interpreted as described in BCP 14
  [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as
  shown here.

- **E2:**

  Use of IPFIX-specific terminology:

  This document uses the IPFIX-specific terminology (Information
  Element, Template Record, Flow, etc.) defined in Section 2 of
  [RFC7011].  As in the base IPFIX specification [RFC7011], these
  IPFIX-specific terms have the first letter of a word capitalized.

Local term definitions in Section 2:

  Extension header chain:  Refers to the chain of extension headers
     that are present in an IPv6 packet.

  This term should not be confused with the IPv6 header chain, which
     includes the IPv6 header, zero or more IPv6 extension headers, and
     zero or a single Upper-Layer Header.

  Flow with varying extension header chains:  Refers to a Flow where
     distinct extension header chains are observed.  Concretely,
     different packets in such a Flow will have a different sequence of
     extension header type codes.

**Evidence Summary:**

- (E1) The BCP 14 boilerplate in Section 2 defines key words and capitalization rules, establishing a clear standard.
- (E2) The document explicitly imports IPFIX terminology and defines local terms so that their usage is consistent throughout the text.


---

## Report 2: 9740-2-2

**Label:** Stylistic Naming Inconsistency in IE Names: ipv6ExtensionHeadersChainLength vs ipv6ExtensionHeaderChainLengthList

**Bug Type:** Stylistic / Naming Inconsistency

**Explanation:**

There is a minor stylistic inconsistency where one Information Element name includes an extra 's' ('ipv6ExtensionHeadersChainLength') compared to the other ('ipv6ExtensionHeaderChainLengthList'), even though their semantics remain clear.

**Justification:**

- The analysis notes that outside Section 2, the IE names differ by an extra 's' in 'Headers', representing a naming quirk rather than a substantive error (E3).

**Evidence Snippets:**

- **E3:**

  Elsewhere in the document (outside Section 2), the IE names `ipv6ExtensionHeadersChainLength` (ElementID 518) and `ipv6ExtensionHeaderChainLengthList` (ElementID 519) differ by an extra “s” in “Headers” vs. “Header”. The descriptions and IANA table consistently use these names, and their semantics are clear and distinct. This looks like a stylistic inconsistency in naming, not a conflicting or misleading definition, because the IEs are always referenced with their exact names and unique IDs, and an implementer cannot reasonably confuse one for the other.

**Evidence Summary:**

- (E3) The document displays a naming inconsistency where one IE name includes an extra 's' compared to the other, a minor stylistic issue noted in the expert analysis.

**Fix Direction:**

Consider aligning the naming convention to remove the extra 's' for clarity, though the current naming does not impact functionality.


---
