<p align="center">
  <img src="https://files.catbox.moe/sdy49y.png" alt="Cube-X icon" width="160" />
</p>

<h1 align="center">Cube-X</h1>

<p align="center">
  A modern in-game menu for <strong>PEAK</strong>, loadable through BepInEx, with two polished interfaces — a classic drill-down list menu and a click-style window GUI — plus a full protection suite, Steam-aware player tools, host controls, visual tools, quality-of-life features, and performance-focused rendering options.
</p>

---

## Overview

Cube-X is designed as a full-featured PEAK menu with a clean interface, organized submenus, cached UI data where
practical, and game-aware actions that prefer existing in-game behavior over fragile shortcuts.

The menu includes features and actions across the main pages, covering player controls,
protections, lobby tools, friends, achievements, visuals, world interaction, spawning, inventory management, search
utilities, Discord access, notifications, keybinds, and menu settings.

Every feature can be driven from either of two interchangeable front-ends, switchable at any time from **Settings > Appearance > Click GUI**.

---

<p align="center">
  <img src="https://files.catbox.moe/n1a6h4.png" alt="Cube-X classic list menu" height="440" />
  &nbsp;&nbsp;
  <img src="https://files.catbox.moe/by3f8b.png" alt="Cube-X Click GUI window interface" height="440" />
</p>

<p align="center">
  <em>Classic drill-down list menu (left) and the new Click GUI window interface (right) — both drive the exact same features.</em>
</p>

---

## Interface

### Classic List Menu

A compact GTA-style drill-down menu built for quick keyboard/controller navigation during gameplay.

| UI Area       | What It Does                                                                                              |
|---------------|-----------------------------------------------------------------------------------------------------------|
| Header        | Menu identity. Can drag menu position.                                                                    |
| Breadcrumbs   | Shows where you are inside nested submenus.                                                               |
| Feature Rows  | Toggle actions, buttons, numbers, colors, text values, and nested pages.                                  |
| Right Panel   | Shows selected-player context, Steam avatars, tags, status, and profile details where available.          |
| Footer        | Shows navigation hints, current selection state, and keybind information.                                 |
| Notifications | Uses a clean rectangular notification style with title, description, accent strip, and dismiss timer bar. |
| Color Picker  | Applies selected colors only after the picker is accepted or closed.                                      |
| Keybinds      | Lets features be bound, listed, and removed individually from the settings menu.                          |

### Click GUI

A mouse-driven window interface with the same features as the classic menu.

| UI Area             | What It Does                                                                   |
|---------------------|--------------------------------------------------------------------------------|
| Sidebar Tabs        | One icon tab per menu page for instant switching.                              |
| Group Boxes         | Two-column category panels with checkboxes, sliders, and buttons.              |
| Expandable Submenus | Nested feature groups expand in place inside their panel.                      |
| Draggable Window    | Drag the header to reposition the whole window.                                |
| Input Capture       | Gameplay controls are blocked while the window is open or while typing.        |
| Shared State        | Uses the same features, config, keybinds, and saved state as the classic menu. |

Default navigation is keyboard-first in the classic menu and mouse-first in the Click GUI; both can be customized from
the settings pages.

---

## Protections

Cube-X includes **29 protection entries** under **Self > Protections**, organized into five categories.
Each entry displays its scope so you can distinguish local blocking, local repairs, detection, and host-only actions.

