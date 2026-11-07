[Dan_RNG_Autopilot_README.md](https://github.com/user-attachments/files/34521159/Dan_RNG_Autopilot_README.md)
<div align="center">

# 🎲 Dan RNG Autopilot

### Automated progression. Intelligent decisions. Built for long sessions.

**My Windows automation macro for the Roblox game *Dan RNG*.**

![Version](https://img.shields.io/badge/Version-R1.6-7657E8?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%2F%2011-0078D6?style=for-the-badge)
![Project](https://img.shields.io/badge/Project-Community%20tool-30363D?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Live%20testing%20recommended-E3A008?style=for-the-badge)

**[Features](#-features) · [Getting Started](#-getting-started) · [Configuration](#configuration) · [Troubleshooting](#-troubleshooting) · [FAQ](#-frequently-asked-questions)**

*Unofficial third-party project. Not affiliated with Roblox or the developers of Dan RNG.*

</div>

---

## 📖 Overview

I made **Dan RNG Autopilot** to automate the repetitive progression in Dan RNG. Instead of just clicking on a fixed timer, it tries to make decisions using what it can actually see in the game.

It handles rolling, upgrades, rebirths, Index Collection and longer sessions. I also added configurable goals, visual detection, session statistics, Discord notifications and recovery tools to make it more reliable.

My main goal is simple: **the macro should know what it is trying to do, verify important actions, and avoid making risky decisions when it cannot tell what is happening.**

> [!IMPORTANT]
> **Version note:** This README covers **R1.6**. Some features have been tested outside live Roblox sessions and still need more in-game testing. Features and UI options can differ between releases, so check the release notes for the version you download.

### At a glance

| Area | Capabilities |
| --- | --- |
| 🎲 Rolling | Automatic rolling and roll-state monitoring |
| 🔁 Rebirths | Rarity-based targets, automatic confirmation and session tracking |
| ⬆️ Upgrades | Speed-first purchasing, Luck progression and adaptive behaviour |
| 📚 Index | Multi-stage Index Collection workflow |
| 🎯 Goals | Hunter Mode, progression targets and gem-balance goals |
| 🧠 Detection | Visual UI checks, OCR safeguards and cutscene awareness |
| 🛠️ Reliability | Watchdogs, retries, recovery logic and diagnostics |
| 📊 Dashboard | Session information, progress indicators and event logs |
| 🔔 Notifications | Optional outgoing Discord webhook alerts |
| 🖥️ Windows | Primary-monitor targeting, resolution presets and optional dimming |

---

## 🖼️ Screenshots

I will add screenshots of the main dashboard, settings, the macro running and Discord notifications here. They will be stored in `docs/images/`.

<!-- Replace these comments when screenshots exist:
![Dashboard](docs/images/dashboard.png)
![Settings](docs/images/settings.png)
![Discord notifications](docs/images/discord-notifications.png)
-->

---

## ✨ Features

### 🎲 Automatic rolling

- Handles the repetitive rolling workflow during an active session.
- Monitors visible game-state indicators to check whether rolling appears to be progressing.
- Includes watchdog logic intended to detect stalled rolling and attempt recovery.
- Accounts for rolling behaviour that may show one, two or three rolls per cycle.
- Avoids treating every temporary UI disappearance as permission to click.

### 🔁 Automatic rebirths

- Works toward a **selected rebirth rarity/target** instead of rebirthing at arbitrary moments.
- Navigates relevant game menus, checks whether the rebirth conditions appear satisfied and performs the confirmation flow when appropriate.
- Tracks observed rebirths for the current macro session.
- Returns to the progression loop after a rebirth.
- Includes safeguards intended to avoid rebirthing when the required state cannot be confirmed.

**Important:** Rebirth eligibility is determined from information the macro can observe. It cannot guarantee that every game update, UI animation or OCR result will be interpreted correctly.

### ⬆️ Speed and Luck upgrade automation

The default upgrade strategy prioritises efficient progression:

1. Buy available **Speed** upgrades until Speed is maxed or blocked.
2. Purchase affordable **Luck** upgrades instead of repeatedly returning to Speed after it has become blocked.
3. Reassess upgrades when the game state or progression stage changes.
4. Respect configured goals or protected gem balances where applicable.

In R1.6, **Adaptive Farming is enabled by default**. It allows the macro to adjust its approach based on progression instead of doing exactly the same thing every cycle.

### 📚 Index Collection automation

For players working through Index Collection, the macro includes a staged workflow that progresses through the following limit sequence:

`1 → 50 → 1,000 → 50,000 → Unlimited`

The goal is to handle Index tasks before returning to normal farming, without requiring the user to manually revisit the menus at every stage. Game changes or recognition failures can interrupt the sequence; the live game UI remains the final source of truth.

### 🎯 Hunter Mode and goal-based farming

I added **Hunter Mode** for when you just want to roll for rare auras **without rebirthing**. It is useful for collecting or chasing rare rolls instead of focusing on rebirth progression.

Other goal-oriented options include:

- Choosing the rarity that should qualify for a rebirth.
- Tracking a desired gem balance or progression milestone.
- Protecting a gem target from avoidable spending, where that setting is enabled.
- Using optional **Smart Secret Farming**, designed to wait for a Secret-tier opportunity in suitable late-game conditions instead of always rebirthing immediately.

Smart Secret Farming is optional rather than mandatory. Its intended late-game use includes situations around **Luck level 800+**, after applicable Index work; actual behaviour depends on the game state and selected settings.

> [!NOTE]
> **Known R1.6 issue:** Hunter Mode can still open the **Rebirth** menu at startup or after Index Collection, even though actual rebirth actions are disabled. I plan to fix the unnecessary navigation in a later release.

### 👁️ Visual recognition and cutscene protection

Dan RNG can temporarily hide its regular interface during rare-roll animations. The macro includes cutscene-aware protection intended to:

- Recognise when normal game UI elements disappear.
- Suspend menu navigation while a rare-roll sequence appears to be playing.
- Wait for the expected interface to return before resuming interaction.
- Use rarity visuals as **supporting evidence**, not as the sole proof of a valuable roll.
- Reduce accidental clicks during large visual effects, flashes and transitional screens.

These checks are especially relevant to Secret, Forbidden and Omega-tier events. **Visual recognition is not infallible**, particularly with unusual avatars, game updates, overlays or intense effects.

### 🛠️ Recovery and reliability

I have added several reliability features to help with longer unattended sessions:

- Rolling-progress watchdogs.
- Retries and state rechecks after uncertain interactions.
- Recovery from common menu and rolling interruptions.
- Protection against duplicate macro instances.
- Session handling for Start, Stop, Pause and Resume.
- More conservative OCR handling for uncertain values.
- Diagnostic logging and screenshots for investigating failures.
- Anti-AFK behaviour that is **disabled while paused**.

The macro is built with unattended sessions in mind, but **I still recommend testing each new version before leaving it running for hours**.

### 📊 Live dashboard and diagnostics

The application includes a live status interface with information such as:

- Current macro state: running, paused, stopped or recovering.
- Session runtime and observed progress.
- Rebirth and gem information when recognised.
- Selected goal and rebirth target.
- Recent actions, warnings and errors.
- Diagnostic information useful when reporting bugs.

Statistics derived from OCR or incomplete event tracking may be estimates or unavailable. A missing value should not be interpreted as zero.

### 🔔 Optional Discord notifications

Configure a **Discord webhook** to receive outgoing notifications about relevant macro events. Depending on your version, alerts can include session starts, session summaries, settings changes, confirmed rare events and recovery messages.

Notifications are **one-way alerts only**. The macro is not a Discord bot and does not accept remote commands through Discord.

### 🌙 Optional screen dimming

An optional dimming feature is designed to reduce visual distraction across **all monitors**, targeting approximately **80% dimming** while active. It is an overlay-style convenience feature rather than a replacement for Windows display calibration. Test it locally and make sure you retain a way to restore your screens.

---

## 🚀 Getting started

### Requirements

- **Windows 10 or Windows 11**.
- The Windows version of **Roblox**, with Dan RNG running.
- A display configuration supported by the particular build; common presets include **1920×1080, 2560×1440 and 3840×2160**.
- Permission for the macro to view the screen and send mouse/keyboard inputs.
- For the **source package**: a compatible Python installation and any dependencies required by that release's setup instructions.
- For Discord alerts: a Discord webhook URL (optional).

> [!TIP]
> The macro was designed around Roblox running **fullscreen** and normally targets the **Windows primary monitor**. If your gaming display is labelled "Monitor 2" in Windows but marked as the primary display, that is fine.

### Download and install

1. Open the repository's **Releases** section.
2. Download the package for the version you want to use.
3. **Extract the ZIP fully** to a folder you can write to. Do not run directly from inside a ZIP preview.
4. Keep the release's supporting files and folders together.
5. Follow the appropriate launch method below.

#### Option A — Run the supplied R1.6 source package

The R1.6 package is distributed as **source code with an optional EXE builder**, rather than a confirmed prebuilt EXE release.

1. Extract the package.
2. Install a compatible Python version if the package requires one.
3. Run **`RUN_FROM_SOURCE.bat`** from the extracted folder.
4. If dependency installation fails, read the error output and follow any included package instructions before retrying.

#### Option B — Build a Windows executable

If your downloaded package includes a Windows EXE builder, use its included build instructions to generate an executable locally. The builder is an **optional packaging route**; do not assume a ready-made EXE exists in every release.

If a future GitHub Release explicitly contains a prebuilt executable, follow that release's own download instructions instead.

### Quick start

1. Launch Roblox and join **Dan RNG**.
2. Put Roblox on your intended screen, preferably in fullscreen mode.
3. Open Dan RNG Autopilot.
4. Select your automation mode, goal and rebirth target (if relevant).
5. Review upgrade priorities, gem goals, Index options and optional Discord settings.
6. Click **Start** or use **F4** where the hotkey is enabled.
7. Watch the first few cycles to confirm that recognition, purchases and menu navigation match your game UI.
8. Use **F5** to pause, inspect or change permitted settings, then resume.
9. Use **Stop** when you want to finish the session completely.

**For a first run:** test it while present, with modest goals, before leaving a session unattended.

---

## 🎮 Controls

| Control | Intended action |
| --- | --- |
| **Start** | Begin a fresh automation session |
| **Stop** | End the current session and finalise its statistics |
| **Pause / Resume** | Suspend or continue the current session |
| **F4** | Start / Stop toggle |
| **F5** | Pause / Resume toggle |
| **F6** | Debug mode toggle |
| **F7** | Capture a diagnostic screenshot |

Hotkeys and diagnostic availability can differ by package or application focus. Follow the controls displayed in your installed version if they differ from this table.

### Stop vs Pause

**Pause is temporary.** The current session is retained, and selected settings can be edited while paused. Changes are intended to take effect on resume.

**Stop is final for that session.** The session is ended, a summary can be produced and the next Start begins a new session with fresh session counters. Stop is not a substitute for Pause.

---

## Configuration

### Modes and progression targets

| Option | Purpose |
| --- | --- |
| **Standard automation** | Roll, upgrade and rebirth according to the active target |
| **Hunter Mode** | Keep hunting rolls without executing rebirth actions |
| **Rebirth target** | Set the minimum qualifying rarity for rebirthing |
| **Adaptive farming** | Adjust progression decisions based on observed conditions; intended default: on |
| **Smart Secret Farming** | Optionally delay a rebirth in suitable late-game circumstances |
| **Gem goal / reserve** | Preserve a target balance or work toward a gem milestone |
| **Index Collection** | Work through the supported Index stages before normal farming |

Select options based on your objective. A player accumulating rebirths should use different settings from someone hunting the rarest possible rolls.

### Upgrade management

The expected baseline is **Speed first until maxed or blocked, then buy affordable Luck upgrades**. The goal is to avoid an inefficient loop that repeatedly revisits Speed without making progress. Adaptive choices and gem protection can further influence spending.

### Monitor and display settings

The macro's ability to locate controls depends on what it sees. For best results:

- Keep the expected Roblox window visible and unobstructed.
- Use a supported resolution preset that matches your display.
- Check which screen Windows considers **primary**.
- Avoid switching resolution or changing Roblox UI scale in the middle of a run.
- Be aware that unusual lighting, bright avatars and UI overlays can disrupt visual checks.
- Test optional all-monitor dimming before leaving the computer.

### Editing settings while paused

In R1.6, you can change supported goals, rebirth targets and other settings while paused. The changes are applied when you resume, and a Discord **configuration updated** alert may be sent if webhooks are enabled.

Do not change underlying files or forcibly restart multiple copies of the macro to adjust a running session.

---

## 🔔 Discord webhook setup

A Discord webhook lets the macro post status information to a channel you choose.

1. In a Discord server where you have permission to manage webhooks, open the appropriate channel settings and create a webhook.
2. Copy the webhook URL.
3. Paste it into the macro's webhook setting.
4. Save the setting and test it using a supported test method or a normal session event.
5. Confirm that the message appears in the intended channel.

### Example notification categories

| Event | Intended information |
| --- | --- |
| Session started | Macro version, mode, goal, selected target and non-secret settings |
| Configuration changed | Updated goal or settings applied when resuming |
| Valuable roll | A verified rare event; details may depend on recognition support |
| Error / recovery | Relevant failure or successful recovery, with anti-spam safeguards |
| Session stopped | Runtime, observed rebirths, gems, rolls and relevant errors where available |

**Never post your webhook URL publicly.** Anyone with that URL may be able to send messages through your webhook. Do not place it in GitHub issues, screenshots, logs, example configuration files or your repository. Regenerate the webhook if it is exposed.

Webhook messages are notifications, **not remote-control commands**. No Discord bot or server-side control feature is required.

---

## 🔍 How the automation works

A normal automated progression cycle broadly follows this pattern:

```text
START SESSION
    |
    v
Verify Roblox and the current game UI
    |
    v
Check for Index Collection tasks, when enabled
    |
    v
Check rolling and upgrade state
    |
    +--> Buy available Speed upgrades
    |
    +--> When Speed is maxed/blocked, buy affordable Luck
    |
    v
Roll and monitor progress
    |
    +--> Rare cutscene? Wait for UI to return
    |
    +--> Stalled/uncertain? Retry or recover safely
    |
    v
Goal or rebirth condition satisfied?
    |
    +--> NO: Continue farming
    |
    +--> YES: Apply mode/goal rules
                   |
                   +--> Hunter Mode: Do not rebirth
                   |
                   +--> Standard: Verify and rebirth
    |
    v
Update session statistics and repeat
```

This is a simplified overview of how my macro works. The actual code also includes timing checks, safeguards and extra recovery steps.

---

## 🧪 Diagnostics and troubleshooting

Use Debug Mode and the available diagnostic-export or screenshot controls when trying to reproduce a problem. If you report an issue, include the macro version, Windows and Roblox resolution, mode, selected target, steps to reproduce and the relevant log excerpt. **Remove webhook URLs and personal information before sharing logs.**

| Problem | What to check |
| --- | --- |
| Macro opens but does not click | Ensure Roblox is open, visible and on the expected primary monitor; check fullscreen/resolution settings. |
| Start after Stop does nothing | Fully stop the session and confirm no duplicate macro instance remains. A Stop → Start lifecycle issue has previously been observed; restart the app and Roblox if necessary. |
| Macro cannot locate Rebirth / Shop | Close unexpected pop-ups, verify Roblox UI scale and display resolution, and capture a diagnostic screenshot. |
| Luck, rarity or gems look wrong | OCR can misread digits or UI text. Check the visible game value and report the screenshot rather than assuming the macro is correct. |
| Index Collection gets stuck | Verify the current stage and whether the game UI has changed; enable diagnostics. |
| Rare cutscene interrupts navigation | Do not force-click through the animation. Let the UI return and check whether recovery resumes normally. |
| Hunter Mode opens Rebirth menu | Known R1.6 issue: Hunter Mode blocks rebirths, but can still open the Rebirth menu unnecessarily. |
| Discord notifications are missing | Check whether webhooks are enabled, the URL is current, the channel permits posting and the triggering event was actually verified. |
| Dimming does not clear correctly | Stop the macro, exit its overlay/process if necessary and restore the normal display state. |
| Automation gets stuck after a UI update | Stop and collect diagnostics; the recognition logic may need to be updated for the new Roblox/Dan RNG interface. |

### Known limitations

- **Visual and OCR-based automation can fail.** Text, animations, display scaling and overlays change over time.
- A rare cutscene does not always produce enough evidence for a verified notification.
- Auto-recovery cannot guarantee recovery from every disconnect, UI state or game update.
- Session statistics may be incomplete if a value was not reliably observed.
- Long unattended sessions require live validation on the machine where the macro is running.
- The **R1.6 Hunter Mode navigation issue** is still present unless a newer release explicitly fixes it.
- Offline tests are not a substitute for real-game tests.

---

## 🔒 Safety and privacy

This project interacts with a live game using desktop automation. Please use it responsibly.

- Review the **Roblox terms and the individual game's rules** before using third-party automation. Use may lead to enforcement actions, including account restrictions.
- Download only from a source you trust. Executables and batch files can be dangerous if modified by someone else.
- Avoid running unverified releases with unnecessary administrator permissions.
- Treat the Discord webhook URL as a **secret**.
- Review exported diagnostics before posting them publicly; screenshots can show usernames, private messages or other personal data.
- Do not run two macro instances against the same Roblox session.
- Do not assume successful testing on one computer guarantees the same result on another.

The macro is not an anti-cheat bypass, does not guarantee account safety and should not be presented as officially supported by Roblox or Dan RNG.

---

## 🗺️ Roadmap and proposed improvements

These are changes and improvements I want to work on. **They are not included in R1.6 unless a newer release specifically says otherwise.**

- [ ] Fully bypass Rebirth menu navigation in Hunter Mode, including startup and post-Index flows.
- [ ] Add **Omega (1 in 1 trillion base rarity)** as an explicit rebirth target.
- [ ] Remove rebirth target choices below **Mythic**, if the updated selector design is adopted.
- [ ] Further refine rarest-roll hunting behaviour and related UI wording.
- [ ] Confirm all recovery, dimming, Discord and OCR features through extended live-game testing.
- [ ] Expand documentation with verified screenshots and real release-by-release changelogs.

Plans might change. Check Releases to see what has actually been added.

---

## ❓ Frequently asked questions

<details>
<summary><strong>Is this an official Dan RNG or Roblox tool?</strong></summary>

No. It is an unofficial community-made automation project and is not endorsed by Roblox or the developers of Dan RNG.

</details>

<details>
<summary><strong>Does the macro require an EXE?</strong></summary>

No. R1.6 can be run from the extracted source using `RUN_FROM_SOURCE.bat`. I have also included an optional Windows EXE builder. If I publish a prebuilt EXE, it will be available in Releases.

</details>

<details>
<summary><strong>Can I change settings during a run?</strong></summary>

The intended R1.6 workflow is to **Pause**, edit supported settings and **Resume**. Avoid changing settings while the macro is actively clicking or using an outdated configuration.

</details>

<details>
<summary><strong>Will Hunter Mode rebirth?</strong></summary>

Hunter Mode blocks actual rebirth actions. In R1.6, it may still open the Rebirth menu unnecessarily. I plan to fix that navigation issue.

</details>

<details>
<summary><strong>Can I automate from a second monitor?</strong></summary>

The macro normally targets the display set as **primary in Windows**, even if Windows calls it Monitor 2. Check your setup and do a short test first.

</details>

<details>
<summary><strong>Does Discord control the macro?</strong></summary>

No. Discord integration is intended for **outgoing notifications only**, not remote commands or control.

</details>

<details>
<summary><strong>Will this work forever without supervision?</strong></summary>

No automation can promise that. Game updates, disconnects, OCR mistakes and unexpected UI states can still cause failures. Watch the initial session and validate new releases before extended use.

</details>

<details>
<summary><strong>Where can I get help with a bug?</strong></summary>

Use the repository's **Issues** section if enabled. Include the version, settings relevant to the problem, steps to reproduce and sanitized diagnostics. Never share your webhook URL.

</details>

---

## 📝 Release information

| Version | Notes |
| --- | --- |
| **R1.6** | Feature expansion: Hunter Mode, adaptive farming, optional Smart Secret Farming, paused configuration changes, goal handling, dashboard, recovery and session features. Live validation remains important. |
| **R1.5.9** | Earlier cutscene-protection and progression base retained by R1.6. |
| **R1.5.4** | Earlier improvements to reconnect/recovery, diagnostic tools, gem/rank recognition and Index Collection workflow. |

This is just a short version history, not a full changelog. I will keep the individual release notes more detailed.

---

## 🤝 Feedback and bug reports

If you find a bug or have an idea for a feature, feel free to open an Issue. Please include the version, what you expected to happen, what actually happened and how to reproduce it. Screenshots and logs are useful, but **remove webhook URLs and other private information** first.

## ⚠️ Disclaimer

**This project was made with the help of AI.** I use AI tools to help develop, improve, debug and document the macro. I make the decisions about its features and direction, and I test the results. AI-assisted code can still contain bugs, so I cannot guarantee that everything will work perfectly.

Dan RNG Autopilot is an **unofficial third-party tool** and is not affiliated with Roblox or the developers of Dan RNG. Using automation may go against game rules or Roblox policies, so **use it at your own risk**. I cannot guarantee compatibility with future updates, uninterrupted operation or account safety.

---

<div align="center">

**🎲 Dan RNG Autopilot — Roll smarter. Manage progression. Keep track of the session.**

*Made for the Dan RNG community.*

</div>
