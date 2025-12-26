# Errata Reports

Total reports: 6

---

## Report 1: 9825-7-1

**Label:** Mis-scoped LSDB 'when' Expression: Wrong Ancestor Level for rt:type

**Bug Type:** Inconsistency

**Explanation:**

The LSDB augments use a derived-from-or-self() XPath that climbs one level too few, causing the rt:type lookup to occur under an ospf:ospf node rather than the intended rt:control-plane-protocol, which forces the condition to always evaluate to false.

**Justification:**

- The candidate issue explains that in the OSPFv2 link-scope case, the XPath uses 15 '../' steps instead of the 16 needed to reach the rt:control-plane-protocol level (see evidence snippets E1 and E2).
- This mis-scoping makes the when condition always false, preventing instantiation of the intended admin-tag nodes.

**Evidence Snippets:**

- **E1:**

  Example (OSPFv2 link-scope case):

augment "/rt:routing/.../ospf:extended-prefix-opaque/ospf:extended-prefix-tlv" {
  when "derived-from-or-self(../../../../../../../../../.."
     + "/../../../../rt:type, 'ospf:ospfv2')" {
    description "This augmentation is only valid for OSPFv2.";
  }
  ...
  uses prefix-admin-tag-sub-tlv;
}

- **E2:**

  Other OSPFv2 and OSPFv3 LSDB augments use the same pattern with slightly shorter '../' chains, e.g.:

when "derived-from-or-self(../../../../../../../../../.."
   + "/../../rt:type, 'ospf:ospfv2')" { ... }

when "derived-from-or-self(../../../../../../../.."
   + "/../../rt:type, 'ospf:ospfv3')" { ... }

**Evidence Summary:**

- (E1) Shows the augment for OSPFv2 Extended Prefix TLV with the long '../' chain leading to a check on rt:type under an ospf:ospf node.
- (E2) Demonstrates the similar pattern for both ospfv2 and ospfv3 augments that suffer from the same off-by-one error.

**Fix Direction:**

Increase the '../' depth in the when expressions so that the path inside derived-from-or-self() correctly reaches the rt:control-plane-protocol ancestor.


---

## Report 2: 9825-7-2

**Label:** Absolute 'when' Condition in OSPFv3 Augments Is Overly Broad

**Bug Type:** Underspecification

**Explanation:**

The OSPFv3 augments use an absolute XPath in their when conditions that checks for any ospf:ospfv3 instance in the datastore instead of constraining the condition to the specific augmented instance.

**Justification:**

- The candidate issue notes that the absolute when condition evaluates to true if any OSPFv3 instance exists, rather than verifying that the current protocol instance is OSPFv3 (see evidence snippets E1 and E2).
- This broad check creates a stylistic inconsistency with other relative, instance-scoped checks and may lead to fragile future behavior if similar subtree shapes are reused.

**Evidence Snippets:**

- **E1:**

  For OSPFv3 E‑Intra-Area-Prefix TLV:

augment "/rt:routing/.../ospfv3-e-lsa:e-intra-area-prefix
         /ospfv3-e-lsa:e-intra-prefix-tlvs
         /ospfv3-e-lsa:intra-prefix-tlv" {
  when "/rt:routing/rt:control-plane-protocols"
     + "/rt:control-plane-protocol/rt:type = 'ospf:ospfv3'" {
    description
      "This augmentation is only valid for OSPFv3.";
  }
  ...
  uses prefix-admin-tag-sub-tlv;
}

- **E2:**

  For OSPFv3 E‑NSSA External-Prefix TLV:

augment "/rt:routing/.../ospfv3-e-lsa:e-nssa
         /ospfv3-e-lsa:e-external-tlvs
         /ospfv3-e-lsa:external-prefix-tlv" {
  when "/rt:routing/rt:control-plane-protocols"
     + "/rt:control-plane-protocol/rt:type = 'ospf:ospfv3'" {
    description
      "This augmentation is only valid for OSPFv3.";
  }
  ...
  uses prefix-admin-tag-sub-tlv;
}

**Evidence Summary:**

- (E1) Presents the absolute when condition for the OSPFv3 E‑Intra-Area-Prefix TLV augmentation, which checks for any ospf:ospfv3 instance in the datastore.
- (E2) Demonstrates a similar absolute when condition used in the OSPFv3 E‑NSSA External-Prefix TLV augmentation.

**Fix Direction:**

Replace the absolute XPath check with a relative, instance-scoped derived-from-or-self() expression that specifically validates the current protocol instance's rt:type.


---

## Report 3: 9825-7-3

**Label:** Ambiguity in Coverage: Missing Administrative Tag Configuration for NSSA Ranges and Redistributed Summaries

**Bug Type:** Underspecification

**Explanation:**

The protocol text mentions that NSSA ranges and redistributed route summaries should support administrative tags, but the YANG model only defines tags for area ranges and local prefixes, leaving it unclear whether the omissions were intentional.

**Justification:**

- The residual uncertainties note highlights that while the protocol specifies additional contexts (NSSA ranges and redistributed summaries), the YANG module does not include corresponding augmentations, raising questions about design intent.

