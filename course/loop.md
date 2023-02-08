# ループ処理

JavaScript には様々なループ文がありますが、よく使う代表的なものの特徴を、下記課題を例にして挙げていきます。

```javascript
// 下記配列の中身を全部足した合計数を出すロジックを組む

const arr = Array.from(Array(10000000).keys()) // [0, 1, 2, ...9999999] という 0 から 9999999 の 1000 万個の整数が入った配列
```

## for

一番ベーシックであるループ処理です。

後述のものより少し長い書き方ですが、単純なループ処理なのでパフォーマンスという面では一番です。

```javascript
const arr = Array.from(Array(10000000).keys())

console.time('test')
let a = 0

for (let i = 0; i < 10000000; i++) {
  a += arr[i]
}

console.log(a)
console.timeEnd('test') // test: 83.834228515625 ms
```

## for of
String, Array, Map, Set などなど、反復可能オブジェクトに対して、反復的な処理をするループを作成します。  
for 文より簡潔に書けますので、主に使うのはこちらになります。

```javascript
const arr = Array.from(Array(10000000).keys()) // [0, 1, 2, ...999999]

console.time('test')
let a = 0

for (const item of arr) {
  a += item
}

console.log(a)
console.timeEnd('test') // test: 178.043212890625 ms
```

### String の場合

```javascript
const string = 'abc'

for (const item of string) {
  console.log(item)
}
// a
// b
// c
```

なお、連想配列は、そのままでは `for of` では回せません。

```javascript
const object = { a: 1, b: 2, c: 3 }

for (const item of object) {
  console.log(item)
}
// TypeError: object is not iterable
```

そのため、連想配列を回す場合 `Object.entries` を使うのが一般的になります。

```javascript
const object = { a: 1, b: 2, c: 3 }

console.log(Object.entries(object))
// [
//   ['a', 1], ['b', 2], ['c', 3]
// ]

for (const [hoge, fuga] of Object.entries(object)) {
  console.log(`${hoge}: ${fuga}`)
  // a: 1
  // b: 2
  // c: 3
}
```

## for in
`for in` はオブジェクトのプロパティを反復するために作られたものであり、配列での使用は推奨されておりません。  
公式ドキュメントにも `最も具体的な使い方はデバッグ目的であるかもしれません。` とありますので、積極的に使うものではないと認識しておきましょう。

```javascript
const object = { a: 1, b: 2, c: 3 }

for (const property in object) {
  console.log(`${property}: ${object[property]}`)
}

// a: 1
// b: 2
// c: 3
```

## forEach()

与えられた関数を、配列の各要素に対して一度ずつ実行するメソッドです。

`for` や `for of` と違い `break` などでループを止めることは出来ません。

```javascript
const arr = Array.from(Array(10000000).keys())

console.time('test')
let a = 0

arr.forEach(value => {
  a += value
})

console.log(a)
console.timeEnd('test') // test: 159.30712890625 ms
```