# このチートシートの約束
```
🪧 = 変数・クラス・配列などの宣言

📛 = メソッド名 + 引数

📦 = フィールド

🏢 = 二次元配列

🛏️ = Object

👀📝 = 暗記
```

# 👀 問題を見る順番
① main() を見る
<br>
↓
<br>
② new を探す
<br>
（実際に作られるオブジェクト）
<br>
↓
<br>
③ 左右判定ある？
```
A a = new B();
```
↓
<br>
④ 呼ばれるメソッドを探す
<br>
↓
<br>
⑤ コンパイルエラー候補を見る

# 📛 左右判定（継承・implements）
`A a = new B()`
### ⭐️ () ある？
```
a.sample();
```
    → メソッド
    ① 左型(A)で存在確認👀
    ↓
    ② 実行は右(new側)
    （overrideなら右が動く）
### ⭐️ () ない？
```
a.value
```

  - フィールド → 左見る

# override（上書き）
親のメソッドを書き換える
<br>
→ 親の中身は使われない
## ⭐️ 実行される場所

右（new側）
```
Parent p = new Child();
p.hello();
```
    hello()は
    Childが実行される

## 📛 チェック
1. メソッド名同じ？
2. 引数同じ？
3. アクセス修飾子
   <br>
   public同じ or 弱くなってない？
```
    public
    ↑
    protected ❌

    弱くするとコンパイルエラー💥
```

# overload（オーバーロード）
## ⭐️ チェック
1. メソッド名同じ
2. 引数が違う（どれか1つでOK🙆‍♀️）
- 数
- 型
- 順番

    戻り値だけ変更
    <br>
    ❌ オーバーロードにならない

⭐️呼び出し：引数の型が一致する方（近い方）

# 📛 implements

1. public？（同じか広い？）
2. メソッド名同じ？
3. 引数同じ？
4. abstractなら未実装OK

### 多重実装OK ⭕️
```
⭕️ implements A, B, C

// ⭕️ カードは何枚でもOK 💳
```

# 🌳 extends（継承）
`extends`

⭐️ 親は1人だけ🐶

```
⭕️ extends A
❌ extends A, B

// ALBAのママは1人だけ🐶
```

子は

親
<br>
↓
<br>
親の親
<br>
↓
<br>
さらに親
<br>
🐶 まで全部引き継ぐ

# 💳 implements
## abstract（抽象クラス=未完成）
### abstract class
⭕ abstract class
- 処理なしOK

❌ final abstract
- 処理あり & なしは一緒に書けない❌

❌ new AbstractClass()
- abstractはnew不可

### abstractメソッド
```
abstract void test();
```
- {}なし❌
- ;で終わる⭕️

abstractメソッドがある👀
<br>
↓
<br>
クラスもabstract必須

### abstractなし(具象メソッド)
-  {} 必須
-  処理必要

# sealed
継承できる子を制限する

### ⭐️ 子は必ずどれか（この3択）
- final
- sealed
- non-sealed

### 子もsealedなら
`permits` 必要

### 💳 インターフェースも使える ⭕️
`sealed interface`

## permits
継承できる子を指定する
```Java
sealed class A
    permits B
```
⭐️ permits は
- extends
- implements
<br>
より後ろに書く

⭐️ 順番を逆にすると
<br>
コンパイルエラー💥

# super
`super()`

親コンストラクタで
<br>
省略すると自動で
<br>
`super();` が入る👻

## super.メソッド()
親のメソッドを呼ぶ

⭐️ オーバーライドした子から
<br>
親を呼ぶときだけ使う

# ポリモーフィズム 👀📝
```Java
Parent p = new Child();

// 📛 探すのは左
// 🚀 動くのは右
```
# throw / throws

- throw
  <br>
→ 今、例外を投げる💥
- throws
  <br>
→ 投げるかも宣言📢

# 例外
📛 解く順番
1. throw 見る
2. catch 上から探す
   <br>
   ⭐️ 最初にヒットしたcatchだけ実行
   <br>
   （ヒットしたらcatch終わり）
3. finally（基本実行）
## try-catch-finally（昔のやり方）
1. try（爆発💥）
<br>
↓
2. catch（例外キャッチ）
<br>
↓
3. finally（最後に実行）

```Java
⭕️
try { }
catch (...) { }
finally { }
```

