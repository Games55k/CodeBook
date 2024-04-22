# 常用STL函数

## 栈
```cpp
stack<T> stk;  初始化
stk.top();  返回栈顶
stk.push();  入栈
stk.pop();  出栈
stk.empty();  返回是否为空
stk.size();  返回元素数量
```

## 队列
```cpp
queue<T> q;  初始化
q.front();  返回队首
q.back();  返回队尾
q.push(T);  队尾入队
q.pop();  队首出队
q.empty();  返回是否为空
q.size();  返回元素数量
```

## 双端队列（deque)
```cpp
dq.front();  返回队首
dq.back();  返回队尾
dq.push_back(T);  队尾入队
dq.pop_back();  队尾出队
dq.push_front(T);  队首入队
dq.pop_front();  队首出队
dq.insert();  在指定位置前插入元素（传入迭代器和元素）
dq.erase();  删除指定位置的元素（传入迭代器）
dq.empty();  返回是否为空
dq.size();  返回元素数量
```
## 字符串
```cpp
str.find(ch, start = 0) 查找并返回从 start 开始的字符 ch 的位置
str.rfind(ch) 从末尾开始，查找并返回第一个找到的字符 ch 的位置（皆从 0 开始）（如果查找不到，返回 -1）
str.substr(start, len) 可以从字符串的 start（从 0 开始）截取一个长度为 len 的字符串（缺省 len 时代码截取到字符串末尾）。
str.append(s) 将 s 添加到字符串末尾。
str.append(s, pos, n) 将字符串 s 中，从 pos 开始的 n 个字符连接到当前字符串结尾。
str.replace(pos, n, s) 删除从 pos 开始的 n 个字符，然后在 pos 处插入串 s。
str.erase(pos, n) 删除从 pos 开始的 n 个字符。
str.insert(pos, s) 在 pos 位置插入字符串 s。
```


## 容器类

### 查找最大值

```cpp
long long max = *max_element(v.begin(), v.end());
long long max = std::ranges::max(v);  C++20
```

### 查找最小值

```cpp
long long min = *min_element(v.begin(), v.end());
long long min = std::ranges::min(v);  C++20
```

### 二分查找

```cpp
lower_bound(v.begin(), v.end(), target);  查找第一个大于等于target目标值的位置
upper_bound(v.begin(), v.end(), target); 查找第一个大于target目标值的位置
binary_search(v.begin(), v.end(), target); 查找target是否存在，找到返回true，否则返回false
```

### 找第k小的数

```cpp
nth_element(v.begin(), v.begin() + k, v.end());
```

### 求和

```cpp
long long sum = accumulate(v.begin(), v.end(), 0ll);
```

### 计数函数

```cpp

```

### 翻转字符串

```cpp
reverse(s.begin(), s.end());
std::ranges::reverse(s);  C++20
```
