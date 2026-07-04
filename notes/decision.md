# 継承の左右判定

```
class Oyako {
    String name = "親";
    void hello() {
        System.out.println("親のこんにちは！");
    }
}

class Kodomo extends Oyako {
    String name = "子";
    @Override
    void hello() {
        System.out.println("子のハロー！");
    }
}

public class Main {
    public static void main(String[] args) {
        Oyako p = new Kodomo(); // ← ここが超重要ポイント！
        
        System.out.println(p.name);
        p.hello();
    }
}
```

## ⭐左右判定の方法

①左はフィールド(18行目)
- Oyako p // Oyakoクラス

②右側は実体・中身(18行目)
- new Kodkmo() // newの後ろのクラス名Kodomo

③何を呼び出してるか見る(20行目)
- p.name // ()がない -> フィールド＝親！！
- p.hello //  ()がある-> メソッド＝子！！

# instanceofの左右判定

```
class Alba { } // 親・Alba

class Vanilla extends Alba { } // 子・Vanilla

public class Main {
    public static void main(String[] args) {
        Alba dog1 = new Alba();    // 中身はALBA
        Alba dog2 = new Vanilla(); // 中身はVANILLA

        // ⭐ instanceof で右左をチェック！
        System.out.println(dog2 instanceof Vanilla); // true
        System.out.println(dog2 instanceof Alba);    // true
        System.out.println(dog1 instanceof Vanilla); // false
    }
}
```

## 判定ルール
```
左 側  instanceof  右 側
(変数)             (クラス名)
 ```

⭐️ 中に入っているオブジェクトの型をチェックする

❌ 変数自体の型（見た目）を見るのではない！

## ⭐ instanceof 左右判定の極意

`dog2 instanceof Vanilla`
- 左側（dog2）：変数の見た目はAlbaだけど、中身（実態）はVanilla
- 右側（Vanilla）：Vanillaの仲間ですか？
- 結果：true！

`dog2 instanceof Alba`
- 左側（dog2）：中身（実態）はVanilla
- 右側（Alba）：Albaの仲間ですか？
- 結果：VanillaはAlbaの子供だからtrue！

`dog1 instanceof Vanilla`
- 左側（dog1）： 中身（実体）はAlba
- 右側（Vanilla）： Vanillaの仲間ですか？
- 結果： 親はAlba、Vanillaの子供にはなれないから false！