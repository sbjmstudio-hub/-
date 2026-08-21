Wirza_Cliant - PHASE 1 NATIVE v2.1 FIX
======================================

■ 今回の修正
1. Right ShiftでWIRZAメニューを開くと、先にMinecraftへESCを渡して
   Minecraft標準の一時停止メニューを開き、その上にWIRZAパネルを表示します。
   WIRZAを閉じるとMinecraft側の一時停止メニューも閉じます。

2. WASD / LMB / RMB / C入力のフォーカス判定を修正しました。
   以前はMinecraftの描画用HWNDとForeground HWNDが一致しない環境で、
   メニューを開いている時しかキー入力が認識されないことがありました。
   v2.1では「同じMinecraftプロセスのウィンドウか」で判定します。

3. Zoom修正
   C長押しの検出も上記フォーカス判定の影響を受けていたため修正しました。
   Zoom本体はMinecraft側のLevelRenderer/LevelRendererPlayerのFOV値へ作用します。
   現在のLatite互換プロファイル（renderLevel signature / FOV offsets）を使用しています。
   対応しないMinecraftビルドでは安全のためZoomだけ無効になります。

4. ロゴ変更
   ユーザー提供画像の上側にある盾・剣・Wのマーク部分だけを使用しています。
   GAMING ESPORTS / WIRZA の文字部分はロゴ画像に入れていません。

5. Custom Crosshairは引き続き未搭載です。

■ Phase 1 機能
- FPS
- CPS
- WASD Keystrokes
- LMB / RMB
- Timer
- Stopwatch
- Zoom（C長押し）
- HUD位置変更
- HUDサイズ変更
- 各項目ON/OFF
- Hide All HUD
- 設定保存
- Right ShiftでWIRZAメニュー

■ ビルド方法
1. ZIPを「すべて展開」
2. BUILD.batを実行
3. BUILD SUCCESSを確認
4. RUN_WIRZA.batを実行

ビルド後は次ができます：
  bin\Wirza_Cliant.exe
  bin\Wirza_Cliant.dll
  bin\assets\wirza_logo_mark.png

■ 必要なもの
- Windows 10/11 x64
- Visual Studio / Build Tools
  - Desktop development with C++
  - MSVC x64
  - Windows SDK
  - CMake tools
- Git for Windows

■ 操作
Right Shift : WIRZAメニュー開閉
C長押し    : Zoom

■ Zoom Status
WIRZAメニュー左側のZOOM STATUSが
  Ready (native camera FOV)
ならネイティブZoomフックは有効です。

Unsupported game build - safely disabled
なら現在のMinecraftビルドと内部構造が一致していません。
その場合、知らないアドレスに書き込むことはせずZoomのみ停止します。

■ 一時停止について
WIRZAメニューを開いた時はMinecraft標準の一時停止画面を開くようにしています。
ただしBedrock Editionのマルチプレイ/Realms/外部サーバーでは、
一時停止画面を開いてもサーバー側の時間や他プレイヤーまで停止するわけではありません。

■ 設定保存先
%APPDATA%\Wirza_Cliant\settings.ini

■ 対応端末
Windows版Minecraft Bedrock: 対象
Switch / iPhone / iPad / Android: 非対応

■ 入れていないもの
Custom Crosshair / KillAura / Reach変更 / Fly / Speed / Aim Assist /
Anti-Cheat回避 / ステルス注入 は入れていません。
