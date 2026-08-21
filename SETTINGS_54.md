# WIRZA v3 - 54 Module Settings

Every remaining module has its own independent ON/OFF and settings schema.
HUD modules also have editable position/scale/text color/background color/accent color/opacity/corner radius.

## Zoom
- Hold C to zoom.
- `Zoom FOV (degrees)` can be set from 5° to 90°.
- While holding C, mouse wheel changes the target FOV by the configured step.
- `Normal FOV` is configured in the FOV module.
- Internally WIRZA scales Bedrock's render FOV by targetFov/normalFov.

## Important runtime note
This package implements the complete settings/configuration layer for all 54 remaining modules.
Modules that need Bedrock internal game data/render hooks still require a verified Game Data Bridge for the exact Minecraft for Windows build.
They are not falsely marked working when no safe signature/adapter exists.

## Per-module options
### 2D Items
- Item scale
- Horizontal offset
- Vertical offset
- Rotation

### Armor Status
- Show durability
- Show held item
- Layout
- Low durability %
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Auto GG
- Delay after victory (ms)
- Use recent victory chat as fallback
- Re-arm after result clears (seconds)
- Message is fixed to `gg` and is sent only once per detected victory result

### Block Outline
- Line width
- Outline color
- Fill opacity

### Boss Bar
- Bar scale
- Hide background
- Bar color
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Chat Mod
- Chat opacity
- Font scale
- Show timestamps
- Compact spacing
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Timer
- 24-hour format
- Show seconds
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Color Saturation
- Saturation
- Contrast
- Brightness

### CPS
- Show LMB
- Show RMB
- CPS window (ms)
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Crosshair
- Length
- Gap
- Thickness
- Color

### Damage Tint
- Tint strength
- Tint color
- Duration (ms)

### Direction HUD
- Display mode
- Degree precision
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Fog / Fog Customizer
- Fog density
- Fog start
- Fog color

### FOV
- Normal FOV (degrees)
- Dynamic FOV

### FPS
- Show FPS label
- Update interval (ms)
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Glint Colorizer
- Glint color
- Glint strength
- Animation speed

### GUI Scale
- GUI scale
- HUD only

### Hit Color
- Hit color
- Strength
- Duration (ms)

### Horse Stats
- Show speed
- Show jump
- Show health
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Item Counter
- Selected item list
- Show icon
- Warn below count
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Item Customizer
- Scale
- X offset
- Y offset
- Rotation

### Item Physics
- Rotation speed
- Ground tilt
- Bob strength

### Keystrokes
- Show Space
- Show Shift
- Show Ctrl
- Show LMB/RMB
- Pressed color
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Kill Sounds
- Volume
- Sound preset

### Lighting
- Brightness
- Gamma
- Full Bright

### Memory Usage
- Unit
- Show process label
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Menu Blur
- Blur strength
- Background dim

### Momentum
- Show movement speed
- Show speed graph
- Graph history

### Motion Blur
- Blur strength
- Samples

### Nick Hider
- Hide own name
- Hide other names
- Replacement text

### 1.7 Visuals
- 1.7 swing
- 1.7 block look
- Visual scale

### Overlay Mod
- Fire opacity
- Water opacity
- In-block opacity

### Pack Display
- Show icon
- Show pack name
- Max name length
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Pack Organizer
- Favorites first
- Compact list
- Search packs

### Particle Changer
- Particle amount
- Particle size
- Particle color
- Override color

### Ping
- Show ms suffix
- Update interval
- Good ping threshold
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Playtime
- Session only
- Show seconds
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Potion Effects
- Show duration
- Show level
- Compact layout
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Radio / Lunar FM
- Volume
- Station / URL
- Autoplay

### Reach Display
- Decimals
- Display timeout
- Accent color
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Scoreboard
- Scale
- Background opacity
- Hide score numbers
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Screenshot / Screenshot Uploader
- Include WIRZA HUD
- Image format
- JPG quality

### Scrollable Tooltips
- Scroll speed
- Allow horizontal scroll

### Server Address
- Hide port
- Hide in local world
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Shields
- Shield scale
- X offset
- Y offset

### Shiny Pots
- Shine color
- Shine strength

### Stopwatch
- Show hundredths
- Auto reset on world join
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Titles
- Title scale
- Opacity
- Title color
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Toggle Sneak / Toggle Sprint
- Toggle sprint
- Toggle sneak
- Sprint key
- Sneak key

### Totem Counter
- Warn below
- Warning color
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### WAILA
- Show block name
- Show entity name
- Show distance
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color

### Waypoints
- Max render distance
- Show vertical beam
- Default color

### Zoom
- Zoom FOV (degrees)
- Mouse wheel FOV step
- Smooth zoom
- Smooth speed

### Potion Counter
- Potion filter
- Warn below
- HUD position / scale / text size / opacity / corner radius / text color / background color / accent color


## Alpha 4F setting semantics
- Fog `density`: multiplier applied to the verified vanilla fog-density scalar (1.0 = vanilla).
- Fog `start_scale`: multiplier applied to the verified vanilla fog-start scalar (1.0 = vanilla).
- Fog `fog_color`: RGB blend target; alpha acts as blend strength in WIRZA's policy.
- Overlay Mod `fire_opacity`, `water_opacity`, `block_opacity`: multipliers of vanilla overlay alpha (1.0 = vanilla, 0.0 = hidden).
These settings only take effect when the exact Minecraft build has a verified environment-render profile.
