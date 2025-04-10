# FastAPI


## FastAPIプロジェクト作成
```bash
uv init backend -p 3.13.1
uv add "fastapi[standard]"
```

## 必要ディレクトリ作成
```bash
mkdir -p app/routers
mkdir -p app/internal
touch app/__init__.py
touch app/routers/__init__.py
touch app/internal/__init__.py
touch app/main.py
```


## ディレクトリ構成
.
├── app
│   ├── __init__.py
│   ├── main.py
│   ├── dependencies.py
│   └── routers
│   │   ├── __init__.py
│   │   ├── items.py
│   │   └── users.py
│   └── internal
│       ├── __init__.py
│       └── admin.py
├── tests
│   ├── test_main.py


## ユニットテスト追加
```bash
uv add pytest
python -m pytest
```

- test_main.py
    ```python
    from fastapi.testclient import TestClient

    from router_app.main import app

    client = TestClient(app)

    def test_read_main():
        response = client.get("/")
        assert response.status_code == 422
        assert response.json() == {"msg": "Hello World"}
    ```

## デバッグ方法
- uviconrnをmainで実行してデバッグする
  ```python
  import uvicorn

  if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
  ```

## Routerの実装例
- main.py
  ```python
    from fastapi import FastAPI

    from .routers import item

    app = FastAPI()

    # routerのinclude
    app.include_router(item.router)

    # ...
  ```


- item.py
  ```python
    from fastapi import APIRouter

    router = APIRouter(
        prefix="/item",
        tags=["item"],
    )

    @router.get("/list")
    async def list():
        pass

  ```
