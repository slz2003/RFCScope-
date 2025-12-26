# Errata Reports

Total reports: 2

---

## Report 1: 9774-3-1

**Label:** Conflicting error handling for AS_CONFED_SET in AS4_PATH between RFC 9774 and RFC 6793

**Bug Type:** Inconsistency

**Explanation:**

RFC 9774 mandates treat‐as‐withdraw for UPDATE messages containing AS_CONFED_SET in AS4_PATH while RFC 6793 requires that such AS_CONFED_SET segments be discarded and the UPDATE processed normally, thus creating a normative conflict.

**Justification:**

- RFC 9774 Section 3 explicitly requires that any UPDATE containing AS_CONFED_SET (or AS_SET) in the AS_PATH or AS4_PATH triggers a treat‐as‐withdraw handling (see E1).
- RFC 6793 Section 6 specifies that when a NEW BGP speaker receives an UPDATE with AS_CONFED_SET in AS4_PATH from an OLD speaker, the offending segments must be discarded and processing should continue (see E2).
- This discrepancy leaves implementers without a clear, unique behavior, potentially leading to divergent processing of the same UPDATE.

**Evidence Snippets:**

- **E1:**

  RFC 9774, Section 3:  
        “Unless explicitly configured by a network operator to do otherwise (e.g., during a transition phase), BGP speakers:  
        * MUST NOT advertise BGP UPDATE messages containing AS_SETs or AS_CONFED_SETs and  
        * MUST use the ‘treat-as-withdraw’ error handling behavior per [RFC7606] upon reception of BGP UPDATE messages containing AS_SETs or AS_CONFED_SETs in the AS_PATH or AS4_PATH [RFC6793].”  
        Followed by: “Per the above specifications, this document updates [RFC4271] and [RFC5065] by deprecating AS_SET … and AS_CONFED_SET …, respectively.”

- **E2:**

  RFC 6793, Section 6 (error handling for AS4_PATH):  
        “The AS4_PATH attribute and AS4_AGGREGATOR attribute MUST NOT be carried in an UPDATE message between NEW BGP speakers. A NEW BGP speaker that receives the AS4_PATH attribute or the AS4_AGGREGATOR attribute in an UPDATE message from another NEW BGP speaker MUST discard the path attribute and continue processing the UPDATE message.”  
        “In addition, the path segment types AS_CONFED_SEQUENCE and AS_CONFED_SET [RFC5065] MUST NOT be carried in the AS4_PATH attribute of an UPDATE message. A NEW BGP speaker that receives these path segment types in the AS4_PATH attribute of an UPDATE message from an OLD BGP speaker MUST discard these path segments, adjust the relevant attribute fields accordingly, and continue processing the UPDATE message.”

**Evidence Summary:**

- (E1) RFC 9774 mandates treat‐as‐withdraw for any UPDATE containing AS_CONFED_SET in AS4_PATH.
- (E2) RFC 6793 instructs a NEW BGP speaker to discard AS_CONFED_SET segments from AS4_PATH and continue processing the UPDATE.

**Fix Direction:**

Clarify the intended scope by either explicitly stating in RFC 9774 that it updates RFC 6793 for AS4_PATH error handling (thereby overriding the discard-and-continue behavior) or by narrowing the treat‐as‐withdraw requirement to only apply to AS_PATH.


---

## Report 2: 9774-3-2

**Label:** Normative tightening for AS_SET in AS4_PATH in RFC 9774

**Bug Type:** Normative Change

**Explanation:**

RFC 9774 mandates treat‐as‐withdraw for any UPDATE containing AS_SET in AS4_PATH, even though RFC 6793 permits AS_SET as a valid segment type, resulting in a stricter behavior than that originally specified.

**Justification:**

- RFC 9774 Section 3 requires treat‐as‐withdraw for UPDATEs containing AS_SET in the AS_PATH or AS4_PATH, thereby deprecating AS_SET usage (refer to E3).
- RFC 6793, however, treats AS_SET in AS4_PATH as valid without imposing a mandatory withdrawal, so the new rule effectively tightens the error handling.
- This change could lead to unexpected route withdrawals and interoperability differences between implementations that expect the legacy behavior versus the stricter approach.

**Evidence Snippets:**

- **E3:**

  Boundary Expert Finding-2:  
        - ExcerptEvidence:
          - RFC 6793 allows AS_SET as a valid AS4_PATH segment type and does not define any special error handling for it beyond the generic malformed-AS4_PATH rules.    
          - RFC 9774 requires “treat-as-withdraw” for any UPDATE containing AS_SET in either AS_PATH or AS4_PATH (unless explicitly configured otherwise).

**Evidence Summary:**

- (E3) RFC 6793 permits AS_SET in AS4_PATH as a valid segment, whereas RFC 9774 unconditionally mandates treat‐as‐withdraw for such cases.

**Fix Direction:**

Either align RFC 9774 with RFC 6793 by allowing AS_SET in AS4_PATH to be processed without withdrawal or explicitly document and justify the tighter error handling for improved clarity.


---
