# SQL recipies

+ AggregateFilter: 所属部署ごとに平均年齢よりも若い社員を表示する
+ AllNotNull: 各グループごとに、グループ内の全てのレコードがnot nullであるようなグループを列挙する
+ CalcMode: mode(最頻値)をもとめる
+ CompleteData: tidyverseでいう[complete](https://tidyr.tidyverse.org/reference/complete.html)のようなことをする
+ PivotLonger: [列持ち -> 行持ち] 変換(Rの`pivot_longer`相当)
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
+ Largest: 各グループごとに最も大きい要素を取得する
+ Largest2: 各グループごとに2番目に大きい要素を取得する
+ MultipleHaving: 複数のhaving条件の実装
+ TwoPhasedAggregate: 二段階の集約を使う場合のスマートな実装
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
+ Cut: Rの`cut`相当のことをする
+ TopN: 各グループで上位n位のリストをもとめる
+ Median: 中央値を求める
+ WithCheckOption: ビューの`with check option`句のレシピ。
+ TreeStructure: 閉包テーブルの例

# 動作方法

```sh
docker compose up
# http://127.0.0.1:8888/lab でjupyter notebookが起動
```

# misc

## NULLについて

| unary | 非NULL | NULL |
| --- | --- | --- |
| nullif(x,x) | NULL | NULL |
| nullif(0, (x-x)) | NULL | 0 |
| nullif(1, (x-x)) | NULL | 1 |

| binary | AがNULL |
| --- | --- |
| A and B | NULL |
| A or B | B |
| A = B | NULL |
| C in (A,B) | C=B |
| C not in (A,B) | NULL |
| where not exists (select ... where C = A) | True |
| C < all(A,B) | NULL |
| C < any(A,B) | C < B |

### 対処法
+ not null制約をつけて極力nullを排除する
+ 極力デフォルト値で設定できないか検討する
    + 未コード化用コードを割り振る(0: 未知, 9: 不能など)
    + 名前の場合: 不明を表す値を与える
    + 数値の場合: 0で代替する
    + 日付の場合: 最大値・最小値で代替する
 
## クエリ実行の順番

1. (with cteを実行する)
2. `from tbl`を実行
3. `where ..`を実行
4. `group by`があればこれを実行
5. `having`があればこれを実行
6. `select ..`の実行

## 集約時に集合の性質を調べるための条件の使い方

|expr|remarks|
|---|---|
|`count(distinct col) = count(col)`|colの値が一意(重複なし)である|
|`count(*) = count(col)`|colにNULLが存在しない|
|`count(*) = max(col) - min(col)+1`|colは連番|
|`min(col) = max(col)`|colは同じ値またはすべてnull|
|`max(col) * min(col) > 0`|すべての符号(sign)が同じ|
|`max(col) * min(col) < 0`|どこかで0で交わる|
|`min(abs(col)) = 0`|colは少なくとも1の0を含む|
|`max(abs(col)) = 0`|colは全て0|

## 期間同士の関係

+ T1とT2はオーバーラップしない: `((T1.end_time < T2.start_time) or (T1.start_time > T2.end_time))`
    + 前者の条件はT1 < T2, 後者の条件はT2 < T1
+ 2つの期間が隣接する: `((T1.end_time = T2.start_time) or (T2.end_time = T1.start_time)`
    + 前者の条件はT1 <= T2, 後者の条件は T2 <= T1
+ T2がT1に含まれる(包含): `((T1.start_time <= T2.start_time) and (T2.end_time <= T1.end_time))`
    + T2 \subset T1
+ T1とT2がオーバーラップする: `(T1.start_time, T1.end_time) overlaps (T2.start_time, T2.end_time)`
    + 隣接は含まない
        + 隣接する場合も含めたいときは、`((T1.end_time >= T2.start_time) and (T1.start_time <= T2.end_time))`
    + 競技のオーバーラップ(はみでる)タイプと包含タイプがある
 
## 関係演算
+ 制限(Restrict): `where`
+ 射影(Project): `select`
+ 積(Product): `cross join`
+ 和(Union): `union`
+ 交差(Intersect): `intersect`
+ 差(Difference): `except`
+ 結合(Join): `(inner/left/right/full) join`
    + 積と制限の2つで表せる
+ 除算(Divide): `having` or `except`