WIRZA v3.4 Alpha 4E — Combat Visuals

This batch adds client-only visual feedback for:
- Damage Tint
- Hit Color

Damage Tint
-----------
- GameDataBridge now reads the local player's minecraft:health attribute (ID 7) through the existing read-only ECS attribute path.
- When current health drops below the previous sample, WIRZA records a damage timestamp.
- VisualEffects draws the configured Tint color/strength over the Minecraft frame for the configured duration.
- The effect fades quadratically and is drawn before WIRZA HUD/menu, so HUD colors are not tinted.
- Health is sampled by the existing 100 ms refresh loop.
- Absorption-only damage is not yet detected because it can occur without minecraft:health decreasing.

Hit Color
---------
- The existing passive Actor::attack hook records the target Actor pointer, ECS entity id and attack timestamp.
- ActorOverlayRenderBridge changes only the local render overlay color for the same recently attacked entity.
- Configurable: Hit color, Strength, Duration (ms).
- The bridge never changes damage, invulnerability time, reach, attack validity, entity state or packets.

Compatibility rule
------------------
ActorOverlaySignatureProfiles.h intentionally ships with zero active profiles.
A Hit Color hook is enabled only after the exact Minecraft for Windows version,
RenderController overlay-color ABI, and actor-pointer offset have been verified
on a real Windows/Minecraft build. Unknown builds safely no-op.

Status
------
Damage Tint: Partial (source path connected; absorption-only damage and runtime verification remain)
Hit Color: Partial (policy and target tracking connected; exact actor-overlay profile required)

This environment cannot launch Minecraft for Windows and cannot perform the final MSVC/Minecraft runtime verification.
