# 確認する順
1. main見る
2. new どこ？
3. 左右判定ある？
4. 呼ばれるメソッド探す
5. コンパイルエラー候補見る

# 左右判定（継承・implements）
`A a = new B()`

⭐️呼び出すメソッド探し
    → 左型で探す
- () ある？
  - メソッド → 右(new側)見る
  - override実行は右(new側)

- () ない？

  - フィールド → 左見る

# implementsあったら
1. public？（同じか緩い？）
2. メソッド名同じ？
3. 引数同じ？
4. abstractなら未実装OK

# throw / throws

- throw
  <br>
→ 今、例外を投げる💥
- throws
  <br>
→ 投げるかも宣言📢

# 例外
1. throw 見る
2. catch 上から探す（ヒットしたらcatch終わり）
3. finally 基本実行

## try-catch-finally（昔のやり方）
1. try（爆発）
2. catch（バグ捕獲）
3. finally（ここで人間が手で蓋を閉める！）

## try-with-resources
    try() ⭐️目印：これあれば👀
1. close（） 最初
2. catch
3. finally（） 最後

⭕️ try + catch + finally （全部入り）

⭕️ try + catch （finallyなし）

⭕️ try + finally （catchなし）

❌ try だけ （後ろに誰もいないからエラー）

```
Exception
├─ IOException
├─ SQLException
└─ RuntimeException
```

```
IndexOutOfBoundsException
├─ ArrayIndexOutOfBoundsException
└─ StringIndexOutOfBoundsException
```

# String
- String
  
  →immutable（不変）
- 変更系メソッド

    →新しいString作るだけ

# intern() 📖👀
Stringのコンスタントプールを使う

⭐️ newとリテラルの比較でもtrueになる

`new String("a").intern() == "a"`

→ true ⭕️

`a.intern() == b.intern()`

→ true ⭕️

# equals / ==
- == ：アドレス
- .equals() ：値

# 初期化子（初期化ブロック）
初期化子 → コンストラクタ

### ⭐️ static初期化子

static{}
```
static {
    // クラスが最初に読み込まれたときに1回実行
}
```

### ⭐️ インスタンス初期化子
```
{
    // newするたびに実行
}
```

⭐️初期化子 → コンストラクタ
<br>
の順番で動く

# 配列 （定義方法）
## 宣言

⭐️ [] の位置はどこでも ⭕️

```
int[] a; ⭕
int a[]; ⭕

int[][] a; ⭕
int[] a[]; ⭕
int a[][]; ⭕
```

⭐️宣言時に要素は書かない ❌
```
int a[3]; ❌
```

## 宣言時
⭐️ 要素数は書かない

```
int[] a; ⭕

int a[3]; ❌ 💥 コンパイルエラー
```

## 初期値

|  データ型  | 初期値  |
|:---------:|:------------:|
| int    | 0  |
| long | 0  |
| double   | 0.0    |
| boolean   | false   |

## インスタンス生成時（右側）
⭐️ 要素数は書かなきゃダメ ❌
```
int[] a = new int[3] ⭕️

int[] a = new int[] ❌💥
```

多次元配列

⭐️ 最初の要素数は省略不可 ❌


⭐️ 最初は必須、後ろは省略可
```
int[][] array = new int[2][3] ⭕️
int[][] array = new int[2][]  ⭕️

int[][] array = new int[][3] ❌💥
```

⭐️ 整数以外 ❌
```
int[][] array = new int[3.5] ❌💥

int[] a = new int[-1] ❌
実行時例外
（NegativeArraySizeException）
```

初期化子
```
int[] a = new int[] {1, 2, 3}; ⭕️

int[] a = new int[3] {1,2,3} ❌`
❌ 要素数と初期化子の併用不可
```

⭐️ {} があれば0個あると分かる ⭕️
```
int a[][] = {}; ⭕️
int[][] a = new int[][]{}; ⭕️
```

# 二次元配列
住所を指定して中身を取る

array[i][j]
- i = 階
- j = 部屋

```
int array[][] = {
    {1,2},
    {2,3,4}
};
```
```
array[0][0] → 1
array[0][1] → 2

