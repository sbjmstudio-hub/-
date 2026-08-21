WIRZA v3.4 - Memory Write / OBS Game Capture Integration

Purpose
- Use direct Minecraft state modification only where it is the appropriate local/cosmetic mechanism.
- Keep WIRZA HUD/menu/visual post-processing inside Minecraft's D3D12 backbuffer so an OBS Game Capture source targeting Minecraft can capture it without a separate overlay window.

Implemented-in-source paths
1) FOV / Zoom
   - Guarded LevelRendererPlayer::getFov hook.
   - Smooth target FOV handling.
   - Preserves the 70-degree hand projection.
   - No reach/camera-to-hitbox coupling or combat modification.

2) GUI Scale
   - Guarded direct writes to GuiData GUI scale, reciprocal scale, and derived GUI size.
   - Validates readable object memory, sane screen/scale ranges, reciprocal consistency, and writable page protection.
   - Does not call VirtualProtect to force arbitrary pages writable.
   - Saves/restores the original GUI scale.
   - HUD-only mode leaves Minecraft GuiData unchanged and scales only WIRZA HUD.

3) Lighting
   - Native Options::getGamma return hook when a supported pattern matches.
   - Full Bright is local gamma only.
   - Existing D3D12 brightness overlay remains the fallback when the native gamma path is unavailable.

OBS Game Capture integration
- WIRZA renders from inside Minecraft's own D3D12 Present path.
- Renderer rejects a swapchain window owned by another process.
- If OBS is already running, Launcher looks for graphics-hook64.dll / graphics-hook32.dll in Minecraft and waits briefly before loading WIRZA to improve capture hook ordering.
- Hook ordering differs by OBS/game/driver configuration, so actual capture must be verified on the target Windows PC.

Explicitly not implemented
- Reach increase
- KillAura / automated attacks
- Fly or movement-speed writes
- Attack-speed or damage changes
- Knockback manipulation
- Inventory/packet tampering
- Anti-cheat bypass, stealth injection, or AV evasion

Current registry state
- Implemented in source: 20
- Partial: 34
- Planned: 1 (Screenshot / Screenshot Uploader, intentionally skipped)

Validation boundary
- Static source checks can be performed in this environment.
- A full Windows/MSVC build, Minecraft runtime test, and OBS Game Capture test must be performed on Windows before runtime compatibility is claimed.