| Category | Protection | Scope | Detects / Blocks |
|---|---|---|---|
| **Crash Events** | Attack Others | Host/Master Local Block + Host Kick | Kill, zombify, or pass-out RPCs sent to another scout by a non-owner. Detected and blocked only when you are host. |
| **Crash Events** | Destroy My Objects | Local Block | Destroy and ownership-transfer events targeting your player objects. |
| **Crash Events** | Destroy Others | Local Block + Host Kick | Destroy or player-wipe events targeting another scout. As host, the attacker is kicked when Kick is on. |
| **Crash Events** | Event Spam | Local Block | High-rate Photon events that can destabilize, lag, or crash the session. |
| **Crash Events** | Invalid Body Sync | Local Repair | Repairs non-finite body positions, velocities, look values and movement data before they reach physics and the stored interpolation state. Never changes another client's state. |
| **Crash Events** | Kill My Scout | Local Block | Death, kill, and zombify RPCs targeting your scout from a non-owner sender. |
| **Crash Events** | Malformed Sync Data | Local Block | Rejects truncated, oversized, invalid-count or non-finite status, affliction, thorn, inventory, run-setting and map-item sync data before PEAK deserializes it. |
| **Crash Events** | Spam Timeout | Opt-in Local Block (30s, per player) | Disabled by default. When Block Event is enabled, players who keep triggering spam protections (crash, RPC, event, sync, malformed, or spawn spam) are counted per sender. After 30 or more full spam detections in a short window, all events and sync traffic from that player are blocked locally for 30 seconds, lifted automatically, and re-applied if the spam continues. Short network bursts never trip this on their own. |
| **Modded Events** | Balloon Abuse | Local Block | Rejects invalid balloon colours or heights and balloons attached to another scout by a non-host. Owner replay on joining remains allowed. |
| **Modded Events** | Buildable Abuse | Local Block | Rejects building with someone else's item, invalid placement data, and more than 20 live build requests per minute. Buffered replay on joining is excluded from the rate limit. |
| **Modded Events** | Explosive Spam | Local Block | Blocks repeated dynamite, beehive/bee-swarm, blowdart-hit, and sunscreen effects. Locally removes the offending dynamite, dart source, or bee objects when blocked. |
| **Modded Events** | Forged Inventory | Local Block / Host Inventory Authority | Outside join/reconnect sync, rejects inventory broadcasts from non-hosts and forced inventories without a nearby backpack swap. Swap checks preserve ordinary item IDs and instance GUIDs, and require an observed backpack release before accepting its transfer. |
| **Modded Events** | Hidden Body | Local Repair | Reveals scouts sent below -5000 metres using their finite ground or climb position. This is a heuristic and does not automatically kick or blacklist anyone. |
| **Modded Events** | Illegal Cloning | Host Request Block | Rejects clone requests without a held cloning amulet, outside its reach, or targeting non-cloneable items. Only the host creates clones. |
| **Modded Events** | Item Injection | Local Block | Unauthorized item spawns or inventory syncs targeting your hand or slots. |
| **Modded Events** | Spawn In Hands | Host Request Block | As host, rejects remote spawn-in-hand requests except the airport passport and the configured Grapple start item. Local host spawns stay allowed. |
| **Modded Events** | Suspicious Prefab | Local Block | Non-vanilla network prefab instantiation from remote clients. |
| **RPC** | Crab Affliction | Local Block + Host Kick | The Crab status is not used anywhere in PEAK, so any attempt to apply it is a mod injection. Incoming Crab is stripped locally while every legitimate status in the same sync still applies. As host, enabling Kick also removes the sender so they cannot crab anyone else. |
| **RPC** | Forced Actions | Local Block | Forced falls, pass-outs, teleports, slips, and other control RPCs targeting your scout. |
| **RPC** | Inventory Manipulation | Local Block | Remote inventory, slot, held-item, and pickup RPCs targeting your scout. |
| **RPC** | Player Kicks | Opt-in Local Block | Disabled by default. Locally ignores another scout's kick animation and its immediate fall/force effects against you. Does not affect lobby removal or send recovery RPCs. |
| **RPC** | RPC Spam | Local Block | Excessive repeated RPCs from the same sender in a short window. |
| **RPC** | Unrequested Pickups | Local Block + Local Inventory Cleanup | Rejects pickup acknowledgements for your scout when you made no recent pickup or item-use request. Join/reconnect sync is exempt. A host-relayed spawn cannot identify the original requester, so it never automatically punishes the host. |
| **RPC** | Unwanted Carry | Local Block | Locally blocks other players from carrying your living scout, impersonating another carrier, or starting a carry from more than eight metres away. Legitimate nearby rescues while dead or fully passed out remain allowed. It never sends a drop RPC or changes another client's carry state. |
| **Host** | Ascent Change | Local Block + Host Re-sync + Host Kick | Ascent difficulty changes sent by a player who is not the current host. Blocked locally; as host, the correct ascent is re-synced to all scouts after a blocked attempt. Authorization follows host migration automatically. |
| **Host** | Fake Host Authority | Host/Master Authority Block + Host Kick | Non-master clients sending expedition, world-state, fog, or end-game control RPCs. |
| **Host** | Host Takeover | Reclaim Your Host | Reclaims host when an identified remote sender takes it from you without your transfer. Legitimate host departure and transfers made by the current host remain allowed. Photon applies the change before it can be reclaimed. |
| **Cheaters** | Identity Spoof | Detection only; no automatic punishment | Reports duplicate Photon user IDs, platform identity mismatches, shared display names, and Steam profile names that differ from in-game nicknames; these do not establish who spoofed whom. |
| **Cheaters** | Known Cheaters | Detect + Local Blacklist + Host Kick | Atlas/Cherry/PEAK-MX-tagged clients. Add to Blacklist auto-blacklists them; Kick auto-kicks as host. |

