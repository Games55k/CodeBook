# 数论

## 最大公因数

```cpp

long long gcd(long long a, long long b) {
    return b == 0 ? a : gcd(b, a % b);
}

```

## 最小公倍数

```cpp

long long lcm(long long a, long long b) {
    return a / gcd(a, b) * b;
}

```