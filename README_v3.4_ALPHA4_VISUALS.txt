WIRZA v3.4 Alpha 4A — Visual Batch 1

IMPLEMENTED IN SOURCE AS PARTIAL VISUAL ADAPTERS

1) Block Outline
- Client-only outline for the block Minecraft is currently targeting.
- Uses GameDataBridge HitResult data already connected in Alpha 3.
- Stores the exact ray-start camera origin and integer block origin.
- Projects the eight block corners into screen space and draws the 12 box edges.
- Optional translucent fill.
- Line width / outline color / fill opacity are configurable.
- Uses WIRZA's current Zoom FOV modifier for better alignment while holding Zoom.
- Partial until verified against a real Minecraft for Windows frame.

2) Motion Blur
- D3D12 history capture added.
- Two GPU textures alternate as read/write history.
- The Minecraft backbuffer is copied before WIRZA HUD/menu drawing.
- Previous Minecraft frame is blended through ImGui at configurable strength.
- Disabling/re-enabling clears stale history before drawing again.
- Current pass is one prior frame; the existing Samples setting is intentionally not faked.
- Partial until Windows compile/runtime verification and multi-history support.

3) Lighting
- Safe screen-space brightness/gamma approximation.
- Brightness below 1 darkens the final Minecraft image.
- Brightness above 1 blends toward white to raise perceived brightness.
- Full Bright raises this post-lighting effect only.
- It does NOT change Minecraft block-light, skylight, gamma internals, or server state.
- Partial by design.

4) Menu Blur
- Configurable dim and subtle haze are now wired into the WIRZA pause-menu backdrop.
- When disabled, the legacy fixed dim remains.
- True Gaussian/separable sampled blur is not yet implemented.
- Partial by design.

CONNECTED IN ALPHA 4B
- Color Saturation (D3D12 fullscreen shader; Partial pending runtime verification)

CONNECTED IN ALPHA 4C
- Item Customizer (first-person transform policy; Partial until exact build profile)
- Shields (shield-filtered transform policy; Partial until exact build profile)
- 1.7 Visuals (local swing/block presentation; Partial until exact build profile)

CONNECTED IN ALPHA 4D
- Glint Colorizer (item/material glint-color policy; Partial until exact build profile)
- Shiny Pots (potion glint-request/shine policy; Partial until exact build profile)

NOT YET CONNECTED AFTER ALPHA 4D
- Damage Tint
- Fog / Fog Customizer
- Hit Color
- Particle Changer
- Overlay Mod

IMPORTANT
This source was modified in a non-Windows environment.
It has NOT been compiled or runtime-tested against Minecraft for Windows here.
Do not interpret Partial/Implemented-in-source as runtime verified.

Security/fair-play boundary remains unchanged:
- no reach increase
- no KillAura
- no movement speed modification
- no packet tampering
- no anti-cheat bypass
- no stealth/AV bypass