### Per-Protection Controls

Protection entries expose six controls. Their effect depends on the entry's scope; detection-only and local-repair entries do not necessarily support automatic punishment:

| Control              | Behavior                                                    |
|----------------------|-------------------------------------------------------------|
| **Notify**           | Shows an in-game notification when the protection triggers. |
| **Block**            | Blocks the hostile event within the labeled scope.          |
| **Log**              | Writes the event to the Cube-X protection log.              |
| **Announce in Chat** | Announces the detection in the in-game text chat.           |
| **Add to Blacklist** | Adds the offender to your local blacklist.                  |
| **Host Kick**        | Kicks the offender when you are the host/master client.     |

### Suite Controls

| Control                      | Behavior                                                                                                      |
|------------------------------|---------------------------------------------------------------------------------------------------------------|
| **Enable All / Disable All** | Enables or disables the suite. Enable All leaves chat announcements and host kicks off; only Known Cheaters keeps automatic blacklist adds on.                                                             |
| **Learn Mode**               | Observes and logs without blocking, useful for tuning.                                                        |
| **Protection Log**           | Written to `%APPDATA%\CubeX\Peak\Log.txt`.                                                                    |
| **Kick Notice**              | Host-side protection kicks replace the native leave notice with `"{Name} has been kicked! Reason: {reason}"`. |

**Local Block** and **Local Repair** affect your client. Host-only checks require you to be the room's
host/master client, and optional host kicks require the matching control. Hidden Body and Identity Spoof
never automatically kick or blacklist players. Player Kicks blocks local kick-animation effects when enabled;
it does not prevent removal from a lobby. Player Kicks and Spam Timeout are disabled by default.

Join/reconnect sync, legitimate nearby rescues, inventory replication, and normal host transfers have dedicated
exceptions. **Learn Mode** observes and logs without blocking.

---

## Feature Map

### Self

- **Local Safety:** God Mode, No Fall Damage, No Ragdoll, No Slip, No Passout, and No Screen Shake.
- **Movement:** Infinite Stamina/Jump, flight speed and acceleration, Noclip, player collision control,
  and speed, sprint, jump, climb, vine and rope multipliers.
- **Camera:** Free Cam with speed, sprint, smoothing and sensitivity controls; FOV, third-person distance/height,
  and hold-to-zoom controls.
- **Body Part Actions:** Display Full Body, Reach Distance, Pull Distance, Infinite Emote, and Kick Animation.
- **Items:** easy backpack access, removed item restrictions, infinite charges/rope/jetpack fuel/rescue-hook range,
  instant item use and throwing, and custom throw power.
- **Rocketpack:** fire/stop controls, fuse time, infinite flight, impact survival, Infinite Rocketpack,
  wheel controls, and Rocketpack HUD.
- **Glider:** Infinite Glider and adjustable Drag Multiplier.
- **Afflictions:** apply or clear individual afflictions, freeze/disable afflictions, remove weight,
  and tune global/per-affliction charge and drain rates plus stamina refill/use rates.
