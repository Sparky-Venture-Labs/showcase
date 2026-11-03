# Mac work

Savant's older Pro Hosts are Macs, and my bench is a Mac, so a good share of this work is macOS.

## On Savant's Mac hosts

- **Helpers that behave like part of the system.** The integrations that need a helper (doorbell ring and
  talk-back, Access doors, camera serving, JellyFish, TV power) run as launchd services on the host. Each one has
  tests, and a watchdog where a missed event would matter.
- **Restarts that don't take the house down.** Savant gets restarted cleanly on a live system instead of rebooting
  the host and hoping.
- **Nothing extra unless it has to be.** A new process on a client's host is the last option, after everything
  inside Savant has been tried.

## Tools on the bench

- **Blueprint project reader.** Reads a saved Blueprint project and reports how audio and video actually route,
  which services Blueprint duplicated and where each one's audio ends up, what a component is wired to, any route
  that loops back on itself, and what a workflow does. No need to open Blueprint to answer "why did that room
  switch?"
- **Profile generators.** Component Profiles are built from code, so a change gets reviewed and tested like code
  instead of hand-edited.
- **Samsung pairing tool.** Gets a Samsung TV's IP control token when Savant's discovery can't see the TV.
- **AquaLink label reader.** Pulls pool and spa circuit names from iAqualink and checks a Savant project against
  them.
- **Leak checks before anything goes public.** Client details stay in encrypted storage, and every public page
  passes a scanner before it's pushed.

## Public Mac repos

| Repo | What it is |
|---|---|
| [mac-automations](https://github.com/Sparky-Venture-Labs/mac-automations) | Two launchd + fswatch background jobs: unzip downloads with safety checks, and file screenshots and screen recordings by year and month |
| [dot-files](https://github.com/Sparky-Venture-Labs/dot-files) | My Apple Silicon setup: zsh config, Brewfile, git config and macOS defaults |
| [ios-build-scripts](https://github.com/Sparky-Venture-Labs/ios-build-scripts) | Build and run on a simulator by UDID, flatten App Store icons, and the XcodeGen keys that fix the tiny-window launch |

---

support@sparkyventurelabs.com · [sparkyventurelabs.com](https://sparkyventurelabs.com)
