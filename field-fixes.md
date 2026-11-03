# Field fixes

A few Savant problems that took real digging: what it looked like, what it turned out to be, and how it ended.

---

## The house went dark after an upload

**What it looked like:** A Mac-based Savant Pro Host came back from a routine config upload running no Savant
services at all. SSH, ping and the network were all fine. Every room was dead.

**What it was:** Savant Application Manager had been run on the host itself earlier that day, and it had emptied
the runtime's system config. Nothing showed until the next upload, hours later, which is why it looked unrelated.

**How it ended:** We put the system config back and the house came back up. The standing rule since: SAM and
Blueprint never run on a Pro Host.

---

## Samsung TVs that "went offline"

**What it looked like:** Savant suddenly couldn't turn the TVs on, and only a full system reboot brought them back.
It looked like a network problem.

**What it was:** Not the network. Savant's own record of the TVs' power state went stale and locked itself in. We
tested and ruled out every plausible cause before settling on that.

**How it ended:** A small service on the host now keeps Savant's power state honest, and the TVs stopped needing
reboots.

---

## Music playing everywhere, heard nowhere

**What it looked like:** The Savant app showed music playing, Savant routed it correctly, and no room made a sound.
Apple TV audio played fine in the same rooms.

**What it was:** The Savant media server's AVB media clock was stuck.

**How it ended:** A power cycle of the media server fixed it, with no changes to the audio system or the project.

---

More of the integration work: [Savant integrations](savant.md).