- **Actions:** kill, slip, fall, pass out, revive, restore stamina/morale, and end-game actions.
- **Entity Control:** Big Ghost, Chicken, Scoutmaster, and Zombie modes.
- **Miscellaneous:** Aura Farm with an item selector, Deaggro Bees, and Cosmetic Spam.

### Network

- **Players:** live list with scout-color indicators, platform identity, alphabetical/actor-ID sorting,
  selectable info panels, Steam profiles, blacklist actions, and player context.
- **Spectate:** native orbit and zoom, plus a draggable, resizable Picture-in-Picture window with adjustable FOV.
- **Player actions:** teleport to/from a selected player, revive/revive teleport, revive with statuses,
  restore stamina, unpass out, Carry and Dismount Carry. Carry teleports a target to you first when at least eight metres away.
- **All Players:** exclude-self selection, automatic/bulk revival, unpass out, stamina recovery,
  teleport-to-me, and character-weight refresh where authority permits.
- **Recent Players, Blacklist and Friends:** search/sorting where available, notes, profile links,
  Steam invites, saved lobby joining, and copyable player/lobby details.
- **Profile:** edit or reset your nickname, apply a uniform name color, edit per-letter colors,
  or reset colors to the game's defaults. Applied colors survive renaming and rejoining.
- **Connection:** leave/rejoin, copy a join link, and inspect current lobby details.
- **Steam Join Link:** enter a Steam link, lobby ID, or PEAK room code; inspect available lobby details and use
  **Join From Link / Code**. Room-code, link, invite, friend and rejoin flows coordinate region changes automatically.
- **Voice Chat:** disable voice filtering, hear passed-out players, repair/reconnect voice, and inspect voice status.
- **Text Chat:** avatars, timestamps, rich text, font size, opacity, scale, fade delay and history controls.
  Outgoing chat uses encrypted payloads and stays out of the room event cache.
- **Achievements:** unlock/reset all achievements or manage individual entries.

### Host

- **Ascent:** choose and apply difficulty during an expedition.
- **Biome:** PEAK Map Picker with daily/random maps and a cached catalog with biome summaries;
  Terrain Customizer with per-segment biome filters.
- **More Scouts:** player limits, extra campfire food, food per extra scout, spare bundles,
  late-join revival and anti-fling controls.
- **Lobby Control:** Steam lobby locking, return to airport, teleport all to you, ghost targeting,
  refresh character weights, skip the end screen, and Host Only Kiosk.

Host and other authority-sensitive actions require the authority indicated by the feature and current game state.

### Visuals

- **ESP:** players, food, items, luggage, ghosts, hazards and bell towers, with boxes, lines, info,
  glow, per-type colors, maximum distance/target limits, and refresh delay.
- **Profile Cards & Awareness:** stamina bars, card distance/scale, downed-player awareness,
  and a player-status HUD with count/range controls.
- **Effects:** player trails and footsteps with lifetime, width/size and exclude-self options;
  item/luggage world tags and item trails.
- **Throw Preview:** projectile paths, landing previews and activation previews.

### World

- **Sky, Rain, Sun & Moon:** visibility, colors, rain intensity, fog control, and scene-default resets.
- **Environment:** wind toggles, lava/fog actions, icicle/bridge shaking and dropping, piton breaking,
  rope detachment, and bugle sound control.
- **Props & Camp Lighting:** flare lighting, Scoutmaster throw actions, guidebook page controls,
  lanterns, and nearby campfire lighting/extinguishing.
- **Luggage:** refresh containers, open nearby/all luggage, open without spawning items,
  and inspect individual containers.
- **Mouse Tools & Pings:** shared ping-pointer controls, mouse-click blowdarts, ping distance/scale and Ghost Ping.

### Teleport

Current biome start, saved XYZ coordinates, nearest campfire/luggage, a refreshable scene campfire list,
selected/nearest players, automatic teleport-to-ping, look-point teleport, and return to your last position.

### Spawn & Items

- **Spawn > Items:** searchable cached item catalog, spawn selected items, and spawn into an empty slot.
- **Spawn > Item Tools:** remove all/your items, freeze/unfreeze, spin, cook/finish cooking,
  smoke toggles, and deny-pickup controls. Remove My Items targets only items explicitly assigned to you.