array[1][0] → 2
array[1][1] → 3
array[1][2] → 4
```
## length

array.lengthは
<br>
階数（外側の要素数）
<br>
→ 2 （2階建てだから）
```
array[0].length
⭐️ 0階の部屋数→2
```
```
array[1].length
⭐️ 1階の部屋数→3
```

## new int[][]
`new int[2][4]`

→ 2階建て、各階4部屋

```
[ ][ ][ ][ ] ← 0階
[ ][ ][ ][ ] ← 2階
```
⭐️最初の数字 → 行数
<br>
⭐️次の数字 → 列数

## ガタガタOK ⭕️
**int[][] array = new int[2][];**
```
array[0] = new int[100];
array[1] = new int[2];
```
各階の部屋数は同じでなくてもOK

```
String[][] array = { { "A", "B", "C" } };
```
左辺：看板
<br>
右辺：マンション構造

## for文ミックス
⭐️ 外側for → 階を回る（縦）
<br>
⭐️ 内側for → 部屋を回る（横）

```
for (int i = 0; i < array.length; i++)
→ 階を回る
```
```
for (int j = 0; j < array[i].length; j++)
→ 部屋を回る
```

## 配列 clone()
外側だけコピー
```
array 1 == array2; // false❌
```

中身の配列は同じアドレス
```
array1[1] == array2[1]; // true
```

配列の出力 → ハッシュコード

`System.out.println(array);`

要素の出力 → 0

`System.out.println(array[0]);`

⭐️ {}  は値を並べる
```
int[][] array = {
    {1,2},   // 0階（行）
    {2,3,4}  // 1階（行）
};           // ２階建て✨
```
⭐️ [] は添字（住所）を書く
```
array[1][2]  // 1階2号室
```

# switch

⭐️ ヒットしたcaseから開始
<br>
↓
<br>
⭐️ breakまで落ち続ける

## switch文

⭐️ ヒットしたら終わりではない
<br>
⭐️ ヒットしたcaseへワープ
<br>s
⭐️ breakにぶつかったら出さずに抜ける

switch (???)

使える値 ⭕️ 📖👀
- char
- byte
- short
- int
- String
- enum

使えない値 ❌ 📖👀
- long ❌
- loat / double ❌
- boolean ❌

    ⭐️ 大きすぎる整数、小数点は ❌

⭐️ defaultはどこに書いてもOK
（switch文・switch式どちらも）

## caseに指定できる値
⭐️ コンパイル時の定数のみ
- final ⭕️
- リテラル値 ⭕️
- コンパイル時に計算できる式 ⭕️
- 変数 ❌

ひっかけ問題
```
⭕️ 1行で宣言＋代入
final int NUM = 10; 
```
```
❌ 2行に分かれてる
final int NUM;
NUM = 10;
```

## switch文はフォールスルー
⭐️ break がないと次の case に落ちる
```
switch (num) {
    case 1:
    case 2:
        System.out.println("A");
}

// num = 1はA
```

⭐️ break がないと最後まで実行
```
case 1:
    A
case 2:
    B
default:
    C   
