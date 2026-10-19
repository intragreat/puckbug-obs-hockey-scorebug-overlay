# OBS setup

Once per computer, about 10 minutes. The same on Windows and Mac. Start PuckBug first (start.bat / start.command, or practice mode) so you can see the scorebug while you set up.

## 1. Video settings

**Settings → Video:**
- **Base (Canvas) Resolution:** 1920×1080.
- **Common FPS Values: 60.** At 30 fps the ticker and animations stutter in OBS, even though they look smooth in a browser.

(The panel's OBS section has a **Smooth graphics: 60 fps** button that sets this for you once OBS remote control is on, step 4.)

## 2. Add the scorebug

In the scene you stream from (for example *ScoreBug (B)*): **+ → Browser**, name it `PuckBug`.

| Setting | Value |
|---|---|
| URL | `http://127.0.0.1:8770/overlay` |
| Width × Height | `1920` × `1080` |
| Custom frame rate | on, `60` |
| Shutdown source when not visible | **off** |
| Refresh browser when scene becomes active | **off** |
| Control audio via OBS | **on** if your sponsors' ads include video with sound (the ad's audio then shows in the Audio Mixer as PuckBug, to set its level) |

Keep it at position 0,0, unscaled, above your camera. The scorebug sits top-left; banners, penalties and the goal bug appear to its right; lineups, scores and the ticker along the bottom; cards fill the screen; ads play full screen, as a lower third or in the corner; the "powered by" watermark sits top-right. Add the same source to other scenes with **Paste (Reference)**, not a second copy.

The overlay reloads itself after PuckBug is updated or restarted. If it ever looks different from the panel's preview: right-click the source → **Refresh**.

## 3. The operator panel inside OBS (optional)

**Docks → Custom Browser Docks…** → name `PuckBug`, URL `http://127.0.0.1:8770/panel` → **Apply**. The panel works just as well in any browser on this computer, or on a tablet on the same network if you change `bindAddress` in `config/settings.json`.

## 4. Let PuckBug control OBS (goal light, instant replay)

1. In OBS: **Tools → WebSocket Server Settings** → tick **Enable WebSocket server**, port **4455**. Tick **Enable Authentication**, click **Show Connect Info**, and copy the password.
2. In the PuckBug panel: **Replays tab → OBS** → paste the password → **Connect**. It reconnects by itself from then on.

With remote control on:
- **Goal light:** on your team's goals, the *Goal GIF (G)* source in the *ScoreBug (B)* scene turns on for 8 seconds. **Fit goal light over scorebug** sizes it to sit exactly over the scorebug; **Test goal light** tries it.
- **Replay buffer:** starts by itself when you start streaming. In **Settings → Output**, tick **Enable Replay Buffer** and set **Maximum Replay Time** to 30–45 s.
- **Instant replay:** Ctrl+R saves the last seconds. Ctrl+Shift+R plays the newest clip in the *Replay (R)* scene through the *Instant Replay (I)* media source, then cuts back to *ScoreBug (B)*. Clips are filed by date under **Videos/Replays** (change it in `config/settings.json`).

Scene and source names are in `config/settings.json` (`obs.goalLight`, `replays`) if yours are named differently. Intermissions and other scene changes stay yours.

**Smooth replays (stream glitches when saving or playing one):**
- **Settings → Output:** in Simple mode set **Recording Quality** to **Same as stream**, so the replay buffer reuses the stream's encoding instead of running a second encoder.
- *Instant Replay (I)* media source: tick **Use hardware decoding when available**.
- Keep the replays folder on the same drive as OBS's recording path (the default: both under Videos), so filing a clip is a rename, not a copy.
- The panel docked in OBS: its replay library loads a clip only while you hover over it, and not at all while a replay is on air. Opening the panel in a separate browser window takes its work off OBS altogether.

## 5. Hotkeys

PuckBug's hotkeys work while OBS has focus (see the [broadcaster guide](docs/BROADCASTER-GUIDE.md#hotkeys)). In **OBS → Settings → Hotkeys**, remove any OBS hotkey that uses the same keys (Ctrl+H, Ctrl+A, Ctrl+P…), so both don't fire.

- **Windows:** if OBS runs **as administrator**, run start.bat as administrator too, or the hotkeys won't reach PuckBug while OBS has focus.
- **Mac:** allow Terminal under **System Settings → Privacy & Security → Accessibility** (and **Input Monitoring** if it's listed), then restart PuckBug.

## 6. Check it

With PuckBug in practice mode: press **Ctrl+H** (a home goal and the goal bug), **Ctrl+Shift+H** (take it back), and air a card from the panel (On air → Graphics → Air). Then **New game** in the panel, close practice mode, and start PuckBug normally on game day.
