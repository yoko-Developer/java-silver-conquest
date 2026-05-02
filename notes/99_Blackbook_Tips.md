## mainメソッドの5つの鉄則

![](img/99-1.jpg)
- **public** であること
- **static** であること（インスタンス化不要！）
- **void** であること（戻り値なし）
- メソッド名は **main** であること
- 引数は **String配列型を1つ** 受け取ること

## javaコマンド
1. javac：コンパイル（.java -> .class生成）
   `javac Hello.java`
2. java：実行（クラス名指定）
   `java Hello`

    【NG】拡張子不要！！
    - ❌ java Hello.class  `javaコマンドにクラスファイル名を渡したらダメ！！`

    ※ publicクラス名＝クラス名.java(ファイル名.java)

    ※ publicなし＝ファイル名じゃなくてOK.java