```
```
答え
A
B
C
```
# nullの罠😈
```
String s = null; ⭕️
```

```
String s = null;
s.length();      ❌
```
nullが存在するだけ
<br>
→ OK ⭕️

null.メソッド() ❌
<br>
null.フィールド ❌
<br>
`.`でnullを触る
<br>
→ ぬるぽ ❌

# ArrayList
## 特徴
- 重複OK ⭕️
- null OK ⭕️
- スレッドセーフではない ❌

- `ArrayList list = new ArrayList<>();`
  <br>
 → どんな型でも入れられるバッグ

## 追加・変更
- add(value)
  <br>
→ 末尾追加
- add(index, value) 
  <br>
 → 指定位置に追加（位置,値） 📖👀
- set(index, value)
  <br>
  → 置き換え

## 削除
- remove(value)
  <br>
  → 
  
  ⭐️ remove判定はequals() 📖👀
  <br>
  equals()の中身次第で削除される要素が決まる

## 不変 ⚠️
`List.of(...)`

⭐️変更不可

- add ❌
- remove ❌
- set ❌

`Arrays.asList(...)`

⭐️固定長
- add ❌
- remove ❌
- set ⭕️

`new ArrayList<>()`

⭐️全部OK

## ひっかけ💥
   ⭐️ for-each中にadd/remove（コレクション変更） 📖👀

   [A,B,C,D,E]
<br>
   ↓
<br>
   C削除
<br>
   ↓
<br>
   まだD,Eが残る
<br>
   ↓
<br>
    実行時例外💥

    ConcurrentModificationException
<br>
    ⭐️ 短い 例外にならない場合あり

    [A,B,C]
    ↓
    Bをremove
    ↓
    Aだけ出力（Bも消える）👻

# インクリメント

⭐️ 左から順番

in a = 10;
- a++ → 今の値を使う（10評価） → 後で増える
- ++a → 先に増える → その値を使う

⭐️評価とは「置くだけ」のこと

長い式は
<br>
「使われる値」を横に書く
<br>
→ 最後に足し算や引き算

# コンストラクタ（親から先）
1. new B() // 子

    ↓

2. 親(A)コンストラクタ

    ↓

3. 子(B)コンストラクタ

# 戻り値（void以外で宣言）
- 全ルートで`return`必須
- `boolean`には`void`なし
- `throw`終了なら`return`なくてOK

⭐️voidは引数に使えない

# メソッド呼び出し
- static → `クラス名.メソッド名()`
- インスタンス → `変数名.メソッド名()`
- default → `インターフェース名.super.メソッド名()`
- static → `this`使えない ❌

### 呼び出しルール
⭐️フィールド → ()なし
<br>
⭐️ メソッド → ()あり

```
Sample sample = new Sample();

sample.hello();   // インスタンスメソッド
Sample.print();   // staticメソッド
```
⭐️引数の数・型は宣言と一致 ⚠️
<br>
→ 違うとコンパイルエラー💥

### ⭐️ メソッド宣言

戻り値の型は必須 ⚠️

void / int / String ...

```
void sample() { } ⭕️
int sample() { } ⭕️
String sample() { } ⭕️

sample() { } ❌
```

# sealed + permits（継承できる子を制限）
子は必須
- final
- sealed
- non-sealed

子もsealed
- permits必要

# override（上書き）
- ()ある？
  
  → メソッド → 右(new側)

- 親メソッドを書き換える

    → 親の中身は使われない

確認
1. メソッド名同じ？
2. 引数同じ？
3. public弱くなってない？

# && と ||（左だけ）
- `&&` → 左falseなら右見ない
- `||` → 左trueなら右見ない

# & と |（両方見る）
- `&` と `|` → 必ず両方実行
- `|` どっちかtrue

# abstract（抽象クラス=未完成）
- abstract class
  
    → `final` ❌

    → `new` できない

- abstract method
    
    →   `{}`なし

    →  ; で終わる

- abstract method ある

  → classもabstract必要

## ⭕️❌判定

⭕ abstract class
- 処理なしOK

❌ final abstract
- 処理あり & なしは両立不可

❌ new AbstractClass()
- abstractはnew不可

---

# abstractメソッド(抽象メソッド)

abstractあり(抽象メソッド)
-  `;` 必須
-  `{}` ダメ❌
-  処理なし

---

abstractなし(具象メソッド)
-  {} 必須
-  処理必要

---

⭕ abstractメソッド持つクラス

→ classもabstract必須

# ループ

⭐️出力が continue / break の上か下か見る
- continue（その周回終了）

    → continue含めて下の処理スキップ
    
    （そのループのみ）


    → 次のループへ

- break

    → 今いるブロック終了（その後の繰り返ししない）
<br>
    → break含めてfinish

- continue;の次の行に実行コードは書けない❌（到達不能コード）

# 二次元配列
例
```
String[][] array = {
    {"A","B"},
    {"C","D","E"}
};
```

```
array[0][0] → A
array[0][1] → B

