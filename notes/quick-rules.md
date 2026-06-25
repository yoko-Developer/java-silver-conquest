# 最初にやること瞬殺チェック✏️
1. コンパイルエラー候補
2. 左右判定
3. override
4. catch順
5. cast
   
# ポリモーフィズム
`犬 dog = new ALBA();`

左：親
<br>
右：子

型＝左
<br>
中身＝右

`Base b = new Sub();`

型   ：Base
<br>
中身：Sub

→ まず左を見る👀

# 左右判定（継承・implements）
⭐️目印

## 親型 = new 子型
```
例
A a = new B();
Animal a = new Dog();
List l = new ArrayList();
```

⭐️()ある？

⭕️ YES
<br>
→ メソッド

1. aの宣言を見る
2. 実行はnew側（override）

❌ NO
<br>
→ フィールド

aの宣言を見る

## 左 （フィールド）
```
A a = new B();
a.num
```
→ Aのnum ⭕️

## 右（メソッド）
```
A a = new B();
a.test();
```
⭕️ Aにtest()ある？

→ Bのtest()実行 ⭕️

❌ ない

コンパイルエラー💥

# this （同じ名前）

同じ名前のフィールドへアクセス

`public void setValue(String value)`

⭕️ this.value = value;

❌ value = value;
（引数 ← 引数）

# override

同じ名前
<br>
同じ引数
<br>
    ⭕️ override

引数違う
<br>
    ❌ override
<br>
    ⭕️ overload

戻り値違うだけ（コンパイルエラー💥）
<br>
    ❌ overload
<br>
    ❌ override

# abstract （抽象メソッド）
⭕️ abstract → ; 必須 （中身なし）

❌ abstract → {} （中身あり）

❌ final

❌ new

## 具象メソッド
⭕️ 普通メソッド → {}

❌ 普通メソッド → ;

## public abstract 👻

Interface（型情報）は必ず`public`

public → 書いてもOK
<br>
public → 書かなくてもpublic（お化け👻）

protected ❌
<br>
private ❌

## class
家系図👨‍👩‍👧‍👦

親は1人

→ 多重継承 ❌

```
class extends A,B ❌
```

❌ ママ犬が2人いる家系図にはできない🐶

## interface
能力カード🎫

何枚でもOK

多重継承 ⭕️

```
interface extends A,B ⭕
implements A,B ⭕
```

```
interface C extends A, B ⭕
```

# interface
default：予備

⭐️ defaultある？

⭕️ ある！

`default void test() {}`
<br>
↓
<br>
実装しなくてもOK
- 実装がなければ default が実行される
- 実装があれば default は使われない

❌ ない！
`void test();`
<br>
↓
<br>
子（実装クラス）が実装必須
<br>
なければコンパイルエラー💥

# default競合⚔️

```
interface A
default log()
```

```
interface B
default log()
```

```
class C implements A, B
```

↓

同じdefaultが2個👻👻

override必須

しないと
<br>
コンパイルエラー💥

# continue （到達不能）

⭕️ continue;
} // ループの外へ

❌ continue;
処理 // 到達不能コード

# String （immutable・不変の掟） 📖👀
- replace
- concat
- substring

⭕️ a = a.concat("A");

❌ a.concat("A"); （aは変わらない）

# コンストラクタ（親子の実行順）
new 子()

→ 親 → 子

⭐️ super() 自動追加

# override修飾子（アクセス修飾子の広さ）

継承（extends） → 親 ≤ 子

1. extends + 引数 ある？ → Yes ⭕️
2. 同じメソッド名（オーバーライド）ある？ → YES ⭕️

- インターフェース（implements） → 実装クラスは`public` のみ ⭕️

# ⭐️overrideできない

private （親） ❌
<br>
→ 継承されない  （子クラスから直接見れない） ❌
<br>
→ オーバーロードにならない ❌
<br>
→ 同じ名前でも別メソッド ⚠️

final （親） ❌
<br>
→ 上書き禁止

static （両方） ❌
<br>
→ overrideではない

## 瞬殺⭐️見る場所
```
()ある？
↓
メソッド

オーバーライドある？
↓
ない

⭐️親のメソッド使う
```

# 瞬殺⭐️ぬるぽを探せ
配列の参照型

```
Item[] items = new Item[3] 👀 見つけた
``` 

↓

Itemは3個作られてない

```
null, null, null` 中身null
```

⭐️ ぬるぽ探せ‼️ 👀

# 瞬殺 ⭐️ returnを探せ（equals） 📖👀
` **equals** 問題

1. return を探す
2. 何を比較しているか見る
3. 比較していない項目は無視

例

✨ **return s.num == this.num;**

    → numだけ比較
    → nameは無視

✨ **A.equals(B)**

    this = A
    obj = B

# 瞬殺 ⭐️ AllayList
add
<br>
→ 増える

set
<br>
→ 置換
```
equals問題だ 👀
↓
this = 左
obj = 右
↓
比較してるのは num
↓
10 == 10
```

⭐️ Objectは古い神様ルール

