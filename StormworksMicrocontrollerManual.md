# Stormworks マイコン仕様
更新日 : 2026-07-14
## 目次
- [パーツ一覧](#パーツ一覧)
    - [Blocks](#blocks)
    - [Vehicle Control](#vehicle-control)
    - [Mechanics](#mechanics)
    - [Propulsion](#propulsion)
    - [Specialist Equipment](#specialist-equipment)
    - [Logic](#logic)
    - [Displays](#displays)
    - [Sensors](#sensors)
    - [Fluid](#fluid)
    - [Electric](#electric)
    - [Jet Engines](#jet-engines)
    - [Weapons](#weapons)
    - [Modular Engines](#modular-engines)
    - [Industry](#industry)
- [マイコンの概要](#マイコンの概要)
    - [プロパティ](#プロパティ)
    - [ロジック](#ロジック)
    - [シンボル](#シンボル)
- [ノード一覧](#ノード一覧)
    - [インターフェース](#インターフェース)
    - [LOGICAL](#logical)
    - [ARITHMETIC](#arithmetic)
    - [CONTROL](#control)
    - [COMPOSITE](#composite)
    - [PROPERTY](#property)
- [Lua Script ノードの詳細](#lua-script-ノードの詳細)
    - [概要](#概要)
    - [文](#文)
    - [nil 型](#nil-型)
    - [bool 型](#bool-型)
    - [number 型](#number-型)
    - [string 型](#string-型)
    - [function 型](#function-型)
    - [table 型](#table-型)
    - [関数](#関数)
    - [描画関数](#描画関数)
    - [小技](#小技)
- [基本動作](#基本動作)

## パーツ一覧
これらはマイコン等と信号のやり取りを行えるパーツの一覧である。マイコンとの入出力は、インターフェースノードを使用する。
##### ※mod等で追加されたパーツはここでは説明しない。

### Blocks
- Handle : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:red">🔴Occupied</span></code>
<br>プレイヤーがインタラクトしている間 true を出力する。

### Vehicle Control
- 各種座席 : <code>**入力** <span style="color:cyan">🔵Headset Video</span>、<span style="color:orange">🟡Headset Audio</span></code> 、<code>**出力** <span style="color:red">🔴Occupied</span>、<span style="color:red">🔴Trigger</span>、<span style="color:red">🔴Hotkey 1</span>、<span style="color:red">🔴Hotkey 2</span>、<span style="color:red">🔴Hotkey 3</span>、<span style="color:red">🔴Hotkey 4</span>、<span style="color:red">🔴Hotkey 5</span>、<span style="color:red">🔴Hotkey 6</span>、<span style="color:green">🟢Look X</span>、<span style="color:green">🟢Look Y</span>、<span style="color:green">🟢Axis 1</span>、<span style="color:green">🟢Axis 2</span>、<span style="color:green">🟢Axis 3</span>、<span style="color:green">🟢Axis 4</span>、<span style="color:magenta">🟣Seat data</span>、<span style="color:orange">🟡Headset Audio</span></code>
<br>プレイヤーが座席に座っている間各種操作を受け付ける。`Trigger`、`Hotkey 1~6` には 名前と Toggle/Push、`Axis 1~4` には名前と感度、キーを離したら値を維持/リセット、トリムが設定できる。`Seat data` は `Hotkey 1~6` が bool ch1~6、`Trigger` は bool ch31、`Occupied` は bool ch32、`Axis 1~4` は number ch1~4、`Look X` は number ch9、`Look Y` は number ch10 となっている。基本的な入出力は上記の通りだが例外が存在する。
- Gyro : <code>**入力** <span style="color:red">🔴Hover mode</span>、<span style="color:green">🟢Roll</span>、<span style="color:green">🟢Pitch</span>、<span style="color:green">🟢Yaw</span>、<span style="color:green">🟢UP/DOWN</span></code> 、<code>**出力** <span style="color:green">🟢Stabilised Roll</span>、<span style="color:green">🟢Stabilised Pitch</span>、<span style="color:green">🟢Stabilised Yaw</span>、<span style="color:green">🟢Stabilised UP/DOWN</span></code>
<br>ジャイロ。説明が思いつかない。

### Mechanics

### Propulsion

### Specialist Equipment

### Logic

### Displays

### Sensors

### Fluid

### Electric

### Jet Engines

### Weapons

### Modular Engines

### Industry

## マイコンの概要
### プロパティ
- 名前 : マイコンの名前を設定する。アルファベット、一部記号が使用可能。
- 説明 : マイコンの説明を設定する。アルファベット、一部記号が使用可能。
- 幅 / 高さ : 幅 / 高さを設定する。最小は各 1 マス。最大は各 6 マス。

### ロジック
- 入力ノード
    - 🔴<span style="color:red">オンオフ</span> : マイコン外から true / false を一つ入力する。
    - 🟢<span style="color:limegreen">数値</span> : マイコン外から float 値を一つ入力する。
    - 🟣<span style="color:magenta">複合信号</span> : マイコン外から bool 32ch + float 32ch の複合信号を一つ入力する。
    - 🔵<span style="color:cyan">映像</span> : マイコン外から映像を一つ入力する。
    - 🟡<span style="color:orange">音声</span> : マイコン外から音声を一つ入力する。
- 出力ノード
    - 🔴<span style="color:red">オンオフ</span> : マイコン外に true / false を一つ出力する。
    - 🟢<span style="color:limegreen">数値</span> : マイコン外に float 値を一つ出力する。
    - 🟣<span style="color:magenta">複合信号</span> : マイコン外に bool 32ch + float 32ch の複合信号を一つ出力する。
    - 🔵<span style="color:cyan">映像</span> : マイコン外に映像を一つ出力する。
    - 🟡<span style="color:orange">音声</span> : マイコン外に音声を一つ出力する。

    各入出力ノードには名前、説明を簡潔に設定できる。アルファベット、一部記号が使用可能。<br>
    設定しなくてもよいが、ノードの配線で地獄を見るので名前だけでも設定することを推奨する。<br>
    説明は、何に使うかではなくどのような信号が入出力されるかを簡潔に書くことを推奨する。

### シンボル
- シンボル : マイコンのシンボルを 16 x 16px で設定できる。

## ノード一覧
これらはマイコン内でのみ使用可能なノードの一覧である。マイコン外との入出力は、インターフェースノードを使用する。

### インターフェース
- 🔴<span style="color:red">オンオフ</span> : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:red">🔴on/off input</span></code>
    <br>マイコン外から true / false を一つ入力する。
- 🟢<span style="color:limegreen">数値</span> : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:limegreen">🟢float input</span></code>
    <br>マイコン外から float 値を一つ入力する。
- 🟣<span style="color:magenta">複合信号</span> : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:magenta">🟣composite input</span></code>
    <br>マイコン外から bool 32ch + float 32ch の複合信号を一つ入力する。
- 🔵<span style="color:cyan">映像</span> : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:cyan">🔵video input</span></code>
    <br>マイコン外から映像を一つ入力する。
- 🟡<span style="color:orange">音声</span> : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:orange">🟡audio input</span></code>
    <br>マイコン外から音声を一つ入力する。
- 🔴<span style="color:red">オンオフ</span> : <code>**入力** <span style="color:red">🔴on/off output</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
    <br>マイコン外に true / false を一つ出力する。
- 🟢<span style="color:limegreen">数値</span> : <code>**入力** <span style="color:limegreen">🟢float output</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
    <br>マイコン外に float 値を一つ出力する。
- 🟣<span style="color:magenta">複合信号</span> : <code>**入力** <span style="color:magenta">🟣composite output</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
    <br>マイコン外に bool 32ch + float 32ch の複合信号を一つ出力する。
- 🔵<span style="color:cyan">映像</span> : <code>**入力** <span style="color:cyan">🔵video output</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
    <br>マイコン外に映像を一つ出力する。
- 🟡<span style="color:orange">音声</span> : <code>**入力** <span style="color:orange">🟡audio output</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
    <br>マイコン外に音声を一つ出力する。

### LOGICAL
- `OR` : <code>**入力** 🔴<span style="color:red">A</span> 、🔴<span style="color:red">B</span></code> 、<code>**出力** 🔴<span style="color:red">A or B</span></code>
    <br>X = A or B
- `AND` : <code>**入力** 🔴<span style="color:red">A</span> 、🔴<span style="color:red">B</span></code> 、<code>**出力** 🔴<span style="color:red">A and B</span></code>
    <br>X = A and B
- `NOT` : <code>**入力** 🔴<span style="color:red">A</span></code> 、<code>**出力** 🔴<span style="color:red">not A</span></code>
    <br>X = not A
- `NOR` : <code>**入力** 🔴<span style="color:red">A</span> 、🔴<span style="color:red">B</span></code> 、<code>**出力** 🔴<span style="color:red">A nor B</span></code>
    <br>X = not A and not B
- `NAND` : <code>**入力** 🔴<span style="color:red">A</span> 、🔴<span style="color:red">B</span></code> 、<code>**出力** 🔴<span style="color:red">A nand B</span></code>
    <br>X = not A or not B
- `XOR` : <code>**入力** 🔴<span style="color:red">A</span> 、🔴<span style="color:red">B</span></code> 、<code>**出力** 🔴<span style="color:red">A xor B</span></code>
    <br>X = A and not B or not A and B
- `Boolean f(x,y,z,w)` : <code>**入力** 🔴<span style="color:red">x</span> 、🔴<span style="color:red">y</span> 、🔴<span style="color:red">z</span> 、🔴<span style="color:red">w</span></code> 、<code>**出力** 🔴<span style="color:red">f(x,y,z,w)</span></code>
    <details><summary>4入力1出力の演算ノード。</summary><div>
        <code>|(or)</code>、<code>&(and)</code>、<code>!(not)</code>、<code>^(xor)</code>、<code>true</code>、<code>false</code> を使用し演算を実行できる。
    </div></details>
- `Boolean f(x,y,z,w,a,b,c,d)` : <code>**入力** 🔴<span style="color:red">x</span> 、🔴<span style="color:red">y</span> 、🔴<span style="color:red">z</span> 、🔴<span style="color:red">w</span> 、🔴<span style="color:red">a</span> 、🔴<span style="color:red">b</span> 、🔴<span style="color:red">c</span> 、🔴<span style="color:red">d</span></code> 、<code>**出力** 🔴<span style="color:red">f(x,y,z,w,a,b,c,d)</span></code>
    <details><summary>8入力1出力の演算ノード。</summary><div>
        <code>|(or)</code>、<code>&(and)</code>、<code>!(not)</code>、<code>^(xor)</code>、<code>true</code>、<code>false</code> を使用し演算を実行できる。
    </div></details>
- `Constant On Signal` : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** 🔴<span style="color:red">on signal</span></code>
    <br>常に true を出力する。
- `Pulse (Toggle to Push)` : <code>**入力** 🔴<span style="color:red">toggle signal</span></code> 、<code>**出力** 🔴<span style="color:red">pulse</span></code>
    <br>入力が true / false (またはその両方) になった瞬間の 1 tick のみ true を出力する。
- `Push to Toggle` : <code>**入力** 🔴<span style="color:red">signal</span></code> 、<code>**出力** 🔴<span style="color:red">internal state</span></code>
    <br>入力が true になるたびに出力が入れ替わる。初期値は false 。
- `SR Latch` : <code>**入力** 🔴<span style="color:red">set</span></code> 、<code>**入力** 🔴<span style="color:red">reset</span></code> 、<code>**出力** 🔴<span style="color:red">output</span></code> 、<code>🔴<span style="color:red">not output</span></code>
    <br>ラッチ回路。入力 `set`、`reset` と、出力 `output`、`not output` があり、入力がすべて true のときはリセット優先。
- `JK Flip Flop` : <code>**入力** 🔴<span style="color:red">set</span></code> 、<code>🔴<span style="color:red">reset</span></code> 、<code>**出力** 🔴<span style="color:red">output</span></code> 、<code>🔴<span style="color:red">not output</span></code>
    <br>ラッチ回路。入力 `set`、`reset` と、出力 `output`、`not output` があり、入力がすべて true のときは反転 (トグル) 。

### ARITHMETIC
- `Add` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🟢<span style="color:limegreen">A + B</span></code>
    <br>X = A + B
- `Subtract` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🟢<span style="color:limegreen">A - B</span></code>
    <br>X = A - B
- `Multiply` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🟢<span style="color:limegreen">A * B</span></code>
    <br>X = A * B
- `Divide` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🟢<span style="color:limegreen">A / B</span></code>
    <br>X = A / B
- `Modulo (fmod)` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🟢<span style="color:limegreen">A % B</span></code>
    <br>X = A % B
- `Abs` : <code>**入力** 🟢<span style="color:limegreen">input number</span></code> 、<code>**出力** 🟢<span style="color:limegreen">absolute value</span></code>
    <br>X = | A |
- `Equal` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🔴<span style="color:red">A = B</span></code>
    <br>数値 A = B のとき true を出力する。`epsilon` を設定可能。
- `Delta` : <code>**入力** 🟢<span style="color:limegreen">input value</span></code> 、<code>**出力** 🟢<span style="color:limegreen">delta of input value</span></code>
    <br>X = 現在値と 1 tick 前の値との増減を出力する。
- `Clamp` : <code>**入力** 🟢<span style="color:limegreen">input number</span></code> 、<code>**出力** 🟢<span style="color:limegreen">clamped input</span></code>
    <br>X = A を `min` から `max` の範囲内に収める。範囲を超えたときは min または max を出力する。
- `f(x)` : <code>**入力** 🟢<span style="color:limegreen">x</span></code> 、<code>**出力** 🟢<span style="color:limegreen">f(x)</span></code>
    <details><summary>1入力1出力の演算ノード。</summary><div>
    <code>+</code>、<code>-</code>、<code>*</code>、<code>/</code>、<code>%</code>、<code>^</code>、<code>pi</code>、<code>pi2</code>、<code>sin(x)</code>、<code>cos(x)</code>、<code>tan(x)</code>、<code>asin(x)</code>、<code>acos(x)</code>、<code>atan(x)</code>、<code>atan2(y, x)</code>、<code>max(x, y)</code>、<code>min(x, y)</code>、<code>ceil(x)</code>、<code>floor(x)</code>、<code>round(x, y)</code>、<code>abs(x)</code>、<code>sgn(x)</code>、<code>sqrt(x)</code>、<code>len(x, y)</code>、<code>len2(x, y)</code>、<code>lerp(x, y, z)</code>、<code>clamp(x, y, z)</code> を使用し演算を実行できる。sgn(x) は x = 0 のとき 1 を出力する。
    </div></details>
- `f(x, y, z)` : <code>**入力** 🟢<span style="color:limegreen">x</span> 、🟢<span style="color:limegreen">y</span> 、🟢<span style="color:limegreen">z</span></code> 、<code>**出力** 🟢<span style="color:limegreen">f(x, y, z)</span></code>
    <details><summary>3入力1出力の演算ノード。</summary><div>
    <code>+</code>、<code>-</code>、<code>*</code>、<code>/</code>、<code>%</code>、<code>^</code>、<code>pi</code>、<code>pi2</code>、<code>sin(x)</code>、<code>cos(x)</code>、<code>tan(x)</code>、<code>asin(x)</code>、<code>acos(x)</code>、<code>atan(x)</code>、<code>atan2(y, x)</code>、<code>max(x, y)</code>、<code>min(x, y)</code>、<code>ceil(x)</code>、<code>floor(x)</code>、<code>round(x, y)</code>、<code>abs(x)</code>、<code>sgn(x)</code>、<code>sqrt(x)</code>、<code>len(x, y)</code>、<code>len2(x, y)</code>、<code>lerp(x, y, z)</code>、<code>clamp(x, y, z)</code> を使用し演算を実行できる。sgn(x) は x = 0 のとき 1 を出力する。
    </div></details>
- `f(x, y, z, w, a, b, c, d)` : <code>**入力** 🟢<span style="color:limegreen">x</span> 、🟢<span style="color:limegreen">y</span> 、🟢<span style="color:limegreen">z</span> 、🟢<span style="color:limegreen">w</span> 、🟢<span style="color:limegreen">a</span> 、🟢<span style="color:limegreen">b</span> 、🟢<span style="color:limegreen">c</span> 、🟢<span style="color:limegreen">d</span></code> 、<code>**出力** 🟢<span style="color:limegreen">f(x, y, z, w, a, b, c, d)</span></code>
    <details><summary>8入力1出力の演算ノード。</summary><div>
    <code>+</code>、<code>-</code>、<code>*</code>、<code>/</code>、<code>%</code>、<code>^</code>、<code>pi</code>、<code>pi2</code>、<code>sin(x)</code>、<code>cos(x)</code>、<code>tan(x)</code>、<code>asin(x)</code>、<code>acos(x)</code>、<code>atan(x)</code>、<code>atan2(y, x)</code>、<code>max(x, y)</code>、<code>min(x, y)</code>、<code>ceil(x)</code>、<code>floor(x)</code>、<code>round(x, y)</code>、<code>abs(x)</code>、<code>sgn(x)</code>、<code>sqrt(x)</code>、<code>len(x, y)</code>、<code>len2(x, y)</code>、<code>lerp(x, y, z)</code>、<code>clamp(x, y, z)</code> を使用し演算を実行できる。sgn(x) は x = 0 のとき 1 を出力する。
    </div></details>

### CONTROL
- `Threshold` : <code>**入力** 🟢<span style="color:limegreen">input number</span></code> 、<code>**出力** 🔴<span style="color:red">within threshold</span></code>
    <br>閾値。入力された数値が `low` から `high` の範囲内のとき true を出力する。
- `Capacitor` : <code>**入力** 🔴<span style="color:red">charge</span></code> 、<code>**出力** 🔴<span style="color:red">discharge</span></code>
    <br>`charge` に指定した秒数 (最大10秒) 以上 true が入力されると true を出力する / 入力が false になってから `discharge` に指定した秒数 true を出力する (最大10秒) 。
- `Blinker` : <code>**入力** 🔴<span style="color:red">control signal</span></code> 、<code>**出力** 🔴<span style="color:red">blinking signal</span></code>
    <br>入力が true の間、`on duration` (最大5秒) の true 出力と `off duration` (最大5秒) の false 出力を繰り返す。
- `Greater Than` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🔴<span style="color:red">A > B</span></code>
    <br>数値 A > B のとき true を出力する。
- `Less Than` : <code>**入力** 🟢<span style="color:limegreen">A</span> 、🟢<span style="color:limegreen">B</span></code> 、<code>**出力** 🔴<span style="color:red">A < B</span></code>
    <br>数値 A < B のとき true を出力する。
- `Numerical Junction` : <code>**入力** 🟢<span style="color:limegreen">value</span> 、🔴<span style="color:red">switch signal</span></code> 、<code>**出力** 🟢<span style="color:limegreen">on value</span> 、🟢<span style="color:limegreen">off value</span></code>
    <br>オンオフで数値の出力先を切り替える。
- `Numerical Switchbox` : <code>**入力** 🟢<span style="color:limegreen">on number</span> 、🟢<span style="color:limegreen">off number</span> 、🔴<span style="color:red">switch signal</span></code> 、<code>**出力** 🟢<span style="color:limegreen">value</span></code>
    <br>オンオフで数値の入力元を切り替える。
- `Timer (RTF)` : <code>**入力** 🔴<span style="color:red">timer enable</span> 、🔴<span style="color:red">reset</span> 、🟢<span style="color:limegreen">duration</span></code> 、<code>**出力** 🔴<span style="color:red">output</span></code>
    <br>1回のみ指定時間の true を出力し、その後はリセットされるまで false を出力する。
- `Timer (RTO)` : <code>**入力** 🔴<span style="color:red">timer enable</span> 、🔴<span style="color:red">reset</span> 、🟢<span style="color:limegreen">duration</span></code> 、<code>**出力** 🔴<span style="color:red">output</span></code>
    <br>1回のみ true を指定時間遅延する。その後はリセットされるまで遅延せず出力する。
- `Timer (TOF)` : <code>**入力** 🔴<span style="color:red">timer enable</span> 、🟢<span style="color:limegreen">duration</span></code> 、<code>**出力** 🔴<span style="color:red">output</span></code>
    <br>入力が true になると指定時間 true を出力する。入力が false になるとリセットされる。
- `Timer (TON)` : <code>**入力** 🔴<span style="color:red">timer enable</span> 、🟢<span style="color:limegreen">duration</span></code> 、<code>**出力** 🔴<span style="color:red">output</span></code>
    <br>入力が true になると指定時間 true を遅延する。入力が false になるとリセットされる。
- `PID Controller` : <code>**入力** 🟢<span style="color:limegreen">setpoint</span> 、🟢<span style="color:limegreen">process variable</span> 、🔴<span style="color:red">active</span></code> 、<code>**出力** 🟢<span style="color:limegreen">control output</span></code>
    <br>PID制御を実行する。`P`、`I`、`D` を設定可能。
- `PID Controller (advanced)` : <code>**入力** 🟢<span style="color:limegreen">setpoint</span> 、🟢<span style="color:limegreen">process variable</span> 、🔴<span style="color:red">active</span> 、🟢<span style="color:limegreen">P gain</span> 、🟢<span style="color:limegreen">I gain</span> 、🟢<span style="color:limegreen">D gain</span></code> 、<code>**出力** 🟢<span style="color:limegreen">control output</span></code>
    <br>PID制御を実行する。
- `Memory Register` : <code>**入力** 🔴<span style="color:red">set</span> 、🔴<span style="color:red">reset</span> 、🟢<span style="color:limegreen">number to store</span></code> 、<code>**出力** 🟢<span style="color:limegreen">stored number</span></code>
    <br>`reset value` が設定可能。set が true の間は常に保存値を更新。reset が true になると、保存値が reset value に更新される。
- `Up Down Counter` : <code>**入力** 🔴<span style="color:red">up</span> 、🔴<span style="color:red">down</span> 、🔴<span style="color:red">reset</span></code> 、<code>**出力** 🟢<span style="color:limegreen">value</span></code>
    <br>`increment`、`reset value`、`clamp` を設定可能。1 tick ごとに increment を up が true の間加算、down が true の間減算する。reset が true になるとカウントが reset value に更新される。

### COMPOSITE
- `Composite Switchbox` : <code>**入力** 🟣<span style="color:magenta">on composite</span> 、🟣<span style="color:magenta">off composite</span> 、🔴<span style="color:red">switch signal</span></code> 、<code>**出力** 🟣<span style="color:magenta">composite output</span></code>
        <br>オンオフで複合信号の入力元を切り替える。
- `Video Switchbox` : <code>**入力** 🔵<span style="color:cyan">video on</span> 、🔵<span style="color:cyan">video off</span> 、🔴<span style="color:red">switch signal</span></code> 、<code>**出力** 🔵<span style="color:cyan">video output</span></code>
        <br>オンオフで映像の入力元を切り替える。
- `Audio Switchbox` : <code>**入力** 🟡<span style="color:orange">audio on</span> 、🟡<span style="color:orange">audio off</span> 、🔴<span style="color:red">switch signal</span></code> 、<code>**出力** 🟡<span style="color:orange">audio output</span></code>
        <br>オンオフで音声の入力元を切り替える。
- `Composite Binary to Number` : <code>**入力** 🟣<span style="color:magenta">signal to convert</span></code> 、<code>**出力** 🟢<span style="color:limegreen">number output</span></code>
        <br>複合信号の bool 32ch を数値に変換して出力する。
- `Number to Composite Binary` : <code>**入力** 🟢<span style="color:limegreen">number to convert</span></code> 、<code>**出力** 🟣<span style="color:magenta">composite output</span></code>
        <br>数値を複合信号の bool 32ch に変換して出力する。
- `Composite Read (Number)` : <code>**入力** 🟣<span style="color:magenta">composite signal</span></code> 、<code>**出力** 🟢<span style="color:limegreen">number output</span></code>
        <br>`read channel` を設定可能。複合信号の指定チャンネルの数値を出力する。read channel は数値入力でも指定可能。
- `Composite Read (on/off)` : <code>**入力** 🟣<span style="color:magenta">composite signal</span></code> 、<code>**出力** 🔴<span style="color:red">on/off output</span></code>
        <br>`read channel` を設定可能。複合信号の指定チャンネルのオンオフを出力する。read channel は数値入力でも指定可能。
- `Composite Write (Number)` : <code>**入力** 🟣<span style="color:magenta">composite signal</span> 、🟢<span style="color:limegreen">input number</span></code> 、<code>**出力** 🟣<span style="color:magenta">composite output</span></code>
        <br>`start channel`、`channel count` を設定可能。複合信号の指定チャンネルに数値を入力する。start channel は数値入力でも指定可能。
- `Composite Write (on/off)` : <code>**入力** 🟣<span style="color:magenta">composite signal</span> 、🔴<span style="color:red">input on/off</span></code> 、<code>**出力** 🟣<span style="color:magenta">composite output</span></code>
        <br>`start channel`、`channel count` を設定可能。複合信号の指定チャンネルにオンオフを入力する。start channel は数値入力でも指定可能。
- `Lua Script` : <code>**入力** 🟣<span style="color:magenta">composite signal</span> 、🔵<span style="color:cyan">video input</span></code> 、<code>**出力** 🟣<span style="color:magenta">composite output</span> 、🔵<span style="color:cyan">video output</span></code>
    <br>スクリプトを設定可能。詳細は後述。

### PROPERTY
- `Property Dropdown` : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** 🟢<span style="color:limegreen">selected option</span></code>
        <br>`property name`、`label`、`value` を設定可能。ドロップダウンで選択した値を出力する。オプションを複数設定可能。Lua Script ノードのスクリプト内で参照可能。
- `Property Slider` : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** 🟢<span style="color:limegreen">slider value</span></code>
        <br>`property name`、`min value`、`max value`、`rounding`、`value` を設定可能。スライダーで数値を出力する。オプションを複数設定可能。Lua Script ノードのスクリプト内で参照可能。
- `Property Number` : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** 🟢<span style="color:limegreen">number value</span></code>
        <br>`property name`、`value` を設定可能。数値を出力する。Lua Script ノードのスクリプト内で参照可能。
- `Property Toggle` : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** 🔴<span style="color:red">on/off value</span></code>
        <br>`property name`、`on label`、`off label`、`value` を設定可能。トグルでオンオフを出力する。Lua Script ノードのスクリプト内で参照可能。
- `Property Text` : <code>**入力** <span style="color:gray">なし</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
        <br>`property name`、`value` を設定可能。テキストを出力する。Lua Script ノードのスクリプト内で**のみ**参照可能。
- `Tooltip Number` : <code>**入力** 🟢<span style="color:limegreen">display number</span> 、🔴<span style="color:red">is error</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
        <br>`property name`、`display` を設定可能。ツールチップで数値を表示する。
- `Tooltip On/Off` : <code>**入力** 🔴<span style="color:red">display signal</span></code> 、<code>**出力** <span style="color:gray">なし</span></code>
        <br>`property name`、`on label`、`off label`、`display` を設定可能。ツールチップでオンオフを表示する。

## Lua Script ノードの詳細
### 概要
- スクリプトは Lua 5.3 で記述される。このセクションでは、Stormworks の Lua Script ノードで使用できる関数や機能について説明する。Lua の基本的な文法や構文については説明しない。
- スクリプトは最大 8192 文字まで記述できる。一回の実行で 1000 ms を超えるスクリプトは強制終了される。

### 文
- Lua Script ノードで使用できる文は、`if`、`while`、`for`、`repeat...until`、`goto`、`break` などの基本的な制御フロー文が使用できる。

### 型
- 型は、値の種類を表すものである。Stormworks の Lua Script ノードでは、`nil`、`bool`、`number`、`string`、`function`、`table` の6つの基本的な型が使用できる。

    ### nil 型
    - nil 型は、値が存在しないことを表す特別な型である。nilは、変数が初期化されていない場合や、存在しないプロパティや入力を参照した場合などに返される。
    - nil は、他の値と等しくない。つまり、nil == nil は true であるが、nil == 0 や nil == "" は false である。

    ### bool 型
    - bool 型は、true または false として扱われる。false になるのは、false と nil のみである。0 や空文字列も true として扱われる。
    - bool 型の演算は、`<`、`>`、`<=`、`>=`、`==`、`~=`、`and`、`or`、`not` などの演算子が使用できる。

    ### number 型
    - number 型は、基本的に倍精度浮動小数点数 (double precision floating point) として扱われる。
    - number 型の演算は、`+`、`-`、`*`、`/`、`%`、`^`、`-n (単項マイナス演算子として)`、`// (切り捨て除算)`、`<< (ビット左シフト)`、`>> (ビット右シフト)`、`& (ビットAND)`、`| (ビットOR)`、`~n (ビットNOT)`、`~ (ビットXOR)` などの演算子が使用できる。
    - `0x` で始まる16進数リテラルや、`0b` で始まる2進数リテラルを使用して表すこともできる。

    ### string 型
    - string 型は、文字列として扱われる。文字列は、ダブルクォーテーション `"` で囲むことで表される。`\n` は改行を表す。
    - 文字列の演算は、`#` (文字列の長さを返す) と `..` (文字列の連結) などの演算子が使用できる。
    - string 型では、文字列を操作するための関数が使用できる。
    - format string を多用する。使用できる format string は以下の通り。
        <details><summary>詳細</summary><div>

        - `%o` : 整数を 8 進数で表す。
        - `%d` : 整数を 10 進数で表す。
        - `%x` : 整数を 16 進数で表す。小文字で表す。
        - `%X` : 整数を 16 進数で表す。大文字で表す。
        - `%u` : 整数を符号なし整数として 10 進数で表す。
        - `%f` : 浮動小数点数を10 進数で表す。`%m.nf` の形式で小数点前後の桁数 (m は整数、n は小数点以下の桁数) を指定できる。
        - `%e` : 浮動小数点数を指数表記で表す。`%m.nex` の形式で指数 x を指定できる。小文字で表す。
        - `%E` : 浮動小数点数を指数表記で表す。`%m.nEx` の形式で指数 x を指定できる。大文字で表す。
        - `%g` : 浮動小数点数を、指数表記 `%e` と通常の表記 `%f` のどちらか短い方で表す。
        - `%G` : 浮動小数点数を、指数表記 `%E` と通常の表記 `%f` のどちらか短い方で表す。
        - `%s` : 文字列を表す。
        - `%q` : nil、true、false、数値を表す。
        - `%0md` のように 0 と m を付けると、整数を m 桁で表し、足りない分を 0 で埋めることができる。  
        - また、`%+d` のように + を付けると正の数に + を付けて、`% d` のようにスペースを付けると正の数にスペースを付けて表すことができる。
        </div></details>
    - 使用できる関数は下記の通り。
        <details><summary>詳細</summary><div>

        - `string.format("format string", a)` で、a を format string に従ってフォーマットした文字列を返す。
        - `a = string.sub(s, i, j)` で、文字列 s のインデックス i から j までの部分文字列を返す。i と j は省略可能で、省略した場合はそれぞれ 1 と #s になる。
        - `a = string.len(s)` で、文字列 s の長さを返す。`a = #s` とすることで同じ値を得ることができる。
        - `a, b = string.find(s, "pattern", init, plain)` で、文字列 s の中から、インデックス init 以降で pattern にマッチする部分を検索する。init と plain は省略可能で、省略した場合はそれぞれ 1 と false になる。検索に成功すると、マッチした部分の開始インデックスと終了インデックスを返す。検索に失敗すると nil を返す。
        - `a = string.gsub(s, "pattern", repl, n)` で、文字列 s の中から pattern にマッチする部分を repl に置換した文字列を返す。n は置換する回数で、省略した場合はすべて置換する。
        - `a = string.upper(s)` で、文字列 s をすべて大文字に変換した文字列を返す。
        - `a = string.lower(s)` で、文字列 s をすべて小文字に変換した文字列を返す。
        - `a = string.reverse(s)` で、文字列 s を逆順にした文字列を返す。
        - `a = string.rep(s, n, sep)` で、文字列 s を n 回繰り返した文字列を返す。sep は区切り文字で、省略した場合は空文字列になる。
        - `a = string.byte(s, i, j)` で、文字列 s のインデックス i から j までの部分文字列の各文字のバイト値を返す。i と j は省略可能で、省略した場合はそれぞれ 1 と #s になる。
        - `a = string.char(...)` で、引数のバイト値を文字に変換した文字列を返す。
        </div></details>

    ### function 型
    - function 型は、関数を表す型である。関数は、`function` キーワードを使用して定義される。関数は、引数を取ることができ、値を返すことができる。
    - 変数に関数を代入することもできる。一例として、`sdT = screen.drawText` とすることで、`sdT(x, y, text)` と呼び出すことができるようになる。

    ### table 型
    - table 型は、唯一のデータ構造であり、配列や辞書などの複雑なデータ構造を表すことができる。主に配列と、キーワードと値のペアを格納する辞書 (連想配列) として使用される。
    - 他のプログラミング言語と異なり、インデックスが 1 から始まることに注意する必要がある。
    - テーブルにテーブルを格納することもできる。
    - 使用できる関数は下記の通り。
        <details><summary>詳細</summary><div>

        - `ipairs(t)` と `pairs(t)` を使用してテーブルを反復処理できる。`ipairs` は配列に対して使用され、`pairs` は連想配列に対して使用される。
        - `table.insert(t, value)` でテーブルの末尾に値を追加できる。
        - `table.insert(t, index, value)` でテーブルの指定した位置に値を挿入できる。
        - `a = table.remove(t)` でテーブルの末尾の値を削除できる。削除された値を返す。
        - `a = table.remove(t, index)` でテーブルの指定した位置の値を削除できる。削除された値を返す。
        - `table.pack(...)` で可変長引数をテーブルにパックできる。
        - `table.sort(t)` でテーブルを昇順にソートできる。
        - `table.sort(t, function(x, y) return y < x end)` でテーブルを降順にソートできる。
        - `table.unpack(t)` でテーブルをアンパックできる。変数のほうがテーブルの要素数より多い場合、足りない分は nil になる。
        - `str = table.concat(t, sep, i, j)` でテーブルの要素のうち、インデックス i から j までを文字列に連結できる。sep は区切り文字で、省略した場合は空文字列になる。i と j は省略可能で、省略した場合はそれぞれ 1 と #t になる。
        - `table.move(t, i, j, k, l)` でテーブルの要素のうち、インデックス i から j までを、インデックス k から始まる位置に移動できる。l は移動先のテーブルで、省略した場合は t になる。
        </div></details>

### 関数
- Lua Script ノードで使用できる関数は、Luaの標準ライブラリの一部と、Stormworksが提供する特定の関数が使用できる。
- 関数は、function名(引数) の形式で呼び出される。可変長引数 (...)も使用できる。関数は値を返すことができる。一例として、以下のような関数が使用できる。
    ```lua
    function clamp(x, a, b)
        return math.max(a, math.min(b, x))
    end
    ```
- デフォルトで `function onTick()` と `function onDraw()` の二つの関数を使用できる。`onTick` は 1 tick ごとに呼び出され、`onDraw` はモニターの描画ごとに呼び出される。
- 入力は `input.getNumber(ch)`、`input.getBool(ch)` を使用して取得できる。ch は入力のチャンネル番号で、32ch まで指定可能。onTick 内で呼び出す必要がある。
- 出力は `output.setNumber(ch, value)`、`output.setBool(ch, value)` を使用して設定できる。ch は出力のチャンネル番号で、32ch まで指定可能。onTick 内で呼び出す必要がある。
- `property.getNumber("label")`、`property.getBool("label")`、`property.getText("label")` を使用してプロパティノードの値を取得できる。label はプロパティノードの名前で、ノードごとに一意である必要があり、完全一致する必要がある。
- `math` オブジェクトの関数も使用できる。使用できる関数は下記の通り。
    <details><summary>詳細</summary><div>

    - `a = math.min(x, y)` : x と y のうち小さい方を返す。
    - `a = math.max(x, y)` : x と y のうち大きい方を返す。
    - `a = math.abs(x)` : x の絶対値を返す。
    - `a = math.floor(x)` : x 以下の最大の整数を返す。
    - `a = math.ceil(x)` : x 以上の最小の整数を返す。
    - `a, b = math.modf(x)` : x を整数部分と小数部分に分割して返す。
    - `a = math.fmod(x, y)` : x を y で割った余りを返す。余りが x と同じ符号を持つことが保証される。
    - `a = math.sin(x)` : x の正弦を返す。x はラジアンで指定する。
    - `a = math.cos(x)` : x の余弦を返す。x はラジアンで指定する。
    - `a = math.tan(x)` : x の正接を返す。 x はラジアンで指定する。
    - `a = math.asin(x)` : x の逆正弦を返す。
    - `a = math.acos(x)` : x の逆余弦を返す。
    - `a = math.atan(x)` : x の逆正接を返す。
    - `a = math.atan(y, x)` : y/x の逆正接を返す。
    - `a = math.deg(x)` : x(ラジアン) を度に変換して返す。
    - `a = math.rad(x)` : x(度) をラジアンに変換して返す。
    - `a = math.pi` : 円周率を返す。
    - `a = math.exp(x)` : e^x を返す。
    - `a = math.log(x, base)` : x = (base)^a を満たす a を返す。
    - `a = math.sqrt(x)` : x の正の平方根 a を返す。
    - `a = math.random()` : 0 ~ 1 の乱数を返す。
    - `a = math.random(n)` : 0 ~ n の乱数を返す。
    - `a = math.random(m, n)` : m ~ n の乱数を返す。
    - `a = math.randomseed(x)` : 乱数のシードを設定する。
    - `str = math.type(x)` : x が整数であれば "integer"、そうでなければ "float" を返す。
    - `a = math.tointeger(x)` : x を整数ならそのまま返す。x が小数の場合は nil を返す。
    - `a = math.maxinteger` : x の最大整数を返す。
    - `a = math.mininteger` : x の最小整数を返す。
    - `a = math.huge` : 無限大を返す。どんな数値よりも大きいとして扱われる。
    - `is_left_large = math.ult(x, y)` : x < y を符号なし整数として比較した結果を返す。
    </div></details>

    #### 補足
    - `math` オブジェクトの関数には、ロジックノードにある関数が一部不足している。以下にその代替関数を示す。
        - `clamp(x, a, b)` : x を a から b の範囲内に収める。範囲を超えたときは a または b を返す。
            ```lua
                function clamp(x, a, b)
                    return math.max(a, math.min(x, b))
                end
            ```
        - `thr(x, a, b)` : x が a から b の範囲内にあるかどうかを判定する。
            ```lua
                function thr(x, a, b)
                    return a <= x and x <= b
                end
            ```
        - `len(x1, y1, x2, y2)` : 座標 (x1, y1) と (x2, y2) の距離を返す。
            ```lua
                function len(x1, y1, x2, y2)
                    return math.sqrt((x2 - x1)^2 + (y2 - y1)^2)
                end
            ```
        - `sgn(x)` : x の符号を返す。x > 0 のときは 1、x < 0 のときは -1、x = 0 のときは 0 を返す。(ロジックノードの sgn(x) は x = 0 のとき 1 を返す。)
            ```lua
                function sgn(x)
                    if x > 0 then
                        return 1
                    elseif x < 0 then
                        return -1
                    else
                        return 0 -- ロジックノードの sgn(x) ではここに 1 を入れている
                    end
                end
            ```

- `tostring(value)` で値を文字列に変換できる。nil は `"nil"` が返される。
- `tonumber(value)` で文字列を値に変換できる。
- `tonumber(value, base)` で値を base で指定した値進数 (2 ~ 36) として、10進数の数値に変換できる。
- これ以外に、httpリクエストを送るための `http` オブジェクトなどが存在するが、ここでは説明しない。

### 描画関数
- 映像入力をスクリプトで処理することはできない。映像出力は、`function onDraw()` を使用して描画することで実現される。描画には、`screen` オブジェクトの関数を使用する。
- `screen.setColor(r, g, b, a)` で描画色を設定できる。r、g、b、a はそれぞれ赤、緑、青、アルファの値で、0 から 255 の範囲で指定する。アルファは省略可能で、省略した場合は 255 (不透明) として扱われる。
- `screen.drawClear()` で画面をクリアできる。
- その他の描画関数は下記の通り。
    <details><summary>詳細</summary><div>

    - `screen.drawCircle(x, y, r)` : 座標 (x, y) を中心とする半径 r の円を描く。
    - `screen.drawCircleF(x, y, r)` : 座標 (x, y) を中心とする半径 r の塗りつぶされた円を描く。
    - `screen.drawRect(x, y, w, h)` : 座標 (x, y) を左上隅とする幅 w、高さ h の長方形を描く。
    - `screen.drawRectF(x, y, w, h)` : 座標 (x, y) を左上隅とする幅 w、高さ h の塗りつぶされた長方形を描く。
    - `screen.drawTriangle(x1, y1, x2, y2, x3, y3)` : 座標 (x1, y1)、(x2, y2)、(x3, y3) を頂点とする三角形を描く。
    - `screen.drawTriangleF(x1, y1, x2, y2, x3, y3)` : 座標 (x1, y1)、(x2, y2)、(x3, y3) を頂点とする塗りつぶされた三角形を描く。
    - `screen.drawLine(x1, y1, x2, y2)` : 座標 (x1, y1) と (x2, y2) を結ぶ線を描く。
    - `screen.drawText(x, y, text)` : 座標 (x, y) にテキストを描く。
    - `screen.drawTextBox(x, y, w, h, text, h_align, w_align)` : 座標 (x, y) を左上隅とする幅 w、高さ h のテキストボックスを描く。テキストは自動で改行される。
    - `screen.getHeight()` : 画面の高さを返す。
    - `screen.getWidth()` : 画面の幅を返す。
    - `screen.setMapColorGrass(r, g, b, a)` : 地図の草地の色を設定する。アルファは省略可能。
    - `screen.setMapColorGravel(r, g, b, a)` : 地図の砂利の色を設定する。アルファは省略可能。
    - `screen.setMapColorLand(r, g, b, a)` : 地図の陸地の色を設定する。アルファは省略可能。
    - `screen.setMapColorOcean(r, g, b, a)` : 地図の海の色を設定する。アルファは省略可能。
    - `screen.setMapColorRock(r, g, b, a)` : 地図の岩の色を設定する。アルファは省略可能。
    - `screen.setMapColorSand(r, g, b, a)` : 地図の砂の色を設定する。アルファは省略可能。
    - `screen.setMapColorShallow(r, g, b, a)` : 地図の浅瀬の色を設定する。アルファは省略可能。
    - `screen.setMapColorSnow(r, g, b, a)` : 地図の雪の色を設定する。アルファは省略可能。
    - `screen.drawMap(gps_x, gps_y, zoom)` : 座標 (gps_x, gps_y) を中心に、画面横幅が zoom [km] となる地図を描く。
    - `map.screenToMap(gps_x, gps_y, zoom, screen_h, screen_w, pixel_x, pixel_y)` : 画面上の座標 (pixel_x, pixel_y) が地図上のどの座標に対応するかを返す。前3個の引数は `screen.drawMap` と同じ値を渡す必要がある。
    - `map.mapToScreen(gps_x, gps_y, zoom, screen_h, screen_w, world_x, world_y)` : 地図上の座標 (world_x, world_y) が画面上のどの座標に対応するかを返す。前3個の引数は `screen.drawMap` と同じ値を渡す必要がある。
    </div></details>

### 小技
- 三項演算子は存在しないが、`x = a and b or c` とすることで、a が true のとき b を、そうでないとき c を x に代入することができる。ただし、b が false または nil の場合は、a が true でも c が代入されてしまうことに注意する必要がある。

## 基本動作
- マイコンの基礎遅延は 1 tick (1/60 秒) 。1 ノード につき 1 tick の遅延が追加される。
- 入出力は 1 マスにつき 1 ノードを設定可能だが、カテゴリの違うノードは入出力問わず重ねて設置できる。🔴<span style="color:red">オンオフ</span> ・ 🟢<span style="color:limegreen">数値</span>がカテゴリ 1 、🟣<span style="color:magenta">複合信号</span>が 2 、🔵<span style="color:cyan">映像</span>が 3 、🟡<span style="color:orange">音声</span>が 4 。
<br>同じカテゴリで入力と出力を重ねることはできない。
- 各ノードの出力配線は無限に設定できる。一方入力配線は入力可能な個数が決まっている。