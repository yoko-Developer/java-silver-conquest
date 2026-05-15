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

⭐左右判定の方法
①フィールドは左(18行目)
　Oyako p // つまりOyakoクラス
②右側は実体・中身(18行目)
　new Kodkmo() // newの後ろのクラス名・Kodomo
③何を呼び出してるか見る(20行目)
　p.name // ()がない -> フィールド＝親！！
　p.hello //  ()がある-> メソッド＝子！！
　