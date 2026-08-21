# WIRZA v3 - 54 Module Implementation Matrix

The user removed 39 modules from the original 93-feature plan.
The original number is kept here only as a reference.

Legend:
- Implemented = real working code in this source
- Partial = some working functionality remains to be completed
- Planned = registered independently, not yet wired to Minecraft

1. 2D Items — Partial (original #1)
2. Armor Status — Implemented (original #3)
3. Auto GG — Partial (original #6; victory-result observer + one-shot vanilla-chat gg sender; exact current-build title/chat adapter still required)
4. Block Outline — Partial (original #8)
5. Boss Bar — Partial (original #9)
6. Chat Mod — Partial (original #10)
7. Timer — Implemented (original #12; countdown timer; Clock removed by user request)
8. Color Saturation — Partial (original #13)
9. CPS — Implemented (original #17)
10. Crosshair — Implemented (original #18)
11. Damage Tint — Partial (original #19; read-only minecraft:health drop detector + timed D3D12/ImGui screen tint; absorption-only damage/runtime verification remain)
12. Direction HUD — Implemented (original #21)
13. Fog / Fog Customizer — Partial (original #23; fog-color + density/start policy wired through EnvironmentRenderBridge; exact current-build environment signature/offset profile required)
14. FOV — Implemented (original #24; guarded LevelRendererPlayer::getFov hook, smooth Zoom/FOV policy, vanilla hand projection preserved; Windows runtime validation pending)
15. FPS — Implemented (original #25)
16. Glint Colorizer — Partial (original #27; material-pass color policy ready, verified item/material signature profile required)
17. GUI Scale — Implemented (original #28; guarded/reversible GuiData scale + reciprocal + size writes, optional WIRZA-HUD-only mode; Windows runtime validation pending)
18. Hit Color — Partial (original #30; recent attacked-entity tracking + actor overlay color policy ready; exact current-build actor-overlay signature profile required)
19. Horse Stats — Partial (original #31)
20. Item Counter — Implemented (original #36; persistent discovered-item history + multi-select per-item counters)
21. Item Customizer — Partial (original #37; transform logic ready, verified first-person signature profile required)
22. Item Physics — Partial (original #38)
23. Keystrokes — Implemented (original #40)
24. Kill Sounds — Partial (original #41)
25. Lighting — Implemented (original #42; native Options::getGamma hook when signature matches, D3D12 brightness fallback otherwise; Windows runtime validation pending)
26. Memory Usage — Implemented (original #44)
27. Menu Blur — Partial (original #45)
28. Momentum — Partial (original #48)
29. Motion Blur — Partial (original #49)
30. Nick Hider — Partial (original #52)
31. 1.7 Visuals — Partial (original #53; local swing/block pose logic ready, verified first-person signature profile required)
32. Overlay Mod — Partial (original #54; fire/water/in-block opacity policy wired through EnvironmentRenderBridge; exact current-build overlay signature/ABI profile required)
33. Pack Display — Partial (original #55)
34. Pack Organizer — Partial (original #56)
35. Particle Changer — Partial (original #57)
36. Ping — Implemented (original #58)
37. Playtime — Implemented (original #59)
38. Potion Effects — Partial (original #60)
39. Radio / Lunar FM — Partial (original #63)
40. Reach Display — Implemented (original #64)
41. Scoreboard — Partial (original #68)
42. Screenshot / Screenshot Uploader — Planned (original #69)
43. Scrollable Tooltips — Partial (original #70)
44. Server Address — Implemented (original #71)
45. Shields — Partial (original #72; shield-only transform logic ready, verified first-person signature profile required)
46. Shiny Pots — Partial (original #73; potion filter/glint-request policy ready, verified item/material signature profile required)
47. Stopwatch — Implemented (original #78)
48. Titles — Partial (original #83)
49. Toggle Sneak / Toggle Sprint — Partial (original #85)
50. Totem Counter — Implemented (original #86)
51. WAILA — Partial (original #87)
52. Waypoints — Partial (original #88)
53. Zoom — Implemented (original #91)
54. Potion Counter — Implemented (original #92)

## Configuration status
All 54 remaining modules now have independent configurable settings. Runtime status above remains separate and honest.

## v3.3 Game Data Bridge
Real read-only bridge connections added:
- Direction HUD: LocalPlayer ActorRotation
- Item Counter: LocalPlayer inventory item IDs/names
- Totem Counter: LocalPlayer inventory
- Potion Counter: LocalPlayer inventory

The bridge uses signature/layout validation and reports Unsupported/Waiting instead of guessing memory addresses.


## v3.4 Alpha 3 — Data Bridge Batch 2
Connected in source:
- Armor Status: ECS ActorEquipmentComponent -> armor inventory -> item durability
- Ping: passive RakPeer average-ping hook
- Server Address: PacketSender -> NetworkSystem -> RemoteConnector -> GameConnectionInfo
- Reach Display: passive Actor::attack hook + current HitResult distance; display-only
- WAILA: real current HitResult; block target is resolved through BlockSource. Entity target uses ray/AABB matching.
- Horse Stats: horse target detection is connected, but hidden movement/jump attribute IDs are intentionally not guessed.
- Potion Effects: UI/capability path exists, but current MobEffect live-data ABI has not been safely verified and remains unsupported.

No module changes attack range, packet contents, or movement speed.


## v3.4 Alpha 4A — Visual Batch 1
Connected in source:
- Block Outline (Partial)
  - Uses the verified current HitResult block origin and ray-start camera position.
  - Projects the target block AABB into the D3D12/ImGui frame.
  - Line width, color, and fill opacity are configurable.
  - Uses the current WIRZA zoom FOV modifier so the overlay follows Zoom.
  - Exact alignment still requires Windows/Minecraft runtime verification.
- Motion Blur (Partial)
  - Keeps two D3D12 history textures and blends the previous Minecraft frame.
  - Captures before WIRZA HUD/menu rendering, avoiding recursive HUD smear.
  - Strength is configurable. The existing multi-sample setting is reserved for a later multi-history pass.
- Lighting (historical Alpha 4A fallback)
  - The screen-space brightness/gamma approximation remains as a fallback.
  - The later Memory Write / OBS integration adds a native Options::getGamma hook when the current signature matches.
  - No block-light/world-state values are rewritten.
- Menu Blur (Partial)
  - Configurable menu dim/haze fallback is connected.
  - True sampled separable blur remains pending.

## v3.4 Alpha 4B — Color Post-process
Connected in source:
- Color Saturation (Partial)
  - D3D12 fullscreen post-process shader samples a copy of the current Minecraft backbuffer.
  - Saturation, contrast, and brightness are applied in the pixel shader.
  - The corrected frame is written before WIRZA HUD/menu drawing, so HUD colors are not modified.
  - Motion Blur history now captures the already color-corrected Minecraft frame, still before WIRZA HUD/menu.
  - No Minecraft offsets/signatures or server-visible state are touched.
  - Partial until Windows compile/runtime verification.

Alpha 4 visual list status:
- Particle Changer is now Partial through the ExtendedFeatureBridge policy contract.


## v3.4 Alpha 4D — Item / Material Visual Bridge
Connected in source:
- Glint Colorizer (Partial)
  - Shared ItemMaterialRenderBridge receives a verified pre-material-pass adapter context.
  - Configurable glint color, strength and animation speed modify local render parameters only.
  - The colorizer runs only when vanilla or WIRZA has requested a glint pass.
- Shiny Pots (Partial)
  - Potion-family item IDs request the normal local glint pass.
  - Shine color and strength are configurable; zero strength does not request extra glint.
  - No ItemStack/enchantment/inventory/network state is modified.
- MaterialSignatureProfiles.h is intentionally empty until an exact Minecraft for Windows build can be verified on a real Windows machine.


## v3.4 Alpha 4E — Combat Visuals
Connected in source:
- Damage Tint (Partial)
  - Reads the local player's `minecraft:health` attribute (ID 7) through the existing read-only ECS attribute bridge.
  - A health decrease records a local damage timestamp; the renderer draws a configurable full-screen tint with a quadratic fade.
  - The tint is drawn over Minecraft but before WIRZA HUD/menu, so WIRZA HUD colors stay unchanged.
  - No damage amount, health, packets or combat state are modified.
  - Absorption-only damage is not yet observable through the health-only path and Windows/Minecraft runtime verification remains pending.
- Hit Color (Partial)
  - The existing passive Actor::attack observation records the target Actor/entity id and timestamp.
  - ActorOverlayRenderBridge applies the configured color only to that recent target's render overlay.
  - ActorOverlaySignatureProfiles.h is intentionally empty until an exact Minecraft for Windows build, ABI and actor-pointer offset are verified.
  - No attack validity, reach, damage, invulnerability time or packets are changed.


## v3.4 Alpha 4F — Environment Visuals
Connected in source:
- Fog / Fog Customizer (Partial)
  - Added EnvironmentRenderBridge with an exact-build profile gate.
  - Fog color policy blends the configured RGB with the vanilla fog color while preserving engine alpha.
  - Fog density and fog-start scaling logic operates only through verified offsets in an opaque fog-state adapter.
  - No biome, resource-pack, world, packet or server state is modified.
- Overlay Mod (Partial)
  - Fire, water and in-block opacity are handled as separate local render paths.
  - Each configured value is a multiplier of vanilla opacity: 1.0 = vanilla, 0.0 = hidden.
  - No burning, underwater, suffocation or collision state is changed.
- EnvironmentRenderSignatureProfiles.h is intentionally empty until the exact Minecraft for Windows build, fog ABI/offsets and overlay ABI are verified on a real Windows machine.


## v3.4 Alpha 4G — Remaining modules sweep (Screenshot excluded)
Source-connected or adapter-contracted in this batch:
- 2D Items (Partial): configurable render policy; exact item renderer adapter pending.
- Auto GG (Partial): watches verified title/chat result snapshots for strong self-victory phrases, sends one fixed `gg` through the vanilla chat UI, and re-arms only after the result clears. Auto Text Hotkey was removed by user request.
- GUI Scale (Partial): configurable scale policy; exact Minecraft GUI render adapter pending.
- Item Physics (Partial): rotation/tilt/bob policy; exact dropped-item renderer adapter pending.
- Kill Sounds (Partial): sound preset/volume policy; reliable kill-event adapter pending.
- Momentum (Partial): local horizontal velocity readout + optional history graph; runtime calibration pending.
- Nick Hider (Partial): replacement/hide policy; exact name/chat render adapters pending.
- Pack Organizer (Partial): favorites/compact/search policy; exact pack-screen adapter pending.
- Boss Bar, Chat Mod, Pack Display, Particle Changer, Radio, Scoreboard, Scrollable Tooltips, Titles, Toggle Sprint/Sneak and Waypoints were also moved to Partial in this batch.
- Screenshot / Screenshot Uploader intentionally remains Planned by user request.

Final source-state count after Auto GG revision: 20 Implemented, 33 Partial, 1 Planned (Screenshot).


## v3.4 Memory Write / OBS Game Capture integration
Completed in source after Alpha 4G:
- FOV / Zoom — upgraded to Implemented in source.
  - Uses a guarded `LevelRendererPlayer::getFov` hook instead of the older render-level raw-field multiplier.
  - Current public Bedrock layouts still expose LevelRendererPlayer FOV storage at the expected offsets, but WIRZA activates through runtime pattern validation rather than blindly writing a fixed address.
  - The 70-degree hand projection is preserved so camera zoom does not resize the hand unexpectedly.
- GUI Scale — upgraded to Implemented in source.
  - Reads the current `GuiData` pointer from the validated ClientInstance path.
  - Writes only GUI scale, reciprocal scale, and derived GUI size after structural/range/page-protection checks.
  - Saves the original scale and restores it when the module is disabled or switched to HUD-only mode.
  - It never changes memory page protection to force a write.
- Lighting — upgraded to Implemented in source.
  - Uses an `Options::getGamma` return-value hook when the current signature matches.
  - Full Bright returns a cosmetic gamma value only; world/block lighting state is not modified.
  - If the native gamma hook is unavailable, the earlier D3D12 screen-space brightness path remains the fallback.
- OBS Game Capture compatibility:
  - WIRZA continues drawing HUD/menu/post-process effects directly into Minecraft's D3D12 backbuffer before Present; there is no external transparent overlay window.
  - The renderer verifies that the swapchain OutputWindow belongs to the current Minecraft process before attaching.
  - The Launcher detects an already-running OBS Game Capture graphics hook and, when possible, loads WIRZA after it to improve hook ordering.
  - Actual OBS capture ordering still requires real Windows/Minecraft/OBS validation and is not claimed as universally guaranteed.

Safety boundary remains unchanged: no writes to reach, attack damage/rate, movement speed, knockback, inventory contents, packet contents, or anti-cheat state.

Current source-state count: **20 Implemented / 33 Partial / 1 Planned**. The only Planned module is Screenshot / Screenshot Uploader, intentionally skipped by user request.
