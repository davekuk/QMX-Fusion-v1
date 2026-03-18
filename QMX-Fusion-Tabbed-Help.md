# QMX Fusion — Tabbed Interface
### Advanced Web-Based Control Interface for the QRP-Labs QMX Transceiver
*by DJ0CU / G4ADF*

---

## Table of Contents

1. [Overview](#overview)
2. [Browser Requirements](#browser-requirements)
3. [Getting Started](#getting-started)
4. [Tab Layout](#tab-layout)
   - [📻 Radio Tab](#-radio-tab)
   - [🎧 Audio & DSP Tab](#-audio--dsp-tab)
   - [🔑 CW & Voice Tab](#-cw--voice-tab)
   - [📋 Log & Memory Tab](#-log--memory-tab)
   - [⚙️ Settings Tab](#️-settings-tab)
5. [Panel System](#panel-system)
6. [Frequency Control](#frequency-control)
7. [Audio Streaming](#audio-streaming)
8. [Spectrum & Waterfall Display](#spectrum--waterfall-display)
9. [DSP Filters](#dsp-filters)
10. [CW Keyer](#cw-keyer)
11. [Voice Keyer](#voice-keyer)
12. [CW Decoder](#cw-decoder)
13. [QSO Logger](#qso-logger)
14. [Memory Channels](#memory-channels)
15. [S-Meter & SWR](#s-meter--swr)
16. [RIT Control](#rit-control)
17. [Audio Recorder](#audio-recorder)
18. [Solar Conditions](#solar-conditions)
19. [Theme Customisation](#theme-customisation)
20. [Zoom & Display Controls](#zoom--display-controls)
21. [Keyboard Shortcuts](#keyboard-shortcuts)
22. [localStorage & Data Persistence](#localstorage--data-persistence)
23. [Troubleshooting](#troubleshooting)

---

## Overview

QMX Fusion is a fully self-contained single HTML file that provides a rich graphical control interface for the QRP-Labs QMX transceiver via the browser's **Web Serial API**. No installation, server, or internet connection is required once the file is downloaded (other than the Solar Conditions image, which is fetched from HamQSL.com).

**Key capabilities:**

- CAT control over USB serial at 115200 baud
- Real-time audio streaming (receive and transmit)
- Spectrum analyser and waterfall display
- DSP filters for SSB and CW
- Auto-notch filter
- CW keyer with 8 memory slots (iambic bug / straight key modes)
- Voice keyer with 8 recorded message slots
- CW decoder
- QSO logger with ADIF export/import
- 10-channel frequency memory
- Analogue S-Meter and SWR meter
- RIT (Receiver Incremental Tuning)
- Audio recorder
- Solar propagation conditions display
- Fully customisable colour theme
- Draggable, rearrangeable panels — including cross-tab drag

---

## Browser Requirements

| Browser | Support |
|---|---|
| **Google Chrome** | ✅ Full support (recommended) |
| **Microsoft Edge** | ✅ Full support |
| **Opera** | ✅ Full support |
| **Firefox** | ❌ Web Serial API not supported |
| **Safari** | ❌ Web Serial API not supported |

The interface uses the **Web Serial API** for CAT control and the **Web Audio API** for audio streaming. Both require a Chromium-based browser. For best results use the most recent version of Chrome, Edge, or Opera.

---

## Getting Started

1. Connect the QMX to your PC via USB.
2. Open `QMX-Fusion-Tabbed.html` in Chrome or Edge.
3. On the **📻 Radio** tab, check the baud rate is set to **115200**.
4. Click **Connect** — the browser will show a serial port picker. Select the QMX port.
5. Once connected the LCD display will show the current frequency and mode.
6. Click **Start** in the Audio Stream panel (🎧 Audio & DSP tab) and select your QMX audio device to enable receive audio.

> **Tip:** The status indicator at the bottom of the centre column shows **CONNECTED** in the accent colour when the serial link is active.

---

## Tab Layout

The interface is divided into five tabs. Click any tab to switch to it. Panels can be freely dragged between columns and between tabs (see [Panel System](#panel-system)).

### 📻 Radio Tab

The primary operating tab — open here for normal use.

| Column | Panels |
|---|---|
| Left | Serial Connection, Tuning Step & Autotune, Mode, Band |
| Centre | LCD Frequency Display, Main Tuning Knob, VFO & Transmit, Status Bar |
| Right | Quick Controls, Controls (AF Gain / CW Speed / RF Gain knobs, Power meter) |

**Serial Connection** — baud rate selector and Connect/Disconnect button.

**Tuning Step & Autotune** — sets the step size for the main tuning knob (1 Hz – 10 kHz). The **AUTOTUNE CW/SSB NOW** button performs an immediate signal-peak scan. The **AUTOTUNE** toggle enables continuous background autotune.

**Mode** — USB · LSB · CW · DIGI. Clicking a mode button sends the appropriate CAT command.

**Band** — 160m through 6m. Switching band recalls the last-used frequency for that band.

**Quick Controls** — compact panel showing S-Meter, SWR, TX/RX buttons, Volume / RF Gain / CW Speed knobs, and a Loudness slider. Useful when other panels have been moved to other tabs.

**Controls** — full-size AF Gain knob, CW Speed knob with Straight/Bug mode toggle, RF Gain knob, and a vertical power output meter.

---

### 🎧 Audio & DSP Tab

| Column | Panels |
|---|---|
| Left | Audio Stream, SSB Control |
| Centre | Spectrum & DSP |
| Right | S-Meter & SWR, RIT Control, Audio Recorder |

See individual sections below for full details on each panel.

---

### 🔑 CW & Voice Tab

| Column | Panels |
|---|---|
| Left | Voice Keyer |
| Centre | CW Keyer Memory |
| Right | CW Decoder |

---

### 📋 Log & Memory Tab

| Column | Panels |
|---|---|
| Left | CAT Log |
| Centre | QSO Logger |
| Right | Memory Channels |

---

### ⚙️ Settings Tab

| Column | Panels |
|---|---|
| Left | Theme Colors |
| Centre | Panel Visibility |
| Right | Solar Conditions |

---

## Panel System

Every panel in the interface can be **repositioned** by dragging it by its **title bar** (the `h3` heading at the top of the panel).

### Dragging within a tab

Grab any panel title and drag it up or down within its column, or left and right across the three columns on the same tab. The ghost preview shows where it will land. Release to drop.

### Dragging to a different tab

1. Start dragging a panel by its title bar.
2. While holding the drag, move the mouse over a **tab button** at the top.
3. After hovering for **~400 ms** the tab switches automatically, revealing the target columns.
4. Drop the panel into any column on the new tab.

The tab button glows brightly while you hover over it during a drag to indicate that it is about to switch.

### Panel lock

The **Panels Unlocked / Panels Locked** button in the centre column of the Radio tab toggles whether panels can be dragged. When locked, a 🔒 icon appears in every panel title bar and dragging is disabled. Use this to prevent accidental repositioning during an operating session.

### Saving and restoring layout

Panel positions are saved automatically to browser **localStorage** whenever a drag ends. The layout is restored on the next page load. The key used is `qmxTabbedPanelLayout` — separate from any previous non-tabbed layout saves.

### Panel Visibility

The **Panel Visibility** panel on the Settings tab contains a checkbox for every panel. Unchecking a panel hides it entirely. **Show All** / **Hide All** buttons are provided. Visibility state is saved to localStorage under `qmxPanelVisibility`.

---

## Frequency Control

### Main tuning knob

The large knob on the Radio tab centre column is the primary VFO control. Interact with it in three ways:

- **Mouse drag** — click and drag clockwise to increase frequency, anticlockwise to decrease.
- **Mouse wheel** — scroll up/down while hovering over the knob.
- **Keyboard** — hover the mouse over the knob, then use **Arrow keys** (Up/Right = increase, Down/Left = decrease). The step size set in the Tuning Step panel applies.

### Direct frequency entry

Click the **LCD display** to open the direct frequency entry keypad. Enter a frequency in MHz (e.g. `14.225`), kHz, or Hz using the format buttons, then press **Enter** or click **Set**. Press **Escape** or **Cancel** to close without changing frequency.

### VFO A / VFO B

The VFO panel provides **VFO A**, **VFO B**, **A↔B** (swap), and **A→B** (copy A to B) buttons, plus TX and RX buttons.

### Band memory

When you switch bands, the last-used frequency for the previous band is saved. Switching back restores it automatically (saved to `qmxLastFrequencies` in localStorage).

---

## Audio Streaming

The **Audio Stream** panel (🎧 Audio & DSP tab, left column) handles receive and transmit audio routing.

1. **Input** — select the QMX audio input device (the USB sound card presented by the QMX).
2. **Output** — select your PC speakers or headphones.
3. Click **Start** to begin streaming. Click **Stop** to end it.
4. **Refresh** rescans available audio devices.

**Audio Gain** — a slider (10–800 range, 1.0× = 100) that boosts or attenuates the received audio before it reaches your speakers.

**Input Level meter** — shows the incoming signal level in dB with a peak indicator. A **CLIPPING DETECTED** warning banner appears if the input is overloading; reduce the Audio Gain or the QMX AF output to resolve.

> The Audio Stream must be running for the Spectrum display, autotune, CW decoder, and Audio Recorder to function.

---

## Spectrum & Waterfall Display

The **Spectrum & DSP** panel (centre column of the Audio & DSP tab) contains a canvas-based real-time spectrum analyser and waterfall.

**Spectrum Mode:**
- **Audio (3.2 kHz)** — displays the audio passband. Best for monitoring SSB and CW signals.
- **I/Q Waterfall (48 kHz)** — full-bandwidth IQ waterfall when using an IQ source.

**Controls:**
| Control | Description |
|---|---|
| Threshold | Signal detection threshold for autotune peak-finding (5–50) |
| Show Noise Floor | Overlays the estimated noise floor on the spectrum |
| Calibrate Noisefloor | Takes a snapshot of the current noise and sets it as the reference |
| Target CW Pitch | Expected CW tone frequency (600 / 700 / 800 Hz) used by autotune and CW decoder |
| Attenuation | Input attenuator (0 to −30 dB) to prevent clipping on strong signals |

---

## DSP Filters

### SSB Filter

Enable **SSB DSP** with the checkbox in the Spectrum & DSP panel. Two sliders set the low and high cutoff frequencies of a bandpass filter applied to the received audio.

| Preset | Low | High |
|---|---|---|
| Narrow | 100 Hz | 2500 Hz |
| Normal | 300 Hz | 2700 Hz |
| Wide | 200 Hz | 3000 Hz |
| Voice | 400 Hz | 2400 Hz |

The current bandwidth is shown below the sliders.

### CW DSP Filter

A dedicated CW bandpass filter, selectable from 50 Hz to 300 Hz (native). Enable with the **ON** checkbox. Works in conjunction with the Target CW Pitch setting.

### Auto-Notch Filter (ANF)

Automatically detects and notches out steady carriers (heterodynes) within the passband. Enable with the **Enable ANF** checkbox.

| Control | Description |
|---|---|
| Notch Depth | How deeply the carrier is attenuated (20–80 dB) |
| Notch Width | Width of the notch in Hz (10–200 Hz) |

Detected notch frequencies are displayed below the controls.

---

## CW Keyer

The **CW Keyer Memory** panel (🔑 CW & Voice tab, centre column) provides an 8-message memory keyer.

### Keyer mode

The **STRAIGHT / BUG** toggle selects between:
- **STRAIGHT** — straight key / single-lever paddle mode.
- **BUG** — iambic bug mode (alternating dits and dahs on squeeze).

The mode toggle appears both in the Controls panel (Radio tab) and the CW Keyer panel.

### CW Speed

The **CW Speed knob** sets the sending speed in WPM (words per minute). Range is approximately 5–40 WPM. The same knob appears in the Controls panel and the CW Keyer panel — both are synchronised.

### Message memory slots

Eight memory slots (CW1–CW8) each hold up to 80 characters. Messages are stored in upper case.

**To store a message:**
1. Click a slot button (CW1–CW8) to select it.
2. Type the message text in the **Message Text** field.
3. Click **STORE**.

**To send a message:**
1. Select the slot.
2. Click **SEND** — the QMX will immediately begin transmitting.

**To edit a stored message:**
1. Select the slot.
2. Click **EDIT** — a modal dialog opens with the label and text fields.
3. Edit and click **Save**.

**CLEAR** erases the current slot. **CLEAR ALL** erases all eight slots after confirmation.

### Keyboard shortcuts — CW

| Key | Action |
|---|---|
| **F1 – F8** | Select and immediately send CW slot 1–8 |

### Export / Import

CW messages can be backed up and restored as a JSON file using the **EXPORT** and **IMPORT** buttons. This allows sharing message sets between computers or browsers.

---

## Voice Keyer

The **Voice Keyer** panel (🔑 CW & Voice tab, left column) records and plays back voice messages for phone operating.

### Recording a message

1. Select a slot (MSG 1–MSG 8).
2. Click **RECORD** — the interface switches to PTT and begins recording from your microphone.
3. Speak your message.
4. Click **STOP** when finished.

### Playing a message

1. Select the slot containing the recording.
2. Click **PLAY** — with **Auto TX/RX** checked, the interface will key the transmitter before playback and return to receive afterwards.

**CLEAR** removes the recording from the current slot. **CLEAR ALL** removes all recordings.

### Keyboard shortcuts — Voice

| Key | Action |
|---|---|
| **Shift + F1 – Shift + F8** | Select and immediately play Voice slot 1–8 |

### Export / Import

Voice message metadata is saved to localStorage automatically. Use **EXPORT** to save to a JSON file and **IMPORT** to restore.

---

## CW Decoder

The **CW Decoder** panel (🔑 CW & Voice tab, right column) automatically decodes incoming CW from the audio stream.

| Control | Description |
|---|---|
| Enable Auto-Polling | Starts the decoder; audio streaming must be active |
| Poll Interval | How often the decoder samples the audio (100–1000 ms) |
| Clear Buffer | Clears the decoded text display |

Decoded text appears in the display area and scrolls automatically. The timestamp of the last decoded character is shown below.

> For best results, enable the CW DSP filter and set the Target CW Pitch to match the incoming signal, and tune so the CW note sits on the target pitch.

---

## QSO Logger

The **QSO Logger** panel (📋 Log & Memory tab, centre column) provides a basic logbook.

### Logging a contact

Fill in the fields and click **Log QSO**:

| Field | Notes |
|---|---|
| Callsign | Automatically converted to upper case |
| RST Sent | Defaults to 599 |
| RST Rcvd | Defaults to 599 |
| Name | |
| QTH | |
| Comments | |

The frequency and mode are filled automatically from the current VFO. Time is logged in UTC.

### Search and filter

Type in the **Search Callsign** box to filter the log display in real time.

### Export / Import (ADIF)

Click **Export** to download the log as an ADIF `.adi` file compatible with most logging programs. Click **Import** to load an existing ADIF file into the log (appends to any existing entries).

**Clear Log** removes all entries after confirmation.

The log is saved to localStorage under `qmxQsoLog` and persists between sessions.

---

## Memory Channels

The **Memory** panel (📋 Log & Memory tab, right column) provides 10 frequency memory slots (M1–M10).

| Button | Action |
|---|---|
| Store | Save the current frequency, mode, and band to the selected slot |
| Recall | Tune to the frequency saved in the selected slot |
| Edit | Open a dialog to manually set frequency, mode, band, and label |
| Clear | Erase the selected slot |
| Export | Save all memories to a JSON file |
| Import | Restore memories from a JSON file |
| Clear All | Erase all ten slots |

Occupied slots are shown with the frequency and label. The currently selected slot is highlighted. Memories are saved to localStorage under `qmxMemoryChannels`.

---

## S-Meter & SWR

The **S-Meter & SWR** panel (🎧 Audio & DSP tab, right column) displays two analogue-style arc meters.

- **S-Meter** — receive signal strength from S1 to S9.
- **SWR** — standing wave ratio from 1.0 to 3.0, derived from the QMX power and SWR reporting.

Numerical readouts appear below each meter. The S-Meter value is also shown in the Quick Controls panel on the Radio tab.

---

## RIT Control

The **RIT** panel (🎧 Audio & DSP tab, right column) provides Receiver Incremental Tuning — shifting the receive frequency without moving the transmit frequency.

| Control | Action |
|---|---|
| RIT ON/OFF | Enables or disables RIT |
| CLEAR | Resets the RIT offset to zero |
| −100 / −10 / −1 / +1 / +10 / +100 | Adjust the RIT offset in Hz steps |

The current RIT status and offset value are shown at the top of the panel.

---

## Audio Recorder

The **Audio Recorder** panel (🎧 Audio & DSP tab, right column) records audio from the QMX to your PC.

| Control | Description |
|---|---|
| Recording Source | RX only, TX only, or RX & TX mixed |
| RECORD | Start recording |
| Set Directory | Choose where recordings are saved (uses File System Access API — Chrome/Edge only) |

Recording status and the current save path are shown in the panel. Audio streaming must be active to record receive audio.

---

## Solar Conditions

The **Solar Conditions** panel (⚙️ Settings tab, right column) shows the current HF propagation conditions image from [HamQSL.com](https://www.hamqsl.com).

| Control | Action |
|---|---|
| Image Size slider | Scales the image (100%–300%) |
| 🔄 Refresh | Reloads the image from HamQSL.com |
| 🎯 Reset View | Scrolls back to the top-left corner |
| ✋ Drag: ON/OFF | Toggles click-and-drag panning of the image |
| 🔗 Full | Opens the full HamQSL solar page in a new tab |

The image container is scrollable. You can also use the mouse wheel to scroll vertically, and the image size slider to zoom.

> **Note:** An internet connection is required to load the solar image. The rest of the interface works entirely offline.

---

## Theme Customisation

The **Theme Colors** panel (⚙️ Settings tab, left column) controls the visual appearance of the entire interface.

| Control | Description |
|---|---|
| Accent Color | The primary highlight colour used for active elements, meters, and labels. Default: `#00ff88` (green). |
| Panel Background | Base colour of panel backgrounds. Default: `#000000`. |
| Panel Opacity | Transparency of panels (0%–100%). Default: 20%. |
| Preview Text | Live preview of the chosen accent colour. |
| Reset Defaults | Returns all three values to their defaults. |

Colour choices are saved to localStorage (`qmx_theme_color`, `qmx_panel_bg_color`, `qmx_panel_opacity`) and applied immediately across the whole interface.

---

## Zoom & Display Controls

A row of zoom controls appears in the left column of the Radio tab:

| Button | Action |
|---|---|
| **−** | Zoom out (minimum 50%) |
| **+** | Zoom in (maximum 200%) |
| **Reset** | Return to 100% |
| **Fit** | Scale the interface to fit the browser window |
| **⛶** | Toggle fullscreen (also **F11**) |
| **⚙** | Toggle the Panel Settings (Panel Visibility) panel |

---

## Keyboard Shortcuts

| Key | Action |
|---|---|
| **F1 – F8** | Send CW memory slot 1–8 immediately |
| **Shift + F1 – F8** | Play Voice Keyer slot 1–8 immediately |
| **F11** | Toggle fullscreen |
| **Arrow keys** (with mouse over tuning knob) | Tune up/down by the current step size |
| **Enter** (in frequency entry) | Confirm frequency |
| **Escape** (in frequency entry) | Cancel without changing frequency |

---

## localStorage & Data Persistence

All user data and settings are stored in the browser's localStorage. No data is sent to any server.

| Key | Contents |
|---|---|
| `qmxTabbedPanelLayout` | Panel positions across all tabs and columns |
| `qmxPanelVisibility` | Which panels are shown or hidden |
| `qmxMemoryChannels` | Frequency memory channel contents |
| `qmxLastFrequencies` | Last-used frequency per band |
| `qmxQsoLog` | QSO log entries |
| `qmxCWMessages` | CW keyer message texts and labels |
| `qmxVoiceMessages` | Voice keyer message metadata |
| `qmxVoiceAutoTx` | Voice keyer Auto TX/RX state |
| `qmxStepSize` | Last-used tuning step |
| `qmx_theme_color` | Accent colour |
| `qmx_panel_bg_color` | Panel background colour |
| `qmx_panel_opacity` | Panel opacity |

> **Note:** localStorage is per-browser and per-origin. If you open the file from a different path or a different browser, a fresh default layout will be used.

---

## Troubleshooting

**The Connect button does nothing / no ports appear**
- Ensure you are using Chrome or Edge (Firefox and Safari do not support Web Serial).
- Check the QMX is powered on and connected via USB.
- On Linux, you may need to add your user to the `dialout` group: `sudo usermod -a -G dialout $USER` and log out/in.
- On Windows, check Device Manager to confirm the QMX appears as a COM port.

**Audio does not start / no device listed**
- Click **Refresh** in the Audio Stream panel.
- Make sure the QMX USB audio device is connected and recognised by the operating system.
- Grant microphone permission if the browser asks.

**Spectrum is blank after starting audio**
- Confirm the Audio Stream status shows **Streaming**.
- Try a different FFT size using the spectrum controls.
- Ensure the audio input device is the QMX, not the PC microphone.

**Panel layout looks wrong on first load**
- The `qmxTabbedPanelLayout` key in localStorage may contain a saved layout from a previous (non-tabbed) version. Open the browser developer tools (F12), go to **Application → localStorage**, find `qmxTabbedPanelLayout`, and delete it to reset to defaults.

**Drag between tabs is not working**
- Grab the panel by its **title bar text** (the `h3` heading), not the panel body.
- Drag the panel up towards the tab bar and hover over the destination tab button for approximately half a second — the button will glow to indicate it will switch.
- Once the tab switches, drop into any column.

**CW is not being sent**
- The radio must be **connected** via serial before CW can be transmitted.
- Check the keyer mode (Straight vs Bug) matches how your paddle is wired.
- Verify the QMX firmware supports CAT-driven CW (check QRP-Labs documentation for your firmware version).

**SWR meter reads 1.0 always**
- The QMX reports SWR only when transmitting. Trigger a short TX to see a reading.

---

*QMX Fusion Tabbed Interface — DJ0CU / G4ADF*
*Interface file: `QMX-Fusion-Tabbed.html`*
