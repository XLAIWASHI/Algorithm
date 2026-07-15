## 思路
Quick-union也是一种简单的实现并查集的算法，他的思路为，每个连通分量看成一颗树，在连接的时候，将这整颗树挂到另一颗树下，实现连接；判断时，通过判断两个对象的根节点是否相同，来判断是否连接

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
    int root(int i);
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
    int i = root(x);
    int j = root(y);
    id[i] = j;
}

bool UF::isConnected(int x, int y)
{
    return root(x) == root(y);
}

int UF::root(int i)
{
    while(i != id[i])
    {
        i = id[i];
    }
    return i;
}

```

## 总结
![image-1784091327036.png](../assets/03%20快速连接%28Quick-union%29/image-1784091327036.png)
虽然他的连接比较快，而且查找也比快速查找好；但是，他也有一个缺点，那就是，连接时，树的深度可能会非常大，所以在找根节点的时候，可能遇到的是一颗瘦长的树，那么，就需要遍历整颗树，所以
**单次最坏查找** O(n)
**全联接最坏查找** O(n^2)