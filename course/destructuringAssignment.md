# 分割代入

ES6 から使えるようになった構文です。  
配列から値を取り出したり、オブジェクトからプロパティを取り出して別個の変数に代入することを可能にする JavaScript の式です。

使えれば非常に便利ですので、ぜひ積極的に使っていきましょう。

```javascript
const [a, b, c] = [10, 20, 30]

console.log(a) // 10
console.log(b) // 20
console.log(c) // 30
```

```javascript
const { a, b } = { a: 10, b: 20, c: 30 }

console.log(a) // 10
console.log(b) // 20
```

```javascript
const main = () => {
  return  { a: 10, b: 20, c: 30 }
}
const { a, b } = main()

console.log(a) // 10
console.log(b) // 20
```

## スプレッド構文

分割代入でよく使うスプレッド構文というものも知っておきましょう。

スプレッド構文、期待された場所で展開する、見たほうが早い構文です。  
残りをすべて引き受けるマンだと思っておけば。

```javascript
const [a, b, ...c] = [10, 20, 30, 40, 50]

console.log(a) // 10
console.log(b) // 20
console.log(c) // [30, 40, 50]
```

```javascript
const { a, b, ...c } = { a: 10, b: 20, c: 30, d: 40, e: 50 }

console.log(a) // 10
console.log(b) // 20
console.log(c) // {c: 30, d: 40, e: 50}
```

```javascript
const obj = { a: 10,  b: 20, c: 30 }
const objClone = { ...obj }

console.log(objClone) // {a: 10, b: 20, c: 30}
```

```javascript
const main = () => {
  return  { a: 10, b: 20, c: 30, d: 40, e: 50 }
}
const { a, b, ...c } = main()

console.log(a) // 10
console.log(b) // 20
console.log(c) // {c: 30, d: 40, e: 50}
```

```javascript
const main = (a, b, ...c) => {
  console.log(a) // 10
  console.log(b) // 20
  console.log(c) // [30, 40, 50]
}

main(10, 20, 30, 40, 50)
```

## 残余構文

スプレッド構文が `いい感じの展開` だったのに対して、残余構文は `いい感じの濃縮` となります。  
引数に使えるスプレッド構文と考えておけばよいです。

```javascript
const main = (a, b, c, d, e) => {
  console.log(a) // 10
  console.log(b) // 20
  console.log(c) // 30
  console.log(d) // 40
  console.log(e) // 50
}

const args = [30, 40, 50]
main(10, 20, ...args)
```