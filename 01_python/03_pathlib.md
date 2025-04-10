# pathlibの使い方

### 基本
```python
from pathlib import Path

# 文字列からPathオブジェクトを作成
path = Path('/home/user/documents/file.txt')

# 現在のディレクトリ
current_dir = Path.cwd()

# ホームディレクトリ
home_dir = Path.home()

# パスの結合
new_path = Path('archive') / 'file.txt'

# パスの構成要素へのアクセス
path = Path('/home/user/documents/file.txt')

print(path.name)      # 'file.txt' - ファイル名
print(path.stem)      # 'file' - 拡張子なしのファイル名
print(path.suffix)    # '.txt' - ファイル拡張子
print(path.parent)    # '/home/user/documents' - 親ディレクトリ
print(path.anchor)    # '/' - パスの先頭部分
```

### ファイル関連
```python
# テキストファイルの書き込み
path = Path('example.txt')
path.write_text('Hello, Pathlib!')

# テキストファイルの読み込み
content = path.read_text()

# バイナリファイルの書き込み
path.write_bytes(b'Binary data')

# バイナリファイルの読み込み
binary_data = path.read_bytes()

# ファイルを開く
with Path('example.txt').open() as f:
    content = f.read()
```

### ディレクトリ関連
```python
# 単一のディレクトリを作成
Path('new_directory').mkdir()

# 親ディレクトリも含めて作成
Path('parent/child/grandchild').mkdir(parents=True)

# すでに存在する場合はエラーを無視
Path('existing_dir').mkdir(exist_ok=True)

# ディレクトリ内のすべてのファイルとディレクトリを取得
for item in Path('.').iterdir():
    print(item)

# 特定のパターンに一致するファイルを取得（現在のディレクトリのみ）
for py_file in Path('.').glob('*.py'):
    print(py_file)

# 再帰的に特定のパターンに一致するファイルを取得
for py_file in Path('.').rglob('*.py'):
    print(py_file)
```

### パスの検証関連
```python
# 存在確認
path.exists()

# ファイルかどうか
path.is_file()

# ディレクトリかどうか
path.is_dir()

# 絶対パスかどうか
path.is_absolute()

# シンボリックリンクかどうか
path.is_symlink()

# 絶対パスに変換
path.absolute()

# シンボリックリンクを解決
path.resolve()
```