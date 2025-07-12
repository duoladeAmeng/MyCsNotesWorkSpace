# 描述

[https://leetcode.cn/problems/permutations-ii/](https://leetcode.cn/problems/permutations-ii/)

给定一个可包含重复数字的序列 `nums` ，**按任意顺序**返回所有不重复的全排列。

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

 

**提示：**

- `1 <= nums.length <= 8`
- `-10 <= nums[i] <= 10`

# 思路和代码

## 基本想法

容易得到这样的搜索过程

![image-20250710170216948](https://my--pic.oss-cn-beijing.aliyuncs.com/img/image-20250710170216948.png)

代码如下：

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int>path;
    bool st[10];
    vector<int> nums;
    void dfs(int u){
        if(u==nums.size()){
            ans.push_back(path);
            return;
        }
        for(int i=0;i<nums.size();i++){
            if(!st[i]){
                st[i]=true;
                path.push_back(nums[i]);
                dfs(u+1);
                st[i]=false;
                path.pop_back();
            }
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        this->nums=nums;
        dfs(0);
        return ans;
    }
};
```

但是对于有重复元素的情况，这版代码回产生重复，原因在于：

以`[1,1,2]`为例，有两个重复的1，如果在搜索树的**同一层**两次选择了这两个1，就会产生重复搜索。

为此，要去重，保证**同一层不重复选择值相同元素**。

## 排序去重

### 思路

🔧 关键步骤一：排序

```cpp
sort(nums.begin(), nums.end());
```

目的：

- 把**相同的数字**排在一起，便于后面**剪枝判断**；
- 剪枝逻辑依赖于**相邻相等**这一前提。



🔧 关键步骤二：剪枝条件

```cpp
if(i > 0 && st[i - 1] && nums[i] == nums[i - 1])
    continue;
```

这个条件是**去重的核心**，避免重复排列。

🚨 理解剪枝逻辑

📌 `nums[i] == nums[i-1]`：判断当前数字和前一个是否相等

说明这两个元素是**值相同的重复元素**。

📌 `st[i-1] == true`：前一个相同元素**已经被选中**

此时如果继续选当前的 `nums[i]`，就会生成与之前**重复结构**的排列。



![image-20250710172502860](https://my--pic.oss-cn-beijing.aliyuncs.com/img/image-20250710172502860.png)

### 代码

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int>path;
    bool st[10];
    vector<int> nums;
    void dfs(int u){
        if(u==nums.size()){
            ans.push_back(path);
            return;
        }
        for(int i=0;i<nums.size();i++){
            if(!st[i]){
                if(i>0&&st[i-1]&&nums[i]==nums[i-1])
                    continue;
                st[i]=true;
                path.push_back(nums[i]);
                dfs(u+1);
                st[i]=false;
                path.pop_back();
            }
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        this->nums=nums;
        dfs(0);
        return ans;
    }
};
```

## 布尔数组去重

### 思路

使用一个布尔数组 **`stcel` 数组** 来标记当前层是否使用过相同值，避免在同一层 DFS 中重复选择相同的数字

🧩 关键变量

```cpp
bool stcel[21] = {0};
```

- 用来记录当前 DFS 层（即树层）中，**本次排列尝试中是否已经使用过某个数值**。
- 数组大小是 `21` 是因为 `nums[i]` 的值域假设在 `[-10, 10]` 之间。
- 索引为 `nums[i] + 10`，用于避免负下标。

🔁 DFS 过程中的逻辑拆解

```cpp
for(int i = 0; i < nums.size(); i++) {
    if(!st[i] && !stcel[nums[i] + 10]) {
        st[i] = true;
        stcel[nums[i] + 10] = 1; // ✅ 本层第一次用 nums[i]，记录一下
        path.push_back(nums[i]);
        dfs(u + 1);
        path.pop_back();
        st[i] = false;
    }
}
```

✅ 去重发生在哪里？

```cpp
!stcel[nums[i] + 10]
```

- 保证当前 DFS 的“这一层”（也就是 `u` 这一层）**不会选两次相同值的数**；
- 即使这些相同的数值来自不同下标。

### 代码

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int>path;
    bool st[10];
    vector<int> nums;
    void dfs(int u){
        if(u==nums.size()){
            ans.push_back(path);
            return;
        }
        bool stcel[21]={0};
        for(int i=0;i<nums.size();i++){
            if(!st[i]&&!stcel[nums[i]+10]){
                st[i]=true;
                stcel[nums[i]+10]=1;
                path.push_back(nums[i]);
                dfs(u+1);
                st[i]=false;
                path.pop_back();
            }
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        this->nums=nums;
        dfs(0);
        return ans;
    }
};
```

