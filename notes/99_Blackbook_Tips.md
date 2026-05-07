## mainメソッドの5つの鉄則
![](img/99-1.jpg)
- public / static / void
- main
- String[] args（1つ）

## javaコマンド
- javac：コンパイル（.java → .class）
  `javac Hello.java`

- java：実行（クラス名）
  `java Hello`

❌ java Hello.class

※ publicクラス名＝ファイル名

## 数値リテラル
- 8進数：0〜7（先頭0）
- 16進数：0x
- _：先頭・末尾・記号の前後❌

## 識別子
- _ $：OK
- 数字始まり：NG
  
## var
- 右辺によって左辺のデータ型を推論できる場合のみ使用可
- ローカル変数のみOK（フィールド不可）
- 初期化必須（右辺から型推論）
- 型推論はコンパイル時に行われる

⭐️初期化必須！！
- ⭕️ `var a = 10;`
- ⭕️ `var e = new ArrayList<>();` ：ダイヤモンド演算子の型情報がない場合は型推論(`Object`など)

## String
オブジェクト生成時
- newを使ってインスタンス化
- `""` で文字列リテラルで記述
- immutable(不変)なオフジェクト
- concat：引数として渡された文字列とインスタンスの文字列を連結して戻す

<br>

- String：不変なのでバッファなし
- StringBuilder：16のバッファ(予備)を持っている
  
## mutable(可変) / imutable(不変)
imutable
- String：変更不可（新しいオブジェクトを作る）
- 全てのフィールドを`private`で定義
- クラスをfinalで宣言(override不可)

mutable
- StringBuilder：変更可（元のオブジェクトが変わる）

## 文字列まわり
長さ
- length()：文字数（例："abc".length() → 3）

位置
- charAt(i)：i番目の文字（0開始）
- indexOf("a")：最初に見つかった位置（なければ-1）
- indexOf()：開始位置(0から順番)

切り出し
- substring(a, b)：a以上b未満

メソッドチェイン
- substring(1, 3).replace("b", "c")：bcだけを抽出してその文字列だけを置換

判定
- startsWith("ab")：先頭が一致するか（true/false）
- endsWith：引数の文字で終わっているか

置換
- replace("a", "b")：置き換え（新しい文字列）

反転
- reverse()：abcde->edcba

replace(start, end, str) の数え方
- 「文字そのもの」ではなく「文字の間の仕切り線」を数える
- `start` は含めて、`end` は含めない（endの直前まで）
![](img/99-2.jpg)

## Stringの比較
true = メモリ内にある文字列への参照を戻す
⭐️同じ値の場合
- intern()：newしてもダブルクォートありのリテラルと比較ならtrue⭕️（intern()のみnewとリテラル比較）
- String a = "a"：ダブルクォートあり（コンスタントプール）⭕️
- .equals()：値比較（new無関係）⭕️⭐自作クラスは絶対Stringではないからfalse❌
false = アドレスが違う
- new：新しい領域（どちらかがnewしていれば❌）

## StirngBuilder
- .equals()：false❌（toStringを使うとtrue⭕️）
- toString().equals()：文字列比較できる⭕️

## 値渡し（参照）
- プリミティブ：値がコピーされる
- 参照型：参照（アドレス）がコピーされる

## 配列
- 1番目の要素の要素数は省略できない
  ```
  // ❌コンパイルエラー
  int f[][] = new int [][3;]
- 初期化子があれば[]はブランクとなる
  ```
  ❌int[] array = int[2] {2, 3};

  ⭕️int[] array = int[] {2,3};
  ```

## ArrayList
- スレッドセーフではない(同時にさわれない並列処理はできない)
- add：追加
- set：インデックス指定して置き換え
- remove：インデックス指定して削除

## 繰り返し構文
- 拡張for文：カーソルを戻せないので、削除した次の要素は必ず飛び越し(スルー)される
- for文：`i--` を使うことで、繰り上がってきた要素をもう一度チェックできる

## 演算子
![](img/99-3.jpg)

![](img/99-4.jpg)

## 比較
equals()

- String(override済み)：**値比較**
- new：**アドレス比較**

    | 比較方法    | Stringの場合   | 自作クラスの場合   |
    | :--------: | :---------: | :-------: |
    | ==    | アドレスを見る（new してれば false）     | アドレスを見る（new してれば false）    |
    | .equals()     | 値を見る（同じなら true）     | アドレスを見る（new してれば false）   |

## 「ぬるぽ」判定ルール
  - ⭐️.equals()：`.`の左側が実行主

    | 比較方法    | a の状態  | b の状態   |結果|
    | :--------: | :---------: | :-------: | :-------: | 
    | a.equals(b)   | new Object() (実体あり) | null|false (安全に比較終了) |
    | b.equals(a)   | null   | new Object()|例外がスロー (ぬるぽ発生)|
    a == b|null|null|true (==ならエラーにならず判定できる)|

<br>

equals()：以下２つがなく、newしていればfalse！！

```
⭐️@Override
⭐️public boolean equals(Object obj) {} //(Object)であること！他は対象外
```
```
// Objectになってるかがポイント

