# List/Map系のはなし

### 配列のループ処理
#### 1. 基本的なループ処理
- for...ofループ
- forループ
- for...inループ　※注意が必要

#### 2. 配列メソッドを使った処理
- forEarch
  ```javascript
    arr.forEach((e, i) => {
      console.log(i, e);
    });
  ```

- map
  ```javascript
    const result = arr.map(item => item.toUpperCase());
  ```

- filter
  ```javascript
    const filtered = arr.filter(item => item !== 'b');
  ```

- find / findLast
  ```javascript
    const item = arr.find(item => item === 'b');
  ```

- reduce / reduceRight
  ```javascript
    const sum = [1, 2, 3].reduce((acc, curr) => acc + curr, 0);
  ```

#### 3. 配列操作の応用
- splice
  指定した位置の要素を削除・追加・置換する
  ```javascript
    arr.splice(1, 1); // インデックス1の要素を1つ削除
  ```

- push / pop / shift / unshift
- sort

#### 4. その他の便利なやつ
- Object.entries() / Array.prototype.entries()
  インデックスと要素のペアを取得してループ
  ```javascript
  for (const [i, e] of Object.entries(arr)) {
    console.log(i, e);
  }  
  ```

- Array.drom()
  配列ライクなオブジェクト（NodeListなど）を配列に変換する
  ```javascript
  const lists = Array.from(document.querySelectorAll('li'));
  lists.forEach(list => console.log(list.textContent));
  ```


### Objectのループ
#### 1. 基本
- for...in文
  - オブジェクトの列挙可能なプロパティ（キー）を順番に取得
  - ただし、プロトタイプチェーン上のプロパティも列挙されるため、hasOwnPropertyで自前のプロパティかチェックするのが安全
  ```javascript
  const obj = { a: 1, b: 2, c: 3 };
  for (const prop in obj) {
    if (Object.prototype.hasOwnProperty.call(obj, prop)) {
      console.log(prop, obj[prop]); // a 1, b 2, c 3
    }
  }  
  ```

- Object.keys()
  - オブジェクトのキー（プロパティ名）だけを配列として取得し、for...ofや配列メソッドでループできます
  ```javascript
  const keys = Object.keys(obj);
  for (const key of keys) {
    console.log(key, obj[key]);
  }
  // または
  Object.keys(obj).forEach(key => console.log(key, obj[key]));
  ```

- Object.values()
  - オブジェクトの値だけを配列として取得
- Object.entries()
  - オブジェクトのキーと値のペアを配列で取得
  ```javascript
  for (const [key, value] of Object.entries(obj)) {
    console.log(key, value);
  }
  ```


### Mapのループ
#### 1. 基本
- forEeachメソッド
  ```javascript
  const myMap = new Map([
    ['apple', 150],
    ['orange', 100],
    ['banana', 120]
  ]);
  myMap.forEach((value, key) => {
    console.log(key, value);
  });
  // apple 150
  // orange 100
  // banana 120
  ```

- for...of文とentries()
  ```javascript
  for (const [key, value] of myMap.entries()) {
    console.log(key, value);
  }
  ```

- keys()やvalues()でキーまたは値だけループ
  


### listからobjectへの変換
#### 1. reduce()を使う方法
```javascript
const obj = array1.reduce((acc, value, index) => {
  acc['key' + index] = value;
  return acc;
}, {});
```

#### 2. Object.fromEntries()を使う方法(ES2019以降)
```javascript
const array = [['a', 1], ['b', 2], ['c', 3]];
const obj = Object.fromEntries(array);
console.log(obj);
// { a: 1, b: 2, c: 3 }
```

#### 3. Object.assign()を使う方法
```javascript
const items = [
  { key: 'a', value: 1 },
  { key: 'b', value: 2 },
  { key: 'c', value: 3 }
];
const obj = Object.assign({}, ...items.map(item => ({ [item.key]: item.value })));
console.log(obj);
// { a: 1, b: 2, c: 3 }
```



### objectからMapに変換
#### 1. Object.entries()とMapコンストラクタを使う方法
```javascript
const obj = { a: 1, b: 2, c: 3 };
const map = new Map(Object.entries(obj));
console.log(map); // Map { 'a' => 1, 'b' => 2, 'c' => 3 }
```

#### 2. Object.keys()とmapメソッドを使う方法
```javascript
const obj = { a: 1, b: 2, c: 3 };
const map = new Map(Object.keys(obj).map(key => [key, obj[key]]));
console.log(map); // Map { 'a' => 1, 'b' => 2, 'c' => 3 }
```

#### 3. for...ofループで追加する方法
```javascript
const obj = { a: 1, b: 2, c: 3 };
const map = new Map();
for (const [key, value] of Object.entries(obj)) {
  map.set(key, value);
}
console.log(map); // Map { 'a' => 1, 'b' => 2, 'c' => 3 }
```

