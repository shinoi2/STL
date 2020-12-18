# C++ STL快速入门

## 简介
Standard Template Library（标准模板库）——简称STL，提供了一系列内置的算法和容器，可以提高编写代码的效率。NOI 系列比赛自 2011 年起允许 C++ 选手使用 STL，所以我们应该利用好 STL，发挥 C++ 语言的优势。


## 容器
![oi-wiki](https://oi-wiki.org/lang/csl/images/container1.png)

### Pair 对
* 用于存储一个树值对
* 减少写struct的代码量
* 默认的比较方式是先比较第一个元素，再比较第二个元素
* 准确的说`pair`不算容器

    ```cpp
    pair<int, int> p; // 定义
    p.first; // 第一个元素
    p.second; // 第二个元素
    make_pair(1, 1); // 构造一个 pair
    ```

### String 字符串
* ~~你们肯定都会用了~~

### Array 树组
* 需要 C++11, CSP / NOIP 不能用
* 效果不大, 直接用树组代替即可
* ~~这个不用学~~

    ```cpp
    // 1. 创建空array，长度为3; 常数复杂度
    std::array<int, 3> v0;
    // 2. 用指定常数创建array; 常数复杂度
    std::array<int, 3> v1{1, 2, 3};
    v0.fill(1);  // 填充数组
    // 访问数组
    for (int i = 0; i != arr.size(); ++i) cout << arr[i] << " ";
    ```

### Vector 可变长树组
* 头文件 `#include <vector>`  
~~`#include <bits/stdc++.h>`~~
* 定义vector

    ```cpp
    vector<int> v1;
    // 定义一个空的vector

    vector<int> v2(n);
    // 定义一个长度为n的vector

    vector<int> v3(n, 1);
    // 长度为n且全部为1的 vector
    ```
* 使用vector

    ```cpp
    v.push_back(100);
    // 在尾部添加一个元素

    v.pop_back();
    // 删除尾部的一个元素

    v.size();
    // 获取树组的长度

    v.empty();
    // 判断树组是否为空

    v.insert(v.begin() + 1, 100);
    // 在指定位置插入一个元素 时间复杂度 o(n)

    v.erase(v.begin() + 1);
    // 删除指定位置的元素
    ```

* Sample Code

    ```cpp
    vector<int> v;
    // v.size() = 0

    v.push_back(23333);
    // v.size() = 1, v = { 23333 }

    v.insert(v.begin() + 0, 890);
    // v.size() = 2, v = { 890, 23333 }

    v.insert(v.begin() + 1, 12345);
    // v.size() = 3, v = { 890, 12345, 23333 }

    v.erase(v.begin() + 0);
    // v.size() = 2, v = { 12345, 23333 }

    for (int i = 0; i < v.size(); i++) {
        printf("%d\n", v[i]);
    }
    // 依次输出 12345、23333

    v.pop_back();
    // v.size() = 1, v = { 12345 }
    ```

### Deque 双向队列
* 头文件 `#include <deque>`  
~~`#include <bits/stdc++.h>`~~
* 定义 deque 和 vector 相同
* 使用 deque  
  - 和 vector 相比多了 `push_front` 和 `pop_front`

    ```cpp
    deque<int> d;
    d.push_front(10);
    d.pop_front();
    ```

### Stack 栈
* 头文件 `#include <stack>`  
~~`#include <bits/stdc++.h>`~~
* 定义 stack 和 vector 相同
* 使用 stack

    ```cpp
    stack<int> s;
    s.push(x); // 向栈中插入元素 x
    s.top(); // 访问栈顶元素（如果栈为空，此处会出错）
    s.pop(); // 删除栈顶元素
    s.size(); // 查询容器中的元素数量
    s.empty(); // 询问容器是否为空
    ```

* 其他注意事项
    - 无法使用 `[]` 访问任意位置的数据
    - 如果想要使用 `[]`, 可以用树组很方便的模拟栈
    - `stack` 的底层实现默认是 `deque`
### Queue 队列
* 头文件 `#include <queue>`  
~~`#include <bits/stdc++.h>`~~
* 使用 queue

    ```cpp
    queue<int> q;
    q.push(x); // 向队列中插入元素 x
    q.front(); // 访问队首元素（如果队列为空，此处会出错）
    q.pop(); // 删除队首元素
    q.size(); // 查询容器中的元素数量
    q.empty(); // 询问容器是否为空
    ```

* 其他注意事项
    - 无法使用 `[]` 访问任意位置的数据
    - 如果想要使用 `[]`, 可以用`deque`模拟, 不推荐用树组手写
    - `queue` 的底层实现默认也是 `deque`

### priority_queue 优先队列/堆
* 头文件 `#include <queue>`  
~~`#include <bits/stdc++.h>`~~
* 默认是大根堆，即`top()`永远为最大的元素
* 我们可以利用 `greater<T>`（若支持）或者自定义比较函数实现小根堆

    ```cpp
    std::priority_queue<int> q2; // 大根堆
    std::priority_queue<int, vector<int>, greater<int> > q2; // 小根堆
    std::priority_queue<int, vector<int>, cmp > q2; // 小根堆
    ```
* 插入和删除的时间复杂度均为`o(logn)`

### List 双向链表
* 头文件 `#include <list>`  
~~`#include <bits/stdc++.h>`~~
* 使用 list
    - front() 返回首元素的引用
    - back() 返回末尾元素的引用
    - 如果要遍历必须使用迭代器

    ```cpp
    list<int> l;
    for (int i=1; i<=10; i++) {
        l.push_back(i);
    }
    for (list<int>::iterator it=l.begin(); it!=l.end(); ++it) {
        printf("%d ", *it);
    }
    return 0;
    ```

* 其他注意事项
    - 无法使用 `[]` 访问任意位置的数据
    - list 的删除和插入的时间复杂度是 o(1)

### forward_list 单向链表
* 需要 C++11, CSP / NOIP 不能用
* 减少了空间开销，但是迭代器只有单向的
* ~~这个不用学~~

### Set 集合
* 数学中的定义 set 中不会出现值相同的元素
* 头文件 `#include <set>`  
~~`#include <bits/stdc++.h>`~~
* 定义和使用

    ```cpp
    set<int> s;
    s.insert(x); // 当容器中没有等价元素的时候，将元素 x 插入到 set 中
    s.erase(x); // 删除值为 x 的元素, 并返回
    s.clear(); // 清空 set
    s.count(x); // 返回 set 内键为 x 的元素数量。
    s.find(x); // 在 set 内存在键为 x 的元素时会返回该元素的迭代器，否则返回 end() 。
    s.lower_bound(x); // 返回指向首个不小于给定键的元素的迭代器。如果不存在这样的元素，返回 end() 。
    s.upper_bound(x); // 返回指向首个大于给定键的元素的迭代器。如果不存在这样的元素，返回 end() 。
    s.empty(); // 返回容器是否为空。
    s.size(); // 返回容器内元素个数。
    ```
* 其他注意事项
    - `insert` 函数的返回值类型为 `pair<iterator, bool>` ，其中 `iterator` 是一个指向所插入元素（或者是指向等于所插入值的原本就在容器中的元素）的迭代器，而 `bool` 则代表元素是否插入成功，由于 `set` 中的元素具有唯一性质，所以如果在 `set` 中已有等值元素，则插入会失败，返回 `false`，否则插入成功，返回 `true`
    - `erase` 函数的返回值类型为 `size_t`, 无符号整数，表示删除元素的数量，所以如果在 `set` 中存在该元素，删除成功，返回 1，否则删除失败，返回 0。
    - set中自带的 `lower_bound` 和 `upper_bound` 时间复杂度为 `o(logn)`。如果使用 `std::lower_bound(s.begin(), s.end(), value)`的时间复杂度则会退化到 `o(n)`
    - set的底层实现是红黑树，所以绝大多数的操作时间负责度均为`o(logn)`

### Map 映射
* 头文件 `#include <map>`  
~~`#include <bits/stdc++.h>`~~
* 定义和使用

    ```cpp
    map<string, int> mp;
    // 插入
    mp["Alan"]=100; // 可以直接通过下标访问来进行查询或插入操作
    mp.insert(pair<string,int>("Alan",100)); // 插入一个类型为 pair<Key, T> 的值可以达到插入元素的目的
    map.erase(key) // 函数会删除键为 key 的元素 
    ```
* 其他注意事项
    - 基本性质和 `set` 类似
    - 底层实现是 `set<pair<Key, T>>`
    - 在利用下标访问 map 中的某个元素时，如果 map 中不存在相应键的元素，会自动在 map 中插入一个新元素，并将其值设置为默认值（对于整数，值为零；对于有默认构造函数的类型，会调用默认构造函数进行初始化）。
    - 当下标访问操作过于频繁时，容器中会出现大量无意义元素，影响 map 的效率。因此一般情况下推荐使用 find() 函数来寻找特定键的元素。

### multiset 具有相同元素的集合
* 头文件 `#include <set>`  
~~`#include <bits/stdc++.h>`~~
* 可以具有相同的元素的集合
* count / erase 返回的数字可能会大于 1

### mulitmap 具有相同键值
* 头文件 `#include <map>`  
~~`#include <bits/stdc++.h>`~~
* 因为 multimap 允许多个元素拥有同一键的特点， multimap 不支持 `[]`

### unordered_set 集合
* 头文件 ~~`#include <unordered_set> // C++11`~~; 在oi比赛中使用需要改为

    ```cpp
    #include <tr1/unordered_map>
    using namespace std::tr1; 
    ```

* 与`set`相比，底层实现从红黑树改为了哈希表。
* 使用迭代器访问时不保证顺序
* 平均情况下，插入/删除/查找 等操作的时间复杂度都为 `o(1)`

### unordered_map 映射
* 头文件 ~~`#include <unordered_map> // C++11`~~; 在oi比赛中使用需要改为

    ```cpp
    #include <tr1/unordered_map>
    using namespace std::tr1; 
    ```

### unordered_multiset / unordered_multimap
* 略