```

⚠️例外：true になるパターン

@Overrideしている場合：同じ「値」ならtrue

- instanceof：型をチェックする（true / false）
    - 親型でもtrue（継承OK）
    - nullはfalse（例外にならない）
    - 無関係な型同士はコンパイルエラー

## instanceof
### 中身をチェックする
- `obj instanceof A` ：obj が A or 子ならtrue（型チェック）
- `obj instanceof A b`：trueのときだけ b として使える（パターンマッチ）
- 無関係な型：コンパイルエラー
- null：false（例外にならない）
  ```
  null instanceof String → false
  ```

## 分岐
Swich
- ❌使えないもの
  - long
  - float
  - double
  - boolean

caseの後ろ
- ⭕️使えるもの（⭐️caseの後ろ）
  - リテラル
  - 定数 (finalがついた変数)
  - 定数式 (2*5など)
- ❌使えないもの
  - 普通の変数

Swich式
- defaultがないとコンパイルエラー
- `{};`：セミコロンがないとコンパイルエラー

do while
- `{}`なし：doとwhileの間に**1文のみ**しか書けない
- `{}`あり：doとwhileの間に**何文書いてもOK**

## static
- static -> クラスに属する（インスタンス不要）
- ❌**staticから非staticは触れない**（アクセス不可！！）

アクセス
- static → static：⭕️
- 非static(インスタンス) -> static：⭕️
- static -> 非static(インスタンス)：❌ NG（this使えない）

ポイント
- static内ではインスタンスメンバに直接アクセス不可
- staticは「クラス名.メンバ」で呼べる

## メンバアクセス
- 参照.メソッド名(引数)：メソッド呼び出し
- 参照.メソッド名：()がないとフィールド参照

（例）
- obj.getName();  // メソッド
- obj.name;       // フィールド

## ラッパー型
- ボクシング：int → Integer（自動）
- アンボクシング：Integer → int（自動）
- nullをintにすると例外（NPE）

## 可変長引数(...)
- 位置のルール： ... は必ず **型のすぐ後ろ** に書く（例：int... values）
- 順番のルール： 他の引数と一緒に使うときは、**一番最後** に書く
- 個数のルール： 1つのメソッドに可変長引数は **1つだけ** しか使えない

## オーバーロード
条件
- 引数の型・数・順番のいずれかが違う
- 戻り値は関係ない（戻り値だけ違いはNG）
- 引数だけで判定（修飾子・戻り値は関係ない）

## アクセス修飾子
- コンストラクタを修飾するアクセス修飾子に制限なし
![](img/99-5.jpg)

- サブクラス宣言
  - static：インナークラスのみ使用可
  - private：インナークラスのみ使用可
  - non-seale：シールクラスのサブクラスのみ使用可
  - protected：クラス宣言で使用不可❌

## コンストラクタ(this)
- new子() → 親 → 子 の順
- super()：親コンストラクタ
- this()：同じクラスの別コンストラクタ
- this() / super() ：1行目のみ & どちらか1つだけ記述できる

ルール
- 1行目に書く（最重要）
- 2行目以降は❌
- this()：同じクラス
- super()：親クラス

## record
### データを保持するためだけのクラスを1行で、超シンプルに書くための仕組み
- 不変クラス（immutable）※newが終わったあと、代入後は不変
- フィールドは自動でfinal
- コンストラクタ・getter・equalsなど自動生成
- `toString`, `hashCode`, `equals`メソッドが定義されている
- publicとアクセス修飾子なしのみ🆗
- サブクラスの定義（継承）不可❌
- 引数なしのコンストラクタ生成不可❌
- static以外のインスタンスフィールドは追加不可❌

例：
record Person(String name, int age) {}

コンストラクタ
- 全引数コンストラクタは自動生成される
- 必要なら追加コンストラクタ定義できる
- コンパクトコンストラクタでバリデーション可能(this❌)

## 継承
引き継ぎNG❌
- コンストラクタ
- privateなフィールド、メソッド
- 多重継承

- フィールド：左辺の見た目で決まる（コンパイル時）
- メソッド：右辺の実際の中身で決まる（実行時）
- （`Parent p = new Child();` のとき）

オーバーライド不可❌
- private
- static
- final

## インターフェース
- 実体化（インスタンス化）不可 ❌
- 多重実装OK ⭕️
- メソッドは基本 public abstract（自動）
- 「できること」（型）を定義するもの
- privateの場合：中身のソースがないと❌

defaultメソッド
- 実装クラスで必須ではない
- そのまま使える
- 必要ならオーバーライド可能
- Objectクラスのメソッド(`toString()` / `equals()` / `hashCode()`)の定義不可❌

## クラスの種類
抽象クラス（abstract class）
- インスタンス化できない
- 抽象メソッド（中身なしの未完成メソッド）を持てる
- 通常のメソッド（中身あり）も持てる
- フィールドも持てる
- コンストラクタも持てる

抽象メソッド
- 中身がないメソッド（処理が書いてない）

具象クラス
- 普通のクラス（インスタンス化できる）
- 抽象メソッドをすべて実装する必要がある
  
##  オーバーライド（override）
- throws句：親より広げられない
- 親クラスのメソッドを上書き
- メソッド名：同じ
- 引数：型・数・順番がすべて同じ
- @Override アノテーション：付けられる（推奨）
- 戻り値：同じ or サブクラス型（子クラスの型）
- アクセス修飾子：子クラス ≥ 親クラス（子は親より強い）

##  オーバーロード（overload）
- 同じクラス内でメソッドを複数定義
- メソッド名：同じ
- 引数：型・数・順番のどれかが違う
- 戻り値だけ違う：NG
- アノテーション不要

## 優先順位
変数
1. ローカル変数
2. フィールド変数

## sealedクラス（シールクラス）
### 継承できるクラスをあらかじめ指名しておく仕組み
- sealed：継承を制限するクラス（継承できるクラスを限定）
- permits：継承できるクラスを指定

子クラス
- final / sealed / non-sealed のいずれか必須
- ⭐️sealedの場合：permits 必須

## 例外処理
- throw：エラー発生（即停止）
- throws：エラー出すかも宣言

流れ
メソッド呼ぶ → throw → catchに飛ぶ

- throwされたら下の処理は実行されない
- catch：上から順にチェック
- finally：
  - 必ず実行される（※強制終了除く）
  - finallyに**return**があると割り込みする(catchのreturnより先に出力)
- returnがなければ通常通り上から（割り込みなし）
- try / finallyブロック：１つのみ記述可
- catchブロック：複数記述可

- エラー：`throw句`に宣言する必要なし

- ネスト：内側から処理開始
- 自作例外のサブクラス： 
  - `java.lang.Exception` ：例外（チェック例外）必要条件
  - `java.lang.RuntimeException`：実行時例外（非チェック例外）必須ではない

## 例外の種類
チェック例外（コンパイル時にチェック）
- Exception：すべての例外の親
- IOException：外部入出力（ファイル・通信）
- SQLException：データベース関連

非チェック例外（実行しないとわからない）
- IndexOutOfBoundsException：スーパークラス（配列、文字列、コレクション）
- ArrayIndexOutOfBoundsException：配列（要素外アクセス）
- StringIndexOutOfBoundsException：文字列（範囲外）
- IllegalStateException：状態がおかしい

Error
- StackOverflowError：無限再帰
- ExceptionInInitializerError：static初期化失敗

 ```
 Index系 → 範囲外
 StackOverflow → 無限ループ（再帰）
 IllegalState → 状態ミス
 InitializerError → static初期化ミス
 ```
  ![](img/99-6.jpg)

## マルチキャッチ
### 1つの catch ブロックで複数の異なる例外をまとめて捕まえるための仕組み
- `|`で区切る
- 継承関係にある例外は同時に指定できない(例：Exception | RintimeException❌)
- 変数は暗黙的にfinal（再代入不可）

## try-with-resources
### ファイルやデータベースなど「使い終わったら必ず閉じなければいけないもの（リソース）」を自動でお片付け（close）してくれる超便利な仕組み
- try() にリソースを書く
- 自動でcloseされる（finallyいらない）
- AutoCloseableを実装している必要あり
- → リソース自動クローズが目的（例外処理ではない）
- `java.io.Closeable`インターフェース / `java.lang.AutoCloseable`インターフェースのいずれかを実装したクラス
- try()の中
→ `AutoCloseable` / `Closeable` のクラスだけOK

書き方
- カッコの中で「宣言」と「作成」をセットで記述する
```
try (型 変数 = new クラス()) {
    処理
}
```

```
try (Scanner sc = new Scanner(System.in)) {
    System.out.println(sc.nextLine());
}
```
<br>

- 外で先に作っておいた「変数」を、あとからカッコに入れる
```
クラス 変数 = new クラス();
    try (変数) {
        処理
    }
```

```
Scanner sc = new Scanner(System.in);

try (sc) {  // ⭕ Java9以降
}
```

※初期化必須

※AutoCloseable系のみOK

## 順番
try-with-resources
- 複数のリソース(a,b,c)を扱う場合：
  - open：a→b→c
  - close：c→b→a
- 例外発生時
  - close→catch→fainally(finallyが最後)

## import文
- ワイルドカード(`*`)：クラス名のみ使用可⭕️ / パッケージの途中は使用不可❌