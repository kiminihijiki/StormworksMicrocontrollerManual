# Stormworks AI Reference

このリポジトリは、StormworksのマイコンをAIで作成するときの統合入口です。実際の定義・資料は役割ごとのリポジトリに分けています。

## 参照先

| 目的 | リポジトリ |
|---|---|
| DSL、ゲート定義、XML変換、配線型検査 | [storm-microcontroller-language](https://github.com/nona-takahara/storm-microcontroller-language) |
| マイコンLuaの実行モデル、API、制限、サンプル | [stormworks-microcontroller-lua](https://github.com/kiminihijiki/stormworks-microcontroller-lua) |
| パーツ、センサー、論理ノード、検索ツール | [stormworks-partdata](https://github.com/kiminihijiki/stormworks-partdata) |

`storm-microcontroller-language`がDSL/XMLの正規ソース、`stormworks-microcontroller-lua`がマイコンLuaの正規資料、`stormworks-partdata`がパーツカタログの正規資料です。このリポジトリではそれらを重複して管理しません。

## AIの参照順

1. [AI作業フロー](docs/ai-workflow.md)で成果物とI/O契約を決める
2. [stormworks-microcontroller-lua](https://github.com/kiminihijiki/stormworks-microcontroller-lua)でLuaの実行モデルとAPIを確認する
3. [stormworks-partdata](https://github.com/kiminihijiki/stormworks-partdata)で`--mcu-relevant`または`--lua-relevant`検索を行う
4. [storm-microcontroller-language](https://github.com/nona-takahara/storm-microcontroller-language)の`spec`、`check-dsl`、`typecheck-dsl`でマイコン構造を検証する
5. ゲーム内で確認した挙動と、資料からの推定を分けて記録する

各リポジトリの対応commitは[data/sources.json](data/sources.json)に記録します。

## このリポジトリに残すもの

- 3リポジトリを組み合わせるためのAI作業フロー
- 参照先と対応commitの一覧
- 旧マニュアルの履歴資料
- `vehicles/`にある利用者の車両資料

旧マニュアルは[アーカイブ](docs/archive/StormworksMicrocontrollerManual-legacy.md)として残しています。新規のLua仕様やパーツ情報は、分離後のリポジトリを参照してください。

## 現在のスナップショット

- パーツカタログ：`stormworks-partdata` の705パーツ版
- マイコンLua資料：`stormworks-microcontroller-lua` の初期版
- DSL/XML定義：`storm-microcontroller-language` の参照commit

パーツデータの再配布条件は確認中です。公開範囲を変更する前に、元データのライセンスと寄稿者の意向を確認してください。

