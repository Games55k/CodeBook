#数据结构

## 并查集

### 初始化
```cpp
for (int i = 1; i <= n; i++) {
    p[i] = i;
}
```

### 合并
```cpp
void merge() {
    p[find(x)] = find(y);
}
```

### 路径压缩
```cpp
int find(int n) {
    return p[n] = (p[n] == n ? n : find(p[n]));
}
```