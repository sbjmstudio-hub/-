# Wirza_Cliant v3.4 - GitHub Actions Build

このリポジトリは Minecraft for Windows 向け WIRZA v3.4 の Windows x64 ビルド用ソースです。

## GitHubだけでEXE/DLLを作る

1. このフォルダ一式を GitHub リポジトリへ置きます。
2. GitHub の **Actions** を開きます。
3. **Build Wirza_Cliant Windows x64** を選びます。
4. **Run workflow** を押します。
5. 完了後、Artifacts の **Wirza_Cliant-v3.4-Windows-x64** をダウンロードします。
6. ZIPの中には次が入ります。
   - `Wirza_Cliant.exe`
   - `Wirza_Cliant.dll`
   - ドキュメント
7. `Wirza_Cliant.exe` と `Wirza_Cliant.dll` は必ず同じフォルダに置いてください。

## ローカルWindows PCでビルドする場合

必要:
- Windows 10/11 x64
- Visual Studio 2022 Build Tools または Visual Studio 2022
- Desktop development with C++
- Windows SDK
- CMake 3.24+
- Git

PowerShell:

```powershell
cmake --preset windows-x64
cmake --build --preset windows-x64-release
```

## 実行について

`Wirza_Cliant.exe` は Minecraft for Windows のプロセスを検出し、同じフォルダの `Wirza_Cliant.dll` を読み込みます。
Wirza_Cliantは見た目・HUD・読み取り系を目的としており、攻撃距離増加、KillAura、Fly、速度改変、パケット改変、アンチチート回避などは対象外です。



## OBS Game CaptureでMinecraftだけを映す場合

推奨手順:
1. OBSを起動します。
2. ソースに **ゲームキャプチャ** を追加し、Minecraft for Windowsを対象にします。
3. Minecraftを起動して、OBS側でMinecraft映像が取得できる状態にします。
4. `Wirza_Cliant.exe` を起動します。

OBSが既に動いている場合、LauncherはMinecraftプロセス内のOBS Game Capture `graphics-hook` を短時間確認してからWirza_Cliantを読み込みます。
Wirza_CliantのHUD/メニュー/画面効果は別の透明ウィンドウではなく、Minecraft自身のD3D12 backbufferに描画されます。

この仕組みはOBSのhook順序に依存するため、実際のMinecraft/OBS/GPUドライバ構成で確認が必要です。映らない場合はまずOBSのゲームキャプチャでMinecraftが取得できている状態にしてからWirza_Cliantを起動してください。

## メモリ書き換えの範囲

ローカル表示・UIに必要な部分だけを対象にしています。
- FOV / Zoom
- GUI Scale
- Lighting / Gamma

GUI Scaleは元値を保存してOFF時に復元します。書き込み前にポインタ・値範囲・メモリページの書き込み可否を検証します。
Reach、攻撃速度/ダメージ、移動速度、ノックバック、パケット、インベントリ、アンチチート回避は対象外です。

## 現在の制約

- GitHub Actions用ビルド構成は用意されていますが、この作業環境では Windows/MSVC の実ビルド結果までは確認していません。
- `Partial` の機能は Minecraft の実際のbuildに対応する検証済みABI/signatureが必要な場合があります。
- Screenshot機能はユーザー指定により未実装のままです。
- 生成物はコード署名されていません。Windows SmartScreen等で警告される可能性があります。

## 今回のUI/Item Counter更新

- 添付された参考画像のダークネイビー + 紫アクセントを基準に、メニューを4列カード式へ変更しています。
- 左メニューとON/OFFスイッチ、Keystrokesなどにアニメーションを追加しています。
- Direction HUDは上部コンパステープ表示です。
- Clockは廃止し、Timer + Stopwatch構成です。
- Item Counterは自分のインベントリ/手/防具で一度観測したアイテムIDを履歴保存し、メニューから1項目ずつON/OFFできます。
- Server Safe ModeはHive/CubeCraft/Lifeboat/MegaSMP/不明なマルチプレイで、禁止または曖昧な機能を自動OFFにします。最新ルールの確認は利用者側でも必要です。
- OBS向けHUD/メニューはMinecraftのD3D12 backbuffer内に描画する方針を維持しています。

## セキュリティソフトについて

検知回避・難読化・除外設定の自動追加は行いません。`asInvoker`、DEP/ASLR/CFG、パッカーなし、ハッシュ出力、ビルド元Commit記録、任意のAuthenticode署名という正攻法を維持します。DLL読み込み方式自体をセキュリティ製品が警戒する可能性は残ります。


## Auto GG更新

- Auto Text Hotkeyは削除しました。
- 旧Auto Text Actionsを **Auto GG** に変更しました。
- 検証済みの勝利結果を観測したときだけ、固定メッセージ `gg` を1試合につき1回送信します。
- Kill時・キー押下・クリック・移動では送信しません。
- The Hiveは公式の許可一覧でAuto GGを明示的に許可しているため、HiveのServer Safe ModeではAuto GGを許可します。
- CubeCraft / Lifeboat / MegaSMP / 不明サーバーでは、明示的な許可を確認できないため保守的にAuto GGをOFFにします。
- 現在のレジストリは54機能（20 Implemented / 33 Partial / 1 Planned）です。
