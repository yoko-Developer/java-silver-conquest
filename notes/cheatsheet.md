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

## String
- String
  
  →immutable（不変）
- 変更系メソッド

    →新しいString作るだけ

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

## for 二重ループ
外側 → 行移動

内側 → 列移動

## instanceof
→ 型チェック

instanceof String str（instanceOfが作った変数）

→ true側だけ str使える

## var
- ローカル変数のみOK ⭕️
- 初期化必須
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

## コンパイルと実行
1. javac → コンパイル
    .java必要

    `javac Sample.java`
    
2. java → 実行
    
    .class書かない❌

    `java Sample`

⭐️Java11+

→ java Sample.java OK

## キャスト
大きい箱から小さい箱に変更 →
キャスト必須

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
