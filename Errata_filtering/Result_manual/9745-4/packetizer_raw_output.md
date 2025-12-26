# Errata Reports

Total reports: 2

---

## Report 1: 9745-4-1

**Label:** Invalid HTTP-date Timezone in Sunset Header Example (UTC instead of GMT)

**Bug Type:** Inconsistency

**Explanation:**

The RFC 9745 example for the Sunset header uses 'UTC' as the timezone token, which is non‐conformant with the HTTP-date syntax defined in RFC 8594 and RFC 7231/RFC 9110 that requires 'GMT'.

**Justification:**

- RFC 9745 Section 4 shows the example 'Sunset: Sun, 30 Jun 2024 23:59:59 UTC' which violates the normative HTTP-date syntax.
- RFC 8594 and the HTTP core specifications mandate using 'GMT' as the timezone token, as evidenced by the provided examples.

**Evidence Snippets:**

- **E1:**

  RFC 9745 Section 4 example:  
        `Deprecation: @1688169599`  
        `Sunset: Sun, 30 Jun 2024 23:59:59 UTC`

- **E2:**

  RFC 8594 defines Sunset as an HTTP-date and references RFC 7231’s HTTP-date syntax:  
        “The Sunset value is an HTTP-date timestamp, as defined in Section 7.1.1.1 of [RFC7231]. … Sunset = HTTP-date”  
        and gives only `GMT` examples:  
        `Sunset: Sat, 31 Dec 2018 23:59:59 GMT` and `Sunset: Wed, 11 Nov 2026 11:11:11 GMT`.

**Evidence Summary:**

- (E1) Shows the example from RFC 9745 Section 4 where the Sunset header uses 'UTC' as the timezone token.
- (E2) Demonstrates that the normative definition of HTTP-date requires the use of 'GMT' as evidenced by the examples in RFC 8594.

**Fix Direction:**

Change the example in RFC 9745 Section 4 to use 'GMT' instead of 'UTC', e.g., 'Sunset: Sun, 30 Jun 2024 23:59:59 GMT'.


---

## Report 2: 9745-4-2

**Label:** Deprecation–Sunset Ordering Constraint Clarity in RFC 9745

**Bug Type:** None

**Explanation:**

RFC 9745 mandates that the Sunset timestamp must not precede the Deprecation timestamp, but the accompanying guidance and flexible handling of misconfigurations could be perceived as ambiguous.

**Justification:**

- The specification asserts that 'The timestamp given in the Sunset HTTP header field MUST NOT be earlier than the one given in the Deprecation header field.'
- It also advises that if this constraint is violated, the client developer should consult the resource developer, which may lead to differing interpretations.

**Evidence Snippets:**

- **E1:**

  “The timestamp given in the Sunset HTTP header field MUST NOT be earlier than the one given in the Deprecation header field.”
“If that happens (for example, due to misconfiguration of deployment of the resource or an error), the client application developer SHOULD consult the resource developer to get clarification.”
“The Sunset header field contains a single timestamp that advertises the point in time when the resource is expected to become unresponsive. The Sunset value … SHOULD be a timestamp in the future.”
“The act of deprecation does not change any behavior of the resource. The presence of a Deprecation header field in a response is not meant to signal a change in the meaning or function of a resource…”
“In cases where the Deprecation header field value is in the past, the client application developers MUST no longer assume that the behavior of the resource will remain the same as before the deprecation date.”

**Evidence Summary:**

- (E1) Provides the normative statement on the ordering of the Deprecation and Sunset timestamps along with guidance for handling misconfigurations, which may be viewed as ambiguous.


---
