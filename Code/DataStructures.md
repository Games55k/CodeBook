#数据结构

## 并查集

### 合并
```cpp
void merge() { p[find(x)] = find(y); }
```
#### 启发式合并

### 路径压缩
```cpp
int find(int n) { return p[n] = (p[n] == n ? n : find(p[n])); }
```

## 01Trie

### 建树
```cpp
constexpr int N = 1 << 25;
int trie[N][2], cnt[N];
int tot = 0;

void insert(int x) {
    int cur = 0;
    for (int i = 30; i >= 0; i--) {
        int v = (x >> i) & 1;
        if (trie[cur][v] == -1) {
            trie[cur][v] = ++tot;
        }
        cur = trie[cur][v];
        cnt[cur]++;
    }
}
```