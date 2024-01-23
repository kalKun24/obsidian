### 繰り返しタスクファイル

カンマ区切りのCSV形式です。

|列index|必須|意味|例|
|---|---|---|---|
|1|O|タスク名|10:00 朝会|
|2|O|繰り返しパターン|every day|
|3||起点日|2022-03-11|

以下の行は無視されます。

- `//`から始まるコメント行
- 空行、もしくはスペースのみの行

#### タスク名

タスクの名称です。

先頭に半角スペースやタブをつけると、[Silhouette: Insert tasks](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#silhouette-insert-tasks)コマンドを実行したとき、タスクがインデントされます。たとえば

```adblock
普通の タスク,every day
    4つインデント,every day
        8つインデント,every day
	タブインデント,every day
```

という4つのタスクを登録したとき、[Silhouette: Insert tasks](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#silhouette-insert-tasks)を実行すると以下が挿入されます。

```adblock
- [ ] 普通の タスク
    - [ ] 4つインデント
        - [ ] 8つインデント
	- [ ] タブインデント
```

#### 繰り返しパターン

[繰り返しタスク](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%B9%B0%E3%82%8A%E8%BF%94%E3%81%97%E3%82%BF%E3%82%B9%E3%82%AF)の繰り返されるパターンを示す文字列です。

> **Warning**  
> 複数のパターンを複合させることはできません。たとえば `weekday/mon` のような表現はできません。

|パターン|例|複数指定|
|---|---|---|
|毎日|every day|不可|
|平日(月～金)|weekday|不可|
|土日|weekend|不可|
|[稼働日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%A8%BC%E5%83%8D%E6%97%A5)|workday|不可|
|[稼働日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%A8%BC%E5%83%8D%E6%97%A5)ではない日|non workday|不可|
|曜日複数指定|sun/mon|`/` 区切り可|
|毎月特定日複数指定|10d/20d|`/` 区切りで可|
|N日ごと|every 3 day|不可|
|[月初](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E6%9C%88%E5%88%9D)|beginning of month|不可|
|[月初の稼働日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E6%9C%88%E5%88%9D%E3%81%AE%E7%A8%BC%E5%83%8D%E6%97%A5)|workday beginning of month|不可|
|[月末](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E6%9C%88%E6%9C%AB)|end of month|不可|
|[月末の稼働日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E6%9C%88%E6%9C%AB%E3%81%AE%E7%A8%BC%E5%83%8D%E6%97%A5)|workday end of month|不可|

##### 曜日

曜日は小文字のアルファベット3文字で表現します。

|表記|意味|
|---|---|
|sun|日曜|
|mon|月曜|
|tue|火曜|
|wed|水曜|
|thu|木曜|
|fri|金曜|
|sat|土曜|
|sun!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない日曜|
|mon!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない月曜|
|tue!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない火曜|
|wed!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない水曜|
|thu!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない木曜|
|fri!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない金曜|
|sat!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない土曜|
|sun*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の日曜|
|mon*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の月曜|
|tue*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の火曜|
|wed*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の水曜|
|thu*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の木曜|
|fri*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の金曜|
|sat*|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)の土曜|

また、曜日表記の前に数字(N)を入れると、[第N曜日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%AC%ACN%E6%9B%9C%E6%97%A5)を表現できます。以下は一例です。

|表記|意味|
|---|---|
|2sat|第2土曜日|
|1fri!|[休日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E4%BC%91%E6%97%A5)ではない第1金曜日|

##### オフセット

末尾にオフセット表記をつけると、特定日の〇日前や〇日後という表現ができます。

|末尾につける表記|意味|
|---|---|
|>N|N日後|
|<N|N日前|
|>N!|N[稼働日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%A8%BC%E5%83%8D%E6%97%A5)後|
|<N!|N[稼働日](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%A8%BC%E5%83%8D%E6%97%A5)前|

以下は具体例です。

```
稼働日の翌日タスク,workday>1
月末の3日前タスク,end of month<3
月末の2稼働日前タスク,end of month<2!
休み前の稼働日,non workday<1!
休み明けの稼働日,non workday>1!
翌日が休み,non workday<1
休日の水曜の1稼働日前,wed*<1!
```

#### 起点日

繰り返しパターンの起点となる日付です。たとえば

```
タスク,every 2 day,2022-03-10
```

のとき、2022/3/10を起点として1日おき(2日に1回)のタスクと判定されます。また、起点日以降にならないとタスクは有効になりません。

具体的な各日付でのタスク有無は以下のようになります。

|日付|有無|
|---|---|
|2022/03/08|無|
|2022/03/09|無|
|2022/03/10|**有**|
|2022/03/11|無|
|2022/03/12|**有**|
|2022/03/13|無|
|2022/03/14|**有**|

#### そのほかの例

私が設定している[繰り返しタスク](https://github.com/tadashi-aikawa/silhouette?tab=readme-ov-file#%E7%B9%B0%E3%82%8A%E8%BF%94%E3%81%97%E3%82%BF%E3%82%B9%E3%82%AF)の一部を例として紹介します。

```
08:30 出勤,mon!/tue!/thu!
22:45 歯磨き,every day
洗濯(洗う),every 2 day,2023-01-14
洗濯(干す),every 2 day,2023-01-14
爪切り,every 7 day,2023-01-13
Minervaバックアップ,mon
```

解説

- 水金はリモートワークなので、月火木は出勤が必要 (休日は不要なので`!`つき)
- 歯磨きは毎日
- 洗濯は2日に1回
- 爪切りは毎週
- Minervaのバックアップは毎週月曜 (休日かどうかは関係ないので`!`なし)