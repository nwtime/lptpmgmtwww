---
title: "pmc(8): PTP management client"
description: "Linux PTP man page for the PTP management client."
date: 2023-02-16 
---

### pmc-ptpmgmt: PTP management client

#### SYNOPSIS

<code>pmc-ptpmgmt [ -f _config-file_ ] [ -2 | -4 | -6 | -u ] [ -b _boundary-hops_ ] [ -d _domain-number_ ] [ -i _interface_ ] [ -s _uds-address_ ] [ -t _transport-specific-field_ ] [ _long-options_ ] [ -v ] [ -z ] [ command ] ...</code>

#### DESCRIPTION

`pmc-ptpmgmt` is a program which implements a PTP management client according to IEEE standard 1588. The program reads from the standard input or from the command line actions specified by name and management ID, sends them over the selected transport and prints any received replies. There are three actions supported:

<code>**GET**</code>

: retrieves the specified information,

<code>**SET**</code>

: updates the specified information and

<code>**CMD**</code> (<code>**COMMAND**</code>)

: initiates the specified event.

By default the management commands are addressed to all ports. The `TARGET` command can be used to select a particular clock and port for the subsequent messages.

Command `help` can be used to get a list of supported actions and management IDs.

#### OPTIONS

<code>**-f _config-file_**</code>

: Read configuration from the specified file. No configuration file is read by default.

<code>**-2**</code>

: Select the IEEE 802.3 network transport.

<code>**-4**</code>
: 
Select the UDP IPv4 network transport. This is the default transport.

<code>**-6**</code>

: Select the UDP IPv6 network transport.

<code>**-u**</code>

: Select the Unix Domain Socket transport.

<code>**-b _boundary-hops_**</code>

: Specify the boundary hops value in sent messages. The default is 1.

<code>**-d _domain-number_**</code>

: Specify the domain number in sent messages. The default is 0.

<code>**-i _interface_**</code>

: Specify the network interface. The default for Unix Domain Sockets is `/var/run/pmc.$pid` for root user and `/var/run/user/$uid/pmc.$pid` for other users.

<code>**-s _uds-address_**</code>

: Specifies the address of the server's UNIX domain socket. The default is `/var/run/ptp4l`.

<code>**-t _transport-specific-field_**</code>

: Specify the transport specific field in sent messages as a hexadecimal number. The default is 0x0.

<code>**-h**</code>

: Display a help message.

<code>**-v**</code>

: Prints the libptpmgmt version and exits.

<code>**-z**</code>

: The official interpretation of the 1588 standard mandates sending `GET` actions with valid (but meaningless) `TLV` values. Therefore the `pmc` program normally sends `GET` requests with properly formed `TLV` values. This option enables the legacy option of sending zero length `TLV` values instead.

#### LONG OPTIONS

Each and every configuration file option (see below in sections [PROGRAM OPTIONS](#program-options) and [PORT OPTIONS](#port-options)) may also appear as a "long" style command line argument. For example, the `transportSpecific` option may be set using either of these two forms:

`--transportSpecific 1`

`--transportSpecific=1`

Option values given on the command line override values in the global section of the configuration file (which, in turn, overrides default values).

#### CONFIGURATION FILE

The configuration file is divided into sections. Each section starts with a line containing its name enclosed in brackets and it follows with settings. Each setting is placed on a separate line, it contains the name of the option and the value separated by whitespace characters. Empty lines and lines starting with `#` are ignored.

The global section (indicated as `[global]`) sets the global program options as well as the default port specific options. Other sections are port specific sections and they override the default port options. The name of the section is the name of the configured port (e.g. `[enp0s25]`).

#### PROGRAM OPTIONS

<code>**domainNumber**</code>

: The domain attribute of the local clock. The default is 0.

<code>**socket_priority**</code>

: Configure the `SO_PRIORITY` of sockets. This is to support cases where a user wants to route pmc traffic using Linux `qdiscs` for the purpose of traffic shaping. This option is only available with the IEEE 802.3 transport (the `-2` option) and is silently ignored when using the UDP IPv4/6 network transports. Must be in the range of 0 to 15, inclusive. The default is 0.

<code>**udp6_scope**</code>

: Specifies the desired scope for the IPv6 multicast messages. This will be used as the second byte of the primary address. This option is only relevant with IPv6 transport. See [RFC 4291](https://datatracker.ietf.org/doc/html/rfc4291). The default is 0x0E for the global scope.

<code>**uds_address**</code>

: Specifies the address of the server's UNIX domain socket, same as the `-s` option.

#### PORT OPTIONS

<code>**network_transport**</code>

: Select the network transport. Possible values are `UDPv4`, `UDPv6`, and `L2`. The default is `UDPv4`.

<code>**ptp_dst_mac**</code>

: The MAC address to which PTP management messages should be sent. Relevant only with L2 transport. The default is `01:1B:19:00:00:00`.

<code>**transportSpecific**</code>

: The transport specific field. Must be in the range 0 to 255. The default is 0.

<code>**udp_ttl**</code>

: Specifies the Time to live (TTL) value for IPv4 multicast messages and the hop limit for IPv6 multicast messages. This option is only relevant with the IPv4 and IPv6 UDP transports. The default is 1 to restrict the messages sent by `ptp4l` to the same subnet.

#### MANAGEMENT IDS

`pmc-ptpmgmt` supports all PTP version 2 (IEEE Std 1588-2019) Management TLVs and those specific to the linuxptp implementation.
Though build of `GRANDMASTER_CLUSTER_TABLE`, `UNICAST_MASTER_TABLE`, and `ACCEPTABLE_MASTER_TABLE` are not supported as they use tables.

#### WARNING

Be cautious when the same configuration file is used for both `ptp4l` and `pmc`.  Keep in mind that values specified in the configuration file take precedence over their default values. If a certain option which is common to `ptp4l` and `pmc` is specified to a non-default value in the configuration file (e.g. for `ptp4l`), then this non-default value applies also for `pmc`. This might be not what is expected.

To avoid securely this unexpected behaviour, different configuration files for `ptp4l` and `pmc` are recommended.

#### SEE ALSO

[pmc(8)](https://linuxptp.nwtime.org/documentation/pmc/) [ptp4l(8)](https://linuxptp.nwtime.org/documentation/ptp4l/)