<div align="center">

# 🎲 Dan RNG Autopilot

### Automated rolling, upgrades and rebirths for Roblox Dan RNG

**A Windows macro I made to automate Dan RNG progression and make long farming sessions easier to manage.**

![Version](https://img.shields.io/badge/Version-R1.6.2-7456E8?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%2F%2011-0078D6?style=for-the-badge)
![Download](https://img.shields.io/badge/Download-Windows%20EXE-288B61?style=for-the-badge)

**[Overview](#-overview) · [Features](#-features) · [Installation](#-download--installation) · [How to use](#-how-to-use-the-macro) · [Settings](#settings--modes) · [Controls](#controls) · [Support](#-support--bug-reports)**

*An unofficial third-party project. Not affiliated with Roblox or the developers of Dan RNG.*

</div>

---

## 📖 Overview

I made **Dan RNG Autopilot** to take care of the repetitive parts of Dan RNG, including rolling, purchasing upgrades, completing rebirths and managing progression goals.

The macro is designed to do more than repeat clicks at fixed intervals. It reads what's happening on the screen and uses that information to decide what to do next. For example, it can check which upgrades are available, work towards a selected rebirth rarity and return to rolling when there isn't anything else to purchase.

You can use it for regular rebirth farming or switch to **Hunter Mode** to focus on collecting rare auras without rebirthing. There are also optional features for Index Collection, Discord notifications, anti-AFK and screen dimming.

**This README covers Dan RNG Autopilot R1.6.2.** The macro is distributed as a Windows **`.exe`**, so you don't need to install Python or build anything yourself.

### What can it do?

| Feature | Description |
| :--- | :--- |
| 🎲 **Automatic rolling** | Handles rolling during an automation session. |
| 🔁 **Automatic rebirths** | Rebirths according to your chosen rarity target. |
| 🎯 **Hunter Mode** | Farms without rebirthing, for players focusing on rare auras. |
| ⬆️ **Automatic upgrades** | Manages Speed and Luck upgrades as you progress. |
| 🪙 **Coin-based Luck upgrades** | Uses in-game coin prices when purchasing Luck levels 1000–1099. |
| 📚 **Index Collection** | Handles the supported Index Collection stages. |
| 💎 **Progression goals** | Includes configurable rebirth, gem and farming goals. |
| 🌌 **Rare-roll awareness** | Handles rare-roll cutscenes and waits for the regular game interface. |
| 🖥️ **Screen dimming** | Optionally darkens connected monitors during farming. |
| 💤 **Anti-AFK** | Includes an inactivity-based anti-AFK routine. |
| 🔔 **Discord notifications** | Sends session and progression updates to a Discord channel. |
| 📊 **Session dashboard** | Displays progress, activity and session information. |

---
<details>
<summary><b>✨ Features</b></summary>

### 🎲 Automatic rolling

The macro handles the normal rolling process while it manages your progression in the background.

- Continues rolling during farming periods.
- Checks the current game interface before moving between menus.
- Switches between rolling, upgrading and rebirthing based on the selected mode.
- Recognises when the usual interface is hidden by a rare-roll animation.
- Returns to rolling after completing other tasks.

You can leave the macro focused on progression rather than manually managing each part of the loop.

### 🔁 Automatic rebirth farming

In standard farming mode, the macro works towards a rebirth target you choose.

You can select **As Soon As Eligible** or choose a specific supported rebirth rarity, starting from **Mythic** and extending up to **Omega**. The available targets are adjusted according to the game's current rebirth requirement.

During a session, the macro:

1. Rolls and purchases relevant upgrades.
2. Checks rebirth progress against your selected target.
3. Opens the Rebirth interface when needed.
4. Completes the rebirth once the selected conditions are met.
5. Returns to farming and repeats the cycle.

This mode is useful if your goal is to accumulate rebirths, gems and permanent progression.

### 🎯 Hunter Mode — farm without rebirthing

**Hunter Mode** is for players who want to keep rolling for rare auras without spending those rolls on rebirths.

In Hunter Mode, the macro:

- Focuses on rolling and upgrades instead of rebirthing.
- Skips unnecessary visits to the Rebirth menu.
- Returns straight to normal rolling after checking the Shop.
- Continues farming after Index Collection tasks.
- Can revisit the Shop when more upgrades become affordable.

Use Hunter Mode if you're trying to obtain a particularly rare aura, improve your collection or just want a roll-focused farming session.

### ⬆️ Automatic Speed and Luck upgrades

The upgrade system automatically manages your progression in the Shop.

The general priority is:

1. **Speed first** — purchase available Speed upgrades until they're maxed or temporarily blocked.
2. **Luck next** — spend on affordable Luck upgrades rather than repeatedly trying to buy unavailable Speed levels.
3. **Return to farming** — continue rolling and check upgrades again as you progress.

The macro also includes **Adaptive Farming**, which adjusts some progression decisions based on the current game state and your selected settings.

#### 🪙 Luck levels 1000–1100

At higher Luck levels, upgrades require **coins**. The macro reads your displayed coin balance and the next upgrade price to manage these purchases.

- Checks your current coins against the displayed next-level cost.
- Purchases high-level Luck upgrades **one level at a time**.
- Reads the updated cost after each purchase.
- Returns to rolling when the next upgrade is not yet affordable.
- Stops purchasing when Luck reaches **level 1100**.

This lets high-level Luck progression fit into the regular farming loop without needing to manage each purchase manually.

### 📚 Index Collection automation

The macro includes support for Dan RNG's Index Collection progression.

It can go through the following stages:

`1 → 50 → 1,000 → 50,000 → Unlimited`

Once the selected Index workflow is completed, the macro returns to your normal farming mode. This is available alongside the regular upgrade and rebirth features.

### 💎 Gem goals and farming options

Depending on how you want to progress, you can configure goals that influence the macro's decisions.

These include:

- **Rebirth targets:** Choose when the macro should rebirth based on rarity.
- **Gem goals or reserves:** Set a balance you want to reach or preserve.
- **Adaptive Farming:** Allow the macro to adjust farming behaviour to current conditions.
- **Smart Secret Farming:** An optional late-game approach that can delay a rebirth in favour of aiming for Secret-tier results under suitable conditions.

You don't need to use every option. The best setup depends on whether you're prioritising rebirths, gems or rare auras.

### 🌌 Rare-roll cutscene awareness

Dan RNG sometimes hides or changes the normal interface when a rare aura is rolled.

The macro accounts for those moments by temporarily holding off on its usual menu actions while the animation is happening. Once the regular interface returns, it continues the current task.

This helps keep farming, upgrading and rebirthing separate from rare-roll animations. Rarity-related visuals can also contribute to relevant Discord notifications.

### 💤 Anti-AFK

The macro includes an anti-AFK routine based on inactivity.

- Tracks mouse movement during the session.
- Uses an inactivity threshold of approximately **five minutes**.
- Includes mouse movement generated by the macro itself when measuring activity.
- Does not perform anti-AFK actions while the macro is paused.
- Resets the inactivity timer when you resume.

It runs alongside normal automation rather than requiring a separate anti-AFK program.

### 🌙 Optional screen dimming

For longer farming sessions, you can enable the screen dimmer to reduce how bright your displays are while the macro is running.

**R1.6.2 uses a display-overlay dimmer**, with the following features:

- Darkens the image by approximately **80%**.
- Covers **all connected monitors**.
- Fades into the dimmed appearance.
- Uses click-through overlays, so normal mouse input passes through them.
- Keeps the underlying display colour and gamma calibration unchanged.
- Separates the dimming overlay from the images used for game recognition.
- Removes the dimming overlays when the macro stops or closes.

For this feature, **borderless/windowed fullscreen** is the recommended Roblox display mode.

Screen dimming is optional and can be left disabled if you prefer to see your screens normally.

### 🔔 Discord webhook notifications

You can connect a Discord channel using a webhook URL to receive updates about your macro sessions.

Notifications can include:

- Session start information, such as the version, mode and selected target.
- Session summaries after stopping the macro.
- Rebirth and progression events.
- Important rare-roll events when recognised.
- Configuration updates and other relevant session messages.

The webhook is used for **outgoing notifications**. It doesn't allow anyone in Discord to control your macro remotely.

### 📊 Dashboard, statistics and activity log

The macro includes an interface for managing your sessions and viewing activity.

Depending on the current game state, you can see information such as:

- Whether the macro is running, paused or stopped.
- Your selected mode and rebirth target.
- Current session duration.
- Rebirths and other recorded progression.
- Gem-related session information.
- Recent actions and event messages.

The log gives you an overview of what the macro has been doing without needing to watch the Roblox screen the whole time.
</details>

## 📥 Download & installation

### Requirements

- **Windows 10 or Windows 11**.
- **Roblox** installed on your PC.
- Access to the **Dan RNG** experience on Roblox.
- A display resolution supported by the macro, such as **1920×1080**, **2560×1440** or **3840×2160**.
- An internet connection for Roblox and, if enabled, Discord notifications.

**You do not need Python, programming knowledge or a development environment.** The public release is intended to be run as a Windows executable.

### Installing the macro

1. Open the project's **GitHub Releases** page.
2. Download the latest **Dan RNG Autopilot `.exe`** release. If it comes inside a ZIP, download and extract the ZIP first.
3. Keep the downloaded release files together in a folder of your choice.
4. Launch the **Dan RNG Autopilot `.exe`**.
5. Open Roblox and join **Dan RNG** if you haven't already.
6. Configure the macro using the steps below.

You only need the release download to run the application. There are no Python setup or code-building steps.

---

## 🚀 How to use the macro

### 1. Launch Dan RNG

Open Roblox, join **Dan RNG** and make sure the game's normal interface is visible.

The macro is designed to target your **Windows primary monitor**. If Windows calls your gaming display "Monitor 2" but it is set as your primary display, that's the display the macro should target.

Choose the matching display/resolution settings in the application where applicable.

### 2. Open the macro

Launch the downloaded `.exe` and open the main control window.

You'll be able to choose your farming options, manage the session and view the activity log from the application.

### 3. Choose your mode

| Mode | Best for | Rebirths? |
| :--- | :--- | :---: |
| **Standard farming** | Collecting rebirths, gems and progressing through upgrades | ✅ Yes |
| **Hunter Mode** | Continuous rolling for rare auras and collection goals | ❌ No |

For standard farming, choose a rebirth target. For Hunter Mode, you can concentrate on rolling and upgrades without setting a rebirth goal.

### 4. Configure your settings

Review the available options, including:

- Your **rebirth rarity target**, if using standard farming.
- **Adaptive Farming** and any optional Smart Secret Farming settings.
- Gem goals or reserved gem balances, if desired.
- **Index Collection** options.
- Optional **Discord webhook** notifications.
- Optional **screen dimming**.

You can start with the regular farming settings and adjust the more specialised options later.

### 5. Start farming

Click **Start** in the macro window or press **F4**.

The macro begins its selected workflow, switching between rolling, upgrades and rebirths as appropriate for your mode and configuration.

### 6. Pause or stop whenever you want

- Use **Pause** or **F5** to temporarily suspend the session.
- Change supported settings while paused, then **Resume** to continue.
- Use **Stop** or **F4** to end the session.

**Pause and Stop are different:** Pause keeps your current session, while Stop ends it. Starting again after Stop begins a new session with new session statistics.

---

## Controls

| Control | Action |
| :--- | :--- |
| **Start button** | Start a new macro session. |
| **Stop button** | End the current macro session. |
| **Pause / Resume** | Temporarily pause or continue the session. |
| **F4** | Start / Stop shortcut. |
| **F5** | Pause / Resume shortcut. |
| **F6** | Toggle debug mode. |
| **F7** | Capture a diagnostic screenshot. |

The main day-to-day controls are **Start**, **Stop**, **Pause** and **Resume**. The extra shortcuts are available for diagnostics.

---

## Settings & modes

### Picking a rebirth target

When you use standard farming mode, you can choose **As Soon As Eligible** or select a specific rarity starting from **Mythic**. Targets include high-end rarities such as **Secret**, **Forbidden** and **Omega**, with the available selection based on the current rebirth requirement.

A lower target generally focuses on more frequent rebirths; a higher target focuses on waiting for a rarer result before rebirthing.

### Hunter Mode vs. regular farming

The simplest way to choose is to ask yourself what you want from the session:

- **Want rebirths and gems?** Use standard farming.
- **Want to hunt rare auras without rebirthing?** Use Hunter Mode.

Both modes can make use of upgrade automation and other supported progression options.

### Choosing upgrade behaviour

Speed upgrades are generally prioritised first, followed by affordable Luck upgrades. The macro also handles coin-based Luck purchases at higher levels and can return to rolling while saving up coins.

You can use Adaptive Farming and other goal settings to change how progression is managed.

### Screen and monitor settings

The macro normally uses the Windows primary display to find the Roblox interface. Supported resolution presets include **1080p**, **1440p** and **4K**.

If you enable screen dimming, the dimmer covers connected monitors rather than only the game display. **Borderless/windowed fullscreen** is the recommended display mode when using dimming.

### Changing settings mid-session

To change a supported setting while farming:

1. Press **Pause** or **F5**.
2. Update the setting in the macro window.
3. Press **Resume** or **F5**.

The session continues with the updated configuration.

---

## 🔔 Setting up Discord notifications

Discord notifications are optional. They let you see key session updates from a channel you choose, including when you're away from the PC.

1. Open Discord and go to a server where you can create webhooks.
2. Open **Server Settings → Integrations → Webhooks** (the exact menu can vary).
3. Create a webhook for the channel you want to use.
4. Copy its **webhook URL**.
5. Paste the URL into the webhook setting in Dan RNG Autopilot.
6. Save your settings and enable the notifications you want.

**Keep the webhook URL private.** Anyone with that URL may be able to post messages to your channel.

---

## 🧠 How the macro works (roughly)

Dan RNG Autopilot uses **screen-based automation**. It looks at the game's interface, recognises relevant menus and values, and uses mouse and keyboard input to carry out the selected tasks.

It doesn't need you to manually complete every rebirth or upgrade cycle.

### Standard farming loop

```text
Start session
    ↓
Read the current game interface
    ↓
Check progression and available upgrades
    ↓
Purchase suitable Speed / Luck upgrades
    ↓
Continue rolling
    ↓
Check selected rebirth target
    ↓
Rebirth when the target is met
    ↓
Update session information
    ↓
Repeat
```

### Hunter Mode loop

```text
Start session
    ↓
Check upgrades and optional goals
    ↓
Roll for auras
    ↓
Check whether more upgrades are affordable
    ↓
Return to rolling
    ↓
Repeat — without rebirthing
```

The macro also keeps track of other events during either loop, including rare-roll animations, Index tasks, anti-AFK activity, optional screen dimming and Discord notifications.

### What happens when I press Stop?

Stopping ends the current session. The macro closes out the session information, removes its optional screen-dimming overlays and can send a Discord session summary if notifications are enabled.

The next time you press Start, it begins a new session.

---

## ❓ Frequently asked questions

<details>
<summary><strong>Do I need to install Python?</strong></summary>

No. The macro is distributed as a Windows `.exe`, so you can download and launch the application directly.

</details>

<details>
<summary><strong>Does Hunter Mode rebirth?</strong></summary>

No. Hunter Mode focuses on rolling, collecting auras and managing upgrades without rebirthing.

</details>

<details>
<summary><strong>Can I choose a specific rarity to rebirth at?</strong></summary>

Yes. Choose **As Soon As Eligible** or a supported rarity from **Mythic** upward, including **Omega**. The target list reflects the current rebirth requirement.

</details>

<details>
<summary><strong>Will it automatically upgrade Speed and Luck?</strong></summary>

Yes. The standard upgrade order prioritises Speed until maxed or blocked, then affordable Luck. At Luck 1000+, the macro also uses the displayed coin balance and upgrade costs to manage purchases up to level 1100.

</details>

<details>
<summary><strong>Can I change settings without starting a new session?</strong></summary>

Yes. Pause the macro, change the supported settings, and Resume. Stop ends the current session completely.

</details>

<details>
<summary><strong>Can I use it on a second monitor?</strong></summary>

The macro targets the display set as **primary** in Windows. That display can be labelled Monitor 1 or Monitor 2 in your Windows settings.

</details>

<details>
<summary><strong>What does screen dimming do?</strong></summary>

It darkens all connected monitors by around **80%** during farming using click-through overlays, without changing your usual Windows gamma calibration. The overlays are removed when the macro stops or exits.

</details>

<details>
<summary><strong>Can Discord control my macro?</strong></summary>

No. The Discord webhook feature sends notifications to your selected channel. It isn't a remote-control system.

</details>

<details>
<summary><strong>Where can I report a bug or ask for help?</strong></summary>

Contact **@resentenced on Discord**. Include the macro version and a brief explanation of the issue. Screenshots can help if they're relevant.

</details>

---

## 🆕 R1.6.2 feature highlights

**R1.6.2** includes the updated screen-dimming system alongside the farming features from previous versions.

| Version | Main additions |
| :--- | :--- |
| **R1.6.2** | All-monitor overlay dimming, smooth transitions, click-through input and automatic overlay removal. |
| **R1.6.1** | Hunter Mode navigation improvements, coin-based Luck upgrades, higher rebirth targets including Omega and inactivity-based anti-AFK. |
| **R1.6** | Hunter Mode, more configurable progression goals, adaptive farming and session-management features. |

For individual release details, see the notes on the GitHub **Releases** page.

---

## 💬 Support & bug reports

If you have **any questions, issues, bugs or suggestions**, you can contact me directly on Discord:

### **Discord: `@resentenced`**

When reporting a bug, please include the **version you're using**, what happened and any useful screenshots or log messages. Please remove any private information, such as your Discord webhook URL, before sending them.

---

## ⚠️ Disclaimer

**I made this project with the help of AI.** I use AI tools to help write, improve and maintain the macro, while I decide on its features, direction and how I want it to behave.

Dan RNG Autopilot is an **unofficial third-party automation tool**. It is not affiliated with, endorsed by or supported by Roblox or the developers of Dan RNG. Make sure you understand the relevant game rules and Roblox policies before using automation.

---

<div align="center">

### 🎲 Dan RNG Autopilot

*Less repetitive clicking. More time for the parts of Dan RNG you care about.*

**Questions or bugs? Discord: `@resentenced`**

</div>
