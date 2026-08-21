WIRZA CLIENT PHASE 1 v2.4 - SINGLE EXE

最終配布物:
  WIRZA.Client.exe  1ファイルのみ

EXE内部:
  - WIRZA.Client.dll 相当のネイティブクライアント
  - WIRZAロゴ画像
  - EXEアイコン（Wの盾＋剣、文字なし）

起動:
  1. WIRZA.Client.exe をダブルクリック
  2. Minecraft Bedrockを自動検出（未起動なら起動）
  3. 内部クライアントを一時展開してMinecraftへ読み込み
  4. 読み込み後、一時DLLを削除

予定機能:
  - FPS
  - CPS
  - WASD
  - LMB / RMB
  - Timer
  - Stopwatch
  - Right Shift メニュー
  - メニュー表示時にMinecraft標準一時停止画面
  - C長押し Zoom（Minecraft内部FOV）
  - HUD位置/サイズ変更
  - 各HUD ON/OFF
  - 設定保存
  - Custom Crosshairなし

注意:
  このZIPは「単一EXEを生成するソース」です。
  このChatGPT実行環境にはWindows/MSVCがないため、
  WindowsネイティブEXE/DLLの最終コンパイルはここでは実行できません。
  .github/workflows/build-single-exe.yml を使えば、Windows PCへ
  Visual StudioをインストールせずGitHub Actions上でビルドできます。
