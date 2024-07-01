---
v: 3

cat: std
stream: IETF
updates: 6690, 7252, 7641, 7959, 8132, 8323
title: >
  Constrained Application Protocol (CoAP): Corrections and Clarifications
abbrev: Corrections and Clarifications to CoAP
docname: draft-bormann-core-corr-clar-latest

venue:
  mail: core@ietf.org
  github: core-wg/corrclar


author:
 -
    name: Carsten Bormann
    org: Universität Bremen TZI
    street: Postfach 330440
    city: Bremen
    code: D-28359
    country: Germany
    phone: +49-421-218-63921
    email: cabo@tzi.org

normative:
  RFC6690: link-format
  RFC7252: coap
  RFC7641: observe
  RFC7959: block
  RFC8132: etch
  RFC8323: coap-tcp
informative:
  RFC8516: RC429
  I-D.bormann-core-responses: responses
  Err4954: 7252
  Err5078: 7252

--- abstract


RFC 7252 defines the Constrained Application Protocol (CoAP), along
with a number of additional specifications, including RFC 7641, RFC
7959, RFC 8132, and RFC 8323.
RFC 6690 defines the link format that is used in CoAP self-description
documents.

Some parts of the specification may be unclear or even contain errors
that may lead to misinterpretations that may impair interoperability
between different implementations.
The present document provides corrections, additions, and
clarifications to the RFCs cited; this document thus updates these
RFCs.
In addition, other clarifications related to the use of CoAP in other
specifications, including RFC 7390 and RFC 8075, are also provided.

--- middle

# Introduction

{{-coap}} defines the Constrained Application Protocol (CoAP), along
with a number of additional specifications, including {{-observe}},
{{-block}}, {{-etch}}, and {{-coap-tcp}}.
{{-link-format}} defines the link format that is used in CoAP
self-description documents.

During implementation and interoperability testing of these RFCs, and
in their practical use, some ambiguities and common misinterpretations
have been identified, as well as a few errors.

The present document summarizes identified issues and provides
corrections needed for implementations of CoAP to interoperate, i.e.,
it constitutes an update to the RFCs referenced.  This document also
provides other clarifications related to common misinterpretations of
the specification.  References to CoAP should, therefore, also include
this document.

In addition, some clarifications and corrections are also provided for
documents that are related to CoAP, including RFC 7390 and RFC 8075.

## Process

### Original text

The present document is an Internet-Draft, which is not intended to be
published as an RFC quickly.  Instead, it will be maintained as a
running document of the CoRE WG, probably for a number of years, until
the need for new entries tails off and the document can finally be
published as an RFC.  (This paragraph to be rephrased when that
happens.)

The status of this document as a running document of the WG implies a
consensus process that is applied in making updates to it.  The rest
of this subsection provides more details about this consensus process.
(This is the intended status; currently, the document is an individual submission only.)

(Consensus process TBD, but it will likely be based on an editor's
version in a publicly accessible git repository, as well as periodic
calls for consensus that lead to a new published Internet-Draft.)

### Proposed text based on IETF 117 and 2023-08-30 CoRE WG interim discussion

This section describes the process that will be used for developing
the present document (called "-corr-clar" colloquially).

This process might be revised as its execution progresses.

{: start="0"}
0. (Done as of this a draft): include the present process proposal.\\
   The document can then already be considered for WG adoption.

1. Go through the following available material and revise/create
   Github issues at [ISSUES] as needed:
    - Existing issues at [ISSUES]
        - More to be opened by Jon Shallow regarding Block-wise, see [JON-ISSUES]
    - CoAP FAQ at the CoRE WIKI [WIKI-FAQ]
        - Each point likely to become a new, short issue

2. Categorize the Github issues at [ISSUES] as to the topics they relate to, by tagging them.\\
Completing a first round of this will be a task for a dedicated team.

3. For each issue or set of issues at [ISSUES], confirm with the CoRE
   WG and gather feedback from affected protocol
   designers/implementors if the issue is best to be:
    - Included and covered in -corr-clar, as is or revised
    - Simply omitted in -corr-clar
    - Omitted in -corr-clar and left for a possible -bis document.\\
      (For example, this might be the case for some specific points related to RFC 7959.)

