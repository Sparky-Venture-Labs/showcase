# Networks

The network decides whether a control system feels instant or flaky, so I design it before anything else goes in.
I build on UniFi, and on Araknis and WattBox when a job calls for Snap One gear.

## How I lay one out

- **Separate networks by job.** Control and AV share a network with the Savant host. Cameras get their own.
  IoT gear and guests are walled off, and the control network only gets what it needs from the rest.
- **Keep together what has to be together.** Some gear only works on the same network as the host (discovery,
  multicast video). That decides the layout first, not last.
- **Addresses that don't move.** Reservations for everything the control system talks to, and a DHCP pool that
  stays out of their way.
- **Remote work without mix-ups.** Over remote access, two houses can look alike on the network, so I confirm
  which one I'm actually on before touching anything off-site.
- **Documented and labeled.** Ports, reservations and rules written down, so the next visit is a quick fix and not
  a rebuild.

## UniFi inside the control system

UniFi isn't only the network on these jobs. Access doors and gates, Protect cameras and doorbells, and PDU Pro
outlets are all driven from Savant. Those are written up in [Savant integrations](savant.md).

---

support@sparkyventurelabs.com · [sparkyventurelabs.com](https://sparkyventurelabs.com)
