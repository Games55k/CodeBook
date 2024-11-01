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

堆优化版 ( $O(m\log m)$ ) 带路径
```cpp
#include <bits/stdc++.h>

using i64 = long long;

struct Edge{
    int v;
    i64 w;
    bool operator < (const Edge &x) const {
        return w > x.w;
    };
};

void solve() {
    int n, m;
    std::cin >> n >> m;
    std::vector<std::vector<Edge>> g(n + 1);
    while (m--) {
        int u, v;
        i64 w;
        std::cin >> u >> v >> w;
        g[u].push_back({v, w});
        g[v].push_back({u, w});
    }
    std::vector<i64> dis(n + 1, LLONG_MAX);
    std::vector<bool> vis(n + 1);
    std::vector<int> pre(n + 1, -1);
    auto dijkstra = [&](int st) {
        dis[st] = 0;
        std::priority_queue<Edge> pq;
        pq.push({st, dis[st]});
        while (!pq.empty()) {
            int x = pq.top().v; pq.pop();
            if (vis[x]) continue;
            vis[x] = true;
            for (auto &[v, w] : g[x]) {
                if (!vis[v] && dis[x] + w < dis[v]) {
                    pre[v] = x;
                    dis[v] = dis[x] + w;
                    pq.push({v , dis[v]});
                }
            }
        }
    };
    dijkstra(1);
    if (dis[n] != LLONG_MAX) {
        std::vector<int> ans;
        int idx = n;
        while (pre[idx] != 1) {
            ans.push_back(idx);
            idx = pre[idx];
        }
        ans.push_back(idx);
        ans.push_back(1);
        std::ranges::reverse(ans);
        for (auto &i : ans) {
            std::cout << i << " \n"[&i == &ans.back()];
        }
        std::cout << dis[n] << "\n";
    } else {
        std::cout << -1 << "\n";
    }
}

int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    int t = 1;
    // std::cin >> t;
    while (t--) {
        solve();
    }
    return 0;
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
        if (!itr[i]) {
            ok = false;
            break;
        }
    }
    std::cout << (ok ? ans : -1) << "\n";
}
```

## 马拉车

### 思路

1. 找到一个中心，向两边扩展，直到遇到相同的字符
2. 计算出以该中心为中心的回文串长度
3. 计算出以该中心为中心，两边扩展的回文串长度
4. 更新最大回文串长度

### 实现

```cpp
    int n;
    std::cin >> n;
    std::vector<int> p(2 * n + 3);
    char s[2 * n + 3];
    std::cin >> s + 1;
    for (int i = 2 * n + 1; i >= 1; i--) {
        i & 1 ? s[i] = '#' : s[i] = s[i >> 1];
    }
    s[0] = '$', s[2 * n + 2] = '@';
    int C = 0, R = 0, ans = 0;
    for (int i = 1; i <= 2 * n + 1; i++) {
        p[i] = i < R ? std::min(p[2 * C - i], R - i) : 1;
        while (s[i + p[i]] == s[i - p[i]]) p[i]++;
        if (i + p[i] > R) C = i, R = i + p[i];
        ans = std::max(ans, p[i] - 1);
    }
    std::cout << ans << "\n";
```