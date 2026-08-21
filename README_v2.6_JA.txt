WIRZA Client v2.6 - Internal HUD / Native Zoom / OBS target

配布物（実行に必要）:
  WIRZA.Launcher.exe
  WIRZA.Client.dll

設計:
  - WIRZA.Client.dll は隠さず、Launcherと同じフォルダに置く
  - TempへのDLL展開なし
  - Hidden属性なし
  - 自己削除なし
  - 難読化なし
  - セキュリティ製品の検知回避コードなし
  - Launcherはログ WIRZA.Launcher.log を残す

HUD:
  - MinecraftのD3D12バックバッファへ直接描画
  - Presentの直前にFPS/CPS/WASD/LMB/RMB/Timer/Stopwatch/Menuを描画
  - OBS Game CaptureでMinecraftを指定したときにHUDも取得される構成を優先
  - OBS側フックとの順番によっては環境差があり、100%の保証はできない

Zoom:
  - Windows拡大鏡ではない
  - C長押しでMinecraft側のカメラFOV値を変更
  - Zoom strength 1x～10x
  - ゲーム更新でシグネチャ/構造が合わない場合は Zoom を安全に停止
  - 非対応時に推測アドレスへ書き込まない

Menu:
  - Right Shift
  - Minecraft標準の一時停止画面を開き、その上にWIRZAメニューを描画

対象:
  Minecraft Bedrock Edition / Minecraft for Windows
  Windows x64 / DirectX 12

注意:
  このクライアントはMinecraftプロセスへDLLを読み込み、必要なゲーム内処理をフックします。
  セキュリティ製品が挙動を警戒する可能性があります。
  このプロジェクトにはセキュリティ回避・隠蔽・アンチチート回避機能は入れていません。