array[1][0] → C
array[1][1] → D
array[1][2] → E
```

行ごとに長さ違ってOK
（ガタガタ配列OK）

`data[i][j]`

- i → 外側（行）
- j → 内側（列）

data.length
→ 行数

data[i].length
→ その行の列数

```
data[0][0]
→ 1行目1列目

data[1][2]
→ 2行目3列目
```

# do-while
*doとwhileの間は必ず1回実行される🐱*

```
do {
    // 繰り返し処理
} while (順不要);

```
```
do {
    System.out.println("にゃん🐱");
} while(false);
```

出力：にゃん🐱
<br>
↓
<br>
条件は後で見る👀

## while
条件 → 処理
## do-while
処理 → 条件

# for文
## 初期化式
```
for (初期化文; 条件文; 更新文) {
    // 繰り返し処理
}
```
⭐️ 初期化式で違う型は使えない ❌💥
```
    ❌💥
    int i = 1, long j = 2
```

## 条件式省略

### ⭐️ 条件式と初期化式は省略可 ⭕️
```
for (;;) // 無限ループ🌀
```
    条件式省略
        ↓    
    true扱い
        ↓
    無限ループ🌀

    ⭐️true 又は 空っぽの時は無限ループ🌀

## 有効範囲

⭐️ for文初期化式の有効範囲に注意⚠️

```
for () {
    // ()で作った変数はブロック内のみ有効⚠️
}
```

# 拡張for文

```
for (型 変数名 : 配列) {
    // 繰り返し処理
}
```

⭐️ 配列から1個ずつ取り出す

⭐️ 変数を書き換えても 配列の中身は変わらない

```
int[] array = {1,2,3};

for (int num : array) {
    System.out.println(num);
}
```
## 二次元配列ミックス
```
String[][] array = {
    {"A","B","C"}
};

for (String[] row : array) {
}
```

⭐️ 二次元配列から1個取り出すと
[] が1個減る

String[][]
<br>
↓
<br>
String[]

# for 二重ループ
外側 → 行移動

内側 → 列移動

# _（アンダースコア）
⭕️ 数字の間
- 123_456
- 0b0_1
- 0_52

❌ 先頭
<br>
❌ 末尾
<br>
❌ 記号の前後
- _123
- 123_
- 3_.14
- 999_L
- 0x_52

# instanceof
```
obj instanceof クラス名
 ↑                ↑
 変数          クラス名or
             インターフェース名
```

左側
<br>
→ オブジェクト（変数）

右側
<br>
→ クラス名 または インターフェース名

⭐️中に入っているオブジェクトの型チェック  
  （❌ 変数の型ではない）

```
Object obj = "ABC";
obj instanceof String

⭐️ objの型：Object
⭐️ 中身の型：String
```

## パターンマッチング

if (obj instanceof String s)

⭕️ trueなら s が使える
<br>
❌ elseでは使えない💥

# record
❌ extends不可（継承できない）💥

⭕️ コンストラクタあり

⭕️ getterは`フィールド名()`

⭕️ toString・equals・hashCodeあり

- フィールド
```
record Data(String value)

// value はフィールド
```

- 値を取り出す
```
data.value()
```

## ⭐️ recordの getter名
getValue() ❌
<br>
value() ⭕️

# recordのコンストラクタ
```
record Data(String value)
```

⬇ 自動📦

```
public Data(String value) {
    this.value = value; // 自動📦
}
```

### OK🙆‍♀️

```
new Data("ABC")

value = "ABC"

📦 valueにABCが入ってる✨
```

```
public Data() {
    this("ABC");
}

📦valueにABCを入れて作って😊
```
### NG🙅‍♀️

```
new Data()

value = ？？？