```Java
⭕️
try { }
catch (...) { }
```

```Java
⭕️
try { }
finally { }
```

```Java
❌
try { }

// 後ろに catch または finally が必要💥
```
## try-with-resources

```Java
⭐️目印 👀

try ()
```
1. try
<br>
↓
2. close() ⭐️ → この中だけ逆順にclose🙃
<br>
↓
<br>
3. catch
 <br>
↓
4. finally
## リソースが2つ😊😊
```Java
 // ⭐️tryの中が2つ👀
try (
    A a = new A();
    B b = new B();
) {
    throw new Exception();
} catch (Exception e) {
    System.out.println("catch");
} finally {
    System.out.println("finally");
}
```

リソースが2つあれば

開く順
```
A を開く
↓
B を開く
```
閉じる順
<br>

```
B close
↓
A close
```
    ⭐️ 逆になるのは close() の中だけ🙃

## catch順
⭐️ 子 → 親
```
⭕️
狭い罠🐶
↓
広い罠🐘
```

❌ 親 → 子
```
下が
到達不能コード💥

コンパイルエラー
```

## finally
⭐️ 基本実行

例外があってもなくても実行される

❌ try だけ （後ろに誰もいないからエラー）💥
<br>
❌ finally複数 （1つしかダメ）💥


⭕️ try + catch + finally （全部入り）
<br>
⭕️ try + catch （finallyなし）
<br>
⭕️ try + finally （catchなし）
<br>
⭕️ catch複数 （何個でもOK）


## RuntimeException
⭐️ throws不要
- NullPointerException
- IndexOutOfBoundsException
- IllegalStateException

    など

## 例外クラス

### 🐶家系図
```
Throwable👴
├── Error💥 ←--------------------- throws不要😊
└── Exception👩 ← ママ
      ├── IOException🐶
      ├── SQLException🐶
      └── RuntimeException🐶 ←-- throws不要😊
             ├── NullPointerException🐶
             └── ArrayIndexOutOfBoundsException🐶
```

```
IndexOutOfBoundsException
├─ ArrayIndexOutOfBoundsException
└─ StringIndexOutOfBoundsException
```

### はみ出しグループ
📦 配列 → ArrayIndexOutOfBoundsException
<br>
📋 List → IndexOutOfBoundsException
<br>
🔤 String → StringIndexOutOfBoundsException

# 📦 配列・ArrayList
## 宣言（看板🪧を作る）

⭐️ [] の位置はどこでも ⭕️

```Java
// 宣言だけOで部屋はまだ作ってない
int[] a; ⭕
int a[]; ⭕

int[][] a; ⭕
int[] a[]; ⭕
int a[][]; ⭕
```

⭐️宣言時に要素数は書かない ❌
```Java
// ❌ 宣言時に部屋数を書く💥
int a[3]; ❌
```

## new（マンションを建てる🏢）
### OK⭕️
```Java
int[] a = new int[3];
/**
 *     
    0号室
    1号室
    2号室
    3部屋できる😊
 */
```

### ❌ 部屋数なし
```Java
new int[]

// 何部屋作るか分からない💥
```

## 初期化子{}
### 全部OK⭕️
```Java
int[] a = {1,2,3}; // ⭕️

int[] a = new int[]{1,2,3}; // ⭕️

int[][] array = {}; // ⭕️部屋は0個ある
```
```Java
int[] a = new int[] {1, 2, 3}; ⭕️

int[] a = new int[3] {1,2,3} ❌`
❌ 要素数と初期化子の併用不可
```

⭐️ {} があれば0個あると分かる ⭕️
```Java
int a[][] = {}; ⭕️
int[][] a = new int[][]{}; ⭕️

### ❌ 両方書く
```Java
new int[3]{1,2,3}

// 部屋数と初期化子は一緒はダメ💥
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
```Java
int[] a = new int[3] ⭕️

int[] a = new int[] ❌💥
```

# 二次元配列🏢
## 宣言時
⭐️ 最初の要素数は省略不可 ❌
```Java
int[][] array = new int[2][3] ⭕️
int[][] array = new int[2][]  ⭕️

int[][] array = new int[][3] ❌💥
```

⭐️ 整数以外 ❌
```Java
int[][] array = new int[3.5] ❌💥