equalsでもアドレス比較（==）になる

# try-with-resources
⭐️ `try()` closeは逆

close → catch → finally

# catch 
小さい → 大きい ⭕

大きい → 小さい ❌💥
（到達不能）


# 配列 clone()

`array1.clone()`

外だけコピー

⭕️ array1[1] == array2[1]

❌ array1 == array2

# 配列 （罠集😈） 📖👀
- []の位置は自由
- 最初の要素数は必須
- 要素数と初期化子は併用不可[]{} （両方数字があるとダメ）
- {}があれば空で良い

# 二次元配列
[][] は二次元配列だよ〜の意味
```
String[][] array
```
array.length
<br>
→ 階数（外側の要素数）

array[i].length
<br>
→ その階の部屋数

array[i][j]
<br>
→ 中身の値

外側for
<br>
→ 階を回る

内側for
<br>
 → 部屋を回る

# package（クラスの住所📮）

名前空間
<br>
＝同じ名前を区別する仕組み📛

packageなし
<br>
→ 無名パッケージ（パッケージに属している）

# getter / setter

set

同じ名前

⭕️ this.必要

❌ value = value;

# コマンド

1. javac （コンパイル）

→ .java 必要 ⭕️

`javac Sample.java`

## c-java
```
javac
↓
cいる👀
↓
コンパイル
↓
ソース(.java)食べる
```
2. java （実行）

→ .class 不要 ❌

`java Sample`

## javaクラス
```
java
↓
cいない👀
↓
実行
↓
クラス名だけ
```
⭐️ Sample.class がない場合

コンパイルしてなければ`.java`必須 ⚠️

`java Sample` ❌

`java Sample.java` ⭕️ （Java11+）

### クラスパス(-cp)の区切り

`.` ⭕️

`/` ❌

## クラスパスの最後

パッケージ名.クラス名 ⭕️

# javaコマンドの起動パラメータ
args.length

⭐️スペース区切り = 1個ずつ
<br>
⭐️"A B" = 1個
<br>
⭐️" = " （ダブルクォート文字）
<br>
⭐️文字数は数えない❌

`"`と表示させるため`¥`をつける
```
¥"
↓
"
```
# var 📖👀
⭕️ ローカル変数のみ
<br>
❌ フィールド
<br>
❌ 引数
<br>
❌ 戻り値

## varの型推論
右辺で型決定👀

`var a = new B();`

↓

`B a = new B();`

と同じ

⭐️ varで決まった型は変わらない

# """（テキストブロック） 📖👀
最初の `”””` の次は改行必須⚠️

最後は改行しなくてOK ⭕️

改行(Enter)も1文字とカウント

# instanceof
お前は誰だ？

親 instanceof 子
❌

子 instanceof 親
⭕️

null
❌ false

無関係
💥 コンパイルエラー

# if文
## 定義方法 📖👀
```
if( 条件式 ) { 
  処理
};
```
() 必須 ⚠️
<br>
{} 1行なら省略可

⭐️ {} がない場合、if が効くのは次の1文だけ
```
if (false) // 🔴不合格！赤信号
    System.out.println("A");

System.out.println("B");
```
答え：B
<br>
Aは不合格
## 三項演算子（if の1行版）
条件 ? true側 : false側

条件？

 YES → true側

 NO  → false側

# if / else / elseif
```
 if (...) {
}
else {  // ここが実行されても
}
if {    // その下も判定される
}
```
    ⭐️ elseが終わったら、その下の処理へ進む

- if
- else
- if ⭐️

    ⭐️ 別のグループなのでelseの下も実行

## else if - else
- if
- else if
- else

    ⭐️ 1つのグループなので1つしか実行されない

## else if -if
- if
- else if
- if ⭐️

    ⭐️ 上の if-else if は終了
    <br>
    ⭐️ 下の if は新しい判定

## ブロックがない場合
⭐️ elseは一番近いifにくっつく
```
if (a)
    if (b)
        X;
    else  // if(b) のグループ
        Y;
```

    ⭐️ else は if(b) のもの
# switch文（フォールスルー） 📖👀
case :
<br>
→ break出さずに抜ける

breakなし
<br>
→ フォールスルー

⭐️ defaultはどこに書いてもOK
（switch文・switch式どちらも）

# switch式（フォールスルーなし） 📖👀
case ->

→ フォールスルーなし（各行お化けbreak👻）

⭐️default必須（全パターン網羅してれば不要）
defaultはどこに書いてもOK⭕️

⭐️ `};` セミコロン必須

`{}`の中から値を返す（複数行）

→ yield（1行なら不要） = return ⭐️ switch式のみ⚠️

→ break ❌

# ラベル 📖👀

⭐️ ラベルは文(statement)に付けられる

⭕️ for
<br>
⭕️ while
<br>
⭕️ do-while
<br>
⭕️ switch
<br>
⭕️ try
<br>
⭕️ return
<br>
⭕️ 代入
<br>
⭕️ 式

# 瞬殺{}がない
{} がない
- if
- while
- for

