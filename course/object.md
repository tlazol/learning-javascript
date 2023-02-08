# オブジェクト操作

JavaScript のほぼすべてのオブジェクトが Object のインスタンスです。  
そんな Object の操作をする主なメソッドを紹介します。

ぱっと見、何に使うのかわからないメソッドかもしれませんが、いつか必ず使いたいと思うメソッドです。

## Object.entries

連想配列を [key, value] からなる配列にして返すメソッドです。

```javascript
const object = { a: 1, b: 2, c: 3 }
console.log(Object.entries(object))
// [
//   ['a', 1], ['b', 2], ['c', 3]
// ]
```

## Object.keys

連想配列の key を配列にして返すメソッドです。

```javascript
const object = { a: 1, b: 2, c: 3 }
console.log(Object.keys(object)) // ['a', 'b', 'c']
```

## Object.values

連想配列の value を配列にして返すメソッドです。

```javascript
const object = { a: 1, b: 2, c: 3 }
console.log(Object.values(object)) // [1, 2, 3]
```

## Object.assign

コピー元オブジェクトからコピー先オブジェクトにコピーするためのメソッドです。たまに使います。

```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// Expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget === target);
// Expected output: true
```