📦 valueは空っぽNG💥
```

# ガベージコレクション🗑️
⭐️ ゴミになるのは Object（ベッド）
<br>
人（変数）はゴミにならない ⚠️

```
Object a = new Object(); // 🐶ALBAのベッド🛏️①
Object b = new Object(); // 🐶VANILLAのベッド🛏️②
Object c = a;            // 🐻c不審者登場（ALBAと同じベッド）
```

```
ALBA(a) ──┐
            ├──→ 🛏️①
c🐻 ────┘

VANILLA(b) ───→ 🛏️②
```

```
a = null;
ALBA😢 ベッドを手放す

c🐻 ─────→ 🛏️①

VANILLA ─→ 🛏️②

🛏️①は c が使ってるので残る⭕️
```

```
b = null;

ALBA😢
VANILLA😢

c🐻 ─────→ 🛏️①

🛏️② 🗑️
```
🛏️②は誰も使っていないので
<br>
ガベージコレクション対象✨🗑️

### ⭐️ new Object() がベッドを作る

⭐️ 代入 (=)
<br>
→ 同じベッドを使うだけ
（ベッドは増えない）

⭐️ null
→ ベッドを手放す

⭐️ 誰も使っていないベッド
→ ガベージコレクション🗑️

# var 📖👀
- ローカル変数のみOK ⭕️
- 初期化必須⚠️
- 引数 ❌
- 型変更NG ❌
- null単体NG ❌

# コンストラクタとメソッドの見分け方
## ⭐️ コンストラクタ

### 役割
- newしたときに最初に呼ばれる
- 📦 フィールドに必要な値を入れる仕事

```
public Data() {
}
```
✅ クラス名（record名）と同じ名前

✅ 戻り値がない（voidやStringがない）

→ コンストラクタ📦

## ⭐️ メソッド
```
public void test() {
}
public String test() {
}
```

✅ 戻り値がある（voidも戻り値の一種）

→ メソッド⚙️

# コンストラクタとインスタンス🐶

```
new Dog()
      ↓
🐶「ALBAをお迎えします♪」
（コンストラクタ）
       ↓
🐶 ALBAが家に来た✨
（インスタンス）
```
### コンストラクタ

    ＝お迎え手続き
    ＝newすると最初に1回だけ

### インスタンス

    ＝できあがったALBA本人
    ＝実際に使うもの

```
クッキー工場🍪

① new：コンストラクタを呼ぶ
🍳「注文入りました！」

↓

② コンストラクタ
🍳「焼きます！」

↓

③ インスタンス完成
🍪「できました！」

↓

④ item
🍪を持つ人
```

## 呼ばれる順番 📖👀
### コンストラクタ

- new Sample()
  <br>
同じ名札と呼び方（引数）のコンストラクタ Sample() が呼ばれる

- ⭐️ newすると
1. フィールド（あれば）
   <br>
      ↓
2. { }（名札なし）
   <br>
      ↓
3. Sample()（名札あり）← コンストラクタ

    ⭐️名札なしの {} が先！

- ⭐️ newある？👀

    newない
    <br>
    ↓
    <br>
    { }動かない
    コンストラクタ動かない
    <br>
    ↓
    <br>
    初期値のまま  
# this
### 同じ名前が2つある👀
```
this.name = name;
     ↑       ↑
