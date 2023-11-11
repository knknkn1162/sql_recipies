# SQL recipies

+ AggregateFilter: 所属部署ごとに平均年齢よりも若い社員を表示する
+ AllNotNull: 各グループごとに、グループ内の全てのレコードがnot nullであるようなグループを列挙する
+ CalcMode: mode(最頻値)をもとめる
+ CompleteData: tidyverseでいう[complete](https://tidyr.tidyverse.org/reference/complete.html)のようなことをする
+ PvotLonger: [列持ち -> 行持ち] 変換(Rの`pivot_longer`相当)
+ PivotWider: [行持ち -> 列持ち] 縦持ちのテーブルからクロス表を作成する(Rの`pivot_wider`相当)
+ PivotWiderSummary: [行持ち -> 列持ち] 縦持ちのテーブルをもとに集計する
+ DetectMissingNumbers: 数列から欠番を見つける
+ CountRecipes: (havingの中の)`count(*)`, `count(col1)`, `count(distinct col1)`の利用例
+ ExtractDuplicate: 完全に重複する要素を抜き出したい(その後にその要素を消すため)
+ ExtractPartiallyDuplicate: 各グループごとに、ターゲット要素が重複しているグループ名を列挙する
+ NotExists: 各グループごとに、すべてのレコード内の要素A(nullもありうる)がある値となるグループを列挙する
+ PrevRows: レコードの値が一つ前のレコードと同じようなものを列挙する
+ SequenceIfAll: n個の連続するシーケンスのうち、すべてある値であるものを求める
+ SetEqual: [厳密な関係除算] `(要求するitem) \equal (グループ内にあるitem)`となるグループを列挙する
+ Subset: [関係除算] `(要求するitem) \subset (店舗にあるitem)`(要求するitemをすべて持つ)となるグループを列挙する
+ GetPrimes: 素数列を求める
+ ConsecutiveId: Rの`consecutive_id`相当のことを行う
+ RowNumberGroup: グループごとに各要素に連番を割り振る
+ fizzbuzz: fizzbuzzを解く
+ LeadLag: Rでいうlead() or lag()をSQLで実装する
+ GetGroupIfs: 各グループごとに、すべての要素が複数の条件をみたすグループを列挙する
+ MaxBy: 各グループごとに最大値を取る行を取得する
+ SecondBiggest: 各グループごとに2番目に大きい要素を取得する
+ MultipleHaving: 複数のhaving条件の実装
+ MUltipleColumnIf: 複数の列に対しての全てみたす/部分的に/どれか満たす条件を実装
+ MinMax: グループごとに条件を満たすような最も大きいvalueの要素を取得する
+ FindMissing: missingの要素を見つける
+ SetEquivalence: [集合の相等性] 数も種類も全く同じ部品を取り扱う供給業者のペアを見つける
+ CoalesceRecipes: coalesce関数のレシピ集
+ GroupJoin: 各categoryについて、複数のテーブルをjoinして複数の指標をだす
+ GroupConcat: 各グループの要素たちを文字列連結する
+ UpdateAllAtOnce: 複数行でそれぞれ異なる値にupdateする
+ MultipleJoin: 複数のテーブルの結合をうまくやる
+ WhereIn: where inが効果的に使える例
+ OverlapsDateRange: 期間の重複に関連するレシピ集
+ ReciprocalPair: (4,6), (6,4)のような対を同一視した結果を取得する
+ TopN: 各グループで上位n位のリストをもとめる
+ TreeStructure: 閉包テーブルの例
