---
tags:
  - clock
relates to:
  - "[[Unreliable Clocks]]"
  - "[[Time-Of-Day Clocks]]"
---
[[Time-Of-Day Clocks]] are quite unreliable

They need to be synchronized with [[NTP]] in order to be useful. But there are problems 
- The quartz clock in the computer ***drifts*** - time starts going faster or slower than it should
- If a computer’s clock differs too much from an [[NTP]] server, it may refuse to synchronize, or the local clock will be ***forcibly reset***. Any applications observing the time before and after this reset may see time go backward or suddenly jump forward.
- If a node is accidentally firewalled off from NTP servers, the misconfiguration may go unnoticed for some time
- NTP synchronization can only be as good as the network delay, so there is a limit to its accuracy
- Some NTP servers are wrong or misconfigured, reporting time that is off by hours
- Leap seconds result in a minute that is 59 seconds or 61 seconds long, which messes up timing assumptions in systems that are not designed with leap seconds in mind
- In virtual machines, the hardware clock is virtualized, which raises additional challenges for applications that need accurate timekeeping. When a CPU core is shared between virtual machines, each [[Virtual Machine]] is paused for tens of milliseconds while another VM is running. From an application’s point of view, this pause manifests itself as the clock suddenly jumping forward
- If you run software on devices that you don’t fully control (e.g., mobile or embedded devices), you probably cannot trust the device’s hardware clock at all