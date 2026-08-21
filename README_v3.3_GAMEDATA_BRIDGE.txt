WIRZA v3.3 - Game Data Bridge Alpha 2

This revision adds the first real Bedrock game-data bridge.

REAL DATA MODULES ADDED
- Direction HUD
- Item Counter
- Totem Counter
- Potion Counter

ZOOM IMPROVEMENTS
- Native Minecraft FOV zoom remains in-process.
- Zoom target FOV is configurable in degrees (5°-90°).
- Normal FOV is independently configurable.
- Hold C + mouse wheel changes target FOV.
- Smooth Zoom now has a real interpolation path for zoom-in and zoom-out.

GAME DATA BRIDGE
The bridge is read-only. It resolves the current Platform_GameCore signature,
then validates the ClientInstance / LocalPlayer / inventory path before use.
If Minecraft updates and the expected signature/layout is unavailable, data
modules show an unsupported/waiting status and do not guess addresses.

IMPORTANT
This source was produced in a non-Windows build environment, so it has not yet
been compiled or run against Minecraft for Windows here. The final Windows
verification will happen later through the fresh GitHub Actions build.

Not yet connected to real Bedrock data:
Armor Status, Ping, Potion Effects, Reach Display, Server Address, WAILA,
Horse Stats and several renderer-dependent modules. Those are the next bridge batches.
