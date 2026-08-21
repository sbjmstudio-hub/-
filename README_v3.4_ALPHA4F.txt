WIRZA v3.4 Alpha 4F — Environment Visuals

Added in this source batch:
- Fog / Fog Customizer: Partial
  - configurable fog color policy
  - density multiplier policy
  - fog-start multiplier policy
- Overlay Mod: Partial
  - fire opacity multiplier
  - water opacity multiplier
  - in-block opacity multiplier
- EnvironmentRenderBridge + EnvironmentRenderSignatureProfiles
- Diagnostics entry for the environment-render adapter

Safety / compatibility behavior:
- The verified environment profile list is intentionally empty in this package.
- Unknown Minecraft for Windows builds install no environment hook.
- No guessed signature, fog-state offset or overlay ABI fallback is present.
- Fog/overlay changes are client-side visuals only; WIRZA does not alter packets,
  player burning/underwater/collision state, biome data or server state.

Runtime status:
- Static C++ source validation is performed in this environment.
- A Windows/MSVC build and Minecraft for Windows runtime test are still required.
- Therefore these modules are Partial, not Implemented.

Next visual batch:
- Particle Changer
