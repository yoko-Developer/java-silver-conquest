# Java Silver 単語帳
- concat
  <br>
  文字列の最後に文字をくっつける

- instanceof
  <br>
  型チェック
  <br>
  「お前は○○型か？」

- instanceof String s

  型チェック＋変数作成
  <br>
  Stringなら s が使える

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

- yield
  <br>
  switch式で値を返す

- extends
  <br>
  継承
  <br>
  親クラスを引き継ぐ

- protected
  <br>
  同じパッケージ または 子クラスからアクセス可能

- instanceof String s
  <br>
  型チェック＋変数作成

  Stringなら s が使える

- strip()
  <br>
  前後の空白削除

- trim()
  <br>
  前後の空白削除（古い書き方）

- protected
  <br>
  同じパッケージ

  または

  子クラスからアクセス可能

- Math.max(a,b)
  <br>
→ 大きい方

- Math.min(a,b)
  <br>
→ 小さい方

- intern()
  <br>
  コンスタントプールを使う

  `new String("a").intern() == "a"`]

  → true

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

- cast
  <br>
  型変換

  `(ALBA)d`

  「dをALBAとして扱え」

- sealed
  <br>
  継承できる子を制限

- permits
  <br>
  継承を許可する子を指定

- non-sealed
  <br>
  継承自由に戻す（普通のクラス）

- AutoCloseable
  <br>
  try-with-resourcesで使える