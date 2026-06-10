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

## 左右判定（継承・implements）
⭐️目印
### 親型 = new 子型
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

---
### 左 （フィールド）
```
A a = new B();
a.num
```
→ Aのnum ⭕️

---
### 右（メソッド）
```
A a = new B();
a.test();
```
⭕️ Aにtest()ある？

→ Bのtest()実行 ⭕️

❌ ない

コンパイルエラー💥

## this （同じ名前）

同じ名前のフィールドへアクセス

`public void setValue(String value)`

⭕️ this.value = value;

❌ value = value;
（引数 ← 引数）

## override

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

## abstract （抽象メソッド）
⭕️ abstract → ; 必須 （中身なし）

❌ abstract → {} （中身あり）

❌ `final` 

❌ `new`

### 具象メソッド
⭕️ 普通メソッド → {}

❌ 普通メソッド → ;

### public abstract 👻

Interface（型情報）は必ず`public`

public → 書いてもOK
<br>
public → 書かなくてもpublic（お化け👻）

protected ❌
<br>
private ❌

### class
家系図👨‍👩‍👧‍👦

親は1人

→ 多重継承 ❌

```
class extends A,B ❌
```

❌ ママ犬が2人いる家系図にはできない🐶

### interface
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

## interface
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

## default競合⚔️

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

## continue （到達不能）

⭕️ continue;
} // ループの外へ

❌ continue;
処理 // 到達不能コード

## String （immutable・不変の掟）
- replace
- concat
- substring

⭕️ a = a.concat("A");

❌ a.concat("A"); （aは変わらない）

## コンストラクタ（親子の実行順）
new 子()

→ 親 → 子

⭐️ super() 自動追加

## override修飾子（アクセス修飾子の広さ）

継承（extends） → 親 ≤ 子

1. extends + 引数 ある？ → Yes ⭕️
2. 同じメソッド名（オーバーライド）ある？ → YES ⭕️

- インターフェース（implements） → 実装クラスは`public` のみ ⭕️

## ⭐️overrideできない

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

### 瞬殺⭐️見る場所
```
()ある？
↓
メソッド

オーバーライドある？
↓
ない

⭐️親のメソッド使う
```

## try-with-resources
⭐️ `try()` closeは逆

close → catch → finally

## catch 

小さい → 大きい ⭕

大きい → 小さい ❌💥
（到達不能）

## 配列 clone()
`array1.clone()`

外だけコピー

⭕️ array1[1] == array2[1]

❌ array1 == array2

## 二次元配列
`new int[2][4]`

ガタガタOK ⭕️
```
array[0] = new int[100];
array[1] = new int[2];
```

`new int[2][4] array.length`

→ 外側の長さ（1番目の数字）

→ 2

⭐️最初の数字 → 行数

⭐️次の数字 → 列数

```
[ ][ ][ ][ ] → 1行目
[ ][ ][ ][ ] → 2行目
```

```
new int[2][4]

array.length
→ 最初の数字

array[0].length
→ 2番目の数字
```


## getter / setter

set

同じ名前

⭕️ this.必要

❌ value = value;

## コマンド

1. javac （コンパイル）

    → .java 必要 ⭕️

    `javac Sample.java`
2. java （実行）

    → .class 不要 ❌

    `java Sample`

    ### クラスパス(-cp)の区切り

    `.` ⭕️

    `/` ❌

    ### クラスパスの最後

    パッケージ名.クラス名 ⭕️

## var
ローカル変数のみ ⭕️

## """（テキストブロック）
最初の `”””` の次は改行必須⚠️

最後は改行しなくてOK ⭕️

改行(Enter)も1文字とカウント

## instanceof

親 instanceof 子
❌

子 instanceof 親
⭕️

null
❌ false

無関係
💥 コンパイルエラー

## 三項演算子（if の1行版）
条件 ? true側 : false側

条件？

 YES → true側

 NO  → false側

## 論理演算子
1. `&` （かつ）🔴
   
    →必ず両方見る
    <br>
    → 両方trueでtrue

2. `^` 🔴

    →  必ず両方見る
    <br>
    →  片方だけtrueでtrue

3. `|` （または）🔴

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

### 優先順位（⭐ 左ほど先に計算）

`&` → `^` → `|` → `&&` → `||`

## switch文（フォールスルー）
case :
<br>
→ breakまで実行

breakなし
<br>
→ フォールスルー

## switch式（フォールスルーなし）
case ->

→ フォールスルーなし（各行お化けbreak👻）

→ ⭐️default必須（値を返す場合）

`{}`の中から値を返す

→ yield（1行なら不要） = return

→ break ❌

## リテラル・変数宣言 瞬殺ルール
英字 ⭕️

数字 ⭕️
（先頭は❌）

_ ⭕️

$ ⭕️

`_` `$` 以外の記号
全部ダメ

## static / インスタンス
インスタンス → static ⭕️
static → インスタンス ❌

🕐 static

    ＝公園の時計

    ＝１個だけ

    ＝みんなで共有

🕐 インスタンス変数

    ＝腕時計

    ＝newの数だけ増える

### staticメソッド
this 禁止 ❌

インスタンス変数を直接見れない ❌

### 初期化順序
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

## オーバーロード（同じ名前のメソッドを増やす）
引数の`型`、`個数`、`順番`のどれかが違う

※変数名は関係ない

### 呼び出しルール
- そのまま一致が最優先
- 変換が必要なら後回し
- 同点なら曖昧 → コンパイルエラー

## ボクシング（自動変換）🎁

int → Integer ： オートボクシング
<br>
Integer → int ： アンボクシング

## リテラルの接尾辞（L / F）
L：longの大きい数で必要
<br>
F：floatの小数で必要

### protected
同じパッケージ → OK

別パッケージ → 要注意⚠️
<br>
子クラス経由 ⭕
<br>
親型変数経由 ❌

## キャスト（型変換）
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

## Silver最終兵器✏️

問題を見る
↓

何の問題？

- override
- catch
- sealed
- default競合
- cast
- try-with-resources
- static
・instanceof

まずジャンルを探す👀