4. Reshape the -corr-clar document in order to reflect a sequence of
 pairs (Diagnosis, Therapy), where:
   - Diagnosis is the gist of a set of Github issues to cover, and
   - Therapy is the correction or clarification to address those.

   Even though at a high-level, the scope should be already clear by
   looking at the table of contents.
   That is, at this stage, there is no need to necessarily elaborate
   the Therapy in detail, but it is necessary to make a reader
   understand "what we are dealing with and taking which direction".

5. WG document work can then focus on improving the therapy parts,
   until all points are satisfactorily addressed and documented.



[ISSUES]: https://github.com/core-wg/corrclar/issues

[WIKI-FAQ]: https://github.com/core-wg/wiki/wiki/CoAP-FAQ

[JON-ISSUES]: https://datatracker.ietf.org/doc/minutes-interim-2023-core-11-202307051400/#attacks-on-the-constrained-application-protocol-coap-christian-amsuss-jon-shallow

[117-side-meeting]: https://notes.ietf.org/notes-ietf-core-side-meeting-ietf-117-core


## Terminology

{::boilerplate bcp14-tagged}

When a section of this document makes formal corrections, additions
or invalidations to text in a referenced RFC, this is clearly summarized.
The text from the RFC that is being addressed is given and labeled
"INCOMPLETE", "INCORRECT", or "INCORRECT AND INVALIDATED", followed
by the correct text labeled "CORRECTED", where applicable.  When text
is added that does not simply correct text in previous
specifications, it is given with the label "FORMAL ADDITION".

Where a resolution has not yet been agreed, the resolution is marked PENDING.

In this document, a reference to a section in RFC nnnn is written
as RFC nnnn-\<number>, where \<number> is the section number.

# RFC 7252

## RFC7252-1.2: Terminology (Request-URI)

{{RFC7252}} uses the term "request URI" repeatedly, but only provides a
vague definition in {{Section 5.7.2 of RFC7252}}.
Text should be added to the definitions in {{Section 1.2 (Terminology)
of RFC7252}}.

{: vspace='0'}
INCOMPLETE; FORMAL ADDITION (Section 1.2):
: Request URI:
  : The URI that identifies a resource on a server intended to be
    addressed by a request; constructed from the context of the
    request combined with Options present in the request using the
    process defined in {{Section 6.5 (Composing URIs from Options) of
    RFC7252}}, see {{Section 5.7.2 (Forward-Proxies) of
    RFC7252}} for further details.
    Related to the HTTP concept of "target URI"; see {{Section 7.1
    (Determining the Target Resource) of ?RFC9110}}; previously called
    "effective request URI" in {{Section 5.5 (Effective Request URI) of
    ?RFC7230}}.

PENDING.

Note that a similar, but distinct concept is the "base URI", relative
to which relative URIs are resolved.
This is more complex in CoAP than in HTTP because CoAP can multicast
requests {{Section 8 of -coap}}, expecting unicast responses; these need
to be interpreted relative to the unicast source address from which
the responses come.

{{Section 8.2 of -coap}} has:

{:quote}
>  For the purposes of interpreting the Location-* options and any links
   embedded in the representation, the request URI (i.e., the base URI
   relative to which the response is interpreted) is formed by replacing
   the multicast address in the Host component of the original request
   URI by the literal IP address of the endpoint actually responding.

Similarly, {{Section 8.2.1 of -coap}} (Caching) says:

{:quote}
>  A response received in reply to a GET request to a multicast group
   MAY be used to satisfy a subsequent request on the related unicast
   request URI.  The unicast request URI is obtained by replacing the
   authority part of the request URI with the transport-layer source
   address of the response message.

Further discussion of a more generalized response concept can be found in
{{-responses}}.


## RFC7252-5.10.5: Max-Age

In the discussion of {{-RC429}}, a comment was
made that it would be needed to define the point in time relative to
which Max-Age is defined.  A sender might reference it to the time it
actually sends the message containing the option (and paragraph 3 of
RFC7252-5.10.5 indeed requests that Max-Age be updated each time a
message is retransmitted).  The receiver of the message does not have
reliable information about the time of sending, though.  It may
instead reference the Max-Age to the time of reception.  This in
effect extends the time of Max-Age by the latency of the packet.
This extension was deemed acceptable for the purposes of {{-RC429}},
but may be suboptimal when Max-Age is about the lifetime of a response
object.