⭐️ 次の1文`;`だけが対象（次の行ではない）
<br>
⭐️ インデントは関係ない

do-while ⚠️
```
do
.
.
.
while (条件);
```
⭐️ do 〜 while(条件); 全体で1文

# for文

```
for (①⭕️初期化; ②❌条件式; ③⭕️更新式)
```

①初期化 → カンマOK ⭕️
<br>
③更新式 → カンマOK ⭕️
<br>
②条件式 → カンマNG ❌💥 
<br>
❌ コンパイルエラー💥
```
for (... ; i < 3, j < 5 ; ...)
❌              ↑💥
```

⭐️ 条件式省略OK ⭕️
<br>
→ 自動的に**true**

`for (;;)`
<br>
→ **true**は無限ループ🌀

⭐️ 更新式省略OK ⭕️

# 拡張for文
for (型 変数 : 配列) 📖👀

# 論理演算子（1はon、0はoff） 📖👀
1. `&` （AND/かつ）🔴
   
    →必ず両方見る
    <br>
    → 両方trueでtrue（両方1ならtrue）

2. `^` 🔴 （XOR/排他的論理和）

    →  必ず両方見る
    <br>
    →  片方だけtrueでtrue（どちらかが1なら1）

3. `|` （OR/または）🔴

    → 必ず両方見る
    <br>
    → どちらかtrueでtrue

4. `&&` （かつ）⭕️

    → 左falseなら右見ない
    <br>
    → 両方trueでtrue

5. `||` （または）⭕️

    → 左trueなら右見ない
    <br>
    →どちらかtrueでtrue

# ビット演算子
```
8 4 2 1
↓ ↓ ↓ ↓
1 0 1 1
```
0b0001 = 1
<br>
0b0010 = 2
<br>
0b0100 = 4
<br>
0b1000 = 8

## 優先順位（⭐ 左ほど先に計算）

`&` → `^` → `|` → `&&` → `||`

## リテラル・変数宣言 瞬殺ルール 📖👀
英字 ⭕️

数字 ⭕️
（先頭は❌）

_ ⭕️

$ ⭕️

`_` `$` 以外の記号
全部ダメ ❌

# static / インスタンス
インスタンス → static ⭕️
static → インスタンス ❌

🕐 static

    ＝公園の時計

    ＝１個だけ

    ＝みんなで共有

🕐 インスタンス変数

    ＝腕時計

    ＝newの数だけ増える

## staticメソッド
this 禁止 ❌

インスタンス変数を直接見れない ❌

## 初期化順序
`new クラス名()` の数だけ実行

① `static {}` ：  最初に1回だけ
<br>
② `{}` ： （コンストラクタ） newの数
<br>
③ `クラス名() ` ： （インスタンス） newの数

```
staticメソッド発見！
↓
インスタンス変数触ってない？
↓
触ってたら怪しい
```

# オーバーロード（同じ名前のメソッドを増やす）
引数の`型`、`個数`、`順番`のどれかが違う

※変数名は関係ない

## 呼び出しルール
- そのまま一致が最優先
- 変換が必要なら後回し
- 同点なら曖昧 → コンパイルエラー

# ボクシング（自動変換） 🥊🎁

int → Integer ： オートボクシング
<br>
Integer → int ： アンボクシング

# リテラルの接尾辞（L / F）
L：longの大きい数で必要
<br>
F：floatの小数で必要

## protected
同じパッケージ → OK

別パッケージ → 要注意⚠️
<br>
子クラス経由 ⭕
<br>
親型変数経由 ❌

# キャスト（型変換）
## char の自動変換
⭐️大は小を兼ねない

小→大 ⭕️
<br>
大→小 ❌（キャスト必要）

ただし

byte ↔ char ❌
<br>
short ↔ char ❌

はキャスト必要⚠️

```
Dog d = new ALBA();
(ALBA)d ⭕️

ALBA a = (ALBA)d; // ⭕️「dをALBAとして扱え！」
(ALBA)d ❌
ClassCastException
```

`(ALBA)d`

dの中身を
<br>
ALBAとして見せてください

## sealed + permits
sealed 🔒
<br>
→ 子を指定

final 🛑
<br>
→ 継承終了

non-sealed 🔓
<br>
→ 継承自由（誰でもOK ⭕️ → 普通のクラス解禁）

# do-while

⭐ do と while の間は必ず1回実行

do
<br>
↓
<br>
処理
<br>
↓
<br>
while(条件)

**条件は後で見る👀**

# 進数 📖👀
0b 〜 ➡️ 2進数（0と1だけ⭕️）

0 〜  ➡️ 8進数（0〜7だけ⭕️）

0x 〜 ➡️ 16進数（0〜9、A〜Fなら⭕️）

# Silver最終兵器✏️

問題を見る
↓

何の問題？

# _（アンダースコア）
⭕️ 数字と数字の間

❌ 先頭

❌ 末尾

❌ 記号の前後(. L F x bなど)

- override
- catch
- sealed
- default競合
- cast
- try-with-resources
- static
・instanceof

まずジャンルを探す👀