# Errata Reports

Total reports: 4

---

## Report 1: 9810-4-1

**Label:** Ambiguous 'new with new' Certificate Validity Period Rule (Undefined 'Next Update' Reference)

**Bug Type:** Underspecification

**Explanation:**

The validity period rule for the 'new with new' certificate uses the undefined phrase 'next update of this certificate', causing ambiguity in determining the proper validity interval and potentially inconsistent key rollover behavior.

**Justification:**

- Section 4.4.1 requires the notAfter time of the 'new with new' certificate to be after the notBefore time of the 'next update', but certificates do not define a 'next update' field.
- Comparison with RFC 4210 shows a clearer requirement tied to the CA's next key update event.

**Evidence Snippets:**

- **E1:**

  ```
  The ‘new with new’ certificate must have a validity period with a notBefore time that is before the notAfter time of the ‘old with old’ certificate and a notAfter time that is after the notBefore time of the next update of this certificate.
  ```

- **E2:**

  ```
  In RFC 4210, the ‘new with new’ certificate validity period was defined to start at the generation time of the new key pair and end at or before the time by which the CA will next update its key pair.
  ```

**Evidence Summary:**

- (E1) shows the ambiguous phrasing regarding the certificate validity period.
- (E2) contrasts this with RFC 4210's clear definition.

**Fix Direction:**

Revise the 'new with new' certificate validity rule by replacing 'next update of this certificate' with a clearly defined reference to the CA's next key update event, as specified in RFC 4210.

**Severity:** Low
  *Basis:* The ambiguity may lead to inconsistent implementation of root CA rollover timing but does not affect on-wire interoperability.

**Confidence:** High

**Experts mentioning this issue:**

- TemporalExpert: T1
- QuantitativeExpert: Issue-1
- DeonticExpert: Issue-1
- CrossRFCExpert: Issue-1

---

## Report 2: 9810-4-2

**Label:** Case 2 Verification Error: 'new with new' Certificate Verified with Old CA Key

**Bug Type:** Causal Inconsistency

**Explanation:**

The verification procedure for Case 2 instructs verifiers to use the old CA key to verify the 'new with new' certificate, which is signed by the new key, leading to guaranteed verification failure.

**Justification:**

- The algorithm in §4.4.2.2 directs verifiers to obtain both 'new with new' and 'new with old' certificates and then verify them with the old trust anchor.
- Since 'new with new' is signed with the new key, using the old key for its verification will always cause the check to fail.

**Evidence Snippets:**

- **E1:**

  ```
  In case 2, the verifier must get the ‘new with new’ and ‘new with old’ certificates. … Verify the signatures using the old root CA key (which the verifier has locally).
  ```

- **E2:**

  ```
  Mechanically, 'new with new' is signed with the new key, so verifying it with the old key will always fail.
  ```

**Evidence Summary:**

- (E1) describes the problematic procedure in Case 2.
- (E2) explains why using the old key to verify a certificate signed by the new key is incorrect.

**Fix Direction:**

Modify the Case 2 verification procedure so that only the 'new with old' certificate is verified using the old CA key, while the 'new with new' certificate is either self-verified or checked using the new key.

**Severity:** High
  *Basis:* This error causes a critical failure in the trust anchor update mechanism, preventing proper certificate verification during key rollover.

**Confidence:** High

**Experts mentioning this issue:**

- CausalExpert: Bug 1

---

## Report 3: 9810-4-3

**Label:** Optional Link Certificates Assumed Present in Verification Procedures

**Bug Type:** Both

**Explanation:**

The verification procedures for Cases 2 and 3 assume that the optional link certificates (newWithOld and oldWithNew) are available, which can lead to failures when a CA legitimately omits these certificates.

**Justification:**

- The ASN.1 definition and operator guidance mark 'new with old' and 'old with new' as OPTIONAL.
- Despite their optionality, the verification steps unconditionally require fetching these certificates, creating an inconsistency in handling mixed key scenarios.

**Evidence Snippets:**

- **E1:**

  ```
  Note: The usage of link certificates has been shown to be very specific for each use case, and no assumptions are done on this aspect. RootCaKeyUpdateContent is updated to specify these link certificates as optional.
  ```

- **E2:**

  ```
  In case 2, the verifier must get the ‘new with new’ and ‘new with old’ certificates, and in case 3, the verifier must get the ‘old with new’ certificate.
  ```

**Evidence Summary:**

- (E1) confirms that link certificates are defined as optional in the document.
- (E2) shows that the verification procedures assume these certificates are always present.

**Fix Direction:**

Clarify the verification procedures to include conditional handling for situations where the link certificates are omitted, such as by falling back to out-of-band trust anchor provisioning or by explicitly failing the verification process.

**Severity:** Medium
  *Basis:* This assumption can lead to interoperability failures in deployments that opt not to issue link certificates, affecting the certificate validation process in mixed key scenarios.

**Confidence:** High

**Experts mentioning this issue:**

- TemporalExpert: T2
- ScopeExpert: Issue-1
- CausalExpert: Issue 2
- DeonticExpert: Issue-2
- StructuralExpert: Issue-2
- CrossRFCExpert: Issue-2

---

## Report 4: 9810-4-4

**Label:** Misnamed LDAP/X.509 CA Certificate Attribute ('caCertificate' vs 'cACertificate')

**Bug Type:** Inconsistency

**Explanation:**

The document inconsistently refers to the CA certificate attribute using 'caCertificate' in some sections instead of the standard 'cACertificate', which may lead to confusion or misconfiguration in LDAP environments.

**Justification:**

- The introductory text correctly uses 'cACertificate' as per X.500/LDAP standards.
- Later verification procedures instruct implementers to look up certificates in the 'caCertificate' attribute, creating an internal naming mismatch.

**Evidence Snippets:**

- **E1:**

  ```
  When an LDAP directory is used to publish root CA updates, the old and new root CA certificates together with the two link certificates are stored as cACertificate attribute values.
  ```

- **E2:**

  ```
  If a repository is available, look up the certificates in the caCertificate attribute.
  ```

**Evidence Summary:**

- (E1) demonstrates the correct usage of the 'cACertificate' attribute as per LDAP standards.
- (E2) shows the inconsistent use of 'caCertificate' in the verification procedures.

**Fix Direction:**

Replace all instances of 'caCertificate' with 'cACertificate' in the verification procedure sections to align with the standard attribute naming.

**Severity:** Low
  *Basis:* Although LDAP attribute names are generally case-insensitive, the discrepancy may cause confusion or minor misconfigurations.

**Confidence:** High

**Experts mentioning this issue:**

- StructuralExpert: Issue-1
- TerminologyExpert: Issue-1
- CrossRFCExpert: Issue-2

---
