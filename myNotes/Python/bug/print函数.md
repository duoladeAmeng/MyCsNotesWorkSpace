# 意外的回车、空格

## 🎯 问题背景

洛谷题目。

[https://www.luogu.com.cn/problem/P1706](https://www.luogu.com.cn/problem/P1706)

按照字典序输出自然数 $ 1 $ 到 $ n $ 所有不重复的排列，即 $ n $ 的全排列，要求所产生的任一数字序列中不允许出现重复的数字。

输入格式   一个整数 $ n $。$ 1 \leq n \leq 9 $。

输出格式

由 $ 1 \sim n $ 组成的所有不重复的数字序列，每行一个序列。

每个数字保留 $ 5 $ 个场宽。

样例输入 

```plain
3
```

样例输出 

```plain
    1    2    3
    1    3    2
    2    1    3
    2    3    1
    3    1    2
    3    2    1
```

## 🐞bug1:多余空行

### 错误代码

输入3

```python
n=int(input())
N=10
path=[]
st=[False for i in range(N)]
def dfs(depth):
    if depth==n:
        for elem in path:
            print("    ",elem,end="")
        print("\n")
        return
    for i in range(1,n+1):
        if not st[i]:
            st[i]=True
            path.append(i)
            dfs(depth+1)
            st[i]=False
            path.pop()
dfs(0)
```

输出：

```she
    1    2    3

    1    3    2

    2    1    3

    2    3    1

    3    1    2

    3    2    1

    1    2    3

    1    3    2

    2    1    3

    2    3    1

    3    1    2

    3    2    1
```

期望输出：

```shell
    1    2    3
    1    3    2
    2    1    3
    2    3    1
    3    1    2
    3    2    1
```

### 原因

这是因为`print`有默认回车，即`print(end="\n")`，而`print("\n")`相当于`print("\n",end="\n")`，相当于打了两个回车。

### 解决方案

```python
n=int(input())
N=10
path=[]
st=[False for i in range(N)]
def dfs(depth):
    if depth==n:
        for elem in path:
            print("    ",elem,end="")
        print()
        return
    for i in range(1,n+1):
        if not st[i]:
            st[i]=True
            path.append(i)
            dfs(depth+1)
            st[i]=False
            path.pop()
dfs(0)
```

```she
     1     2     3
     1     3     2
     2     1     3
     2     3     1
     3     1     2
     3     2     1
```

## 🐞bug2:数字间多了一个空格

### 错误代码

刚才修改后输出还是不对

期望输出

```shell
    1    2    3
    1    3    2
    2    1    3
    2    3    1
    3    1    2
    3    2    1
```

实际输出

```shell
     1     2     3
     1     3     2
     2     1     3
     2     3     1
     3     1     2
     3     2     1
```

数字之间多了一个空格

### 原因

**逐字符分析**这句代码：

```python
print("    ", elem, end="")
```

本以为它输出的只是 `4 个空格 + 数字`，但实际上它输出的是：

```
"    " + str(elem) + " "
```

即：✅ 实际行为：

- `"    "`：4 个空格（手动加的）
- `elem`：数字（`print` 会自动调用 `str(elem)`）
- `print` 中的多个参数之间，**自动会插入一个空格**（**这点很关键！**）
- `end=""` 只是防止 `print` 末尾换行，**不影响中间的自动空格**

🔍 举个例子：

假设：

```python
elem = 7
print("    ", elem, end="")
```

输出的其实是：

```
'    7 '
```

- 前面 4 个空格来自 `"    "`

- 数字 `7`

- 后面还有一个空格：是因为 `print("    ", elem)` 中间自动加的！

### 解决方案

```python
n=int(input())
N=10
path=[]
st=[False for i in range(N)]
def dfs(depth):
    if depth==n:
        for elem in path:
            print("    ",elem,end="",sep="")
        print()
        return
    for i in range(1,n+1):
        if not st[i]:
            st[i]=True
            path.append(i)
            dfs(depth+1)
            st[i]=False
            path.pop()
dfs(0)
```

这样才通过

## ✅更好的方式

**用格式化控制宽度**

```python
print(f"{elem:5d}", end="")
```

解释：

- `f"{elem:5d}"`：表示这个数字按十进制输出，**总宽度为5**，右对齐；
- `elem=1` → `'    1'`
- `elem=12` → `'   12'`
- `elem=123` → `'  123'`

这样无论是几位数字，打印出来都是**严格 5 个字符宽**，整体排列就整齐对齐了。

```python
n = int(input())
N = 10
path = []
st = [False for _ in range(N)]

def dfs(depth):
    if depth == n:
        for elem in path:
            print(f"{elem:5d}", end="")  # 每个数字宽度为5
        print()
        return
    for i in range(1, n + 1):
        if not st[i]:
            st[i] = True
            path.append(i)
            dfs(depth + 1)
            path.pop()
            st[i] = False

dfs(0)

```

## 🧠总结

| 问题类型      | 教训                                               |
| ------------- | -------------------------------------------------- |
| 多余换行      | `print("\n")` 会额外换行，应使用 `print()`         |
| print自动空格 | `print(a, b)` 默认以空格分隔，应使用 `sep=""` 控制 |