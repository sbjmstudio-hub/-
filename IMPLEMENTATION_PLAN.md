# WIRZA v3 - 54 Module Plan

## Current direction
The original 93-module plan has been reduced to 55 independent modules.
The 38 deleted modules are listed in REMOVED_MODULES.md.

## Common systems
- Independent module ON/OFF
- Per-module settings
- HUD position / scale / opacity / background foundation
- HUD editor
- Profile save / load / delete
- D3D12 in-game renderer
- OBS Game Capture oriented rendering
- Minecraft version diagnostics
- Safe unsupported-build handling
- Settings persistence

## Implemented now
- FPS
- CPS
- Keystrokes
- Clock
- Crosshair
- Memory Usage
- Playtime
- Stopwatch
- Zoom

## Partial
- FOV

## Next data-backed modules
- Armor Status
- Direction HUD
- Item Counter
- Ping
- Potion Effects
- Reach Display (display only)
- Server Address
- Totem Counter
- WAILA
- Potion Counter
- Horse Stats

## Next visual/UI modules
- 2D Items
- Block Outline
- Boss Bar
- Chat Mod
- Color Saturation
- Damage Tint
- Fog / Fog Customizer
- Glint Colorizer
- GUI Scale
- Hit Color
- Item Customizer
- Item Physics
- Lighting
- Menu Blur
- Motion Blur
- Nick Hider
- 1.7 Visuals
- Overlay Mod
- Pack Display
- Pack Organizer
- Particle Changer
- Scoreboard
- Scrollable Tooltips
- Shields
- Shiny Pots
- Titles
- Waypoints

## Utility / larger modules that remain
- Auto Text Actions
- Auto Text Hotkey
- Kill Sounds
- Radio / Lunar FM
- Screenshot / Screenshot Uploader
- Toggle Sneak / Toggle Sprint

## Important
A module is only marked Implemented when real Bedrock code exists.
Deleted modules must not be silently re-added.


## Alpha 2 completed
- Read-only Game Data Bridge
- Direction HUD connected
- Item Counter connected
- Totem Counter connected
- Potion Counter connected
- Game Data status shown in WIRZA menu
- Smooth native Zoom
- C + mouse-wheel Zoom FOV adjustment

## Next bridge batch
- Armor Status
- Potion Effects
- Ping
- Server Address
- Reach Display (display only)
- WAILA
- Horse Stats


## Alpha 3 completed in source
- Armor Status bridge
- Passive Ping capture
- Server Address bridge
- Reach Display successful-attack measurement (display only)
- WAILA real target bridge (block complete, entity partial)
- Horse target detection
- Potion Effects capability gate

## Alpha 4 candidate
Renderer/UI modules:
- Block Outline
- Color Saturation
- Damage Tint
- Fog Customizer
- Glint Colorizer
- Hit Color
- Lighting
- Menu Blur
- Motion Blur
- Particle Changer
- Overlay Mod
- 1.7 Visuals
- Item Customizer
- Shields
- Shiny Pots


## Alpha 4A completed in source
- Block Outline: projected current-target block box (Partial)
- Motion Blur: one-frame D3D12 temporal history blend (Partial)
- Lighting: screen-space brightness approximation (Partial)
- Menu Blur: configurable dim/haze fallback (Partial)

Next Alpha 4 batch should prioritize render hooks that can be version-gated cleanly, without guessing ABI/offsets.


## Alpha 4B completed in source
- Color Saturation: D3D12 fullscreen post-process for saturation / contrast / brightness (Partial)
- Color correction is applied to Minecraft before WIRZA HUD/menu drawing

## Alpha 4C completed in source
- Added FirstPersonRenderBridge common adapter
- Item Customizer: scale / X / Y / rotation transform logic (Partial)
- Shields: shield-only scale / X / Y transform logic (Partial)
- 1.7 Visuals: local visual swing / sword-block pose / scale logic (Partial)
- Added thread-safe held-item identifier cache for render-time classification
- Added exact-version SignatureProfiles allow-list
- No wildcard or guessed first-person signature fallback

The current first-person verified-profile list is intentionally empty until a real Minecraft for Windows executable can be inspected and tested. These three modules therefore stay Partial and safely no-op on an unverified build.

Next Alpha 4 batch after a runtime-profile checkpoint:
- Glint Colorizer + Shiny Pots
- Damage Tint + Hit Color
- Overlay Mod + Fog Customizer
- Particle Changer


## v3.4 Alpha 4D
- Added ItemMaterialRenderBridge with strict exact-build activation.
- Glint Colorizer and Shiny Pots visual policies are now wired as Partial.
- No guessed material signature was added; MaterialSignatureProfiles.h remains empty until Windows real-build verification.
- Next visual batch: Damage Tint + Hit Color.


