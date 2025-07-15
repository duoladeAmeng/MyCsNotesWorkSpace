# display属性的用法

## 作用

改变元素的类型

## 语法

```css
display: 取值 ;
```

# display属性的取值

## block

### block元素（块元素）的特点

- 独占一行，排斥其他元素跟其位于同一行，包括块元素和行内元素
- 块元素内部可以容纳其他块元素和行内元素
- 宽度默认是父元素的宽度，高度默认由内容撑开
- 可以定义 width，也可以定义 height
- 可以定义 4 个方向的 margin

### 常见块元素

|   块元素   |        说明        |
| :--------: | :----------------: |
|  `h1-h6`   |        标题        |
|    `p`     |        段落        |
|   `div`    |       `div`        |
|    `hr`    |       水平线       |
| `ol`、`ul` | 有序列表、无序列表 |

## inline

### inline 元素（行内元素）的特点

- 可以与其他行内元素位于同一行
- 行内元素内部可以容纳其他行内元素，但不可以容纳块元素，不然会出现无法预知的结果
- 宽度和高度默认由内容撑开
- 无法定义 height，也无法定义 width
- 可以定义 margin-left 和 margin-right，无法定义 margin-top 和 margin-bottom

### 常见inline 元素

| 行内元素 |  说明  |
| :------: | :----: |
|   `a`    | 超链接 |
|  `span`  | `span` |

## inline-block

### inline-block 元素（行内块元素）的特点

- 可以定义 width 和 height

- 可以与其他行内元素位于同一行

也就是说，inline-block 元素同时具备了 block 元素和 inline 元素的特点

### 常见行内块元素

| 行内块元素 |  说明  |
| :--------: | :----: |
|   `img`    |  图片  |
|  `input`   | 输入框 |
| `textarea` |        |
|  `button`  |        |
|  `select`  |        |

### 默认间距问题

#### 代码

```html
<!DOCTYPE html> 
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <style type="text/css">
        span
        {
            display:inline-block;
            width:60px;
            height:100px;
            background-color:pink;
            text-align: center;
            line-height:80px;
            font-size: 70px;
            color: blue;
        }
    </style>
</head>
<body>
    <span>A</span>
    <span>B</span>
    <span>C</span>
</body>
</html>

```

#### 效果

<iframe src="./examples/行内块元素默认间距问题.html"></iframe>

inline-block 元素之间有一定的间距。在实际开发中，这种间距有时会对布局产生影响。大多数时候为了不影响布局，需要去除 inline-block 元素的间距。

#### 去除间距方法

为父元素定义一个`font-size:0;`来去除 `inline-block` 元素的间距

```html
<!DOCTYPE html> 
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <style type="text/css">
        div{
            font-size: 0;
        }
        span
        {
            display:inline-block;
            width:60px;
            height:100px;
            background-color:pink;
            text-align: center;
            line-height:80px;
            font-size: 70px;
            color: blue;
        }
    </style>
</head>
<body>
    <div>
    <span>A</span>
    <span>B</span>
    <span>C</span>
    </div>
</body>
</html>

```

<iframe src="./examples/行内块元素默认间距问题解决.html"></iframe>

### 案例1

在实际开发中，可能经常需要为`span`、`a` 等行内元素定义一定的 `width` 和` height`，此时 就应该考虑使用 `display:inline-block; `来实现

#### 代码

```html
<!DOCTYPE html> 
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <style type="text/css">
        a
        {
            /*去除默认样式*/
            text-decoration:none;
            /*转换为inline-block元素*/
            display: inline-block;
            width:100px;
            height:36px;
            line-height:38px;
            text-align:center;
            border:1px solid #DADADA;
            border-radius:5px;
            font-family: "微软雅黑";
            cursor:pointer;
            cursor:pointer;
            background: linear-gradient(to bottom,#F8F8F8,#DCDCDC);  /*使用CSS3渐变*/
        }
        a:hover
        {
            color:white;
            background:linear-gradient(to bottom,#FFC559,#FFAF19);   /*使用CSS3渐变*/
        }
    </style>
</head>
<body>
    <a href="http://www.baidu.com" >百度</a>
</body>
</html>

```

#### 效果

<iframe src="./examples/行内块元素1.html"></iframe>

## none

可以使用 `display:none` 来隐藏一个元素

# 元素类型显示转换的情况

## 改display属性

- inline
- block
- inline-block
- ......

## 改为absolute定位

- 改成absolute定位
  - 会改变标签的显示模式特点：具备了行内块的特点（在一行共存，宽高生效）

## 浮动

- 改成float

  - 浮动元素有特殊的显示效果

    - 拥有了行内块元素的性质

      - 一行可以显示多个

      - 可以设置宽高

# 总结

| 属性值       | 说明                                 |
| ------------ | ------------------------------------ |
| inline       | 行内元素                             |
| block        | 块元素                               |
| inline-block | 行内块元素                           |
| table        | 以表格形式显示，类似于 table 元素    |
| table-row    | 以表格行形式显示，类似于 tr 元素     |
| table-cell   | 以表格单元格形式显示，类似于 td 元素 |
| none         | 隐藏元素                             |
