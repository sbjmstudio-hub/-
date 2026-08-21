WIRZA v3.4 Alpha 4B — Color Post-process

NEW IN THIS BATCH

Color Saturation (Partial)
- Adds a dedicated D3D12 fullscreen post-process path.
- Copies the current Minecraft swapchain backbuffer into a shader-readable texture.
- Pixel shader applies:
  * Saturation: 0.0 to 2.0
  * Contrast: 0.5 to 1.8
  * Brightness: 0.5 to 1.8
- Processing happens before WIRZA HUD/menu rendering, so WIRZA UI colors remain unchanged.
- Motion Blur history is captured after color correction but before WIRZA HUD/menu.
- No Minecraft game-memory offsets or signatures are required by this module.
- No packet, reach, movement, or server-state changes are made.

FILES ADDED
- src/client/ColorPostProcess.cpp
- src/client/ColorPostProcess.h

RENDER ORDER
1. Minecraft finishes its frame.
2. If Color Saturation is active, raw backbuffer -> colorSource copy.
3. ColorPostProcess fullscreen shader writes corrected frame to swapchain buffer.
4. If Motion Blur is active, corrected Minecraft frame -> motion history copy.
5. WIRZA HUD/menu is rendered with Dear ImGui.
6. Present.

STATUS
Source implementation is complete enough for Windows compilation/testing, but this environment
cannot run Minecraft for Windows. Therefore the module remains Partial until real compile/runtime verification.
