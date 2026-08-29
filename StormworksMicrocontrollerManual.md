# Stormworks AI向けマイコン資料

この文書は、StormworksのマイコンをAIで作成するための統合入口です。役割ごとの資料は次の2つです。

- [stormworks-microcontroller-lua](https://github.com/kiminihijiki/stormworks-microcontroller-lua)：マイコンLuaの実行モデル、API、制限
- [stormworks-partdata](https://github.com/kiminihijiki/stormworks-partdata)：パーツ、センサー、論理ノード、検索

作業時は[AI作業フロー](docs/ai-workflow.md)に従い、Lua資料とパーツデータを確認してから、必要に応じて外部のDSL/XML検証環境を使います。

旧来の総合マニュアルは[アーカイブ](docs/archive/StormworksMicrocontrollerManual-legacy.md)に保存しています。旧マニュアルの記述は、現在の仕様と照合せずにコード生成の根拠として使わないでください。
