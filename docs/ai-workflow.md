# AI作業フロー

目的は、パーツの説明から勝手にチャンネル番号やゲーム挙動を発明することではなく、実際に配線できるI/O契約を先に固定し、その契約に対してLuaとマイコンDSLを作ることです。

## 1. 成果物の種類を分ける

最初に次のどれを作るかを明確にします。

- Lua Script本文だけ
- `.sw-net` / `.sw-mcl` / `project.json` を含むマイコン一式
- パーツ接続を含む車両側の設計資料

Lua本文だけなら、パーツカタログから論理ノードを調べてI/O契約を作ります。マイコン一式なら、ゲートやLuaノードの構造は `storm-microcontroller-language` の `spec` を正規ソースとして使います。

## 2. 参照DSLを先に調べる

参照リポジトリを作業環境に用意した場合は、まず次を実行します。

```powershell
pnpm cli spec LUA --json
pnpm cli spec --list
```

`LUA` のポートとプロパティを自作の定義で置き換えません。特に、Luaノードのスクリプト本体と、`.sw-net` の `script_ref` によるファイル参照を混同しないようにします。

`script_ref` を使う場合のファイルパスは、参照リポジトリの仕様に従い、`script_ref` を含む `.sw-net` 文書からの相対パスとして管理します。最終的には次の検証を行います。

```powershell
pnpm cli check-dsl <project.json>
pnpm cli typecheck-dsl <project.json>
```

## 3. パーツからI/O契約を作る

`stormworks-partdata`の`data/parts-catalog.json`で目的のパーツを検索し、`logicNodes`のラベルと説明を確認します。マイコンの配線候補なら`--mcu-relevant`、LuaのI/O候補なら`--lua-relevant`を付け、ノードなし・物理接続だけのパーツを先に除外します。

```powershell
# stormworks-partdata のリポジトリルートで実行
python tools/query_parts.py --mcu-relevant --search "radar" --json
python tools/query_parts.py --lua-relevant --category Sensors --json
```

最低限、次を表にします。

| 項目 | 例 | 決めること |
|---|---|---|
| パーツ | `Physics Sensor` | どの部品を使うか |
| 論理ノード | `Composite Output` | どの端子を配線するか |
| 方向 | `output` | マイコンの入力か出力か |
| 種別 | `composite` | `input.get*` の対象か、映像・物理接続か |
| 意味 | `Value 1 = x position` | コード上の変数名、単位、範囲 |
| MCUチャンネル | 車両ごとに決定 | 実際のインターフェースノードの番号 |

パーツの`logicNodes`の配列位置をLuaチャンネル番号へ直接変換してはいけません。チャンネル番号は、マイコンのインターフェースノードと車両配線で決まります。

## 4. Luaの契約をコードより先に書く

例として、次のような契約を作ってからコードを書きます。

```text
number input 1  = vehicle speed [m/s]
boolean input 1 = master enable
composite input, number channel 1 = Physics Sensor x position [m]
number output 1 = steering command [-1, 1]
boolean output 1 = sensor valid
```

Compositeの説明にあるチャンネル番号は、パーツが出力するComposite内部の番号です。`composite input` 自体を何番の外部インターフェースへ接続するかとは別の番号です。

## 5. Luaコードを作る

Lua Script補足の実行モデルに従い、次の順序で実装します。

1. `onTick` で入力を読む。
2. 入力値の単位、符号、範囲、無効値を処理する。
3. 必要な状態をトップレベルの変数またはテーブルで保持する。
4. `onTick` で数値・真偽値出力を設定する。
5. モニター出力が必要なときだけ `onDraw` で描画する。
6. Luaノードの文字数制限内か確認する。

`onDraw` のフレーム周期と `onTick` の周期は同じとは限らないため、描画側で制御ロジックを進めません。制御状態は `onTick` 側で更新し、`onDraw` は最後に計算された状態を表示します。

## 6. 検証する

検証結果には、少なくとも次を記録します。

- DSLの構造検証結果
- DSLの信号型検証結果
- Luaの文字数
- 入出力チャンネル一覧
- 実機またはゲーム内で確認した項目
- まだ確認していない挙動

ローカルのLua処理系で構文が通っても、StormworksのAPI、実行タイミング、センサーの出力意味まで検証できたことにはなりません。

## 事実の扱い

- `verified`：参照リポジトリの検証済みメモ、または明示的なゲーム内確認に基づく。
- `documented`：既存資料またはデータに記載されているが、この作業で実機確認していない。
- `inferred`：複数の記述から導いた解釈。
- `unconfirmed`：候補として残しているが、断定できない。

AIは`documented`や`inferred`の記述を、実機で確認済みの事実として言い換えてはいけません。