{: vspace='0'}
INCOMPLETE:
: The value is intended to be current at the time of transmission.

PENDING.

## RFC7252-7.2.1: "ct" Attribute (content-format code)

As has been noted in {{Err5078}}, there is no information in {{RFC7252}}
about whether the "ct" target attribute can be present multiply or
not.

The text does indicate that the value of the attribute MAY be "a
space-separated sequence of Content-Format codes, indicating that
multiple content-formats are available", but it does not repeat the
prohibition of multiple instances that the analogously structured "rt"
and "if" attributes in {{Sections 3.1 and 3.2 of RFC6690}} have.

This appears to be an oversight.
Published examples in {{Section 4.1 of ?RFC9148}} and {{Section 4.3 of
?RFC9176}} further illustrate that the space-separated approach is
generally accepted to be the one to be used.
There is no gain to be had from allowing both variants, and it would
be likely to cause interoperability problems.

At the 2022-11-23 CoRE WG interim meeting, there was agreement that
{{Err5078}} should be marked "VERIFIED", which was done on 2023-01-18.

{: vspace='0'}
INCOMPLETE; FORMAL ADDITION:
: The Content-Format code attribute MUST NOT appear more than once in a
  link.

## RFC 7252-12.3: Content-Format Registry {#ct}

{{Section 12.3 of RFC7252}} established the CoAP Content-Formats
Registry, which maps a combination of an Internet Media Type
with an HTTP Content Coding, collectively called a Content-Format, to
a concise numeric identifier for that Content-Format.
The "Media Type" is more than a Media-Type-Name (see {{?RFC9193}} for an
extensive discussion), i.e., it may contain parameters beyond the mere
combination of a type-name and a subtype-name registered in
{{?IANA.media-types}}, as per {{?RFC6838}}, conventionally identified by
the two names separated by a slash.
This construct is often called a Content Type to reduce the confusion
with a Media-Type-Name (e.g., in {{Section 8.3 of ?RFC9110}}, which then
however also opts to use the term Media Type for the same information set).

The second column of the Content-Format registry is the Content
Coding, which is defined in {{Section 8.4.1 of ?RFC9110}}.
For historical reasons, the HTTP header field that actually carries
the content coding is called Content-Encoding; this often leads to the
misnaming of Content Coding as "content encoding".

As has been noted in {{Err4954}}, the text in {{Section 12.3 of RFC7252}}
incorrectly uses these terms in the context of content types and
content coding:

1. The field that describes the Content Type is called "Media Type".
   This can lead to the misunderstanding that this column just carries
   a Media-Type-Name (such as "`text/plain`"), while it actually also
   can carry media type parameters (as in "`text/plain; charset=UTF-8`").

2. The field that describes the Content Coding uses the incorrect name
   "Content Encoding".

{: vspace='0'}
INCORRECT, CORRECTED:
: The VERIFIED Errata Report {{Err4954}} corrects the usage of
  "Content-Encoding" in the text and changes the name of the first
  column of the Content-Format registry to "Content Type" and the name
  of the second field to "Content Coding"; this change has been
  carried out by IANA.

# IANA Considerations

This document makes no new requests to IANA.

Individual clarifications may contain IANA considerations; as for
example in {{ct}}.

# Security Considerations

This document provides a number of corrections and clarifications to
existing RFCs, but it does not make any changes with regard to the security
aspects of the protocol.  As a consequence, the security
considerations of the referenced RFCs apply without additions.

(To be changed when that is no longer true; probably the security
considerations will then be on the individual clarifications.)

--- back

# Acknowledgements
{: numbered='no'}

The present document is modeled after RFC 4815 and the Internet-Drafts
of the ROHC WG that led to it.  Many thanks to the co-chairs of the
ROHC WG and WG members that made this a worthwhile and successful
experiment at the time.

<!--  LocalWords:  interoperate invalidations retransmitted ROHC
 -->
<!--  LocalWords:  suboptimal
 -->
