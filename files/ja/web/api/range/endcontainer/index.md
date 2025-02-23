---
title: Range.endContainer
slug: Web/API/Range/endContainer
---
{{ApiRef("DOM")}}

**`Range.endContainer`** は読み取り専用プロパティで、 {{domxref("Range")}} の終了位置にあるノード ({{domxref("Node")}}) を返します。ノードの終了位置を変更するために {{domxref("Range.setEnd()")}} または同様のメソッドを利用します。

## 値

{{domxref("Node")}} オブジェクト。

## 例

```js
const range = document.createRange();

range.setStart(startNode,startOffset);
range.setEnd(endNode,endOffset);
endRangeNode = range.endContainer;
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [DOM インターフェイス索引](/ja/docs/Web/API/Document_Object_Model)
