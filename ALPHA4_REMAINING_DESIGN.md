# WIRZA v3.4 Alpha 4 — Remaining Visual Adapter Design

Alpha 4A connected four modules as Partial: Block Outline, Motion Blur, Lighting, Menu Blur.
Alpha 4B additionally connects Color Saturation with a renderer-only fullscreen shader.
Alpha 4C adds the shared first-person transform bridge and module logic for Item Customizer, Shields and 1.7 Visuals.
Alpha 4D adds the shared item/material pass bridge and module logic for Glint Colorizer and Shiny Pots.
Alpha 4E adds read-only local-health damage observation plus the actor-overlay adapter/policy for Damage Tint and Hit Color.
Alpha 4F adds EnvironmentRenderBridge plus fog-color/fog-scalar and fire/water/in-block overlay opacity policies.
Modules remain Partial until their exact current-build adapter profile is verified; later visual modules below stay Planned until their stated adapter is verified.
No guessed offset/signature should be added merely to make the UI say Implemented.

| Module | Bedrock feasibility | Preferred implementation point | Client-only | Multiplayer | Existing settings | Build dependency |
|---|---|---|---|---|---|---|
| Damage Tint | Partial | Read-only minecraft:health drop observation -> timed screen tint | Yes | Visual-only | strength, tint color, duration | Health path wired; absorption-only damage + runtime verification remain |
| Fog / Fog Customizer | Partial | EnvironmentRenderBridge fog-color + opaque fog-state adapter | Yes | Visual-only | density, start scale, fog color | Policy implemented; exact fog signatures + scalar offsets required |
| Glint Colorizer | Partial | ItemMaterialRenderBridge MaterialPassRefV1 adapter | Yes | Visual-only | color, strength, animation speed | Policy implemented; exact current-build material signature profile required |
| Hit Color | Partial | ActorOverlayRenderBridge + recent attacked entity id | Yes | Visual-only | color, strength, duration | Policy implemented; exact actor-overlay signature/ABI/actor offset profile required |
| Particle Changer | Partial | ExtendedFeatureBridge particle policy | Yes | Visual-only | amount, size, color override | Exact-build particle renderer ABI still required |
| Overlay Mod | Partial | EnvironmentRenderBridge separate fire/water/in-block alpha adapters | Yes | Visual-only | three opacity values | Policy implemented; exact overlay signatures/ABI required |
| 1.7 Visuals | Partial | FirstPersonRenderBridge MatrixRefV1 adapter | Yes | Visual-only | old swing, old block, scale | Transform logic implemented; exact current-build signature profile still required |
| Item Customizer | Partial | FirstPersonRenderBridge MatrixRefV1 adapter | Yes | Visual-only | scale, x/y offset, rotation | Transform logic implemented; exact current-build signature profile still required |
| Shields | Partial | FirstPersonRenderBridge + held-item ID cache | Yes | Visual-only | scale, x/y offset | Shield filtering + transform logic implemented; exact current-build signature profile still required |
| Shiny Pots | Partial | ItemMaterialRenderBridge + potion identifier filter | Yes | Visual-only | shine color, strength | Potion/glint-request policy implemented; exact current-build material signature profile required |

## Recommended next order

1. First-person profile verification — Item Customizer + Shields + 1.7 Visuals already have Alpha 4C logic.
2. Material profile verification — Glint Colorizer + Shiny Pots already have Alpha 4D logic.
3. Damage Tint + Hit Color — Alpha 4E source logic added; Hit Color still needs exact actor-overlay profile and Damage Tint needs runtime/absorption verification.
4. Environment profile verification — Overlay Mod + Fog logic added in Alpha 4F; exact signatures/offsets remain.
5. Particle Changer — Alpha 4G policy/adapter contract added; exact-build particle renderer ABI still requires Windows/Minecraft validation.

## Safety boundary

These modules must remain cosmetic/read-only. Do not add packet edits, movement changes,
reach changes, hidden injection behavior, anti-cheat bypass, AV bypass, or server-state mutation.
