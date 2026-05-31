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

➡️ メソッド

1. aの宣言を見る
2. 実行はnew側（override）

❌ NO

➡️ フィールド

aの宣言を見る

---
### 左 （フィールド）
```
A a = new B();
a.num
```
➡️ Aのnum ⭕️

---
### 右（メソッド）
```
A a = new B();
a.test();
```
⭕️ Aにtest()ある？

➡️ Bのtest()実行 ⭕️

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

同じ引数

    ⭕️ override

引数違う

    ❌ override

    ⭕️ overload

戻り値違うだけ（コンパイルエラー💥）

    ❌ overload

    ❌ override

## abstract （抽象メソッド）

⭕️ abstract ➡️ ; 必須 （中身なし）

❌ abstract ➡️ {} （中身あり）

❌ `final` 

❌ `new`

### 具象メソッド
⭕️ 普通メソッド ➡️ {}

❌ 普通メソッド ➡️ ;

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

→ 親 ➡️ 子

⭐️ super() 自動追加

## override修飾子（アクセス修飾子の広さ）

継承（extends） ➡️ 親 ≤ 子

1. extends + 引数 ある？ ➡️ Yes ⭕️
2. 同じメソッド名（オーバーライド）ある？ ➡️ YES ⭕️

- インターフェース（implements） ➡️ 実装クラスは`public` のみ ⭕️

## ⭐️overrideできない

private （親） ❌

→ 継承されない

final （親） ❌

→ 上書き禁止

static （両方） ❌

→ overrideではない

## try-with-resources
⭐️ `try()`

close ➡️ catch ➡️ finally

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

➡️ 外側の長さ（1番目の数字）

➡️ 2

⭐️最初の数字 → 行数

⭐️次の数字 → 列数

```
[ ][ ][ ][ ] ➡️ 1行目
[ ][ ][ ][ ] ➡️ 2行目
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

## 三項演算子（if の1行版）
条件 ? true側 : false側

条件？

 YES → true側

 NO  → false側

## 論理演算子
1. `&` （かつ）🔴

    ➡️ 必ず両方見る

    ➡️ 両方trueでtrue

2. `^` 🔴

    ➡️  必ず両方見る

    ➡️  片方だけtrueでtrue

3. `|` （または）🔴

    ➡️ 必ず両方見る

    ➡️ どちらかtrueでtrue

4. `&&` （かつ）⭕️

    ➡️ 左falseなら右見ない

    ➡️ 両方trueでtrue

5. `||` （または）⭕️

    ➡️ 左trueなら右見ない

    ➡️ どちらかtrueでtrue

### 優先順位（⭐ 左ほど先に計算）

`&` → `^` → `|` → `&&` → `||`