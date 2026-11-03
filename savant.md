# Savant integrations

Savant ships profiles for a lot of gear, but not all of it, and some of what it ships doesn't behave the way a
homeowner expects. These are the integrations we built to close that gap. Unless a note says otherwise, every one
below is running on a live Savant system.

Most of them are a custom Component Profile, the driver Savant loads for a device. A few also need a small helper
on the Savant host, for devices that talk in a way a profile can't. We only add one of those when nothing inside
Savant can do the job.

The profiles carry Sparky Venture Labs as the manufacturer. They aren't published here.

## Contents

- **Entry, cameras and access:** [UniFi doorbells as door stations](#unifi-doorbells-as-door-stations) ·
  [UniFi Access doors and gates](#unifi-access-doors-and-gates) · [UniFi Protect cameras, live](#unifi-protect-cameras-live) ·
  [Garage doors through ratgdo](#garage-doors-through-ratgdo)
- **Lighting, fans and lifts:** [JellyFish permanent lighting](#jellyfish-permanent-lighting) ·
  [Q-SYS lighting](#q-sys-lighting) · [Big Ass Fans i6](#big-ass-fans-i6) · [Bond TV lift](#bond-tv-lift)
- **TVs, video and audio:** [Sony BRAVIA fast power-on](#sony-bravia-fast-power-on) ·
  [Samsung TV power and tokens](#samsung-tv-power-and-tokens) · [NovaStar LED walls](#novastar-led-walls) ·
  [Theory DLC-250.8 amplifier](#theory-dlc-2508-amplifier) · [Breaking a receiver audio loop](#breaking-a-receiver-audio-loop)
- **Power and outdoor:** [Jandy AquaLink pool and spa](#jandy-aqualink-pool-and-spa) ·
  [UniFi PDU Pro outlets](#unifi-pdu-pro-outlets)
- [Also](#also) · [How we build them](#how-we-build-them)

---

## Entry, cameras and access

### UniFi doorbells as door stations

**Problem:** To Savant, a UniFi Protect doorbell is a camera at best. No ring on the phones, no house chime, no
talking to whoever is at the door.

**Built:** A door-station profile for the G4 Doorbell and a helper on the Savant host that handles the ring and the
audio. The UniFi Access readers with cameras (UA G2 Pro, G6 Pro Entry) are set up as door stations the same
way.

**Result:** A press chimes the rooms you pick and rings every phone with the Savant app, even with the app closed.
The Entry screen shows the door live, Tap to Talk is two-way, and the doorbell's package camera is its own camera
in Savant.

### UniFi Access doors and gates

**Problem:** There was no clean way to open a UniFi Access door or a Gate Hub gate from Savant, or to see whether it
was actually locked.

**Built:** A UniFi Access door profile, one per door or gate, plus door-station profiles for the Access readers.

**Result:** A buzz-open from touch panels and the app that Access relocks on its own, and a lock tile that shows
the real state. The readers show their camera in Savant and are set up to ring the app and buzz their own door.

### UniFi Protect cameras, live

**Problem:** Doorbells, package cameras, the G6 Pro Entry, the G6 Pro 360 fisheye and the Access readers don't hand
Savant video it can play. They showed black, or stills at best.

**Built:** A profile for each camera type, and the piece on the Savant host that serves them to Savant.

**Result:** Live video and stills in the Savant app and on the Entry screen, and package cameras that start right
away instead of spinning.

### Garage doors through ratgdo

**Problem:** LiftMaster and Chamberlain openers want their cloud. Savant needs local control and a door status it
can trust.

**Built:** A ratgdo board on each opener running ESPHome firmware, and a profile that makes each one a native
Savant garage door. No cloud, and nothing running on the host.

**Result:** Open, close, opener light and remote lockout from Savant, with obstruction and real door status.
Getting the status right was the hard part.

---

## Lighting, fans and lifts

### JellyFish permanent lighting

**Problem:** JellyFish controllers have no Savant profile, and their local API isn't something a profile can talk
to on its own.

**Built:** A profile and a small bridge on the Savant host, with the controllers kept on their own isolated network.

**Result:** Each controller is a Savant light with on/off, brightness and live feedback, plus an "all" light and
buttons for saved patterns like warm white and the holidays. Changes made in the JellyFish app show up in Savant
within about three seconds.

### Q-SYS lighting

**Problem:** Some of the lights (DMX LED bars, DMX playbacks, switched plugs) were run by a QSC Q-SYS Core. Savant
has no Q-SYS profile, and the Core's published controls don't report whether anything is on.

**Built:** One profile that puts the Core's lights on Savant's lighting screens.

**Result:** Presets, toggles and all on/off, with buttons that show the right state.

### Big Ass Fans i6

**Problem:** i6 ceiling fans have no Savant profile and only speak their own protocol.

**Built:** A profile that talks to each fan directly. Nothing running on the host.

**Result:** Savant's native fan control (off, low, medium, high), a slider for all seven speeds, plus auto, reverse
and whoosh. Power and speed update live, even when someone uses the BAF app or the wall control.

### Bond TV lift

**Problem:** A TV lift learned on a Bond Bridge Pro as a generic device. Savant's own Bond profile has no way to
send a generic device's commands from the room's controls.

**Built:** A small profile for any Bond generic device that has up, down and stop.

**Result:** The lift sits in the room's shade controls as Up, Down and Stop.

---

## TVs, video and audio

### Sony BRAVIA fast power-on

**Problem:** Sony TVs took around 17 seconds to turn on from Savant, read their volume wrong, and some ignored
remote buttons outright.

**Built:** Modified versions of Savant's own Sony BRAVIA profiles for the XR70, XR90 and X90L lines.

**Result:** Power-on in about 2.5 seconds, the right volume, and a TV someone switched off with its own remote
comes back on at the next source pick.

### Samsung TV power and tokens

**Problem:** Samsung's IP control needs a pairing token, and Savant's discovery couldn't see some TVs to get one.
On top of that, Savant's record of a Samsung's power state can go stale and lock itself in, so the TVs look
offline until the whole system reboots.

**Built:** A tool that gets the token without discovery, and a small service on the host that keeps Savant's power
state honest.

**Result:** Tokens for the TVs discovery missed, and TVs that turn on from Savant without a system reboot.

### NovaStar LED walls

**Problem:** Savant's own profile for the NovaStar COEX MX40 Pro did nothing useful on these LED wall controllers:
power did nothing, and every input picked the same source.

**Built:** A profile that makes the wall the room's display and talks to the controller's own API. Nothing running
on the host.

**Result:** Power (picture or black), input and brightness from Savant, with power feedback.

### Theory DLC-250.8 amplifier

**Problem:** Savant has no profile for Theory Audio Design's 8-zone DLC-250.8, and the profile for its smaller
sibling doesn't fit.

**Built:** A profile that runs each zone on its own or in groups.

**Result:** Volume slider, up/down, mute and power from Savant, with live level feedback from the amp.

### Breaking a receiver audio loop

**Problem:** A receiver's HDMI output fed the video matrix while the matrix's audio fed the receiver. Blueprint
routed around that loop in strange ways: extra service variants, one room's source switching another room's
receiver, even a doorbell press flipping a receiver's input.

**Built:** A fix in the Blueprint design itself, using a custom part. No hardware change and nothing running.

**Result:** Clean services, and rooms that stop stepping on each other.

---

## Power and outdoor

### Jandy AquaLink pool and spa

**Problem:** The pool company relabeled the pool and spa controllers, and Savant's pool screens had to match them
exactly, names and order both. Later, a SavantOS update knocked pool and spa control out.

**Built:** A reader that pulls the circuit names from iAqualink and a checker that compares them with the Savant
project.

**Result:** Savant's pool and spa screens match the controllers name for name and in the same order, a live press
on each controller proved the mapping, and control came back after the update.

### UniFi PDU Pro outlets

**Problem:** When gear hangs, somebody has to power cycle it. Doing that at the rack is a truck roll, and a bare
power button in a homeowner's hands invites trouble.

**Built:** A profile that reads each outlet on a UniFi PDU Pro and restarts one on request, from a custom screen in
the Savant app.

**Result:** Each outlet shows on/off, volts and watts, and a Restart button that locks itself out for 10 to 12
minutes afterward, so nobody can bounce a device over and over.

---

## Also

- **Apple TV over HomeKit:** Apple TVs controlled over IP with no IR emitters, using Savant's own HomeKit profile.
- **OREI BKA-1 audio extractor:** a routing-only profile so Blueprint knows what the box passes. Built, not in a
  project yet.

## How we build them

- Most profiles are generated from code and tested before they go near a house. Most of the hand-written ones
  have tests too.
- A helper on the host only when nothing inside Savant can do the job.
- Changes go into a house from its latest saved project, and get proved on the real equipment before we call them
  done.

---

Want one of these in your system? support@sparkyventurelabs.com · [sparkyventurelabs.com](https://sparkyventurelabs.com)
