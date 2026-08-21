# Wirza_Cliant v3.4

Minecraft for Windows 向けのネイティブ Windows クライアントです。

## GitHub Actions で Windows x64 をビルド

GitHub の **Actions** → **Build Wirza_Cliant Windows x64** → **Run workflow** でビルドできます。
完了後の Artifacts に `Wirza_Cliant-v3.4-Windows-x64` が生成されます。

生成ZIPの主なファイル:

- `Wirza_Cliant.exe`
- `Wirza_Cliant.dll`

詳細は [README_GITHUB_BUILD_JA.md](README_GITHUB_BUILD_JA.md) を参照してください。

## Status

Auto Text Hotkey をユーザー指定で削除したため、現在は **54モジュール**です。ソース状態は **20 Implemented / 33 Partial / 1 Planned** で、Plannedはユーザー指定で除外したScreenshotだけです。
Minecraft内部のbuild依存ABI/signatureが未検証の機能は `Partial` として安全側に留めています。




## Auto GG

- `Auto Text Hotkey` は削除しました。
- 旧 `Auto Text Actions` は **Auto GG** に置き換えました。
- Wirza_Cliantが検証済みのTitle/Chat結果アダプターから `VICTORY` / `You won` / `You win` / `勝利` などの強い勝利結果を観測したときだけ、1試合につき1回 `gg` をMinecraftの通常チャットUIから送信します。
- Kill時・キー押下・クリック・移動をトリガーにはしません。
- The Hiveは公式client-modification allow-listでAuto GGを明示的に許可しているためServer Safe Modeでも許可します。CubeCraft/Lifeboat/MegaSMP/不明サーバーでは保守的に無効化します。
- 正確なMinecraft buildのTitle/Chat adapterが未検証のため、モジュール状態は `Partial` です。

## Memory Write / OBS Game Capture

必要なローカル表示系だけ、検証付きでMinecraft側の状態を変更します。

- **FOV / Zoom**: `LevelRendererPlayer::getFov` の検証済みパターンが見つかった場合だけカメラFOVを変更
- **GUI Scale**: `GuiData` のscale / reciprocal / GUI sizeだけを範囲・ページ権限チェック後に変更し、OFF時は元へ復元
- **Lighting**: `Options::getGamma` が一致した場合はネイティブgamma経路、未対応buildではD3D12の画面側フォールバック
- Reach、攻撃力/速度、移動速度、KB、インベントリ、パケット、アンチチート状態は変更しません

HUD・メニュー・Motion Blur・Color Saturationなど、メモリ書き換えより描画処理が適切な機能はMinecraftの **D3D12 backbuffer内** に描画します。別ウィンドウのオーバーレイではありません。

LauncherはOBSが起動済みの場合、Minecraft内のOBS Game Capture `graphics-hook` を短時間確認してからWirza_Cliantを読み込みます。これによりMinecraftだけを対象にしたGame CaptureでWirza_Cliant描画を含めやすくします。ただしOBS/ドライバ/ゲームbuildによるhook順序差があるため、実機確認までは100%保証しません。

## Build requirements

- Windows x64
- Visual Studio 2022 / MSVC v143
- Windows SDK
- CMake 3.24+
- Git

依存ライブラリ（MinHook / Dear ImGui / EnTT）はCMake FetchContentで取得します。

## Safety scope

Wirza_CliantはHUD・表示・読み取り・視覚カスタマイズ用途です。攻撃距離増加、KillAura、Fly、移動速度改変、パケット改変、アンチチート回避、ステルス化・AV回避は対象外です。


## Security / false-positive handling

See `SECURITY_FALSE_POSITIVE_JA.md`. WIRZA does not use AV bypass, packing or obfuscation. The GitHub workflow supports optional Authenticode signing via repository secrets.

## Reference UI / item counter / server-safe revision

- The in-game menu now uses the supplied dark navy / purple card layout as its design reference: animated sidebar, animated module switches, four-column module cards, and animated key-state transitions.
- Direction HUD is rendered as a top-center compass tape when enabled.
- `Clock` was removed and replaced by `Timer`; `Stopwatch` remains a separate module.
- Item Counter keeps a persistent local history of item IDs observed in your own inventory/hand/armor and lets you select any number of them individually for display.
- Wirza_Cliant Server Safe Mode recognizes The Hive, CubeCraft, Lifeboat and MegaSMP-style host strings and automatically turns off modules that WIRZA treats as disallowed or ambiguous for that network. Unknown multiplayer uses a conservative profile. This is a safety aid, not a guarantee of server approval.
- HUD/menu rendering remains inside Minecraft's D3D12 backbuffer before Present, so it is designed to be included when OBS Game Capture targets Minecraft for Windows.
- Security-hardening remains transparent: no AV bypass, no obfuscation/packer, no security-product exclusion changes, no auto-start, optional Authenticode signing.
