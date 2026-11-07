<div align="center">

# 🎲 Dan RNG Autopilot

### Automated progression. Intelligent decisions. Built for long sessions.

**My Windows automation macro for the Roblox game *Dan RNG*.**

![Version](https://img.shields.io/badge/Version-R1.6.1-7657E8?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%2F%2011-0078D6?style=for-the-badge)
![Project](https://img.shields.io/badge/Project-Community%20tool-30363D?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Live%20testing%20recommended-E3A008?style=for-the-badge)

**[What's new](#-whats-new-in-r161) · [Features](#-features) · [Getting started](#-getting-started) · [Configuration](#configuration) · [Troubleshooting](#-diagnostics-and-troubleshooting) · [FAQ](#-frequently-asked-questions)**

*Unofficial third-party project. Not affiliated with Roblox or the developers of Dan RNG.*

</div>

---

## 📖 Overview

I made **Dan RNG Autopilot** to automate the repetitive progression in Dan RNG. Instead of just clicking on a fixed timer, it tries to make decisions using what it can actually see in the game.

It handles rolling, upgrades, rebirths, Index Collection and longer sessions. I also added configurable goals, visual detection, session statistics, Discord notifications and recovery tools to make it more reliable.

My main goal is simple: **the macro should know what it is trying to do, verify important actions, and avoid making risky decisions when it cannot tell what is happening.**

> [!IMPORTANT]
> **Version note:** This README covers **R1.6.1 — Hunter, Coins & Anti-AFK Patch** (7 November 2026). It includes the existing R1.6 features plus the changes listed below. Offline checks passed, but I have **not yet confirmed every behaviour in a live Roblox session**. Always read the release notes and test new builds before running them unattended.

### At a glance

| Area | Capabilities |
| --- | --- |
| 🎲 Rolling | Automatic rolling and roll-state monitoring |
| 🔁 Rebirths | Rarity-based targets, automatic confirmation and session tracking |
| ⬆️ Upgrades | Speed-first purchasing, adaptive farming and coin-checked Luck levels 1000–1100 |
| 📚 Index | Multi-stage Index Collection workflow |
| 🎯 Goals | Rebirth-free Hunter Mode, dynamic Mythic+ targets (including Omega) and gem goals |
| 🧠 Detection | Visual UI checks, OCR safeguards and cutscene awareness |
| 🛠️ Reliability | Watchdogs, retries, safe five-minute anti-AFK, recovery and diagnostics |
| 📊 Dashboard | Session information, progress indicators and event logs |
| 🔔 Notifications | Optional outgoing Discord webhook alerts |
| 🖥️ Windows | Primary-monitor targeting, resolution presets and optional dimming |

---

## 🆕 What's new in R1.6.1

This update is mainly about making **Hunter Mode more reliable** and handling the newer **coin-based Luck upgrades** properly. I also fixed the anti-AFK logic so it reacts to real inactivity instead of blindly running on a timer.

| Change | What it does |
| --- | --- |
| **Hunter Mode navigation fix** | Skips the startup Rebirth check, closes Shop back to normal gameplay and returns to normal gameplay after Index Collection restoration. Hunter Mode no longer intentionally routes through the Rebirth menu. |
| **Coin-aware Luck levels 1000–1099** | Reads the visible coin balance and the **Next level** cost, verifies affordability with a small buffer, then buys **one level at a time** and rechecks the UI. |
| **Luck cap handling** | Stops attempting coin-based Luck purchases at **level 1100**. |
| **Smarter retry behaviour** | If the next Luck level is unaffordable, Hunter Mode returns to rolling instead of staying stuck in Shop; it can check again after roughly **12 seconds**. |
| **Updated rebirth target selector** | Offers **As Soon As Eligible** and **Mythic+** targets, including **Omega (1 in 1 trillion base rarity)**. Targets below the currently recognised game requirement are filtered out. |
| **Five-minute anti-AFK** | Tracks actual cursor movement (including movement caused by the macro), only acts after around **five minutes without movement** when safe, stays off while paused and restarts its timer on Resume. |

**Testing:** R1.6.1 passed offline regression and integration checks, existing R1.5.9 cutscene tests, source compilation checks and ZIP integrity checks. **Real Roblox testing is still needed** to confirm behaviour across different screens and game states.

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

- Works toward a **selected rebirth rarity** instead of rebirthing at arbitrary moments.
- Supports **As Soon As Eligible** or a specific rarity from **Mythic upward**, including **Omega** (1 in 1 trillion base rarity).
- Filters target choices below the game's currently recognised minimum rebirth requirement, so the list better reflects what can actually be selected.
- Navigates the Rebirth menu, checks eligibility and handles confirmation **in standard rebirth modes**.
- Tracks observed rebirths for the current session and returns to progression afterward.
- Avoids attempting a rebirth when the necessary visual evidence is missing.

**Hunter Mode deliberately does not rebirth.** In R1.6.1, I also corrected the related navigation so Hunter Mode does not intentionally visit Rebirth at startup, when closing Shop or after Index Collection restoration.

**Important:** Eligibility still depends on what the macro can recognise from the game. UI updates and OCR mistakes can affect detection, so test a new release before relying on it unattended.

### ⬆️ Speed and Luck upgrade automation

The normal upgrade strategy prioritises efficient progression:

1. Buy available **Speed** upgrades until Speed is maxed or blocked.
2. Purchase affordable **Luck** upgrades instead of endlessly revisiting Speed after it has become blocked.
3. Reassess upgrades as the game state changes, with **Adaptive Farming** enabled by default in the R1.6 progression system.
4. Respect supported goals and protected gem balances where configured.

#### Coin-based Luck upgrades (R1.6.1)

At **Luck level 1000 and above**, the macro uses the game's **coins** and the displayed **Next level** cost to decide whether it can afford another level. This part is intentionally conservative:

- It reads the visible **yellow coin balance** and labelled next-level price using OCR.
- It checks whether there appears to be enough coins, with approximately a **3% safety buffer**.
- It confirms the values and the relevant **purple +1** purchase button against a fresh screenshot before buying.
- It buys **exactly one Luck level per successful validation**, then checks again. It does **not** blindly batch-buy high-level upgrades.
- If the purchase is not affordable or cannot be verified, it does not guess and spam the button.
- When Hunter Mode cannot afford another level, it goes back to normal rolling and tries checking Shop again after roughly **12 seconds**.
- It stops at **Luck level 1100**.

For example, if the HUD shows **1.18T coins** and the next Luck upgrade costs **908.70B**, the macro can compare those values instead of assuming that a button is always affordable. This is an **OCR test example**, not a promise that every in-game number will be recognised correctly.

**Why one level at a time?** Once the price changes after a purchase, the macro needs to read the new cost. This is slower than blind clicking but much safer when upgrades become expensive.

### 📚 Index Collection automation

For players working through Index Collection, the macro includes a staged workflow that progresses through the following limit sequence:

`1 → 50 → 1,000 → 50,000 → Unlimited`

The goal is to handle Index tasks before returning to normal farming, without requiring the user to manually revisit the menus at every stage. Game changes or recognition failures can interrupt the sequence; the live game UI remains the final source of truth.

### 🎯 Hunter Mode and goal-based farming

I added **Hunter Mode** for when I want to keep rolling for rare auras **without rebirthing**. In **R1.6.1**, I also fixed the unnecessary Rebirth-menu navigation that existed in R1.6:

- Hunter Mode **skips the Rebirth check at session startup**.
- After checking upgrades in Shop, it returns to **normal rolling**, not the Rebirth menu.
- After finishing or restoring Index Collection settings, it returns to **normal rolling** instead of navigating to Rebirth.
- When a coin-based Luck upgrade is unaffordable, it carries on rolling and checks the price again later rather than blocking the farming loop.

Other goal-oriented options include:

- Choosing an eligible rebirth target, from **Mythic to Omega**, or **As Soon As Eligible**, when using a rebirth-capable mode.
- Tracking a desired gem balance or progression milestone.
- Protecting a gem target from avoidable spending, where that setting is enabled.
- Using optional **Smart Secret Farming**, designed to wait for a Secret-tier opportunity in suitable late-game conditions rather than always rebirthing immediately.

Smart Secret Farming is optional. Its intended use includes certain late-game situations around **Luck level 800+**, after relevant Index work. The exact results depend on the selected settings and what the macro can read from the game.

> [!NOTE]
> The R1.6.1 Hunter fix changes **navigation**, not just whether the final confirmation button gets clicked. Hunter Mode is meant to remain in normal rolling/upgrade states without unnecessarily entering Rebirth. I still recommend checking this behaviour live when installing a new build.

### 👁️ Visual recognition and cutscene protection

Dan RNG can temporarily hide its regular interface during rare-roll animations. The macro includes cutscene-aware protection intended to:

- Recognise when normal game UI elements disappear.
- Suspend menu navigation while a rare-roll sequence appears to be playing.
- Wait for the expected interface to return before resuming interaction.
- Use rarity visuals as **supporting evidence**, not as the sole proof of a valuable roll.
- Reduce accidental clicks during large visual effects, flashes and transitional screens.

These checks are especially relevant to Secret, Forbidden and Omega-tier events. **Visual recognition is not infallible**, particularly with unusual avatars, game updates, overlays or intense effects.

### 🛠️ Recovery, anti-AFK and reliability

I have added reliability features for longer unattended sessions, including:

- Rolling-progress watchdogs and checks for stalled activity.
- Retries and visual rechecks after uncertain interactions.
- Recovery from common menu and rolling interruptions.
- Protection against duplicate macro instances.
- Clear separation between **Start**, **Stop**, **Pause** and **Resume**.
- Conservative OCR handling when important values cannot be confirmed.
- Diagnostic logs and screenshots for tracking down failures.

#### Anti-AFK in R1.6.1

The anti-AFK system looks at **actual cursor displacement** rather than simply assuming the player has been inactive after a fixed amount of time. Movements generated by the macro itself count as movement too.

- The inactivity threshold is **five minutes** without movement.
- It only performs anti-AFK behaviour when the macro considers the current situation safe.
- It is **disabled during Pause** so it does not interfere while I am inspecting the game or changing settings.
- The timer is reset when I **Resume**, so it does not immediately fire based on time spent paused.

This is designed to avoid unnecessary anti-AFK actions while the macro is already moving the mouse. It is not a guarantee against all game idle/disconnect behaviour.

The macro is built with unattended sessions in mind, but **I still recommend supervising the first run of each version before leaving it running for hours**.

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
- For Luck 1000+, a readable in-game **coin balance** and **Next level** price. The included OCR dependencies must be installed/configured as described by the release package.

> [!TIP]
> The macro was designed around Roblox running **fullscreen** and normally targets the **Windows primary monitor**. If your gaming display is labelled "Monitor 2" in Windows but marked as the primary display, that is fine.

### Download and install

1. Open the repository's **Releases** section.
2. Download the package for the version you want to use.
3. **Extract the ZIP fully** to a folder you can write to. Do not run directly from inside a ZIP preview.
4. Keep the release's supporting files and folders together.
5. Follow the appropriate launch method below.

#### Option A — Run the supplied R1.6.1 source package

The **R1.6.1 Hunter, Coins & Anti-AFK Patch** is distributed as **full source code with a Windows EXE builder**. The patch archive does **not** include a precompiled EXE.

1. Extract the package.
2. Install a compatible Python version if the package requires one.
3. Run **`RUN_FROM_SOURCE.bat`** from the extracted folder.
4. If dependency installation fails, read the error output and follow any included package instructions before retrying.

#### Option B — Build a Windows executable

The R1.6.1 package includes an **optional Windows EXE builder**. Run the included build script on Windows and follow any instructions it displays. The builder is a separate packaging step: **the patch ZIP does not already contain a compiled EXE**.

If a future GitHub Release explicitly contains a prebuilt executable, follow that release's own download instructions instead.

### Quick start

1. Launch Roblox and join **Dan RNG**.
2. Put Roblox on your intended screen, preferably in fullscreen mode.
3. Launch Dan RNG Autopilot using **`RUN_FROM_SOURCE.bat`** (or an EXE that you built from the same release).
4. Choose **Hunter Mode** if you only want to collect rolls without rebirthing, or a standard mode if you want automated rebirths.
5. In standard mode, choose **As Soon As Eligible** or an available **Mythic+** target, including **Omega** if you want that threshold.
6. Review Speed/Luck upgrades, gem goals, Index options and any Discord settings. If you are already around **Luck 1000+**, check that the visible coin balance and **Next level** price are readable.
7. Review the session controls and the five-minute anti-AFK behaviour before starting.
8. Click **Start** or press **F4** where the hotkey is enabled.
9. Watch the first few cycles to confirm recognition, coin-cost checks and menu navigation match your game UI.
10. Press **F5** to pause when needed, then resume after making supported changes.
11. Use **Stop** when you want to end the session completely.

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
| **Hunter Mode** | Keep hunting rolls without rebirthing or unnecessarily entering the Rebirth menu |
| **Rebirth target** | Choose **As Soon As Eligible** or an available **Mythic+** rarity, including Omega (filtered by the current game requirement) |
| **Adaptive farming** | Adjust progression decisions based on observed conditions; intended default: on |
| **Smart Secret Farming** | Optionally delay a rebirth in suitable late-game circumstances |
| **Gem goal / reserve** | Preserve a target balance or work toward a gem milestone |
| **Index Collection** | Work through the supported Index stages, then return to normal rolling (including in Hunter Mode) |

Select options based on your objective. A player accumulating rebirths should use different settings from someone hunting the rarest possible rolls.

### Upgrade management

The expected baseline is **Speed first until maxed or blocked, then buy affordable Luck upgrades**. At **Luck 1000–1099**, the macro also checks the **coin balance and next-level cost**, re-verifies affordability and buys at most one level per validation. If a level is unaffordable in Hunter Mode, it resumes rolling and checks again later. It stops trying at **Luck 1100**. Adaptive choices and gem protection may also influence spending.

### Monitor and display settings

The macro's ability to locate controls depends on what it sees. For best results:

- Keep the expected Roblox window visible and unobstructed.
- Use a supported resolution preset that matches your display.
- Check which screen Windows considers **primary**.
- Avoid switching resolution or changing Roblox UI scale in the middle of a run.
- Be aware that unusual lighting, bright avatars and UI overlays can disrupt visual checks.
- Test optional all-monitor dimming before leaving the computer.

### Editing settings while paused

In R1.6.1, you can change supported goals, rebirth targets and other settings while paused. The changes are applied when you resume, and a Discord **configuration updated** alert may be sent if webhooks are enabled.

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

The main workflow depends on the selected mode. This is a simplified look at how I designed it:

```text
START SESSION
    |
    v
Verify Roblox and the visible game UI
    |
    v
INDEX TASKS (if enabled)
    |  Restore settings / return to normal rolling
    v
Choose mode
    |
    +--> HUNTER MODE ----------------------------------------+
    |       No startup Rebirth-menu check                    |
    |       Roll and monitor                                 |
    |       Check Shop upgrades when appropriate             |
    |       Luck 1000+: read coins + Next level price         |
    |       Buy only one verified affordable level           |
    |       Unaffordable? close Shop, roll, retry ~12s        |
    |       Never intentionally initiate a rebirth           |
    |                                                        |
    +--> STANDARD MODE --------------------------------------+ 
            Check available Speed / Luck upgrades            |
            Roll toward selected eligible rebirth target     |
            Verify Rebirth eligibility and confirmation      |
            Complete rebirth if appropriate                  |
                                                             v
                                             Update session stats
                                                             |
                                              UI/cutscene safeguards
                                                             |
                                             Retry / recover if needed
                                                             |
                                                      Repeat
```

During active operation, R1.6.1's anti-AFK watcher measures **real mouse movement**. Only after about five minutes without movement, and only when it is safe, can it take an anti-AFK action. It does nothing while paused and restarts its timer on Resume.

The actual code has extra timing checks, OCR safeguards and recovery steps. This diagram is intended to explain the workflow, not every internal state.

## 🧪 Diagnostics and troubleshooting

Use Debug Mode and the available diagnostic-export or screenshot controls when trying to reproduce a problem. If you report an issue, include the macro version, Windows and Roblox resolution, mode, selected target, steps to reproduce and the relevant log excerpt. **Remove webhook URLs and personal information before sharing logs.**

| Problem | What to check |
| --- | --- |
| Macro opens but does not click | Ensure Roblox is open, visible and on the expected primary monitor; check fullscreen/resolution settings. |
| Start after Stop does nothing | Fully stop the session and confirm no duplicate macro instance remains. A Stop → Start lifecycle issue has previously been observed; restart the app and Roblox if necessary. |
| Macro cannot locate Rebirth / Shop | Close unexpected pop-ups, verify Roblox UI scale and display resolution, and capture a diagnostic screenshot. |
| Luck, coins, rarity or gems look wrong | OCR can misread digits or UI text. For Luck 1000+, check the visible **coins** and **Next level** price and capture the relevant screenshot. |
| Index Collection gets stuck | Verify the current stage and whether the game UI has changed; enable diagnostics. |
| Rare cutscene interrupts navigation | Do not force-click through the animation. Let the UI return and check whether recovery resumes normally. |
| Hunter Mode opens Rebirth menu | **R1.6.1 is intended to fix this.** Check that you are actually running R1.6.1, stop any older macro instance and capture diagnostics if the problem persists. |
| Luck 1000+ stops buying | Confirm that your coin balance exceeds the next-level price (including the safety buffer), that the purple **+1** button is visible and that you have not reached Luck 1100. |
| Anti-AFK does not trigger | The macro checks for **five minutes of actual inactivity**, including its own mouse movement, and does not operate while paused or when unsafe. |
| Discord notifications are missing | Check whether webhooks are enabled, the URL is current, the channel permits posting and the triggering event was actually verified. |
| Dimming does not clear correctly | Stop the macro, exit its overlay/process if necessary and restore the normal display state. |
| Automation gets stuck after a UI update | Stop and collect diagnostics; the recognition logic may need to be updated for the new Roblox/Dan RNG interface. |

### Known limitations

- **Visual and OCR-based automation can fail.** Text, animations, display scaling and overlays change over time.
- A rare cutscene does not always produce enough evidence for a verified notification.
- Auto-recovery cannot guarantee recovery from every disconnect, UI state or game update.
- Session statistics may be incomplete if a value was not reliably observed.
- Long unattended sessions require live validation on the machine where the macro is running.
- R1.6.1 includes a fix for the earlier **Hunter Mode navigation problem**, but live-game behaviour still needs validation.
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

R1.6.1 already includes the Hunter Mode navigation fix, Mythic+ rebirth targets (including Omega), coin-aware Luck 1000–1100 purchasing and five-minute anti-AFK. **Those are not future features anymore.**

These are areas I still want to improve:

- [ ] Verify the R1.6.1 changes during extended **live Roblox** sessions, including low-coin and high-level Luck situations.
- [ ] Continue stress-testing Stop → Start, recoveries and unexpected game UI states.
- [ ] Refine OCR for changing coin values, upgrade costs, rarity text and unusual visual effects.
- [ ] Keep improving long-running stability, cutscene detection and useful diagnostics.
- [ ] Add verified screenshots and fuller release-by-release changelogs to this page.

Plans can change, and I will update the README when something is actually included in a release.

## ❓ Frequently asked questions

<details>
<summary><strong>Is this an official Dan RNG or Roblox tool?</strong></summary>

No. It is an unofficial community-made automation project and is not endorsed by Roblox or the developers of Dan RNG.

</details>

<details>
<summary><strong>Does the macro require an EXE?</strong></summary>

No. **R1.6.1** is supplied with the full source and a `RUN_FROM_SOURCE.bat` launcher, plus an optional Windows EXE builder. The R1.6.1 patch ZIP does **not** include a prebuilt EXE.

</details>

<details>
<summary><strong>Can I change settings during a run?</strong></summary>

The intended R1.6.1 workflow is to **Pause**, edit supported settings and **Resume**. Avoid changing settings while the macro is actively clicking or using an outdated configuration.

</details>

<details>
<summary><strong>Will Hunter Mode rebirth?</strong></summary>

Hunter Mode is designed to **never intentionally perform a rebirth**. In **R1.6.1**, I also fixed the unnecessary Rebirth-menu navigation at startup, after Shop, and following Index Collection. If it still opens that menu, please report the issue with diagnostics.

</details>

<details>
<summary><strong>How does Luck level 1000+ purchasing work?</strong></summary>

From **Luck 1000 through 1099**, the macro reads the coin balance and the labelled **Next level** cost, uses a small affordability buffer and validates each purchase individually. It stops at **Luck 1100**. When Hunter Mode cannot afford the next level, it keeps rolling rather than getting stuck in Shop.

</details>

<details>
<summary><strong>Does the anti-AFK timer keep running while I am paused?</strong></summary>

No. R1.6.1 disables anti-AFK while paused and resets the five-minute inactivity timer when the session resumes. Mouse movement from the macro itself also counts as activity.

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
| **R1.6.1 — Hunter, Coins & Anti-AFK Patch** | Fixed Hunter Mode's unnecessary Rebirth navigation, added dynamic Mythic+ and Omega targets, added one-by-one coin-verified Luck purchases at levels 1000–1099 (cap 1100), safe five-minute anti-AFK and retry-to-rolling behaviour when a high-level Luck upgrade is unaffordable. |
| **R1.6** | Added the Hunter Mode and adaptive/goal-oriented progression foundation, optional Smart Secret Farming, paused setting changes, dashboard, recovery and session features. |
| **R1.5.9** | Earlier cutscene-protection and progression base retained by subsequent releases. |
| **R1.5.4** | Earlier reconnect/recovery work, diagnostics, gem/rank recognition and Index Collection improvements. |

**R1.6.1 distribution:** Full source + `RUN_FROM_SOURCE.bat` + optional Windows EXE builder. **No precompiled EXE** in the patch archive. I will include any more detailed changes and known issues in the release notes.

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
