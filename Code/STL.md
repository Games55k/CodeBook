# 常用STL函数

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
