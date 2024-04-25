# 算法

## 快速幂

```cpp

long long binpow(long long a, long long b, long long p) {
    long long res = 1;
    while (b) {
        if (b & 1) res = res * a % p;
        a = a * a % p;
        b >>= 1;
    }
    return res;
}

```

## 最大子段和

```cpp
long long ans = 0, max = 0;
for (int i = 0; i < n; i++) {
    int x;
    std::cin >> x;
    max = std::max(0ll, max + x);
    ans = std::max(ans, max);
}
```

## 最长公共子序列（LCS）( $O(nm)$ )

```cpp
for (int i = 1; i <= s1.size(); i++) {
    for (int j = 1; j <= s2.size(); j++) {
        if (s1[i] == s2[j]) {
            dp[i][j] = dp[i - 1][j - 1] + 1;
        } else {
            dp[i][j] = std::max(dp[i - 1][j], dp[i][j - 1]);
        }
    }
}
```
## 最短路

### Floyd最短路 (多源最短路)
时间复杂度( $O(n^3)$ )
```cpp
void Floyd() {
    for (int k = 1; k <= n; k++) {
        for (int i = 1; i <= n; i++) [
            for (int j = 1; j <= n; j++) {
                dp[i][j] = std::min(dp[i][j], dp[i][k] + dp[k][j]);
            }
        ]
    }
}

void solve() {
    memset(dp, 0x3f, sizeof(dp));
    while (m--) {
        int u, v, d;
        std::cin >> u >> v >> d;
        dp[u][v] = std::min(dp[u][v], d); 单向边
        dp[v][u] = std::min(dp[v][u], d); 双向边
    }
}
```

### Dijkstra最短路 (单源最短路)

堆优化版 ( $O(m\log m)$ )
```cpp
const int N = 2e5 + 10;
int n, m;
long long dp[N];
std::bitset<N> vis;
struct Edge {
    int v;
    long long w;
    bool operator < (const Edge &x) const {
        return w > x.w;
    }
}
std::vector<Edge> g[N];

void dijkstra(int st) {
    memset(dp, 0x3f, sizeof(long long) * (n + 1));
    dp[st] = 0;
    std::priority_queue<Edge> pq;
    pq.push({st, dp[st]});
    while (pq.size()) {
        int x = pq.top().v; pq.pop();
        if (vis[x]) continue;
        vis[x] = true;
        for (auto &[v, w] : g[x]) {
            if (!vis[v] && dp[x] + w < dp[v]) {
                dp[v] = dp[x] + w;
                pq.push({v, dp[v]});
            }
        }
    }
}


void solve() {
    std::cin >> n >> m;
    while (m--) {
        int u, v, w;
        std::cin >> u >> v >> w;
        g[u].push_back({v, w});
    }
    dijkstra(1);
}
```

## 最小生成树

### Prim算法（ $O((n+m)\log n)$ ）
思路：从一个点开始，每次不断加最小的点，从而确保每一个点到其它点都是最优

```cpp
const int N = 1e5 + 4;
long long d[N];

struct Edge {
    int v;
    long long w;
    bool operator < (const Edge &v) const {
        return w > v.w;
    }
};

std::vector<Edge> g[N];
std::bitset<N> itr;

void solve() {
    int n, m;
    std::cin >> n >> m;
    memset(d, 0x3f, sizeof(d));
    while (m--) {
        int u, v;
        long long w;
        std::cin >> u >> v >> w;
        g[u].push_back({v, w});
        g[v].push_back({u, w});
    }
    std::priority_queue<Edge> pq;
    long long ans = 0;
    pq.push({1, 0});
    while (pq.size()) {
        auto [x, w] = pq.top(); pq.pop();
        if (itr[x]) continue;
        itr[x] = true;
        ans += w;
        for (auto &[v, w] : g[x]) {
            if (!itr[v] && w < d[v]) {
                d[v] = w;
                pq.push({v, w});
            }
        }
    }
    bool ok = true;
    for (int i = 1; i <= n; i++) {
        if (！itr[i]) {
            ok = false;
            break;
        }
    }
    std::cout << (ok ? ans : -1) << "\n";
}
```