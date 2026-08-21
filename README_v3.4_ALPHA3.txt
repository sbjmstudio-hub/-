WIRZA v3.4 Alpha 3 — Game Data Bridge Batch 2

REAL BRIDGE WORK ADDED
- Armor Status
  - Current armor inventory
  - Item identifiers
  - Current/max durability path
  - Configurable warning threshold / HUD appearance

- Ping
  - Passive capture of Minecraft/RakNet average ping
  - Does not alter packets

- Server Address
  - Host / unresolved URL / port / region where available
  - Configurable port hiding / hostname preference

- Reach Display
  - Display only
  - Triggered from Minecraft's actual attack callback
  - Uses current HitResult start -> hit position
  - Never changes reach or hit validity

- WAILA
  - Real HitResult
  - Block identity through BlockSource + BlockLegacy
  - Entity target is partial and uses current ray/AABB matching
  - No wall-through entity scanning is intentionally displayed

PARTIAL
- Horse Stats
  - Horse target recognition is connected.
  - Hidden movement/jump Attribute IDs are NOT guessed.
  - These remain pending until the Minecraft version adapter is verified.

- Potion Effects
  - The module UI/capability path is present.
  - No current safe MobEffectInstance ABI was found in the reference source,
    so WIRZA shows Unsupported rather than fabricated effect data.

DEPENDENCY
- EnTT is pinned to the exact commit used by the current public Latite Bedrock ECS adapter:
  fe8d7d78c4823e8a66a050bf86f5c6318cf76ce7

IMPORTANT
This source was generated in a non-Windows environment.
It has NOT been compiled or runtime-tested against Minecraft for Windows here.
Final compile and game verification still need the fresh GitHub Actions Windows build later.

Security/fair-play:
- No reach increase
- No KillAura
- No packet tampering
- No movement automation
- No anti-cheat bypass
