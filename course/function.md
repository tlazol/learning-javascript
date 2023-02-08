# 関数

JavaScript は関数を定義する方法がいくつかあります。  
主な関数の定義の方法も見てみましょう。

## <span style="color: red;">関数定義</span>

```javascript
function main () {
  console.log('hello')
}

main() // hello
```

基本の関数です。

関数定義の特徴としては、関数の巻き上げが可能です。  
つまりは下記のように関数の定義の前に実行分があっても動作します。

```javascript
main() // hello

function main () {
  console.log('hello')
}
```

巻き上げは JavaScript 特有の動きで、コードの難読化を引き起こす可能性が高いので、あまり使用しないようにしましょう。

## <span style="color: red;">匿名関数（無名関数）</span>

```javascript
const main = () => {
  console.log('hello')
}
main()
```

一番よく使うのはこの匿名関数です。  
JavaScript は変数に関数を格納できますので、名無しの関数を変数に格納する事で使用します。

## <span style="color: red;">即時関数</span>

```javascript
(() => {
  console.log('hello')
})()
// hello 
```

即時関数は、関数の呼び出しを行わずとも、即実行される関数です。  
あまり使われませんが `let` を使わないために使用されるケースが多いです。

`let` を使わざるを得ないシチュエーションを考えてみましょう。例えば下記のようなロジックです。

```javascript
// 本当はこう書きたいけどブロックスコープで出来ないから…
if (hoge !== fuga) {
  // do something
  const piyo = false
}
console.log(piyo)  // ReferenceError: piyo is not defined

// こう書くしかないが…
let piyo = true
if (hoge !== fuga) {
  // do something
  piyo = false
}

// 即時関数を使えばこう書ける
const piyo = (() => {
  if (hoge !== fuga) {
    // do something
    return false
  }
  return true
})()

// 処理が単一であれば、三項演算子でもよい
const piyo = hoge !== fuga ? false : true
```

このテクニックを覚えておくと `let` を使用する機会はぐっと減らせます。