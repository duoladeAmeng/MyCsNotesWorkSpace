# display属性的用法

## 作用

改变元素的类型

## 语法

```css
display: 取值 ;
```

# display属性的取值

| 属性值       | 说明                                 |
| ------------ | ------------------------------------ |
| inline       | 行内元素                             |
| block        | 块元素                               |
| inline-block | 行内块元素                           |
| table        | 以表格形式显示，类似于 table 元素    |
| table-row    | 以表格行形式显示，类似于 tr 元素     |
| table-cell   | 以表格单元格形式显示，类似于 td 元素 |
| none         | 隐藏元素                             |

# block、inline和inline-block

## block元素（块元素）的特点

- 独占一行，排斥其他元素跟其位于同一行，包括块元素和行内元素
- 块元素内部可以容纳其他块元素和行内元素
- 可以定义 width，也可以定义 height
- 可以定义 4 个方向的 margin

## inline 元素（行内元素）的特点

- 可以与其他行内元素位于同一行
- 行内元素内部可以容纳其他行内元素，但不可以容纳块元素，不然会出现无法预知的结果
- 无法定义 height，也无法定义 width
- 可以定义 margin-left 和 margin-right，无法定义 margin-top 和 margin-bottom

## inline-block 元素（行内块元素）的特点

- 可以定义 width 和 height

- 可以与其他行内元素位于同一行

也就是说，inline-block 元素同时具备了 block 元素和 inline 元素的特点

# 常见元素的类型

|      类型      |       元素       |
| :------------: | :--------------: |
|    `block`     |                  |
|    `inline`    |                  |
| `inline-block` | `img`<br>`input` |

# display:none

## 作用

