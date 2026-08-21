WIRZA v3.4 Alpha 4G — Remaining UI / Utility Batch
2026-08-20

This batch continues from Alpha 4F. Screenshot / Screenshot Uploader is intentionally not implemented because the user explicitly said it was not needed.

Updated to Partial:
- Particle Changer
- Scoreboard
- Boss Bar
- Chat Mod
- Titles
- Scrollable Tooltips
- Pack Display
- Waypoints
- Radio / Lunar FM
- Toggle Sneak / Toggle Sprint

Highlights:
- ExtendedFeatureBridge provides one safe snapshot/policy contract for version-sensitive Bedrock UI/particle paths.
- The verified ExtendedFeature signature profile list is intentionally empty. No guessed offsets are shipped.
- Waypoints parses local text settings in the format Name,x,y,z;Name2,x,y,z and renders markers, distance and optional beams.
- Radio uses Windows Media Foundation / MFPlay and expects a direct audio stream/media URL. Runtime format/codec support depends on Windows.
- Toggle Sprint/Sneak latches the configured Windows-message key and releases it before WIRZA opens its menu. Bedrock builds using a different Raw Input path still need real-device validation.

Important:
- Source/static validation only in this environment.
- No Windows/MSVC full build was performed here.
- No Minecraft for Windows runtime test was performed here.

Additional recount sweep:
- 2D Items, Auto Text Actions, Auto Text Hotkey, GUI Scale, Item Physics, Kill Sounds, Momentum, Nick Hider and Pack Organizer were also moved from Planned to Partial after the registry recount.
- Momentum has a local velocity display/history graph.
- Auto Text Hotkey has a non-blocking chat-input state machine. Auto Text Actions exposes the delayed queue entry point but still needs a verified gameplay-event trigger.

Registry result in this package: 17 Implemented / 37 Partial / 1 Planned. The one Planned module is Screenshot, intentionally skipped.
