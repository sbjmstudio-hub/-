# WIRZA: セキュリティソフトの誤検知を減らすための方針

WIRZA は Minecraft for Windows のプロセス内に `Wirza_Cliant.dll` を読み込むため、
Launcher が `OpenProcess` / `VirtualAllocEx` / `WriteProcessMemory` / `CreateRemoteThread` / `LoadLibraryW` を使用します。
この API の組み合わせは正当なデバッグ・拡張ツールでも使われますが、セキュリティ製品が警戒することがあります。

WIRZA は検知回避を目的とした次の処理を行いません。

- 実行ファイル/DLLの難読化、暗号化、パッキング
- セキュリティソフトやWindows Defenderの停止・除外登録
- プロセス名や署名の偽装
- DLLの一時展開、自己削除、隠しファイル化
- shellcodeの実行、RWXメモリの確保、process hollowing
- 永続化、自動起動、サービス登録

誤検知を減らすために以下を採用します。

- Launcher は `asInvoker` 固定（管理者権限を要求しない）
- DLLはLauncherと同じフォルダからのみ読み込む
- `system("pause")` を使わず、`cmd.exe` を不要に起動しない
- DEP / ASLR / High Entropy ASLR / Control Flow Guard を有効化
- GitHub Actionsでコミット情報とSHA-256を成果物に保存
- Authenticode証明書を所有している場合のみ、GitHub Secrets経由でEXE/DLLを署名可能
- パッカー/難読化ツールを使用しない

## Authenticode署名（任意）

GitHub repository secrets に次の2つを登録すると、Windowsビルド時に署名します。

- `WIRZA_SIGNING_PFX_BASE64`: PFXファイルをBase64化した内容
- `WIRZA_SIGNING_PFX_PASSWORD`: PFXのパスワード

証明書そのものをリポジトリへコミットしないでください。

署名証明書がない状態でもビルドできます。その場合は未署名のため、SmartScreenやAVの
レピュテーション判定が厳しくなる可能性があります。

誤検知が起きた場合はセキュリティ機能を無効化せず、対象製品の公式false-positive提出窓口へ
EXE/DLL、SHA-256、GitHubの該当コミットを添えて提出する方法を推奨します。
