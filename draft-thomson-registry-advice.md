---
title: Advice for Creating IANA Registration Policies
abbrev: Registry Advice
docname: draft-thomson-registry-advice-latest
category: std
ipr: trust200902
area: General
workgroup: None

stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]

author:
 -
    ins: M. Thomson
    name: Martin Thomson
    org: Mozilla
    email: martin.thomson@gmail.com

normative:

informative:


--- abstract

RFC 5226 defines procedures for establishing a registry of protocol parameters.
That document contains minimal advice about what policies might be adopted and
the implications of those choices.  This document provides some advice,
primarily that strict registration policies for IANA registries are rarely
advisable.

--- middle


# Introduction

Many protocols use the protocol registries that are managed by the Internet
Assigned Numbers Authority (IANA) {{?IANA-MOU=RFC2860}} to manage the allocation
of protocol parameters.  When establishing a registry for protocol parameters,
choosing an appropriate registration policy is critical.  RFC 5226 {{?IANA-CONS}} 

While registries might be perceived as a way of retaining some sort of control
over use of protocols, stricter policies tend to inappropriately constrain
protocol deployment and can lead to violation of those policies.  A permissive
registration policy for IANA registries avoids these issues and encourages
better use of registries.

RFC 5226 {{?IANA-CONS}} provides a small amount of advice, notably this from
Section 5.3:

> In addition, documented IANA considerations are sometimes found to be too
> stringent to allow even working group documents (for which there is strong
> consensus) to obtain code points from IANA in advance of actual RFC
> publication.

This document examines the common registration policies defined in RFC 5226
{{?IANA-CONS=RFC5226}} and provides advice on how to define appropriately
permissive registration policies based using those building blocks.


# Registries Are Not a Tool for Control {#control}

It is often stated in the defense of a strict registration policy, such as
Standards Action, that this this is necessary to ensure a measure of control
over how the protocol develops.  The rationale being that use of new codepoints
in a given space requires careful consideration and discussion and that
interoperation would be adversely affected by the use of codepoints that are
poorly specified.

In practice, choosing stricter registry policies does little to discourage the
use of codepoints.  A strict policy tends to discourage registration, though
less discouragement on the use of codepoints.

The primary purpose of a registry is to ensure that incompatible semantics are
not associated with the same code point.  Avoiding registration of codepoints
that are in use is highly likely to result in interoperability failures.  Thus,
interoperability is not served by a policy that makes it difficult to register a
codepoint.


# Private and Experimental Use Leaks

Many protocols reserve a range of codepoints for "Private Use" or "Experimental
Use" {{?IANA-CONS}}.  The motivation for using these policies being that
experimentation or proprietary use of extensions can be enabled by reserving a
portion of the space for codepoints.

Private and experimental use of protocol extensions can become more widely used
than originally intended.  Separately, implementations might create rules for
special treatment of codepoints in these spaces.  RFC 6648 {{?X-DASH=RFC6648}}
provides more detail on the various issues with reserving experimental or
private use protocol identifiers.

Moving a protocol semantic from an established experimental or private use
codepoint to a new codepoint is difficult.  For codepoints that become widely
used, this difficulty increases.  The success of a protocol extension that is
defined in a private or experimental use space often leads to long term use of
that codepoint.

Avoid using the "Private Use" or "Experimental Use" policies.  Selecting more
lenient registration policies is a better way of enabling private use.
Provisional registrations are more appropriate for supporting experimentation.


# Consider Provisional Registrations {#provisional}

Some existing registries have a policy that allows provisional registration, for
example RFC 7595 {{?URI-REG=RFC7595}} or RFC 3864 {{?HEADER-REG=RFC3864}}.
Registrations that are designated "provisional" are usually defined as being
more readily created, changed, reassigned, moved to another status, or even
removed.  For instance, RFC 7595 allows a provisional registration to be made
with incomplete information.

Allowing provisional registration ensures that the primary goal of maintaining a
registry - avoiding collisions between incompatible semantics - is preserved
without inadvertently creating statements about the value of the protocol
mechanism that are identified in a registry.

Provisional registrations for codepoints that are ultimately standardized can be
promoted to permanent status.  The criteria that are defined for marking a
provisional registration as permanent could be made as strict as desired.

To support experimentation, provisional registrations could be defined as having
expiration dates.  However, renewing an expiration date should be no harder than
the creation of the registration.  If a policy allows for explicit removal of
registrations, stronger controls are advised to avoid accidental or malicious
removals.

A similar system to provisional registration is adopted for TLS registries
{{?TLS-REG=I-D.ietf-tls-iana-registry-updates}}.  Permissive registration
policies are defined for the creation of new entries.  TLS registries include a
field that identifies codepoints as "Recommended".  A Standards Track document
{{?IETF-STD=RFC2026}} is required in order to mark a codepoint as "Recommended".


# Experts aren't Guardians

The "Expert Review" and "Specification Required" policies rely on review of
registration applications by a designated expert.  A registry that is
established without guidance to an expert effectively cedes decisions about
registration policy to the expert, which can lead to arbitrary policy.

Experts, by their nature, can be predisposed to reject registrations.  This
discourages use of the registry, which can harm interoperability.

If a registry has a designated expert, define a narrow set of conditions for
rejection of registration applications (see {{security}} for a sample
criterion).  This encourages approval of registrations and can made the task of
the expert easier.


# RFC Required is Rarely Appropriate

The "RFC Required" policy {{?IANA-CONS}} is often used inappropriately as a
proxy for another property.

For example, if the intent is to require community consensus then "IETF
Consensus", "Standards Action" or possibly "IESG Approval" are likely to be more
appropriate.  Where the intent is to insist on a particular standard of
documentation for a specification, then the "Specification Required" policy with
additional guidance to a designated expert can acheive the same end.

In general, avoid the use of the "RFC Required" policy.


# Security Considerations {#security}

Increased use of limited codepoint spaces is a potential adverse outcome of a
more lenient registration policy.  For registries with designated experts,
detecting and blocking this sort of attack can be easy.  If a policy includes
review from an expert, allowing experts to reject registrations that are
excessive or duplicative can help.

To avoid exhaustion of limited space, registries that have limited space are
advised to avoid the First Come, First Served policy {{?IANA-CONS}}.


# IANA Considerations

This document makes no request of IANA.


--- back
