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
    email: mjoras@meta.com

normative:
  RFC9293:

informative:
  I-D.joras-scone-video-optimization-requirements:

--- abstract

This document describes a TCP option that permits network elements to provide
TCP endpoints advice on rate limits within the network.  The functionality for
TCP is analogous to SCONE packets within the QUIC protocol.

--- middle

# SCONE Background and Introduction

TODO {{I-D.joras-scone-video-optimization-requirements}},

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# TCP Option for SCONE

TODO

## Option Format

TODO picture

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

TODO

# IANA Considerations

TODO: TCP option kind value

--- back

# Acknowledgments
{:numbered="false"}

This document represents collaboration and inputs from others, including:

- Alan Frindell
* Bryan Tan
* Anoop Tomar
