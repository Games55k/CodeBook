#数据结构

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