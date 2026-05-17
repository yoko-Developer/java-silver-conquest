## 継承`(A a = new B())`
- () ある？
→ メソッド → 右(new側)
- () ない？
→ フィールド → 左

## implementsあったら
1. public？（同じか緩い？）
2. メソッド名同じ？
3. 引数同じ？
4. abstractなら未実装OK

## 例外
1. throw 見る
2. catch 上から探す（ヒットしたらcatch終わり）
3. finally 基本実行

## try-with-resources

    try() ⭐️目印：これあれば

    ↓

    close() 自動

    ↓

    catch

    ↓

    finally

## String
- String
  
  →immutable（不変）
- 変更系メソッド

    →新しいString作るだけ

## equals / ==
- == ：アドレス
- .equals() ：値

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

## & と |（両方）
- `&` と `|` → 必ず両方実行
- `|` どっちかtrue

## abstract（抽象クラス=未完成）
- abstract class
  
    → `final` ❌

    → `new` できない

    →`{}`内を`;`で終わらせるなら
    中身の頭に`abstract`必須

- abstract method
    
    →   `{}`なし

    →  ; で終わる

- abstract method ある

  → classもabstract必要

## ループ
- continue

    → continue含めて下の処理スキップ
    → 次のループへ

- break

    → 今いるブロック終了
    → break含めてfinish

## 二次元配列

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
- ローカル変数のみOK
- 初期化必須
- 型変更NG
- null単体NG

## this
- 同じ名前 x なら → ローカル変数優先
- this.x → フィールド

## オーバーロード
メソッド名同じ

引数違い
（型・数・順番）

⭐️呼び出し：引数が一致する方