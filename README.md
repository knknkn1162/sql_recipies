# SQL recipies

+ AggregateFilter: 所属部署ごとに平均年齢よりも若い社員を表示する
+ AllNotNull: 各グループごとに、グループ内の全てのレコードがnot nullであるようなグループを列挙する
+ CalcMode: mode(最頻値)をもとめる
+ CompleteData: tidyverseでいう[complete](https://tidyr.tidyverse.org/reference/complete.html)のようなことをする
+ CrossTabulation: 縦持ちのテーブルからクロス表を作成する
+ DetectMissingNumbers: 数列から欠番を見つける
+ ExtractDuplicate: 完全に重複する要素を抜き出したい(その後にその要素を消すため)
+ ExtractPartiallyDuplicate: 各グループごとに、ターゲット要素が重複しているグループ名を列挙する
+ NotExists: 各グループごとに、すべてのレコード内の要素A(nullもありうる)がある値となるグループを列挙する
+ PrevRows: レコードの値が一つ前のレコードと同じようなものを列挙する
+ SequenceIfAll: n個の連続するシーケンスのうち、すべてある値であるものを求める
+ SetEqual: `(要求するitem) \equal (グループ内にあるitem)`となるグループを列挙する
+ Subset: `(要求するitem) \subset (店舗にあるitem)`(要求するitemをすべて持つ)となるグループを列挙する
+ GetPrimes: 素数列を求める
+ fib: フィボナッチ数列を求める
+ RowNumberGroup: グループごとに各要素に連番を割り振る
+ fizzbuzz: fizzbuzzを解く
+ LeadLag: Rでいうlead() or lag()をSQLで実装する
+ GetGroupIfs: 各グループごとに、すべての要素が複数の条件をみたすグループを列挙する
+ MaxBy: 各グループごとに最大値を取る行を取得する
+ SecondBiggest: 各グループごとに2番目に大きい要素を取得する