**Evidence Snippets:**

- **E1:**

  ResidualUncertainties:
  - The protocol text (Sections 3–4) mentions NSSA ranges and redistributed route summaries as candidates for configurable tags, but the YANG only models tags on area ranges and local prefixes. It is unclear whether this omission is intentional (left to future modules) or an oversight.

**Evidence Summary:**

- (E1) Indicates that the YANG model omits administrative tag configurations for NSSA ranges and redistributed summaries even though the protocol text suggests they should be supported.

**Fix Direction:**

Clarify in the design whether these tag configurations were intentionally omitted or add the missing augmentations in a future revision.


---

## Report 4: 9825-7-4

**Label:** Ambiguity in Sub-TLV Admin-Tag Lists: Empty vs. Omitted Semantics

**Bug Type:** Ambiguity

**Explanation:**

The YANG grouping for the administrative tag sub-TLV allows an empty leaf-list, even though the wire protocol mandates that a sub-TLV must contain at least one administrative tag to be valid.

**Justification:**

- The sub-TLV definition in the protocol states that at least one administrative tag MUST be advertised and that a sub-TLV with a length of 0 or non-multiple-of-4 octets must be ignored, yet the YANG model does not enforce a minimum number of elements.
- This could potentially lead to ambiguities in representing a deliberately empty versus a malformed sub-TLV.

**Evidence Snippets:**

- **E1:**

  ExcerptEvidence:
  - The sub-TLV definition says: “At least one administrative tag MUST be advertised … If the length is 0 or not a multiple of 4 octets, the sub-TLV MUST be ignored” (Section 2).  
  - The YANG grouping for the sub-TLV is:

        grouping prefix-admin-tag-sub-tlv {
          container prefix-admin-tag-sub-tlv {
            config false;
            leaf-list admin-tag {
              type uint32;
              description "Administrative tags.";
            }
          }
        }
  - Configurable admin-tags for ranges and local prefixes are also modeled as leaf-list admin-tag { type uint32; } without min-elements.

**Evidence Summary:**

- (E1) Details the protocol requirements for the sub-TLV and shows that the YANG model allows an empty list, which may not differentiate between a missing and a malformed sub-TLV.

**Fix Direction:**

Either enforce a min-elements constraint in the YANG model or add documentation that clarifies that an absent container versus an empty list correctly represents the intended semantics.


---

## Report 5: 9825-7-5

**Label:** Potential Visibility Inconsistency: Admin-Tag Augmentation Applied Only to Local RIB Next-Hop Entries

**Bug Type:** Ambiguity

**Explanation:**

The YANG module augments administrative tags on per-next-hop entries in the OSPF local RIB, while global RIB routes do not receive similar tag augmentations, which may lead to inconsistent visibility.

**Justification:**

- The model explicitly augments the next-hop list under the OSPF local RIB and omits similar augmentation on global RIB routes, raising questions about whether this was an intentional design decision or an oversight in maintaining consistent tag visibility.

**Evidence Snippets:**

- **E1:**

  ExcerptEvidence:
  - The model augments the OSPF local RIB’s per-next-hop entries:

        augment "/rt:routing"
              + "/rt:control-plane-protocols/rt:control-plane-protocol"
              + "/ospf:ospf/ospf:local-rib/ospf:route/ospf:next-hops"
              + "/ospf:next-hop" {
          leaf-list admin-tag {
            type uint32;
          }
        }
  - The base OSPF local-rib grouping already defines next-hop entries, but no augmentation is provided for the global RIB.

**Evidence Summary:**

- (E1) Shows that admin-tag augmentation is only applied to next-hop entries within the local RIB, not to the global RIB routes, posing potential consistency concerns.

**Fix Direction:**

Clarify in the specification whether administrative tags should also be applied to global RIB routes or if the design intentionally isolates tag exposure to next-hop entries.


---

## Report 6: 9825-7-6

**Label:** Design Incompleteness: Missing Augmentation for SRv6 Locator TLV Context

**Bug Type:** Design Incompleteness

**Explanation:**

The YANG module does not include an augmentation for the SRv6 Locator TLV context mentioned in Section 3, representing a gap in the modeled sub-TLV usages.

**Justification:**

- The notes state that the YANG model omits an augmentation for the SRv6 Locator TLV context (via RFC 9513), which is a design incompleteness relative to the full set of possible sub-TLV usages.

**Evidence Snippets:**

- **E1:**

  Not a bug: The YANG model does not include an augmentation for the SRv6 Locator TLV context mentioned in Section 3 (via RFC 9513). This is a coverage/design incompleteness relative to the set of all possible sub-TLV usages, but it does not affect the correctness of the boundaries or exceptional cases in the behaviors that are modeled.

**Evidence Summary:**

- (E1) Indicates that the omission of an augmentation for the SRv6 Locator TLV context is recognized as a design incompleteness in the module.

**Fix Direction:**

Either add the missing augmentation for the SRv6 Locator TLV context or document the deliberate exclusion of SRv6 support as part of the module's design scope.


---
