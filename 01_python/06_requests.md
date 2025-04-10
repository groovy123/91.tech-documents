# Requests

### GETリクエスト
```python
import requests

# GETリクエストの送信
response = requests.get('https://example.com')

# ステータスコードの確認
print(response.status_code)  # 200

# レスポンスヘッダーの確認
print(response.headers['content-type'])

# レスポンスの内容を取得
print(response.text)

# JSONレスポンスの場合
print(response.json())
```

### POSTリクエスト
```python
import requests

url = 'https://api.example.com/update_user'
data = {'user_id': 123, 'new_email': 'new@example.com'}

response = requests.post(url, json=data)
print(response.json())
```

### ページ取得
```python
import requests

url = 'https://example.com/product-page'
response = requests.get(url)

if response.status_code == 200:
    page_content = response.text
    # HTMLコンテンツから必要な情報を抽出する処理
    print("ページの読み込みに成功しました")
else:
    print("ページの読み込みに失敗しました")
```