## v3.4 Alpha 4E
- Added local minecraft:health (attribute ID 7) observation to GameDataBridge.
- Damage Tint now records health decreases and renders a configurable timed screen tint before WIRZA HUD/menu.
- Added recent attacked-target Actor/entity-id tracking to the existing passive Actor::attack hook.
- Added ActorOverlayRenderBridge and strict ActorOverlaySignatureProfiles allow-list for Hit Color.
- Hit Color now has color, strength, and duration settings.
- No guessed actor-overlay signature/actor offset was added; the verified profile list is intentionally empty until real Windows build verification.
- Alpha 4F target: Overlay Mod + Fog Customizer (completed in source below).


## v3.4 Alpha 4F
- Added EnvironmentRenderBridge with strict exact-build activation.
- Fog / Fog Customizer is now wired as Partial: configurable fog RGB plus density/start scaling policy.
- Overlay Mod is now wired as Partial: separate fire, water and in-block opacity multipliers.
- EnvironmentRenderSignatureProfiles.h is intentionally empty; no current-build signature, fog-state offset or overlay ABI was guessed.
- Public Bedrock client code was used only to verify the fog-render design concept; no external signature was activated in WIRZA.
- Next visual batch: Particle Changer.


## Alpha 4G — Remaining UI / Utility batch (source complete, runtime validation pending)

Screenshot was explicitly excluded by user request and remains Planned.

Moved to Partial in this batch:
- Particle Changer — render policy (amount/size/color) + exact-build ExtendedFeatureBridge contract.
- Scoreboard — HUD renderer + snapshot contract.
- Boss Bar — HUD renderer + progress/color contract.
- Chat Mod — HUD renderer with timestamps + snapshot contract.
- Titles — configurable WIRZA title renderer + snapshot contract.
- Scrollable Tooltips — exact-build adapter slot reserved; no guessed tooltip ABI.
- Pack Display — HUD renderer + pack-name snapshot contract.
- Waypoints — local coordinate parser and world-to-screen markers/beams using GameDataBridge camera data.
- Radio / Lunar FM — Windows Media Foundation URL playback, volume, autoplay, play/stop controls.
- Toggle Sneak / Toggle Sprint — Windows-message key latch with safe release on WIRZA menu entry; Raw Input builds still require validation.

No unverified Minecraft offsets/signatures were added. The ExtendedFeatureBridge verified profile list is intentionally empty until exact executable testing.


## Alpha 4G extension — registry cleanup after recount
A recount found nine Planned modules that had been omitted from the earlier conversational remaining-count summary. They are included in the same source batch instead of leaving hidden Planned work:
- 2D Items
- Auto Text Actions
- Auto Text Hotkey
- GUI Scale
- Item Physics
- Kill Sounds
- Momentum
- Nick Hider
- Pack Organizer

All nine are now Partial. Screenshot remains the only Planned module and is intentionally skipped.


## v3.4 Memory Write + OBS Game Capture integration — completed in source
- Added `MemoryWriteBridge` as the single policy boundary for local visual/UI Minecraft state changes.
- FOV / Zoom now use a guarded `LevelRendererPlayer::getFov` hook with smooth camera FOV handling and hand-projection preservation.
- GUI Scale now performs reversible `GuiData` scale/reciprocal/size writes only after pointer, value-range, and writable-page validation.
- Lighting now prefers a native `Options::getGamma` hook and falls back to the existing D3D12 brightness overlay when unavailable.
- FOV, Gamma, and GuiData activation are independent; failure of one path does not disable the others.
- D3D12 renderer verifies the swapchain window belongs to the current Minecraft process.
- Launcher detects OBS Game Capture's `graphics-hook` when OBS is already running and delays WIRZA loading briefly to improve capture hook ordering.
- WIRZA HUD/menu remain in Minecraft's own D3D12 frame, so no separate overlay window is required for OBS Game Capture.
- Explicitly excluded from memory writes: reach, damage, attack rate, movement speed, knockback, inventory, network packets, anti-cheat bypass/evasion.
- Source registry state after Auto GG revision: 20 Implemented / 33 Partial / 1 Planned (Screenshot only).

Runtime checkpoint still required:
1. GitHub Actions / MSVC x64 Release build.
2. Minecraft for Windows load test on the user's exact game build.
3. Verify FOV/gamma signatures and GuiData structural validation in diagnostics.
4. OBS Game Capture test with a source targeting Minecraft only; confirm WIRZA HUD/menu/post-process are present in the captured frame.
5. Convert remaining exact-build-gated Partial adapters only after their ABI/signatures are verified on that build.


## Auto GG / Hotkey removal revision

- Removed Auto Text Hotkey (original #7) from the active registry by user request.
- Replaced Auto Text Actions (original #6) with Auto GG.
- Auto GG observes verified Title/Chat result snapshots for strong self-victory phrases and sends one fixed `gg` through the vanilla chat UI.
- One-shot round latch prevents repeated sends from a persistent result screen; it re-arms only after victory evidence clears.
- Hive Server Safe Mode allows Auto GG because Hive's official allow-list explicitly includes Auto GG.
- CubeCraft/Lifeboat/MegaSMP/unknown multiplayer keep Auto GG disabled conservatively.
- Active registry count is now 54: 20 Implemented / 33 Partial / 1 Planned.