- **Spawn > Guns:** Aimbot, Gravity Gun, Delete Gun, and Draw With Selected Item.
- **Spawn > Objects:** spawned-object management, quick Scoutmaster/MushroomZombie/PlayerGhost/Tornado spawns,
  tornado removal, and spawned-object cleanup.
- **Items:** held-item stats and cooking, searchable slot assignment, slot recharge/cooking,
  backpack type/assignment and contents, and extra-slot tools.

Networked deletion respects ownership and waits for transferable control when required; cleanup can depend on host
or object authority.

### Performance

- **Frame Rate:** performance presets, target FPS, and frame-pacing restoration after changing focus.
- **Rendering:** render distance, LOD bias, texture mipmap limit, post-processing/grass/mirror toggles,
  and simplified menu layout.
- **World Entities:** distant mob sleep, rigid-body state coalescing, simplified items, minimal explosion particles,
  and dead-scout physics controls.
- **Remote Characters:** automatic crowd optimization, simplified skinning, ragdoll update/speed guards,
  and near/medium/far update tuning.
- **Wind Simulation & Runtime:** local-only character wind, item wind control, runtime state safeguards,
  and redundant physics filtering.

### Misc, Search & Settings

- **Misc > Startup / Interface:** skip the intro, compact scrollable pause-menu player list with avatars/platform
  fallbacks, and remove the pause background.
- **Misc > Network:** Crossplay Network Fix prepares missing expedition map bundles to help prevent infinite loading;
  Use WSS Transport selects secure WebSockets for future gameplay/voice connections and requires reconnecting;
  Bypass Login Version Check bypasses login rejection without making different game versions compatible.
  WSS does not disable connection timeouts.
- **Misc > Notifications:** player lifecycle, host changes, in-game events/tags, protection detections,
  and keybind-toggle notifications. Discord community access is here too.
- **Search:** find menu features by name and jump to their location.
- **Settings > Config:** save/load, auto-save, auto-load on start, and custom saves.
- **Settings > Appearance / Layout:** Click GUI, accent color, UI scale, highlight speed, menu width,
  visible rows, breadcrumbs, descriptions, footer and scrollbar.
- **Settings > HUD & UI:** numerical HUD with altitude/afflictions, day/night time, scout count, watermark and cache alerts.
- **Settings > Keybinds:** menu bind, open-on-launch, and individual feature bindings.
  Replay Tutorial and Reset to Defaults are also available.

---

## Player Tags

Cube-X adds readable tags to player entries so status and context are easier to scan.

| Tag                  | Meaning                                                                                       |
|----------------------|-----------------------------------------------------------------------------------------------|
| **Friend**           | Player is recognized from the Steam friends list.                                             |
| **Blacklisted**      | Player exists in the local blacklist list.                                                    |
| **Recent**           | Player was recently seen.                                                                     |
| **Online / Offline** | Steam or game-aware presence state where available.                                           |
| **Name Spoof**       | In-room identity or nickname differs from the associated platform profile; a mismatch alone does not establish abuse.    |
| **{modname}**        | Player is using a known third-party mod/mod menu.                                             |
| **Modder**           | Player triggered a protected illegal network action and is not labeled as a known mod client. |

Name spoof detection is intended to apply only to players observed inside the current game or room, avoiding false
positives from stale recent-player or blacklist data.

---

## Achievements

The achievements page includes individual achievement controls and bulk actions.

| Action                  | Description                                                            |
|-------------------------|------------------------------------------------------------------------|
| **Unlock All**          | Unlocks achievements through the game-aware achievement flow.          |
| **Lock All**            | Resets achievement state where supported.                              |
| **Individual Entries**  | Lets achievements be managed one by one from the achievements submenu. |
| **Ascent Achievements** | Includes ascent-related achievements where supported by the game.     |

---

## Keybinds

Cube-X supports feature-level keybinds.

