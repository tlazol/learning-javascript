# ループと反復処理とパフォーマンス

JavaScript には様々なループ文がありますが、よく使う代表的なものの特徴を上げていきます。

## for
```
for (let step = 0; step < 5; step++) {
  // 値が 0 から 4 まで計 5 回実行される
  console.log('一歩西に歩く');
}
```

## for of
・列挙可能なオブジェクト（配列、NodeList、arguments等）を操作する。
・要素ではなく値が出力される

## for in
- 連想配列（オブジェクト）を操作する（配列を使ってはならない）
- 値ではなく要素を出力する。
- prototypeで拡張すると意図せず出力されてしまう。
```
function dump_props(obj, obj_name) {
  let result = '';
  for (let i in obj) {
    result += obj_name + '.' + i + ' = ' + obj[i] + '<br>';
  }
  result += '<hr>';
  return result;
}
```

