# WIRZA Server Safe Mode

更新日: 2026-08-21

WIRZAは大手サーバー接続時に、サーバールール上で禁止または曖昧と判断した機能を自動でOFFにします。
これはサーバー運営による承認を保証する機能ではありません。ルール変更時はサーバーの最新ルールが優先されます。

## The Hive
公開allow-listにWIRZAで対応するものだけを許可する厳格モードです。CPS、Armor HUD、FOV/Zoom、Full Bright、Toggle Sprint/Sneakに加え、公式に明示許可されている **Auto GG** を許可します。Auto GGは勝利結果を観測したときだけ1回 `gg` を送信し、Chat on Killには使用しません。

## Lifeboat
公開acceptable-mod listに合わせ、Full Bright、FOV/Zoom、CPS/Reach表示、自己Armor HUDを対象とし、それ以外はOFFにします。

## CubeCraft
不公平な優位を与える改造を禁止する方針に合わせ、WIRZAではWaypoints、WAILA、Horse Stats、Auto GG、Nick Hiderなど情報/自動化面で曖昧な機能をOFFにします。CubeCraftはMacrosを禁止しており、Auto GGの明示許可をこの版では確認できていないため保守的にOFFです。

## MegaSMP / InPvP
公開ルールでHacked Client、Macros/Scripts、Auto Clickerが禁止されています。WIRZAでは保守的なHUD/表示セットのみを許可します。

## Unknown multiplayer
ルールを判定できないサーバーでは保守的なセットのみを許可します。

## Important
- WIRZAにはReach延長、KillAura、Fly、Speed、Anti-KB、Auto Clicker、パケット改ざん、アンチチート回避は実装しません。
- Server Safe Modeはゲーム内機能を隠して規約違反を回避する仕組みではなく、危険/曖昧な機能を使用しないための安全装置です。


## 参考
- Hive official allowed/denied client modifications: https://support.playhive.com/allowed-and-denied-mods/
- CubeCraft official rules: https://help.cubecraft.net/en/article/cubecraft-rules-1403lij/
