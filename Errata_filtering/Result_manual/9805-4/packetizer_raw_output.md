# Errata Reports

Total reports: 3

---

## Report 1: 9805-4-1

**Label:** Ambiguous classification between 'future versions' and new protocols for RAO use

**Bug Type:** Underspecification

**Explanation:**

The document does not clearly define the criteria for distinguishing a 'future version' of an existing RAO‐using protocol from an entirely new protocol, which could lead to inconsistent application of RAO usage policies.

**Justification:**

- The normative text permits continued RAO use for existing protocols in their 'future versions' while prohibiting new protocols, but it fails to specify how to decide which category a protocol belongs to.
- Multiple expert analyses (Scope, Deontic, Terminology, and Boundary) highlight this as an underspecified boundary that may affect future protocol revisions such as MLDv3 or RSVPv3.

**Evidence Snippets:**

- **E1:**

  Protocols that use the IPv6 Router Alert option MAY continue to do so, even in future versions. However, new protocols that are standardized in the future MUST NOT use the IPv6 Router Alert option. Appendix A contains an exhaustive list of protocols that MAY continue to use the IPv6 Router Alert option. (RFC 9805, Section 4)

- **E2:**

  Table 1 contains an exhaustive list of protocols that use the IPv6 Router Alert option. (RFC 9805, Appendix A)

- **E3:**

  It is left for future work to develop new versions of MLDv2 and MRD that do not rely on the IPv6 Router Alert option. That task is out of scope for this document. (RFC 9805, Section 5)

**Evidence Summary:**

- (E1) Presents the dual normative statements regarding RAO use for 'future versions' versus new protocols.
- (E2) Lists the protocols in Appendix A without clarifying versioning criteria.
- (E3) Acknowledges future work on protocol revisions without providing normative classification rules.

**Fix Direction:**

Clarify in Section 4 the criteria that determine when a protocol revision is considered a 'future version' of an existing protocol versus when it qualifies as a 'new protocol', for example by linking the classification to protocol identity or continuity markers.


---

## Report 2: 9805-4-2

**Label:** MPLS Ping entry inconsistent: Global permission versus deprecation note

**Bug Type:** Inconsistency

**Explanation:**

The MPLS Ping entry in Appendix A includes a note that its use of the IPv6 Router Alert option is deprecated, which conflicts with the global statement that all protocols in Appendix A may continue to use the option.

**Justification:**

- Section 4 asserts that 'Appendix A contains an exhaustive list of protocols that MAY continue to use the IPv6 Router Alert option', suggesting a blanket permission.
- The MPLS Ping row, however, specifically notes '(Use of the IPv6 Router Alert option is deprecated)', creating an internal textual conflict about its status.

**Evidence Snippets:**

- **E1:**

  Appendix A contains an exhaustive list of protocols that MAY continue to use the IPv6 Router Alert option. (Section 4)

- **E2:**

  Table 1: Protocols That Use the IPv6 Router Alert Option (Appendix A table heading)

- **E3:**

  MPLS Ping (Use of the IPv6 Router Alert option is deprecated) (Appendix A, Table 1, MPLS Ping row)

**Evidence Summary:**

- (E1) Establishes the global permission for protocols in Appendix A to continue using the RAO.
- (E2) Provides the context of the list as defined in Appendix A.
- (E3) Shows the specific deprecation note for MPLS Ping, which contradicts the global statement.

**Fix Direction:**

Revise either the global statement in Section 4 or the MPLS Ping entry in Appendix A to consistently reflect the intended status regarding RAO use.


---

## Report 3: 9805-4-3

**Label:** Apparent policy shift between RFC 9805 and RFC 9673 deprecation discussions

**Bug Type:** None

**Explanation:**

There is a perceived discrepancy between RFC 9673's non-normative discussion suggesting future flexibility in RAO use and RFC 9805's explicit prohibition for new protocols, though this is viewed as an evolution in policy rather than a normative error.

**Justification:**

- RFC 9673 includes a DISCUSSION section that considers the possibility of using RAO with new functions under controlled conditions.
- RFC 9805, meanwhile, clearly states that new protocols MUST NOT use the RAO and closes the value registry, reflecting a stricter policy which is a later design decision.

**Evidence Snippets:**

- **E1:**

  [DISCUSSION] … One approach would be to deprecate this, because current usage beyond the local network appears to be limited, and packets containing Hop-by-Hop options are frequently dropped. Deprecation would allow current implementations to continue, and its use could be phased out over time. … Keeping this as the single exception for processing in the Control Plane with the restrictions that follow is a reasonable compromise to allow future flexibility. (RFC 9673, 5.2.1)

- **E2:**

  However, new protocols that are standardized in the future MUST NOT use the IPv6 Router Alert option. (RFC 9805, Section 4)

- **E3:**

  IANA has also made a note in the ‘IPv6 Router Alert Option Values’ registry stating that the registry is closed for allocations. (RFC 9805, Section 7)

**Evidence Summary:**

- (E1) Presents the non-normative flexibility discussed in RFC 9673.
- (E2) States the strict prohibition for new protocols in RFC 9805.
- (E3) Indicates the administrative change in the RAO registry per RFC 9805.


---
