---
title: "SCONE TCP Option"
abbrev: "SCONE for TCP"
docname: draft-tbd-scone-tcp-00
category: std

ipr: trust200902
area: Web and Internet Transport
workgroup: SCONE
stream: IETF
keyword: Adaptive Bit-Rate Video
keyword: TCP
keyword: SCONE

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs]

author:
  -
    ins: W. Eddy
    name: Wesley Eddy
    organization: Meta
    email: wesleyeddy@meta.com
  -
    ins: M. Joras
    name: Matt Joras
    organization: Meta
    email: matt.joras@gmail.com

normative:
  RFC9293:

informative:
  RFC9000:
  I-D.joras-scone-video-optimization-requirements:
  I-D.ietf-scone-protocol:

--- abstract

This document describes a TCP option that permits network elements to provide
TCP endpoints advice on rate limits within the network.  The functionality for
TCP is analogous to SCONE packets within the QUIC protocol.

--- middle

# SCONE Background and Introduction

Standard Communication with Network Elements (SCONE)
{{I-D.ietf-scone-protocol}} is an extension to QUIC {{RFC9000}} that provides
the capability for network elements to provide QUIC application endpoints with
guidance on potential permitted throughput, e.g. in order to make explicit the
presence of traffic limiting mechanisms within the network that can be
problematic for video streaming
{{I-D.joras-scone-video-optimization-requirements}} and other applications.

In QUIC, SCONE is negotiated between endpoints using a transport parameter, and
the QUIC endpoints send SCONE packets periodically.  The SCONE packets are
visible to network elements that modify the throughput guidance within them.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# TCP Option for SCONE

This document defines a TCP {{RFC9293}} option to provide analogous SCONE
functionality for TCP.  This could be viewed as similar to the way that TCP MSS
clamping works traditionally, with the TCP MSS options included by endpoints
being inspected and modified en-route by elements on the network path that can
provide more pertinent guidance.

## Option Format

~~~ aasvg
+------------+------------+-------------------------+
| Kind = TBD | Length = 4 |    Throughput Guidance  |
+------------+------------+-------------------------+
~~~

TODO: Explain the throughput guidance values used, which should include the present QUIC values.


TODO note assumed interaction with other options, namely TCP-AO.

## Use During Handshake

TODO: include on SYN and SYN-ACK; serves as client hint, network elements can use that right away

## Use Post-Handshake

TODO: could be sent either by endpoints or a packet with no data could be spoofed within the network; this will be controversial

### Endpoint-Included

TODO: can be included either with application data or alone on an any generated normal ACK, when not in loss recovery.  Can also be sent by itself, and the receiving side shouldn't treat it as a dupack (should not trigger progression towards fast retransmit).

### Network-Initiated

TODO: generate a pure ACK (no data) matching last observed sequence and ack values.  This is okay because it proves the device has credible threat of network violence, as assumed by SCONE.

# API for TCP Applications

TODO: describe informationally a possible socket option to request SCONE use

TODO: describe informationally a possible socket option to get SCONE info

# Security Considerations

The security considerations for SCONE-TCP are similar to those for SCONE as
present in QUIC, however, some differences arise because TCP security lacks the
same cryptographic methods that are present in QUIC.

# IANA Considerations

TODO: TCP option kind value is TBD.

--- back

# Acknowledgments
{:numbered="false"}

This document represents collaboration and inputs from others, including:

- Alan Frindell
* Bryan Tan
* Anoop Tomar
