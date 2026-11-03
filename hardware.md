# Hardware

The physical side: boards we flash and wire, signal paths we untangle, racks, and the 3D printing that turned
into an app.

## Garage door controller boards

**Problem:** LiftMaster and Chamberlain openers lock you into their cloud and give a control system no local way in.

**Built:** A ratgdo board on each opener (an ESP8266 board on ratgdo's open-source design), flashed with an ESPHome
config per door and wired in at the opener. A Savant profile on top makes each door native in Savant.

**Result:** Local open, close, light and lockout with real door and obstruction status, and no cloud anywhere in
the path. The Savant side is in [Savant integrations](savant.md#garage-doors-through-ratgdo).

## Signal paths

- **An audio loop that wasn't wiring.** A receiver feeding a video matrix that fed audio back to it made Blueprint
  route rooms into each other. Fixed in the design with no hardware change:
  [Breaking a receiver audio loop](savant.md#breaking-a-receiver-audio-loop).
- **Audio extractors that Blueprint understands.** A routing-only profile for the OREI BKA-1 8K HDMI audio
  extractor, so Blueprint knows which outputs carry what. Built, not in a project yet.
- **Racks built to be serviced.** Clean racks, cabling labeled at both ends, documented settings and remote
  monitoring, so a future fix is a quick visit.

## 3D printing

We print on a Creality K2 Plus and Bambu Lab machines, and years of chasing first layers and stringing are what
[Printer Studio](https://apps.apple.com/us/app/printer-studio/id6779811553) is built on: starting settings for
78 printers from 23 brands, 12 slicers and filament from more than 50 brands, on iPhone and iPad.

---

support@sparkyventurelabs.com · [sparkyventurelabs.com](https://sparkyventurelabs.com)
