---
title: "phc_ctl-ptpmgmt(8): directly control PHC device clock"
description: "Linux PTP man page for directly controlling a master PTP hardware clock."
date: 2020-06-15 
---

### phc_ctl-ptpmgmt: directly control PHC device clock

#### SYNOPSIS

<code>phc_ctl-ptpmgmt [ options ] \<device> [ commands ]</code>

#### DESCRIPTION

`phc_ctl-ptpmgmt` is a program which can be used to directly control a PHC clock device. Typically, it is used for debugging purposes, and has little use for general control of the device. For general control of PHC clock devices, [phc2sys(8)](https://linuxptp.nwtime.org/documentation/phc2sys/) should be preferred.

<code>\<device></code> may be either `CLOCK_REALTIME`, any `/dev/ptpX` device, or any ethernet device which supports `ethtool`'s `get_ts_info` ioctl.

#### OPTIONS

<code>**-h**</code>

: Display a help message.

<code>**-v**</code>

: Prints the libptpmgmt version and exits.

#### COMMANDS

`phc_ctl-ptpmgmt` is controlled by passing commands which take either an optional or required parameter. The commands (outlined below) will control aspects of the PHC clock device. These commands may be useful for inspecting or debugging the PHC driver, but may have adverse side effects on running instances of [ptp4l(8)](https://linuxptp.nwtime.org/documentation/ptp4l/) or [phc2sys(8)](https://linuxptp.nwtime.org/documentation/phc2sys/).

<code>**set _seconds_**</code>

: Set the PHC clock time to the value specified in seconds. Defaults to reading `CLOCK_REALTIME` if no value is provided.

<code>**get**</code>

: Get the current time of the PHC clock device.

<code>**adj _seconds_**</code>

: Adjust the PHC clock by an amount of seconds provided. This argument is required.

<code>**freq _ppb_**</code>

: Adjust the frequency of the PHC clock by the specified parts per billion. If no argument is provided, it will attempt to read the current frequency and report it.

<code>**phase _seconds_**</code>
: Pass an amount in seconds to the PHC clock's phase control keyword. This argument is required.

<code>**cmp**</code>

: Compare the PHC clock device to `CLOCK_REALTIME`, using the best method available.

<code>**caps**</code>

: Display the device capabilities. This is the default command if no commands are provided.

<code>**wait _seconds_**</code>

: Sleep the process for the specified period of time, waking up and resuming afterwards. This command may be useful for sanity checking whether the PHC clock is running as expected.

The arguments specified in seconds are read as double precision floating point values, and will scale to nanoseconds. This means providing a value of 5.5 means 5 and one half seconds. This allows specifying fairly precise values for time.

#### EXAMPLES

Read the current clock time from the device

`phc_ctl-ptpmgmt /dev/ptp0 get`

Set the PHC clock time to `CLOCK_REALTIME`.

`phc_ctl-ptpmgmt /dev/ptp0 set`

Set PHC clock time to 0 (seconds since Epoch).

`phc_ctl-ptpmgmt /dev/ptp0 set 0.0`

Quickly sanity check frequency slewing by setting slewing frequency by positive 10%, resetting clock to 0.0 time, waiting for 10 seconds, and then reading time. The time read back should be (roughly) 11 seconds, since the clock was slewed 10% faster.

`phc_ctl-ptpmgmt /dev/ptp0 freq 100000000 set 0.0 wait 10.0 get`

#### SEE ALSO
[pmc-ptpmgmt(8)](/documentation/man/pmc-ptpmgmt/) [phc_ctl(8)](https://linuxptp.nwtime.org/documentation/phc_ctl/) [ptp4l(8)](https://linuxptp.nwtime.org/documentation/ptp4l/), [phc2sys(8)](https://linuxptp.nwtime.org/documentation/phc2sys/)