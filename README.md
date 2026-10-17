# StreamScan

**Scan your PC and get the exact settings to stream with.**

StreamScan checks your hardware, Windows settings, audio and internet connection, then tells you the best resolution, bitrate and encoder for your stream. It writes them out for your platform and streaming software, so you can copy them straight in.

It only **reads** your system. It never changes a setting on its own.

**[⬇ Download StreamScan-Setup.exe](https://github.com/AntiLegend93/streamscan-updates/raw/main/StreamScan-Setup.exe)**  ·  Current version: see [`version.txt`](version.txt)

---

## Features

- **One-click scan:** CPU, graphics card, driver age, memory, display, capture cards, microphones and speakers.
- **Readiness score:** a 0–100 score with your recommended stream, for example **1080p60 · 6000 Kbps · NVIDIA NVENC**.
- **Platforms:** Twitch, YouTube (up to 1440p), Kick and Facebook Live. Each uses its own bitrate limits.
- **Streaming software:**
  - **OBS Studio:** settings laid out the way OBS shows them, plus **one-click profile export**. Import it in OBS with *Profile → Import* and you're done.
  - **Streamlabs Desktop** and **XSplit Broadcaster:** settings with their own menu paths and setting names.
  - **Other:** general setting names that work in any streaming app.
- **Connection tests:** an upload speed test plus a Twitch server ping test that finds your fastest server.
- **Live Monitor:** leave it open while you stream. It graphs CPU, GPU, encoder, memory and upload, and warns you before viewers notice problems.
- **Windows tweaks:** checks Game Mode, Game Bar recording, power plan, GPU scheduling, audio sample rates and more. Each check has a button that opens the right settings page.
- **Game tips:** advice for Valorant, Fortnite, CS2, Apex, Call of Duty, League, Minecraft, GTA and Just Chatting.
- **Dual-PC mode:** for streaming from a second PC with a capture card.
- **Reports:** save as a web page or text, or copy to the clipboard.
- **Dark and light themes** with seven accent colors.
- **Remembers your last scan** and shows what changed since then.
- **Updates itself:** new versions download and install automatically.

## Requirements

- Windows 10 or Windows 11
- Nothing else to install. StreamScan uses the PowerShell built into Windows.

## Install

1. Download **[StreamScan-Setup.exe](https://github.com/AntiLegend93/streamscan-updates/raw/main/StreamScan-Setup.exe)**.
2. Run it and click **Install**. No admin password is needed; it installs just for your user account.
3. Open StreamScan from the Start menu or your desktop, then click **Scan Now**.

> **"Windows protected your PC"?** That's Windows SmartScreen. It appears for apps that aren't code-signed. Click **More info → Run anyway**.

### Uninstall

Go to **Settings → Apps → Installed apps → StreamScan → Uninstall**. It asks whether to also delete your saved settings.

## Updates

StreamScan checks this repo for a newer version each time it starts. When one is available, it downloads in the background and a **Restart & update** banner appears. If you'd rather keep working, the update installs quietly when you close the app.

You can turn the startup check off, or check manually, in **Settings → Updates**.

## Privacy

- The only internet traffic StreamScan makes:
  - the update check (this repo)
  - the upload speed test (Cloudflare's speed test server)
  - the Twitch ping test (Twitch's own servers)
- No accounts, no tracking, no data sent anywhere.
- Your settings and last scan are saved only on your PC, in `%APPDATA%\StreamScan`. You can turn this off or clear it in Settings.

## FAQ

**Does it change my OBS or Windows settings?**
No. It shows you what to change, and the buttons open the right settings page. The OBS profile export creates a new profile that *you* import; your existing profiles stay untouched.

**Why is it recommending 720p when I have a good PC?**
Usually your upload speed is the limit. Twitch also caps bitrate at 6000 Kbps, and at that bitrate 720p60 often looks cleaner than 1080p60 in fast games. Check the **Network** page to see the bitrate math.

**My mic shows a warning about 44.1 kHz.**
Streaming apps run at 48 kHz. Mismatched rates can cause crackling or audio drift. Click **Open Sound settings**, open your mic's Properties → Advanced, and pick a 48000 Hz option.

**The XSplit menu names look slightly different.**
Menu names vary between XSplit versions. Match each setting to the closest name.

---

## For the developer: publishing a new version

This repo holds just two files that the app reads:

| File | What it is |
|---|---|
| `version.txt` | The latest version, e.g. `v1.0.1` (`v.1.0.1` also works) |
| `StreamScan-Setup.exe` | The installer for that version |

To release an update:

1. In `StreamScan.bat`, change `$AppVersion = '1.0.0'` to the new number (e.g. `'1.0.1'`).
2. Run `Build.bat`. It creates `dist\StreamScan-Setup.exe` and `dist\version.txt`.
3. Upload both files here to the **main** branch, replacing the old ones.

Everyone on an older version is updated the next time they open StreamScan. GitHub can take a few minutes to serve newly uploaded files.

The app's update address is set by `$UpdateBase` near the top of `StreamScan.bat`.
