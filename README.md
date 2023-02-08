# JavaScript の基本

下記サンプルコードを使用して、JavaScriptの基本を解説します。

基本が終わった人は [course](./course/README.md) の教材を進めていきましょう。

# サンプルコード

```javascript
// 配列を回すだけの処理

const nums = [1, 2, 3]

let flag = false

function main (items) {
  for (let i = 0; i < items.length; i++) {
    console.log(items[i], flag)
    flag = true
  }
}

main(nums)
```

```
// 実行結果
1 false
2 true
3 true
```

# 解説

## <span style="color: red;">const</span>

```javascript
const nums = [1, 2, 3]
```

定数を宣言するものです。  
再代入による変更ができず、再宣言もできません。  
基本的にはこれを使って様々なものを宣言していきます。

しかし配列の場合、ちょっと癖があるので、下記の動きも知っておきましょう。

```javascript
// 配列
const a = [1, 2, 3]
a = [4, 5, 6] // TypeError: Assignment to constant variable.

const b = [1, 2, 3]
b.push(4) // [1, 2, 3, 4]

// 連想配列
const c = {'key': 'value'}
c = {'OTHER_KEY': 'value'} // TypeError: Assignment to constant variable.

const d = {'key': 'value'}
d.key = 'otherValue' // {'key': 'otherValue'}
d.otherKey = 'hoge' // {key: 'otherValue', otherKey: 'hoge'}
```

## <span style="color: red;">let</span>

```javascript
let flag = false
```

変数を宣言する時に使用します。  
任意で値を代入して初期化（破壊）できるので、可能な限り使いません。

## <span style="color: red;">{}</span>

{} を Curly bracket (カーリーブラケット) と言います。

```javascript
function main (items) {}

for (let i = 0; i < items.length; i++) {}

if (Math.random() > 0.5) {}
```

などでよく見かけますね。

カーリーブラケットで定義された `const` `let` はブロックスコープされ、外からは参照できません。

```javascript
if (Math.random() > 0.5) {
  const y = 5
}
console.log(y)  // ReferenceError: y is not defined
```

グローバルを汚さないためにもよく使うテクニックですので、覚えておきましょう。

## <span style="color: red;">function</span>

```javascript
function main (items) {}
```

関数定義といわれるものです。  
実行すれば中に書かれたロジックが動きます。

詳細は [course](./course/README.md) で解説します。