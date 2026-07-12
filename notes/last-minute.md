🔀 switch文のフォールスルー：ヒットしたら終わりじゃない → breakまで

🔀 default：どこに書いてもいい

🔀 switch式：フォールスルーしない

🔀 yield：switch式で値を返す

🔁 {} がない:次の1文だけが対象

🔁 for文：条件式だけカンマNG💥

🏢 二次元配列：array[i][j] = i階j部屋

🏢 配列：array.length = 階数（行数）

🔍 instanceof：変数の型じゃなく中身チェック、📦 中の人は右側の型ですか？

🔍 instanceof：中身 = 右側の型ならtrue

🔍 instanceof変数：true側だけ使える（else❌）

💿 record：継承できない（extends❌）

💿 record：新しいフィールドは追加できない ❌

💿 record：引数なしコンストラクタを作るなら this("値")

🌳 継承：子が使うフィールド📦がない → 親を見ろ👀

🌳 継承：子が使う📛がない → 親を見ろ👀

🌳 継承：コンストラクタは引き継がない❌

🌳 継承：📦フィールドは上書きしない（親子で別々）

🌳 extends：親は1人🐶

💳 implements：カードは何枚でもOK🐶🐶🐶

💳 interface：セルフ処理{}あり → default / private / static必須💥

💳 interface：セルフ処理なし → 子が実装💥

💳 default：子も使える😊

💳 private🔐：interfaceだけ😐

💳 static📌：インターフェース名.📛()で呼ぶ😗

💳 interface：{}あり → default / private / staticだけ⭕️

💳 interface：privateとdefault💥 → 一緒に書けない💢

💳 interface：public abstract と public static final はお化け👻

💳 インターフェース名.super.メソッド名();：🐶直接のママ犬⭕️、おばあちゃん犬❌

💳 interfaceのdefaultが2人🐶🐶：implementクラスでoverrideして選ぶ

💳 interface / abstract→ newできない💥

📛 override：同じ名札📛（メソッド名＋引数）の{}の中身を上書きすること

📛 俺のメソッド📛：2段階👀

📛 override：親 <= 子 / 戻り値は逆 親 >= 子

📛 メソッド：上書き（override）😊

📦 フィールド：同じ名前でも上書きしない（親子で別々）

🏗️ コンストラクタ：子をnew → this → super をたどれ👀 👉 表示は親→子😊

🏗️ this(...)：同じクラスの🏗️引数が同じ📛のを探せ👀

🏗️ super(...)：親クラスの🏗️ 引数が同じ📛のを探せ👀

⭐️ シグニチャ：メソッド名 + 引数の型の数と順番

⭐️ 独立：一番外側のclass/record = public又は修飾子なし

⭐️ コンパクトコンストラクタ：`public Data {` → this.❌

👈 this. = 自分の📦（スコープ内の同じ名前を区別）

🦭 sealedの子：final / sealed / non-sealed の3択😊

💥 RuntimeException：throws不要😊

💥 IOException・SQLException：throws必要😊

💥 args（コマンドライン引数）なし：args == null ❌、args.length == 0 ⭕（長さ0の配列）ArrayIndexOutOfBoundsException💥

💥 finally：最後に必ず実行

💥 catch：親を先に書くと子は到達不能💥

💥 try()：close逆順🙃

💥 try()：例外→close→catch→finally

💥 return・throw → 後ろは到達不能💥

📋 List宣言：List<String> list = new ArrayList<>();

📋 はみ出しList：範囲外→IndexOutOfBoundsException

📦 はみ出し配列：範囲外 → ArrayIndexOutOfBoundsException

🔤 はみ出しString → StringIndexOutOfBoundsException

📮 return（予約）：finally → returnで終了 🏆 （🚨ブロック外のreturn❌）

📮 return（予約）：finallyにreturnあり 🏆 → 前のreturn上書き💥

📮 return（予約）：finallyにreturnなし（独り言） → 予約return
が勝つ 🏆

🚨 tryの相棒：catch又はfinallyどっちか必須、finally複数❌💥

🚒 例外ネスト：内側で消火されたエラー🔥は外には広がらない

🚨 独自例外：オリジナル例外のみんなのママはException🐶

🚨 throws：RuntimeExceptionファミリー🐶🐶 → 書かなくていい😊

💥 Error：JVM重大トラブル💣（catchはできる⭕、throws不要😊）

🚨 はみ出しList📋：範囲外→IndexOutOfBoundsException

🚨 はみ出し配列📦：範囲外 → ArrayIndexOutOfBoundsException

🚨 はみ出しString🔤 → StringIndexOutOfBoundsException

🚨 null.equals：左がnullなら瞬殺⭐️ぬるぽ💥

🎭 cast：equalsの(A)obj → 中身✅違う犬❌ → ClassCastException💥