int[] a = new int[-1] ❌
実行時例外
（NegativeArraySizeException）
```

# 二次元配列🏢
## length
```Java
array.length

// 何階建て？
```

```Java
int[][] array = {
    {1,2},
    {3,4,5}
};

// array.length：2
```

マンション構造 🏢
```Java
array[0][0] → 1
array[0][1] → 2
// 0階
// 101号室→1
// 102号室→2

array[1][0] → 2
array[1][1] → 3
array[1][2] → 4
//  1階
//  201号室→3
//  202号室→4
//  203号室→5

部屋数 🚪
```java
array[0].length // 0階に2部屋
array[1].length // 1階に3部屋
```
## 住所
住所を指定して中身を取る
```Java
array[i][j]

// i 何階 🏢 
// j 部屋 🚪 
```

```Java
array[1][2]
// 🏢1階
// 2号室
```

### new int[][]
```Java
new int[2][4]
// 2階建て
// 各階4部屋
```

```Java
[ ][ ][ ][ ] ← 0階
[ ][ ][ ][ ] ← 1階

// ⭐️最初の数字 → 行数
// ⭐️次の数字 → 列数
```

## ガタガタOK ⭕️
**int[][] array = new int[2][];**
```Java
array[0]=new int[100]; // 0階100部屋
array[1]=new int[2];   // 1階2部屋
```
各階の部屋数は同じじゃなくてもOK

```Java
String[][] array = { { "A", "B", "C" } };

// 左辺：看板🪧
// 右辺：マンション構造🏢
```

## length
```Java
array.length
⭐️ 階数（外側の要素数）
   → 2 （2階建てだから）
```
```Java
array[0].length
⭐️ 0階の部屋数→2
```
```Java
array[1].length
⭐️ 1階の部屋数→3
```

# 🔁for（二次元配列ミックス）
## マンション構造 👀📝

⭐️ 外側for → 🏢 階を回る（縦）
<br>
⭐️ 内側for → 🚪 部屋を回る（横）

🏢 階を回る
### ⭐️ 外側
```Java
for(int i=0;i<array.length;i++)

// 階を歩く 👀📝
// 0階 → 1階 → 2階
```
### ⭐️ 内側
```Java
for(int j=0;j<array[i].length;j++)

// その階の部屋を歩く🚶 👀📝
// 101号室 → 102号室 → 103号室
```

## 拡張for
```Java
for(String[] row : array)
```

二次元配列から
<br>
1階だけ取り出す

String[][]
<br>
↓
<br>
String[]

⭐️

[]が1個減る

## 配列 clone()
外側だけコピー🏢
```Java
array 1 == array2; // false❌
```

中身の配列は同じアドレス🚪
<br>
中は繋がってる2世帯住宅
```Java
array1[1] == array2[1]; // true
```

## 配列の出力
住所（ハッシュコード）
```Java
System.out.println(array);

// 要素の出力 → 0
// 0階の住所
```

⭐️ {}  は値を並べる
```Java
int[][] array = {
    {1,2},   // 0階（行）
    {2,3,4}  // 1階（行）
};           // 2階建て✨
```
⭐️ [] は添字（住所）を書く
```Java
array[1][2]  // 1階2号室
```

# ArrayList
## 特徴
- 重複OK ⭕️
- null OK ⭕️
- 増えたり減ったりする ⭕️
- スレッドセーフではない ❌

## 🪧宣言方法
  ```
  ArrayList list = new ArrayList<>();
  ```
    → どんな型でも入れられるバッグ

## 追加・変更
  ### add(value)
→ 末尾追加
### add(index, value) 
→ 途中の指定位置に追加（位置,値） 📖👀
### set(index, value)
→ 住人を入れ替える
### remove(value)
→ 住人を追い出す😈
    <br>
    ⭐️ remove判定はequals() 📖👀
    <br>
    equals()の中身で削除される要素が決まる
###  List.of()
→ 変更禁止🚫
  - add❌
  - remove❌
  - set❌
### Arrays.asList()
→  固定長

    住人は変更OK
    増築・取り壊しNG
- add❌
- remove❌
- set⭕️
### new ArrayList()
→  全部OK😊
- add⭕️
- remove⭕️
- set⭕️
### 💥 for-each中にremove
→  まだ後ろに住人がいる
<br>
→  マンション構造が変わる
<br>
→  💥
 ```Java
 💥
 ConcurrentModificationException
 ```

