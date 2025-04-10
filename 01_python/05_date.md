# 日付関連

### 主要なクラス
- date: 年、月、日を表現するクラス
- time: 時、分、秒、マイクロ秒を表現するクラス
- datetime: 日付と時刻を組み合わせたクラス
- timedelta: 2つの日付や時刻の差を表現するクラス
- tzinfo: タイムゾーン処理のための基底クラス

### 基本
```python
import datetime
# または特定のクラスだけをインポート
from datetime import datetime

# 現在の日付と時刻
now = datetime.datetime.now()
print(now)  # 例: 2025-03-02 10:14:48.511139

# 現在の日付のみ
today = datetime.date.today()
print(today)  # 例: 2025-03-02

# 特定の日付を作成
my_date = datetime.date(2024, 6, 14)
print(my_date)  # 2024-06-14

# 特定の時刻を作成
my_time = datetime.time(17, 7, 45)
print(my_time)  # 17:07:45

# 日付と時刻を組み合わせたdatetimeオブジェクトを作成
my_datetime = datetime.datetime(2024, 6, 14, 17, 7, 45)
print(my_datetime)  # 2024-06-14 17:07:45
```

### 書式設定
```python
current_date = datetime.datetime.now()

# 例1: "月 日, 年 時:分 午前/午後"
formatted_date1 = current_date.strftime("%B %d, %Y %I:%M %p")
print(formatted_date1)  # 例: March 02, 2025 10:14 AM

# 例2: "日-月-年 時:分:秒"
formatted_date2 = current_date.strftime("%d-%m-%Y %H:%M:%S")
print(formatted_date2)  # 例: 02-03-2025 10:14:48

# 例3: "曜日, 月 日, 年"
formatted_date3 = current_date.strftime("%A, %B %d, %Y")
print(formatted_date3)  # 例: Sunday, March 02, 2025
```

|指定子|説明|例|
|--|--|--|
|%Y|4桁の年|2025|
|%m|月（01-12）|3|
|%d|日（01-31）|2|
|%H|24時間表記の時（00-23）|10|
|%I|12時間表記の時（01-12）|10|
|%M|分（00-59）|14|
|%S|秒（00-59）|48|
|%p|AM/PM|AM|
|%A|曜日の完全名|Sunday|
|%B|月の完全名|March|
|%a|曜日の短縮名|Sun|
|%b|月の短縮名|Mar|


### 文字列から日付への変換（strptime）
```python
from datetime import datetime

# 文字列から日付オブジェクトへの変換
date_string = "1 August, 2019"
date_object = datetime.strptime(date_string, "%d %B, %Y")
print("date_object:", date_object)  # 2019-08-01 00:00:00

# 別の形式の文字列
dt_string = "12/11/2018 09:15:32"
dt_object = datetime.strptime(dt_string, "%m/%d/%Y %H:%M:%S")
print("dt_object:", dt_object)  # 2018-12-11 09:15:32
```


### 日付の比較
```python
date1 = datetime.date(2022, 1, 1)
date2 = datetime.date(2023, 1, 1)
print(date1 < date2)  # True
```


### timedeltaによる日付計算
```python
from datetime import datetime, timedelta

# 現在の日時
now = datetime.now()

# 5日後
five_days_later = now + timedelta(days=5)
print(five_days_later)

# 2時間前
two_hours_ago = now - timedelta(hours=2)
print(two_hours_ago)
```

