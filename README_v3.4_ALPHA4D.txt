WIRZA v3.4 Alpha 4D — Item / Material Visual Bridge

This batch adds the shared client-only material adapter for:
- Glint Colorizer
- Shiny Pots

What is implemented now
-----------------------
1. ItemMaterialRenderBridge
   - Exact-version profile gate, similar to FirstPersonRenderBridge.
   - No wildcard or guessed signature fallback.
   - Safe no-op when the current Minecraft for Windows build has no verified profile.
   - Sidebar diagnostic text shows the bridge state.

2. Glint Colorizer policy
   - Uses the module's Glint color setting.
   - Strength 0.0-2.0 blends/boosts the glint color.
   - Animation speed 0.1-3.0 changes a small render-only brightness pulse.
   - Runs only for a vanilla or WIRZA-requested glint pass.

3. Shiny Pots policy
   - Detects potion-family item identifiers in the verified material-pass adapter.
   - Requests the normal local Bedrock glint pass for those items.
   - Uses configurable Shine color and Shine strength.
   - Strength 0 means no extra glint request.

Safety / multiplayer
--------------------
These features are cosmetic only. They do not add enchantments, modify ItemStack data,
change inventory contents, edit packets, alter combat, or change server-visible state.

Compatibility rule
------------------
MaterialSignatureProfiles.h intentionally contains zero active profiles in this package.
This environment cannot launch the user's Minecraft for Windows executable, so the exact
material-pass ABI/signature cannot be honestly verified here. The two modules therefore
remain Partial until a real Windows build is inspected and an exact matching profile is
added. The visual policy and bridge plumbing do not need redesign after that.

Why this path
-------------
Bedrock treats enchantment glint as a dedicated render/material effect. Alpha 4D therefore
hooks the item/material pass instead of applying a fake whole-screen tint.