```
🧸最後に覚えること

🏢 マンション = 二次元配列

🏢 階 = i

🚪 部屋 = j

🚶 外側for = 階を歩く

🚶 内側for = 部屋を歩く
```

# String
⭐️ 特徴 📖👀
- immutable（不変）

    ⭐️変更系メソッドでも元は変わらない

## 変更系メソッド
新しいStringを作るだけ
```Java
String s = "ABC";
s.concat("D");

// ABCは変わらない
```

変更したい場合
```Java
s = s.concat("D");
```

# equals / ==
- == ：アドレス
- .equals() ：値
# intern() 📖👀
Stringのコンスタントプールを使う

⭐️ newとリテラルの比較でもtrueになる

`new String("a").intern() == "a"`
    
→ true ⭕️

`a.intern() == b.intern()`

→ true ⭕️

# Stringのメソッド 📖👀
⭐️ よく出る
## length()：文字数
```Java
"ABC".length() // 3
```
## charAt()：添字
charAt(n)
<br>
n文字目ではない⚠️
```Java
"ABC".charAt(0) // 
```
## indexOf()：見つかった位置
最初に見つかった位置（0から順番）
  ⭐️なければ-1
## substring()
### substring(a,b)：a以上b未満
```Java
0 1 2 3
A B C D

substring(1,3) // BC
```
## replace()：置き換える
元は変わらない⚠️

## startsWith()：前から一致 📖👀
```Java
startsWith("ab") 
// 先頭が一致するか
  （true/false）
```

## concat()：後ろに文字を追加

⭐️ 元のStringは変わらない

```java
String s = "ABC";
s.concat("D");
```

# ループ
# continue
⭐️出力が continue / break の上か下か見る
continue（その周回だけ終了）
↓
<br>
↓
continue含めて下の処理スキップ
↓
<br>
↓   
次のループへ

# break
今いるブロック終了（その後の繰り返ししない）
<br>
↓
<br>
↓
break含めてfinish

# 到達不能コード💥
```Java
continue;
System.out.println("A");

// continue;の次の行に実行コードは書けない❌
```
    コンパイルエラー💥
# while
条件
<br>
↓
<br>
処理
```Java
while (条件) {

}
```

# do-while
*doとwhileの間は必ず1回実行される🐱*

処理
<br>
↓
<br>
条件
```
do {
    // 繰り返し処理
} while (条件j);

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

# for文
## 🪧初期化式
```
for (初期化文; 条件文; 更新文) {
    // 繰り返し処理
}
```
⭐️ 違う型は並べられない ❌💥
```
    ❌💥
    int i = 1, long j = 2
```

## 条件式省略

### ⭐️ 条件式と初期化式は省略可 ⭕️
```Java
for (;;) // 無限ループ🌀
```
    条件式なし
        ↓    
    true扱い
        ↓
    無限ループ🌀

    ⭐️true 又は 空っぽの時は無限ループ🌀

## 初期化式の有効範囲

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
## 二次元配列 × 拡張for
```
String[][] array = {
    {"A","B","C"}
};

for (String[] row : array) {
}
```

⭐️ 二次元配列から1個取り出すと
[] が1個減る

String[][] array
<br>
↓
<br>
String[]

# for 二重ループ
🏢 外側 → 階を回る（行移動）

🚪内側 → 部屋を回る（列移動）
```Java
for (i)
↓
🏢
0階
1階
2階
```

```Java
for (j)
↓
🚪
101
102
103
```

```
🧸 問題を見たら

① continue の上下を見る👀

② break の上下を見る👀

③ 出力はどこにある？👀
```

# switch
## switch文
⭐️ ヒットしたcaseから開始（ワープ）
<br>
↓
<br>
breakまで落ち続ける（フォールスルー）
<br>
breakにぶつかったら出さずに抜ける

👀 breakがない
<br>
↓
<br>
次へ落ちる（フォールスルー）
```Java
case 1:
case 2:
    System.out.println("A");

// 1でも2でもA😊
```

## switch式
⭐️ フォールスルーしない

値を返す
```Java
int result = switch(num) {
    case 1 -> 100;
    default -> 0;
};
```
```Java

case 1:
    A
case 2:
    B
default:
    C