| Control                     | Behavior                                                       |
|-----------------------------|----------------------------------------------------------------|
| **Open Menu**               | Opens or closes the menu (either interface).                   |
| **Set Feature Keybind**     | Assigns a keybind to the hovered feature.                      |
| **Keybind List**            | Shows every assigned keybind as its own option.                |
| **Remove Selected Keybind** | Removes one selected keybind without clearing the entire list. |
| **Notify Keybind Toggles**  | Optional notification when a keybind toggles a feature.        |

Default controls:

| Input                      | Action                                                |
|----------------------------|-------------------------------------------------------|
| `Insert`                   | Open or close the menu.                               |
| `Arrow Up / Arrow Down`    | Move selection.                                       |
| `Enter`                    | Activate selected option.                             |
| `Backspace / Escape`       | Go back.                                              |
| `Arrow Left / Arrow Right` | Adjust values.                                        |
| `Shift + Enter`            | Edit compatible numeric/text values.                  |
| `F8`                       | Assign a keybind to the hovered feature.              |
| `D-pad Right + RB`         | Open or close the menu with a controller.             |
| `D-pad`                    | Move selection; left/right adjusts compatible values. |
| `A`                        | Activate selected option.                             |
| `B`                        | Go back, or close the menu from Home.                 |
| `Mouse`                    | Full navigation inside the Click GUI.                 |

---

## Notifications

Notifications use a modern scale-aware layout, redesigned in 2.0.0:

| Element      | Purpose                                                                          |
|--------------|----------------------------------------------------------------------------------|
| Main Rect    | Holds the notification content with adaptive width and border.                   |
| Accent Strip | One colored strip on the left side.                                              |
| Timer Bar    | Thin bar showing time until auto-dismiss.                                        |
| Title        | Short event name.                                                                |
| Description  | Clear action result or status message.                                           |
| Animations   | Smooth fade in/out with a brief flash on arrival; up to 15 stored notifications. |

Notification behavior can be adjusted from the notification submenu, including keybind toggle notifications.

---

## Performance Focus

Cube-X includes menu and game-facing performance work intended to reduce unnecessary frame cost.

| Area              | Approach                                                                                                                                    |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Menu Rows         | Organized and cached where practical to avoid rebuilding expensive UI state unnecessarily.                                                  |
| Player Data       | Steam avatars, tags, and player metadata are reused instead of being repeatedly fetched every frame.                                        |
| ESP               | Rendering is scoped to useful targets and avoids unnecessary object rendering where possible.                                               |
| Visual Effects    | Heavy visual options can be disabled or tuned from **Home > Performance**.                                                                  |
| Notifications     | Lightweight drawing style with minimal layout complexity.                                                                                   |
| Feature Pages     | Large menus are split into focused submenus to reduce clutter and scanning cost.                                                            |
| Ragdoll Physics   | Optional remote ragdoll velocity clamp prevents extreme physics spikes (70+ m/s) from destabilizing frame rate.                             |
| Runtime Safety    | Configurable state guards skip incomplete update frames, while exact no-op filters avoid redundant body-part physics writes.                |
| Character Queries | Uses native squared range checks; cached renderer hierarchies and optional two-bone skinning lower crowded-scene rendering cost. |
| Spawn Cache       | JSON-backed spawn item cache avoids rebuilding the item list every menu visit.                                                              |

Some actions still depend on live game state and must refresh while playing, especially player lists, lobby state,
online state, ESP targets, and world objects.

---

## Discord Community & Website

Cube-X includes a first-time prompt asking whether the user wants to join the Discord community server for Cube-X.

The link is also available in:

```text
Misc > Discord Community > Join Discord
```

Community link:

```text
https://discord.gg/cHmp58MqPf
```

Website link:

```text
https://cube-x-website.vercel.app
```

---

## Notes

Cube-X is built for PEAK modding and testing workflows. Game updates may change internal behavior, player data,
achievements, networking, or object layouts, so some features may need updates after PEAK patches.

Use responsibly and preferably in private, modded, or trusted lobbies.

Cube-X is not affiliated with PEAK, Landfall, Aggro Crab, Steam, Photon, BepInEx, or any related official project/Mods.

Developed only by: **Mister9982**
