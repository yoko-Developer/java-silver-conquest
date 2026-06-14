# 確認する順
1. main見る
2. new どこ？
3. 左右判定ある？
4. 呼ばれるメソッド探す
5. コンパイルエラー候補見る

## 左右判定（継承・implements）
`A a = new B()`

⭐️呼び出すメソッド探し
    → 左型で探す
- () ある？
  - メソッド → 右(new側)見る
  - override実行は右(new側)

- () ない？

  - フィールド → 左見る

## implementsあったら
1. public？（同じか緩い？）
2. メソッド名同じ？
3. 引数同じ？
4. abstractなら未実装OK

## 例外
1. throw 見る
2. catch 上から探す（ヒットしたらcatch終わり）
3. finally 基本実行

### try-catch-finally（昔のやり方）
1. try（爆発）
2. catch（バグ捕獲）
3. finally（ここで人間が手で蓋を閉める！）

### try-with-resources
    try() ⭐️目印：これあれば
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

## String
- String
  
  →immutable（不変）
- 変更系メソッド

    →新しいString作るだけ

## intern()
Stringのコンスタントプールを使う

⭐️ newとリテラルの比較でもtrueになる

`new String("a").intern() == "a"`

→ true ⭕️s

`a.intern() == b.intern()`

→ true ⭕️

## equals / ==
- == ：アドレス
- .equals() ：値
  
### 配列 clone()
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

## 配列 （定義方法）
### 宣言

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

### 宣言時
⭐️ 要素数は書かない

```
int[] a; ⭕

int a[3]; ❌ 💥 コンパイルエラー
```

### インスタンス生成時（右側）
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

### nullの罠😈
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

## ArrayList
### 特徴
- 重複OK ⭕️
- null OK ⭕️
- スレッドセーフではない ❌

- `ArrayList list = new ArrayList<>();`
  <br>
 → どんな型でも入れられるバッグ
### 追加・変更
- add(value)
  <br>
→ 末尾追加
- add(index, value) 
  <br>
 → 指定位置に追加（位置,値）
- set(index, value)
  <br>
  → 置き換え

### 削除
- remove(value)
  <br>
  → 
  
  ⭐️ remove判定はequals()
  <br>
  equals()の中身次第で削除される要素が決まる

### ひっかけ💥
    ⭐️ for-each中にadd/remove（コレクション変更）

    → 実行時例外💥

    ConcurrentModificationException

    ⚠️ ただし次の要素取得前にループ終了すると
    
    例外にならない場合あり

## コンストラクタ（親から先）
1. new B() // 子

    ↓

2. 親(A)コンストラクタ

    ↓

3. 子(B)コンストラクタ

## 戻り値（void以外で宣言）
- 全ルートで`return`必須
- `boolean`には`void`なし
- `throw`終了なら`return`なくてOK

## メソッド呼び出し
- static → `クラス名.メソッド名`
- default → `インターフェース名.super.メソッド名()`
- static → this使えない ❌

## sealed + permits（継承できる子を制限）
子は必須
- final
- sealed
- non-sealed

子もsealed
- permits必要

## override（上書き）
- ()ある？
  
  → メソッド → 右(new側)

- 親メソッドを書き換える

    → 親の中身は使われない

確認
1. メソッド名同じ？
2. 引数同じ？
3. public弱くなってない？

## && と ||（左だけ）
- `&&` → 左falseなら右見ない
- `||` → 左trueなら右見ない

## & と |（両方見る）
- `&` と `|` → 必ず両方実行
- `|` どっちかtrue

## abstract（抽象クラス=未完成）
- abstract class
  
    → `final` ❌

    → `new` できない

- abstract method
    
    →   `{}`なし

    →  ; で終わる

- abstract method ある

  → classもabstract必要

### ⭕️❌判定

⭕ abstract class
- 処理なしOK

❌ final abstract
- 処理あり & なしは両立不可

❌ new AbstractClass()
- abstractはnew不可

---

## abstractメソッド(抽象メソッド)

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

## ループ

⭐️出力が continue / break の上か下か見る
- continue（その周回終了）

    → continue含めて下の処理スキップ（そのループのみ）
<br>
    → 次のループへ

- break

    → 今いるブロック終了（その後の繰り返ししない）
<br>
    → break含めてfinish

- continue;の次の行に実行コードは書けない❌（到達不能コード）

## 二次元配列
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

## _（アンダースコア）
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

## do-while
*doとwhileの間は必ず1回実行される🐱*

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

### while
条件 → 処理
### do-while
処理 → 条件

## for 二重ループ
外側 → 行移動

内側 → 列移動

## instanceof
→ 型チェック

instanceof String str（instanceOfが作った変数）

→ true側だけ str使える

## var
- ローカル変数のみOK ⭕️
- 初期化必須⚠️
- 引数 ❌
- 型変更NG ❌
- null単体NG ❌

## this
- 同じ名前 x なら → ローカル変数優先
- this.x → フィールド

## オーバーライド

⭐️チェック
1. メソッド名同じ？
2. 引数同じ？
3. 戻り値は 同じ or 
4. public弱くなってない？

## オーバーロード
メソッド名同じ

引数違い
（型 or 数 or 順番）⇦どれか1つでOK

⭐️呼び出し：引数の型が一致する方（近い方）

### メソッド呼び出し
◽️どのメソッド呼ぶ？
- 左型で探す
（オーバーロード）
- 実際に実行されるメソッド
→ 右(new側)
（オーバーライド）

### コンストラクタ呼び出し
- super()：親のコンストラクタ
- this()：自分のクラスの別ブロックのコンストラクタ
## catch順
子 → 親
  
    狭い罠（チワワ） → 広い罠（動物）

親 → 子
- 下（狭い罠）のcatch到達不能
- コンパイルエラー

## 継承
extends：子 → 親 → その親（全員呼ばれる）

super → 親

finalメソッド → override不可❌

super() → 親コンストラクタ

## super
- コンストラクタ：super() 省略OK
（自動追加）

- 親と子で同じメソッド名で子が親を呼ぶ：super.メソッド名() 省略できない
- 子が親を呼ぶ：super()省略化
 
  ※オーバーライドなしの場合

## アクセス修飾子
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

## コマンド

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

### javaクラス
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

## キャスト
大きい箱から小さい箱に変更 →
キャスト必須

### charの自動変換
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

### to char
byte → char ❌
<br>
short → char ❌

int → char ❌（キャスト必要）

## getter/setter
- getter：privateで値を見るボタン（値取得）
- setter：privateな値を変えるボタン（値変更）


## 三項演算子（if の1行版）
条件 ? trueの時 : falseの時

例
```
int a = 5;
int x = (a > 3) ? 100 : 200;
```

a > 3 ？

YES → 100

NO  → 200

## StringBuilder

new StringBuilder()
<br>
→ capacity 16

new StringBuilder("abcde")
<br>
→ 文字数 + 16

"abcde"
<br>
→ 5 + 16 = 21