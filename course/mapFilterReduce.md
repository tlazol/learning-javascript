# map filter reduce について

まずは、よく見かけるあの図を。

```javascript
map([🌽, 🐮, 🐔], cook)
 => [🍿, 🍔, 🍳]

filter([🍿, 🍔], isVegetarian)
 =>  [🍿]

reduce([🍿, 🍳], eat)
 => 💩
```

上記がすべてを物語っていますが、各詳細を見てきましょう。

## map()

与えられた関数を、配列のすべての要素に対して呼び出し、その結果からなる新しい配列を生成します。  
要するに、配列から、特定のロジックを元に、新しい配列を生み出します。

```javascript
// 中身を2倍にするロジック
const arr = [1, 2, 3]

const double = (value) => {
  return value * 2
}

const newArr = arr.map(double)
// 処理が単一であるならば下記でも OK
// const newArr = arr.map(value => value * 2)

console.log(newArr) // [2, 4, 6]
```

## filter()

配列の中から、提供された関数で実装されたテストに合格した要素のみを抽出したシャローコピーを作成します。

```javascript
// 3の倍数だけ取り出すロジック
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]

const isMultipleOfThree  = (value) => {
  if (value % 3 === 0) {
    return true
  }
  return false
}

const newArr = arr.filter(isMultipleOfThree)
// 処理が単一であるならば下記でも OK
// const newArr = arr.filter(value => value % 3 === 0)
console.log(newArr) // [3, 6, 9]
```

ここで注意なのが、テストに合格するか否かの為には `filter` を使ってはいけないという事です。  
上記コードは言い換えれば「3の倍数があるかどうか」にも使えますが、その場合は `some()` を使用します。  
`some()` 配列の中の少なくとも 1 つの要素がテストに合格した場合 true を返します。  
ちなみに全部通ったら true を返す `every()` もありますので、ケースバイケースで使いこなしていきましょう。

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]

const isMultipleOfThree  = (value) => {
  if (value % 3 === 0) {
    return true
  }
  return false
}

const is = arr.some(isMultipleOfThree)
console.log(is) // true
```

## reduce()

`reduce` はややこしいですが `配列のすべての値を使用して新しい何かを作る場合に使う` と説明するのがわかりやすいかもしれません。

例えば「配列の中身を全部足す」というロジックも `reduce`ß の使い所です。

```javascript
// 配列の中身を全部足すロジック
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]

const init = 0
const sum = arr.reduce(
  (pre, cur) => pre + cur,
  init
)

console.log(sum) // 45
```

ややこしいですが、まずは登場人物紹介です。

### pre (previousValue)

この名前からしてややこしいですが「前の値」というよりも「これまでの結果」だと思いましょう。

### cur (currentValue)

現在の値です。

### init

初期値です。設定しなかった場合、元になる配列の1番目が初期値になります。

ちょっとわかりにくいので、もう少しわかりやすく書いてみましょう。  
下記を実行してコンソールログを見ると、理解しやすいかもしれません。

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]

const reducer = (pre, cur, index) => {
  const value = pre + cur
  console.log(`これまでの値: ${pre}`)
  console.log(`現在の値: ${cur}`)
  console.log(`index: ${index}`)
  console.log(`----------------`)
  return value
}

const sum = arr.reduce(reducer)

console.log(sum)
```

ちなみにパフォーマンスはまずまずです。

```javascript
const arr = Array.from(Array(10000000).keys())

console.time('test')
const sum = arr.reduce(
  (pre, cur) => pre + cur,
  0
)

console.log(sum)
console.timeEnd('test') // test: 111.257080078125 ms
```

## reduce() の使い所

`配列のすべての値を使用して新しい何かを作る場合に使う` という使用ケースですので、下記のような事もできます。

```javascript
// 多次元配列を1次配列に
const arr = [
  [0, 1],
  [2, 3],
  [4, 5],
]

const reducer = (pre, cur, index) => {
  const value = pre.concat(cur)
  console.log(`これまでの値: ${pre}`)
  console.log(`現在の値: ${cur}`)
  console.log(`index: ${index}`)
  console.log(`----------------`)
  return value
}

const concatArr = arr.reduce(reducer, [])
console.log(concatArr) // [0, 1, 2, 3, 4, 5]
```

```javascript
// 配列の中身をカウント
const arr = ['Sato', 'Suzuki', 'Takeda', 'Suzuki']

const reducer = (pre, cur, index) => {
  const count = pre[cur] ?? 0
  console.log(`これまでの値: ${pre}`)
  console.log(`現在の値: ${cur}`)
  console.log(`index: ${index}`)
  console.log(`----------------`)
  return {
    ...pre,
    [cur]: count + 1,
  }
}

const object = arr.reduce(reducer, {})
console.log(object) // {Sato: 1, Suzuki: 2, Takeda: 1}
```