// 出力
// A
// B
// C
```

switch (???)

使える型 ⭕️ 📖👀
- char
- byte
- short
- int
- String
- enum

使えない値 ❌ 📖👀
- long ❌
- loat ❌
- double ❌
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
    Aだけ出力（Cも消える）👻

# 👀📝 ループの問題を見る順
```
① switch文？

→ break探す👀

② switch式？

→ break不要

③ caseは定数？

→ final・リテラル確認👀
```
# インクリメント

⭐️ 左から順番

int a = 10;
- a++ → 今の値を使う（10評価） → 後で増える
- ++a → 先に増える → その値を使う

⭐️評価とは「置くだけ」のこと

長い式は
<br>
「使われる値」を横に書く
<br>
→ 最後に足し算や引き算

# コンストラクタ
1. new B() // 子

    ↓

2. 親(A)コンストラクタ

    ↓

3. 子(B)コンストラクタ

## ⭐️ メソッド
```
public void test() {
}
public String test() {
}
```

✅ 戻り値がある（voidも戻り値の一種）

→ メソッド⚙️

## コンストラクタとインスタンス🐶

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

## 呼ばれる順番（親から先） 📖👀
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

## コンストラクタとメソッドの見分け方
### ⭐️ コンストラクタ

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

## this
### this.
⭐️ 自分のフィールド・メソッド
```Java
this.name = name;
     ↑       ↑
フィールド📦   引数🎁
```
- 左
  
  this.name
<br>
→ フィールド📦
- 右
<br>
→ 引数🎁

⭐️引数をフィールドに入れる 🎁 → 📦

### this() 📖👀
⭐️ 同じクラスの別コンストラクタを呼ぶ
- this(...)
<br>
    → 引数が一致するコンストラクタ
    <br>
    💥 コンストラクタの1行目だけ

## コンストラクタ呼び出し 📖👀
- super()：親のコンストラクタ
- this()：自分のクラスの別ブロックのコンストラクタ

💥 どちらもコンストラクタの1行目だけ

this.はどこでも書ける対象外

# 戻り値（void以外で宣言）
- 全ルートで`return`必須
- `boolean`には`void`なし
- `throw`終了なら`return`なくてOK

⭐️voidは引数に使えない

# ⭐️ メソッド宣言

戻り値の型は必須 ⚠️

void / int / String ...

```
void sample() { } ⭕️
int sample() { } ⭕️
String sample() { } ⭕️

sample() { } ❌
```

# メソッド呼び出し
- static → `クラス名.メソッド名()`
- インスタンス → `変数名.メソッド名()`
- default → `インターフェース名.super.メソッド名()`
- static → `this`使えない ❌
## メソッド呼び出し
◽️どのメソッド呼ぶ？
- 左型で探す
（オーバーロード）
- 実際に実行されるメソッド
→ 右(new側)
（オーバーライド）

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


# && と ||（左だけ）
- `&&` → 左falseなら右見ない
- `||` → 左trueなら右見ない

# & と |（両方見る）
- `&` と `|` → 必ず両方実行
- `|` どっちかtrue

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

    # アクセス修飾子（見える範囲）

    | 修飾子       | 見える範囲     |
    |:---------:|:------------------:|
    | public    | 世界中  |
    | protected | 同じ家 + 別の家の子供 |
    | なし        | 同じ家のみ         |
    | private   | 同じ部屋だけ               |


    | 修飾子       | 入れる人               |
    |:---------:|:------------------:|
    | public    | 🌍世界中            |
    | protected | 🏫同じパッケージ + 👶子クラス |
    | （無印）      | 🏫同じパッケージだけ        |
    | private   | 🏠自分のクラスだけ         |

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

## ① -d（destination）：クラス指定（.java⭕️）
### classファイルの保存場所を指定

`javac -d 出力先 ソース.java`

```
// .classを現在の場所へ作る
javac -d . Sample.java
      ↑          ↑
 行き先指定    作りたいクラス.java
```

```
javac
↓
コンパイルする

-d .
↓
.classを置く場所は「今いる場所」

Sample.java 👈 このファイルを指定
↓
材料（ソース）
```

## ② -cp / -classpath：置き場所のpath（.java❌）
`java -cp 場所 クラス名`

```
// クラスを探す場所を指定
java -cp . Sample
             ↑
          探す場所
```

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

数値以外の比較：等符号 ❌
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