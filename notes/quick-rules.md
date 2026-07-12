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

# 継承の修飾子 📖👀
👀 修飾子は使いたいものを見る！

⭐️修飾子はすぐ右を見ろ👀
- クラスを使う → public class
- フィールドを使う → public int
- メソッドを使う → public void

⭐️変数宣言の修飾子👀

# 左右判定（継承・implements）
⭐️目印

## 親型 = new 子型
```
例
A a = new B();
```

### ⭐️()ある？
### ⭕️ YES → 📛メソッド
⭐️ ある場合は2段階

    1. 左に同じ📛ある？👀

        ❌ ない
        → コンパイルエラー💥

        ⭕️ ある
        → 右（new側）のメソッド実行😊
### ❌ NO → 📦フィールド
        左（aの宣言）を見る👀

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
Aにtest()📛ある？👀

    ❌ ない
    → コンパイルエラー💥

    ⭕ある
    → Bのtest()実行 ⭕️ （実行はnew側）

# this. （同じ名前）
⭐️ 同じ名前のフィールドへアクセス

`public void setValue(String value)`

⭕️ this.value = value;

❌ value = value;
（引数 ← 引数）

# this()
⭐️ 別コンストラクタ

⭐️ this( 見つけた👀
<br>
↓
<br>
コンストラクタ呼び出し
<br>
↓
<br>
同じクラスの別コンストラクタ

💥 1行目以外に書けない 💥

# super()
super( 見つけた👀
<br>
↓
<br>
親コンストラクタ
<br>
↓
<br>
💥 1行目以外に書けない 💥
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

Interfaceのメソッドは必ず`public`

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
## 役割
🟦 interface → ルールを決める・defaultでセルフ処理😊（new❌）

🟨 abstract class → 😴サボり先輩（未完成OK・完成してもOK・new❌）

🟩 class implements → 💪下っ端後輩（完成必須・new⭕）


| 教科書    | ようちゃん語           |
| :------: | :----------------: |
| 抽象メソッド | 🛏️ベッドだけ（`;`）    |
| 具象メソッド | 🐶ALBA入り（`{}`あり） |
| 抽象クラス  | 😴 サボり先輩（未完成OK）|
| 具象クラス  | 💪 下っ端後輩（完成必須） |

## default：予備（実装がない時）

⭐️ defaultある？

⭕️ defaultあり！

`default void test() {}`

interfaceがセルフ実装😊
<br>
子が何もしない → interfaceがやる
<br>
子が実装する → 子がやる

❌ defaultなし！

`void test();`

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

implementしたクラスがoverride必須

しないと、どっちの名札📛？？💢
<br>
コンパイルエラー💥

# 💳 interfaceメソッド

### 処理なし
戻り値 メソッド();

### 処理あり（セルフ処理は3人⭕️）
- default 戻り値 メソッド() {}
- private 戻り値 メソッド() {}
- static 戻り値 メソッド() {}

💥 private default 両方はダメ

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

# コンストラクタ 📖👀
⭐️ アクセス修飾子は何でもアリ
- public      ⭕
- protected   ⭕
- （無印）    ⭕
- private     ⭕

→ 制限なし✨

⭐️ルール
- メソッド名とクラス名は同じ
- 戻り値を書かない ❌
- newすると最初に1回だけ呼ばれる

| 修飾子       | 誰が使える？         |
| --------- | -------------- |
| `default` | implementsした子  |
| `private` | interfaceの中だけ  |
| `static`  | interface名から呼ぶ |


# コンストラクタ（コンストラクタorメソッド） 📖👀
### voidを探せ 🔑

- Sample() ← コンストラクタ

- void Sample() ← メソッド💥（コンストラクタじゃない💢）

# コンストラクタ（親子の実行順）
new 子()

→ 親 → 子

⭐️ super() 自動追加

# override修飾子（アクセス修飾子の広さ）

継承（extends） → 親 ≤ 子

1. extends + 引数 ある？ → Yes ⭕️
2. 同じメソッド名（オーバーライド）ある？ → YES ⭕️

- インターフェース（implements） → 実装クラスは`public` のみ ⭕️

# 配列と継承
```
A[] array = {}
// A型専用マンションはA型のみ入居可⭕️
```
⭕ A
<br>
⭕ Aの子
<br>
❌ 関係ないクラス
<br>
❌ interfaceはnewできない

# キャスト
```
💥
class Alba { }

class Vanilla extends Alba { }

public class Main {
    public static void main(String[] args) {

        Alba a = new Alba();      // 🏠 中身はALBA
        Vanilla b = (Vanilla) a;  // 💥 実行時エラー

    }
}
```
🏠ハウスの中を見ろ👀

🏠
<br>
🐶 ALBA😴
<br>
😡「ALBAじゃん！！」

💥 ClassCastException

```
⭕️
Alba a = new Vanilla();
Vanilla b = (Vanilla) a;
```
🏠
<br>
🐶 VANILLA😴

🏠のラベルを変えても
<br>
🐶中身は変わらない💥

## 🐶 子 → 親 ⭕️
```
Alba a = new Vanilla();
Alba b = (Alba) a;
```
🏠の中は
<br>
🐶 VANILLA😴

⭕️😊

VANILLAはALBAの子供だから
<br>
VANILLAをALBAとして扱うのはOK⭕️

⭐️キャストなしでOK

## 🐶 親 → 子
```
Vanilla b = (Vanilla) a;
```
⚠️ キャストは必要

🏠の中が
- 🐶VANILLA → ⭕
- 🐶ALBA → 💥ClassCastException

#  recordのデフォルトコンストラクタ
record(String value)
<br>
↓
<br>
value📦を元に value() が自動生成される👻 （見えない）

📛同じ名札に注意💥

# equals + キャスト

⭐ equalsを見たら中を見る👀

a.equals(b)
<br>
↓
<br>
equalsの中に (型)obj がある？
<br>
↓
<br>
🎭 cast発見👀
<br>
↓
<br>
🏠 中身を見る👀
<br>
↓
<br>
違う犬🐶なら ClassCastException💥

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

# 可変長引数 (...) 📖👀
⭐️1つの可変長引数で何個でも定義できる
- 型... 変数名

```
⭕️ int... values
❌ int values...
```

- 引数が複数なら、一番最後に書く
- 1つだけ

# メソッド呼び出し 📖👀
### ⭐️名札を探せ📛
📛 = メソッド名 + 引数（型・数）のセット

👀 呼んでるメソッドを探す
<br>
↓
<br>
👀 同じ名札を探す
<br>
↓
<br>
👀 修飾子を見る（`.`で呼べる？）
<br>
↓
<br>
👀 主役（誰が呼んでる？）
<br>
↓
<br>
⭕ 呼べる
💥 コンパイルエラー

# 即断⭐️独立 📖👀
### 一番外側（独立）の class / interface / enum / record

使える修飾子
- public ⭕️
- 修飾子なし⭕️
- private ❌
- protected ❌ 

### ⭐️ recordのコンストラクタ
→ recordより厳しいアクセス修飾子は使えない ❌ 
<br>
（public または無印）

# 即断⭐️コンストラクタ or メソッド

()がある
<br>
    ↓
<br>
クラス名と同じ？👀
<br>
    ↓
<br>
⭕️YES → 📦コンストラクタ

❌NO → ⚙️メソッド

# 即断⭐️インターフェース💥 👀📖
## 👻メソッド
**public** abstractが勝手につく

## 👻 フィールド
public static **final** が勝手に付く

⭐️final = 定数🔐

## 処理を書く → default必須💥
❌ void sample() {}

⭕ default void sample() {}

## 抽象クラス
未完成でOK⭕️
<br>
↓
<br>
子クラスに実装させる👦

# 即断⭐️例外🚨
## 🔚 finally
### 🔚 finallyにreturnあり⭕️
📮 return（予約）
<br>
↓
<br>
前のreturn・throwは採用されない🙅‍♀️
<br>
↓
<br>
🔚 finallyのreturnが勝つ🏆
<br>
↓
<br>
ブロック外のreturnは出番なし❌（あれば）

### 🔚 finallyにreturnなし❌
📮 return（予約）
<br>
↓
<br>
finally（独り言🗣️）
<br>
↓
<br>
📮 予約したreturnが勝つ🏆

## 💥ネスト例外発生🔥
↓
<br>
一番近い（深い）catch🧯
<br>
↓
<br>
消火成功😊
<br>
↓
<br>
外へ飛ばない❌
<br>
# 瞬殺⭐️tryの相棒🚨
❌ tryだけ💥
<br>
❌ finally複数💥

✅ try + catch
<br>
✅ try + finally
<br>
✅ try + catch + finally
<br>
✅ catch複数⭕️

# 瞬殺⭐️コンパイルエラー 📖👀
- 宣言が間違い
<br>
→ その行💥

- 呼び出し・使用が間違い
<br>
→ 使った行💥

# 瞬殺⭐️ぬるぽを探せ
配列の参照型

```
Item[] items = new Item[3] 👀 見つけた
``` 

↓

```
items
 ┌───┬───┬───┐
 │ null │ null │ null │
 └───┴───┴───┘
 ```
    Itemは1つも作られてない💥

```
null, null, null // 中身全部null
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

# 瞬殺 ⭐️ ArrayList
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

# 瞬殺⭐️recordのコンパクトコンストラクタ💥 👀📖
```
public Data { // 👈コンパクトコンストラクタ👀
```
コンパクトコンストラクタ👀
<br>
↓
<br>
❌ this.フィールド📦💥
⭕ value🎁（引数）

⭐️{}の中にsthis. 👀即死💥
<br>
⭐️セットで死亡

# 瞬殺⭐️void
- 戻り値（return）はなし
  <br>
  →戻り値あればコンパイルエラー💥

  # 瞬殺⭐️実行順 📖👀
  ### newを探せ
- newある👀
1. 名札なし { } 
   <br>
    ↓
   <br>
2. 名札付き Sample()
- newない👀
    <br>
    ↓
    <br>
- { }  ： 出番なし😴❌
- コンストラクタ ： 出番なし😴❌
    <br>
    ↓
    <br>
    ⭐️ 初期値を見る👀

# 瞬殺⭐️record💥 📖👀
❌ extends不可（継承できない）💥

🔒 immutable（作ったら変更不可）

# 瞬殺⭐️return💥 📖👀
- メソッド終了
- returnの後は書けない💥
  <br>
  → 到達不能コード
  <br>
  → コンパイルエラー

# 瞬殺⭐️throw💥
- throwの後は書けない💥
  <br>
  → 到達不能コード
  <br>
  → コンパイルエラー

# 瞬殺⭐️値渡し

### 👀 引数の型を見る

① 基本型(int, double, boolean...)
<br>
↓
<br>
**コピー**を渡す✨
<br>
↓
<br>
元は変わらない

② 参照型(Sample)
<br>
↓
<br>
同じインスタンス✨
<br>
↓
<br>
元が変わる

# 瞬殺⭐️オーバーロード 📖👀
⭐️複数のメソッドに同じように一致💥

→ どっちを呼ぶかわからない💢
<br>
→ コンパイルエラー💥

# 瞬殺⭐️オーバーライド
```
()ある？
↓
メソッド

オーバーライドある？
↓
ない

⭐️親のメソッド使う
```

# try-with-resources
⭐️ `try()` 

💥 複数resource：closeは逆順🙃

💥 例外：close → catch → finally

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

# ガベージコレクション

⭐️ 誰からも参照されないインスタンス
<br>
→ ガベージコレクション対象🗑️

⭐️ null = 「参照を外す」

⭐️ まだ誰かが参照している
<br>
→ ガベージコレクション対象にならない

# null📖👀

リテラルのnullは小文字のみ ⭕️

NULL ❌

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

### 🕐 static

    ＝公園の時計
    ＝１個だけ
    ＝みんなで共有
⭐️ 誰かが変更すると
<br>
→ 全員その値を見る（上書き）

ALBA🐶「20時！」
<br>
        ↓
        <br>
VANILLA🐶も20時を見る👀

### 🕐 インスタンス変数

    ＝腕時計
    ＝newの数だけ増える
⭐️ 自分だけ変わる

ALBA🐶 20時
<br>
VANILLA🐶 10時

別々✨

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