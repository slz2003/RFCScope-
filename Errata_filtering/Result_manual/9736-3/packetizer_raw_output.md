# Errata Reports

Total reports: 3

---

## Report 1: 9736-3-1

**Label:** Ambiguous Multiplicity Rules for Non‐String Peer Up Information TLV Types (Types 3 and 4)

**Bug Type:** Underspecification

**Explanation:**

The RFC explicitly permits repetition for the String TLV type in Peer Up messages but does not specify whether TLV types 3 (VRF/Table Name) and 4 (Admin Label) may be repeated, leaving their cardinality ambiguous.

**Justification:**

- RFC 7854 originally defined only the String TLV as repeatable and RFC 9736 restates this rule without extending it to the new TLV types.
- Both Scope and Boundary experts note that there is no guidance on the occurrence of types 3 and 4, which can lead to inconsistent interpretations by implementers.

**Evidence Snippets:**

- **E1:**

  Original Peer Up text in RFC 7854 §4.10 (excerpted): “Information: Information about the peer, using the Information TLV (Section 4.4) format. Only the string type is defined in this context; it may be repeated.”
Updated Peer Up text in RFC 9736 §3.2: “Information: Information about the peer, using the Peer Up Information TLV format defined in Section 3.3 of RFC 9736. The String type may be repeated. Inclusion of the Information field is OPTIONAL.”
New Peer Up TLV types in RFC 9736 §3.3:
  “Type = 0: String. … If multiple strings are included, their ordering MUST be preserved when they are reported.”
  “Type = 3: VRF/Table Name. … The string size MUST be within the range of 1 to 255 bytes.”
  “Type = 4: Admin Label. … The value is administratively assigned.”
No statement anywhere on whether type 3 or type 4 TLVs may, must, or must not appear multiple times in a single Peer Up message.

- **E2:**

  Original BMP Peer Up text (RFC 7854) says: “Information: Information about the peer, using the Information TLV (Section 4.4) format. Only the string type is defined in this context; it may be repeated. Inclusion of the Information field is OPTIONAL.” RFC 7854’s Information TLV definition allows multiple String TLVs but is silent on multiplicity for other types. RFC 9736 replaces the Peer Up “Information” definition with: “Information: Information about the peer, using the Peer Up Information TLV format defined in Section 3.3 of RFC 9736. The String type may be repeated.” RFC 9736’s Peer Up Information TLV then defines Type 0 with explicit repetition, while types 3 and 4 are described only by their length and content constraints.

**Evidence Summary:**

- (E1) Shows that RFC 9736 explicitly permits repetition only for the String TLV while providing no rules for types 3 and 4.
- (E2) Reinforces that the multiplicity for non‐String TLVs remains unspecified, creating ambiguity in how multiple instances should be handled.

**Fix Direction:**

Explicitly state the allowed cardinality for TLV types 3 and 4, such as specifying whether only one instance is permitted or if multiple instances are allowed with defined semantics.


---

## Report 2: 9736-3-2

**Label:** Editorial Typographical Error in Admin Label TLV Description

**Bug Type:** Editorial

**Explanation:**

The Admin Label TLV description contains a typographical error with an extraneous 'a' in the phrase regarding string termination.

**Justification:**

- The text incorrectly states 'There is no requirement to terminate the string a with null or any other character' which introduces an unnecessary and confusing article.
- Both Terminology and Structural experts note that this is a minor editorial issue that does not affect the technical encoding.

**Evidence Snippets:**

- **E1:**

  Typo noted by the router in the Admin Label description: “There is no requirement to terminate the string a with null or any other character.”

**Evidence Summary:**

- (E1) Directly indicates the presence of an extraneous 'a' in the text, which serves no technical purpose.

**Fix Direction:**

Remove the extraneous 'a' so that the phrase reads 'There is no requirement to terminate the string with null or any other character.'


---

## Report 3: 9736-3-3

**Label:** Ambiguous Scope Wording for Peer Up Information TLV Usage

**Bug Type:** Ambiguity

**Explanation:**

The specification’s wording for the usage of the Peer Up Information TLV is asymmetric when compared to the Initiation Information TLV, potentially leading to misinterpretation of its allowed message contexts.

**Justification:**

- The Initiation Information TLV is explicitly defined as being used only in the Initiation message, while the Peer Up Information TLV is only described as being 'used by the Peer Up message' without an exclusive restriction.
- This asymmetry might be read to imply that Peer Up Information TLVs could appear in other message types, even though the registry name suggests a Peer‑Up‑only scope.

**Evidence Snippets:**

- **E1:**

  ResidualUncertainties:
- The asymmetry between “used only by the Initiation message, not by the Peer Up message” (for the Initiation Information TLV) and “used by the Peer Up message” (for the Peer Up Information TLV) might be read as allowing use of Peer Up Information TLVs in other message types, even though the registry name (“BMP Peer Up Message TLVs”) and overall intent suggest Peer‑Up‑only scope. This is arguably self‑evident from context but could have been made symmetric to avoid any doubt.

**Evidence Summary:**

- (E1) Highlights that the asymmetric phrasing between the two TLV types could lead to ambiguity about whether Peer Up Information TLVs are restricted exclusively to the Peer Up message.

**Fix Direction:**

Revise the text to explicitly restrict the Peer Up Information TLV to the Peer Up message, mirroring the unambiguous language used for the Initiation Information TLV.


---
