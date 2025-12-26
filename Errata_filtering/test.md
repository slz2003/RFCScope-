# Errata Reports

Total reports: 3

---

## Report 1: 9810-E-1

**Label:** Ambiguity in transactionID handling in Appendix E KEM flows

**Bug Type:** Editorial/Underspecification

**Explanation:**

Appendix E’s diagrams do not explicitly indicate that messages carrying KemCiphertextInfo must include a transactionID as required in Sections 5.1.1 and 5.1.3.4, which may confuse implementers.

**Justification:**

- Multiple experts noted that while the normative sections mandate that any message carrying KemCiphertextInfo be populated with a transactionID, Appendix E omits an explicit mention of this requirement (Deontic Expert Issue-1, Causal Expert Issue 1, Boundary Expert Finding-1).

**Evidence Snippets:**

- **E1:**

  A client MUST populate the transactionID field if the message contains an infoValue of type KemCiphertextInfo… If a server receives such request with a missing transactionID field, then it MUST populate the transactionID field if the message contains a KemCiphertextInfo field.

- **E2:**

  transactionID MUST be the value from the message containing the ciphertext (ct) in KemCiphertextInfo.

- **E3:**

  Appendix E Figure 3: format unprotected genm … of type KemCiphertextInfo without value… format unprotected genp of type KemCiphertextInfo providing KEM ciphertext

**Evidence Summary:**

- (E1) States the normative requirement to populate the transactionID when a KemCiphertextInfo is present.
- (E2) Binds KemOtherInfo.transactionID to the ciphertext‐bearing message.
- (E3) Illustrates that Appendix E’s flow descriptions do not explicitly mention transactionID.

**Fix Direction:**

Clarify Appendix E to explicitly state that messages carrying KemCiphertextInfo, including the genp message that provides the ciphertext, MUST include a transactionID as specified in Sections 5.1.1 and 5.1.3.4.

**Severity:** Low
  *Basis:* Although the normative text ensures correctness, the lack of explicit reference in Appendix E could lead to implementation confusion.

**Confidence:** High

**Experts mentioning this issue:**

- Causal Expert: Issue 1
- Deontic Expert: Issue-1
- Boundary Expert: Finding-1

---

## Report 2: 9810-E-2

**Label:** Inconsistent portrayal of Alice's role in Appendix E

**Bug Type:** Inconsistency

**Explanation:**

Appendix E inconsistently describes the role of Alice, sometimes as the PKI entity holding a KEM key pair and sometimes as the PKI management entity, which may lead to confusion regarding which party is expected to possess the KEM key pair.

**Justification:**

- ActorDirectionality Expert NewIssue-1 points out that the introductory text in Appendix E labels Alice as the PKI entity using a KEM key pair, while the captions for Figures 3 and 4 assign differing roles (alternating between PKI entity and PKI management entity), which may mislead implementers.

**Evidence Snippets:**

- **E1:**

  In the following message flows, Alice indicates the PKI entity that uses a KEM key pair for message authentication and Bob provides the KEM ciphertext using Alice's public KEM key, as described in Section 5.1.3.4.

- **E2:**

  Figure 3 caption: “Message Flow When the PKI Entity Has a KEM Key Pair and Certificate” with “PKI entity (Alice)” / “PKI management entity (Bob)” and Figure 4 caption: “Message Flow When the PKI Entity Knows That the PKI Management Entity Uses a KEM Key Pair and Has the Authentic Public Key” with “PKI entity (Bob)” / “PKI management entity (Alice)”.

**Evidence Summary:**

- (E1) Introduces Alice as the PKI entity that uses the KEM key pair.
- (E2) Demonstrates conflicting role assignments in the figure captions, thereby introducing ambiguity.

**Fix Direction:**

Revise Appendix E to use consistent role designations and clearly indicate which party holds the KEM key pair in each illustrated flow.

**Severity:** Medium
  *Basis:* Ambiguities in role assignment can lead to misinterpretation during implementation, affecting which party is responsible for certain cryptographic operations.

**Confidence:** High

**Experts mentioning this issue:**

- ActorDirectionality Expert: NewIssue-1

---

## Report 3: 9810-E-3

**Label:** Inconsistent and ambiguous use of wrongIntegrity in KEM discovery/upgrade flow

**Bug Type:** Inconsistency

**Explanation:**

The discovery/upgrade flow in Appendix E instructs the sending of an unprotected ErrorMsg with failInfo 'wrongIntegrity', which conflicts with the normative requirement that a CA always sign error messages, and the semantics of wrongIntegrity as a KEM upgrade signal remain under-specified.

**Justification:**

- ActorDirectionality Expert NewIssue-2 identifies the conflict between an unprotected error and the CA's obligation to sign per Section 5.3.21.
- Causal Expert Issue 2 and Deontic Expert Issue-2 further note that using wrongIntegrity in conjunction with a KEM certificate as an upgrade signal is ambiguous, potentially leading to inconsistent client behavior.

**Evidence Snippets:**

- **E1:**

  Section 5.3.21 (ErrorMsgContent): “If protection is desired on the message, the client MUST protect it using the same technique… The CA MUST always sign it with a signature key.”

- **E2:**

  Appendix E, Figure 5, step 3: “format unprotected error with status 'rejection' and failInfo 'wrongIntegrity' and KEM certificate in extraCerts”

- **E3:**

  PKIFailureInfo.wrongIntegrity: “KEM ciphertext missing for MAC-based protection of response, or not valid integrity of message received (password based instead of signature or vice versa).”

**Evidence Summary:**

- (E1) Establishes the normative requirement that error messages from a CA MUST be signed.
- (E2) Shows that Appendix E directs the use of an unprotected error message with wrongIntegrity.
- (E3) Defines wrongIntegrity with dual meanings, which contributes to ambiguity regarding its intended use in KEM upgrade flows.

**Fix Direction:**

Amend Section 5.3.21 or Appendix E to clarify that, even in KEM discovery/upgrade flows, error messages from a CA must be signed, and provide explicit guidance on how clients should interpret an ErrorMsg carrying wrongIntegrity along with a KEM certificate.

**Severity:** Medium
  *Basis:* The normative conflict and ambiguity in interpreting wrongIntegrity may lead to inconsistent implementations and uncertain client behavior in KEM upgrade scenarios.

**Confidence:** High

**Experts mentioning this issue:**

- ActorDirectionality Expert: NewIssue-2
- Causal Expert: Issue 2
- Deontic Expert: Issue-2
- Boundary Expert: Finding-2

---
