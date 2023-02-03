# JavaScript の基本

下記サンプルコードを使用して、JavaScriptの基本を解説します。

基本が終わった人は course の教材を進めていきましょう。

# サンプルコード

```javascript
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

## const

```javascript
const nums = [1, 2, 3]
```

定数を宣言するものです。

再代入による変更ができず、再宣言もできません。

基本的にはこれを使って様々なものを宣言していきます。

## let 

```javascript
let flag = false
```

変数を宣言する時に使用します。

任意で値を代入して初期化（破壊）できるので、可能な限り使いません。

## function

```javascript
function main (items) {}
```

関数定義といわれるものです。

JavaScript は関数を定義する方法がいくつかありますが、関数の巻き上げができるのはこの関数定義だけになります。

主な関数の定義の方法も見てみましょう。

```javascript
// 関数定義
function main () {}
main() // 実行
```

```javascript
// 関数を変数に格納（ほぼ使わず）
const exeMain = function main () {}
exeMain() // 実行
```

```javascript
// 匿名関数（無名関数）
const main = () => {}
main()
```

```javascript
// 即時関数（関数呼び出しがなく、即実行されます）
(() => {})()
```

一番よく使うのは匿名関数です。

JavaScript は変数に関数を格納できますので、名無しの関数を変数に格納する事で使用します。

即時関数は、昔は await/async を書くためにたまに使用していましたが、今は `let` を使用しないで済むためによく使います。

`let` を使わざるを得ないシチュエーションを考えてみましょう。例えば下記のようなロジックです。

```javascript
let flag = true

if (hoge !== fuga) {
  // Do something
  flag = false
}
```

flag という bool 型変数が、直後のロジックにより true/false が切り替わるというよくあるコードですが、下記のように書き換える事ができます。

```javascript
const flag = (() => {
  if (hoge !== fuga) {
    // Do something
    return false
  }
  return true
})()
```

このテクニックを覚えておくと `let` を使用する機会はぐっと減らせます。