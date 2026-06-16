# Java Silver 単語帳

## StringBuilder
⭐️ mutable（可変）

変更系メソッドで元が変わる

- append("a")
  <br>
  後ろに追加

- toString()
  <br>
  Stringに変換

- reverse()
  <br>
  反転

- toString()
  <br>
  Stringへ変換

- .capacity()
  <br>
  16

## String
⭐️ mutable（可変）

変更系メソッドでも元は変わらない

### 位置
- charAt(i)
  <br>
  i番目の文字（0開始）⭐️範囲外は実行時エラー

- indexOf()
  <br>
  最初に見つかった位置（0から順番）
  <br>
  ⭐️なければ-1

### 判定
- startsWith("ab")
  <br>
  先頭が一致するか（true/false）

- endsWith()
  <br>
  引数の文字で終わっているか

### 置換
- replace("a", "b")
  <br>
  aをbに置き換え
  <br>
  ⭐️新しいStringを返す

- replace(1,3,"a")
  <br>
  1以上3未満をaに入れ替える

### 切り出し
- substring(a, b)
  <br>
  a以上b未満

- substring(a)
  <br>
  aから後ろを切り出し

### 文字列操作
- concat
  <br>
  文字列の最後に文字をくっつける

- strip()
  <br>
  文字列の前後の空白を削除

- trim()
  <br>
  前後の空白削除
  （昔からある）

- length()
  <br>
  文字数を取得

- intern()
  <br>
  コンスタントプール（秘密の倉庫）を使う

  `new String("a").intern() == "a"`]
  <br>
  → true

## 型
- instanceof
  <br>
  型チェック
  <br>
  「お前は○○型か？」

- instanceof String s

  型チェック＋変数作成
  <br>
  Stringなら s が使える

 - cast
  <br>
  型変換

    `(ALBA)d`

    「dをALBAとして扱え」
- varargs (...)
  <br>
  可変長引数
  <br>
  何個でも引数を渡せる
  <br>
  実態は配列
  ```
  String... value
  int... nums
  ```

## コピー
- clone()
  <br>
  配列をコピーする

  ⭐️ clone()した配列は別物
  
  `arrayA == arrayB`
  <br>
  → false

  ⭐️ 多次元配列は浅いコピー

  `arrayA[0] == arrayB[0]`
  <br>
  → true

## switch
- yield
  <br>
  switch式で値を返す

## 継承
- extends
  <br>
  継承
  <br>
  親クラスを引き継ぐ

- protected
  <br>
  同じパッケージ または 子クラスからアクセス可能
- override
  <br>
  上書き
  <br>
  メソッド名同じ
  <br>
  引数同じ

- overload
  <br>
  同じ名前のメソッドを増やす
  <br>
  引数違い

- sealed
<br>
継承できる子を制限

- permits
  <br>
  継承を許可する子を指定

- non-sealed
  <br>
  継承自由に戻す（普通のクラス）

## 例外
- Exception例外クラスの親
  <br>
  例外クラスの親

- RuntimeException
  <br>
  実行時例外
  <br>
  throws不要
  
- IOException
  <br>
  ファイル・通信

- SQLException
  <br>
  データベース

- IndexOutOfBoundsException
  <br>
  範囲外アクセスの親

- ArrayIndexOutOfBoundsException
  <br>
  配列の範囲外

- StringIndexOutOfBoundsException
  <br>
  文字列の範囲外

- NullPointerException
  <br>
  nullに対してメソッド・フィールドを使った

- IllegalStateException
  <br>
  オブジェクトの状態が不正（閉じた後に使うなど）

- Error
  <br>
  例外ではない重大エラー

- 例外ではない重大エラー
  <br>
  無限再帰

- ExceptionInInitializerError
  <br>
  static初期化失敗

## 数学
- Math.max(a,b)
  <br>
→ 大きい方

- Math.min(a,b)
  <br>
→ 小さい方

## try-with-resources

- AutoCloseable
  <br>
  try-with-resourcesで使える