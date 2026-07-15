## 思路
Quick-find是一种简单的，实现并查集的一个算法，他的思路为，用一个id数组作为组号，属于同一个连通分量的话，他们的组号是相同的，判断时，通过判断组号，实现快速查找

## 代码

```cpp
//UF类
#include <vector>

class UF
{
public:
    UF(int n);
    ~UF();
    void unite(int x, int y);
    bool isConnected(int x, int y);
private:
    std::vector<int> id;
};
```

```cpp
//UF类实现
#include <iostream>
#include "UnionFind.h"

UF::UF(int n)
{
    id.resize(n);
    for(int i = 0; i < n; i++)
    {
        id[i] = i;
    }
}

UF::~UF()
{
}

void UF::unite(int x, int y)
{
    int xid = id[x];
    int yid = id[y];
    for(int i = 0; i < id.size(); i++)
    {
        if(id[i] == xid)
        {
            id[i] = yid;
        }
    }
}

bool UF::isConnected(int x, int y)
{
    return id[x] == id[y];
}

```

## 总结
Quick-find算法，顾名思义，就是查找很快，但是同样的，他的缺点也很明显；当我们连接的时候，他要遍历整个数组；那么假设，有 n 个对象，我们要进行 n - 1 次连接，使这n个对象，构成一个整体，那么此时就需要 n^2 次了，这是非常巨大的
**单词最坏连接** O(n)
**全连接** O(n^2)