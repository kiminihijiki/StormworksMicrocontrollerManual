# Stormworks AI Reference

このリポジトリは、StormworksのマイコンをAIで作成するときの統合入口です。実際の資料は役割ごとの専門リポジトリに分けています。

## 参照先

| 目的 | 参照先 |
|---|---|
| マイコンLuaの実行モデル、API、制限、サンプル | [stormworks-microcontroller-lua](https://github.com/kiminihijiki/stormworks-microcontroller-lua) |
| パーツ、センサー、論理ノード、検索ツール | [stormworks-partdata](https://github.com/kiminihijiki/stormworks-partdata) |

`stormworks-microcontroller-lua`がマイコンLuaの資料、`stormworks-partdata`がパーツカタログの資料です。このリポジトリではそれらを重複して管理しません。DSL/XMLの定義と検証は、別途用意された外部の検証環境を使います。

## AIの参照順

1. [AI作業フロー](docs/ai-workflow.md)で成果物とI/O契約を決める
2. [stormworks-microcontroller-lua](https://github.com/kiminihijiki/stormworks-microcontroller-lua)でLuaの実行モデルとAPIを確認する
3. [stormworks-partdata](https://github.com/kiminihijiki/stormworks-partdata)で`--mcu-relevant`または`--lua-relevant`検索を行う
4. 必要に応じて外部のDSL/XML検証環境で`spec`、`check-dsl`、`typecheck-dsl`を実行する
5. ゲーム内で確認した挙動と、資料からの推定を分けて記録する

各リポジトリの対応commitは[data/sources.json](data/sources.json)に記録します。

## このリポジトリに残すもの

- 2つの専門リポジトリを組み合わせるためのAI作業フロー
- 参照先と対応commitの一覧
- 旧マニュアルの履歴資料
- `vehicles/`にある利用者の車両資料

旧マニュアルは[アーカイブ](docs/archive/StormworksMicrocontrollerManual-legacy.md)として残しています。新規のLua仕様やパーツ情報は、分離後のリポジトリを参照してください。

## 現在のスナップショット

- パーツカタログ：`stormworks-partdata` の705パーツ版（`b4c9b67c30246752853f3df2f00027cfbc306870`）
- マイコンLua資料：`stormworks-microcontroller-lua`（`80f7bb9cb7f4b9b33ea44ed73ba2c104242b1e04`）
- DSL/XML定義：外部のDSL/XML検証環境で確認

パーツデータの再配布条件は確認中です。公開範囲を変更する前に、元データのライセンスと寄稿者の意向を確認してください。