フィールド   引数
```
- 左
  
  this.name
<br>
→ フィールド📦
- 右
<br>
→ 引数🎁

⭐️引数をフィールドに入れる 🎁 → 📦

### this.
- this.x
  <br>
    → 自分のフィールド・メソッド

### this() 📖👀
⭐️コンストラクタ
- this(...)
<br>
    → 引数が一致するコンストラクタ

# オーバーライド

⭐️チェック
1. メソッド名同じ？
2. 引数同じ？
3. 戻り値は 同じ or 
4. public弱くなってない？

# オーバーロード
メソッド名同じ

引数違い
（型 or 数 or 順番）⇦どれか1つでOK

⭐️呼び出し：引数の型が一致する方（近い方）

## メソッド呼び出し
◽️どのメソッド呼ぶ？
- 左型で探す
（オーバーロード）
- 実際に実行されるメソッド
→ 右(new側)
（オーバーライド）

## コンストラクタ呼び出し 📖👀
- super()：親のコンストラクタ
- this()：自分のクラスの別ブロックのコンストラクタ

💥 どちらもコンストラクタの1行目だけ

this.はどこでも書ける対象外

# catch順
子 → 親
  
    狭い罠（チワワ） → 広い罠（動物）

親 → 子
- 下（狭い罠）のcatch到達不能
- コンパイルエラー

# 継承
extends：子 → 親 → その親（全員呼ばれる）

super → 親

finalメソッド → override不可❌

super() → 親コンストラクタ

# super
- コンストラクタ：super() 省略OK
（自動追加）

- 親と子で同じメソッド名で子が親を呼ぶ：super.メソッド名() 省略できない
- 子が親を呼ぶ：super()省略化
 
  ※オーバーライドなしの場合

# アクセス修飾子
- override（上書き）

    親 <= 子（同じか広く）

- interface → public 必須

- catch

    子

    ↓

    親

    ---

    親

    ↓

    子 ❌ （下に到達できない）

    | 修飾子       | 見える範囲     |
    |:---------:|:------------------:|
    | public    | 世界中  |
    | protected | 同じ家 + 別の家の子供 |
    | なし        | 同じ家のみ         |
    | private   | 同じ部屋だけ               |

# コマンド

1. javac（コンパイル）

→ .java 必須 ⭕

`javac Sample.java`

### c-java

javac
<br>
↓
<br>
cいる👀
<br>
↓
<br>
Compile
<br>
↓
<br>
ソース(.java)食べる

2. java（実行）

→ 通常はクラス名だけ ⭕

`java Sample`

→ .class は書かない ❌

`java Sample.class ❌`

## javaクラス
java
<br>
↓
<br>
cいない👀
<br>
↓
<br>
実行
<br>
↓
<br>
クラス名だけ(`java Sample`)

⭐️ Java11+

コンパイルしていない .java を
直接実行できる

`java Sample.java ⭕️`

# 型変換
byte
 <br>
 ↓
 <br>
short
 <br>
 ↓
 <br>
int
 <br>
 ↓
 <br>
long
 <br>
 ↓
 <br>
float
 <br>
 ↓
 <br>
double

byte
<br>
-128 ～ 127

⭐️ 小→大 ⭕️

⭐️ 大→小 ❌（キャスト必要）

long が混ざる
<br>
→ 結果も long

float は F が必要

float f = 10.0F ⭕️
<br>
float f = 10.0  ❌

int c = 6L;💥
<br>
値（大） → 小（箱）だからキャスト必要

# キャスト
大きい箱から小さい箱に変更 →
キャスト必須

## charの自動変換
char → int ⭕️
<br>
char → long ⭕️
<br>
char → float ⭕️
<br>
char → double ⭕️
<br>
<br>
char → byte ❌
<br>
char → short ❌

## to char
byte → char ❌
<br>
short → char ❌

int → char ❌（キャスト必要）

# getter/setter
- getter：privateで値を見るボタン（値取得）
- setter：privateな値を変えるボタン（値変更）

# 真偽値（boolean）の比較（関係演算子）
boolean

`==` ⭕️
<br>
`!=` ⭕️

数値以外の比較：等符合 ❌
<br>
`< ` ❌
<br>
`>`  ❌
<br>
`<=` ❌
<br>
`>=` ❌

# 三項演算子（if の1行版） 📖👀
条件 ? trueの時 : falseの時

例
```
int a = 5;
int x = (a > 3) ? 100 : 200;
```

a > 3 ？

YES → 100

NO  → 200

# StringBuilder

new StringBuilder()
<br>
→ capacity 16

new StringBuilder("abcde")
<br>
→ 文字数 + 16

"abcde"
<br>
→ 5 + 16 = 21