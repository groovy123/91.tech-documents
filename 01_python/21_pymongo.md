# PyMongo

### 基本CRUD
```python
from datetime import datetime

from pydantic import BaseModel
from pymongo import MongoClient

class Content(BaseModel):
    _id: str | None
    category: str
    text: str
    created_at: datetime
    update_at: datetime
    update_no: int

def get_client():
    url = "mongodb://localhost:27017"
    client = MongoClient(url)

    try:
        database = client.get_database("ContentStore")
        return (client, database.get_collection("Contents"))
    except Exception as e:
        raise Exception("error: ", e)

def get_content():
    client, collection = get_client()
    with client as c:
        query = {"_id": "1"}
        return collection.find_one(query)

def create_content():
    client, collection = get_client()
    with client as c:
        content = Content(category="1", text=text, created_at=datetime.now(), update_at=datetime.now(), update_no=1)
        collection.insert_one(content.model_dump())

```