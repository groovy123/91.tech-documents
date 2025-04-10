# Loggingについて


### ()の役割
() キーは、指定されたクラスをファクトリーとして使用することを logging システムに伝えます。これにより、カスタムクラスのインスタンスを生成してロギングコンポーネントとして使用できるようになります

```python
"formatters": {
    "logstash": {
        "()": "logstash_formatter.LogstashFormatter"
    }
}
```
この設定は Python のロギングフレームワークに対して、logstash_formatter モジュールから LogstashFormatter クラスをインポートし、そのクラスのインスタンスをフォーマッターとして使用するよう指示しています


### uvicornの例
```python 
"formatters": {
    "default": {
        "()": "uvicorn.logging.DefaultFormatter",
        "fmt": "%(levelprefix)s %(message)s",
        "use_colors": False,
    }
}
```
この設定では、uvicorn.logging.DefaultFormatter クラスをインスタンス化し、fmt と use_colors パラメータを渡します。


### dictConfigの基本構造
```python
dict_logging_settings = {
    'version': 1,  # 必須の設定
    'handlers': {
        'newStreamHandler': {
            'class': 'logging.StreamHandler',
            'formatter': 'newFormatter',
            'level': DEBUG
        }
    },
    'formatters': {
        'newFormatter': {
            'format': '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        }
    },
    'root': {
        'handlers': ['newStreamHandler'],
        'level': INFO
    },
    'loggers': {}
}
```


### yamlファイルから読み込み
```python
import logging.config
import yaml

with open('config.yaml', 'r') as f:
    config = yaml.safe_load(f.read())
    logging.config.dictConfig(config)
```


### uvicornのデフォルト
```python
import uvicorn

custom_logging_config = {
    "version": 1,
    "disable_existing_loggers": False,
    "formatters": {
        "default": {
            "()": "uvicorn.logging.DefaultFormatter",
            "fmt": "%(levelprefix)s %(message)s",
            "use_colors": False,
        },
        "access": {
            "()": "uvicorn.logging.AccessFormatter",
            "fmt": '%(levelprefix)s %(client_addr)s - "%(request_line)s" %(status_code)s',
        },
    },
    "handlers": {
        "default": {
            "class": "logging.StreamHandler",
            "formatter": "default",
            "level": "INFO",
        },
        # Additional handlers for file logging, etc.
    },
    "loggers": {
        "uvicorn": {"handlers": ["default"], "level": "INFO", "propagate": False},
        "uvicorn.error": {"handlers": ["default"], "level": "INFO", "propagate": False},
        "uvicorn.access": {"handlers": ["default"], "level": "INFO", "propagate": False},
    },
}

if __name__ == "__main__":
    uvicorn.run(
        "asgi:app",
        host="0.0.0.0",
        port=8000,
        log_config=custom_logging_config
    )
```


### ログ出力サンプル
```python
import logging

logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')

logger = logging.getLogger(__name__)

logger.info("This is an info message")
logger.warning("This is a warning message")
logger.error("This is an error message")

```