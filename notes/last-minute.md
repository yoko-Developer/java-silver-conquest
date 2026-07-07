✅ switch文のフォールスルー：ヒットしたら終わりじゃない → breakまで

✅ default：どこに書いてもいい

✅ switch式：フォールスルーしない

✅ yield：switch式で値を返す

✅ {} がない:次の1文だけが対象

✅ 二次元配列：array[i][j] = i階j部屋

✅ 配列：array.length = 階数（行数）

✅ instanceof：変数の型じゃなく中身チェック、📦 中の人は右側の型ですか？

✅ instanceof：中身 = 右側の型ならtrue

✅ instanceof変数：true側だけ使える（else❌）

✅ for文：条件式だけカンマNG💥

✅ record：継承できない（extends❌）

✅ record：新しいフィールドは追加できない ❌

✅ record：引数なしコンストラクタを作るなら this("値")

✅ 独立：一番外側のclass/record = public又は修飾子なし

✅ コンパクトコンストラクタ：`public Data {` → this.❌

✅ 継承：子が使うフィールドがない → 親を見ろ👀

✅ 継承：コンストラクタは引き継がない❌

✅ interface：セルフ処理あり → default必須💥

✅ interface：セルフ処理なし → 子が実装💥

✅ interface：public abstract と public static final はお化け👻

✅ interface：default は直接 implements している interfaceだけ

✅ interfaceのdefaultが2人🐶🐶：implementクラスでoverrideして選ぶ

✅ interface / abstruct → newできない💥

✅ override：同じ名札📛（メソッド名＋引数）の{}の中身を上書きすること

✅ override：親 <= 子 / 戻り値は逆 親 >= 子

✅シグニチャ：メソッド名 + 引数の型の数と順番