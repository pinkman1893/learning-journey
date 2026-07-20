# C++ unordered_map 与 unordered_set

`std::unordered_map` 和 `std::unordered_set` 是基于哈希表实现的无序关联容器。它们不会像 `map` 和 `set` 那样按键的比较顺序自动排列元素。

使用前需要包含相应头文件：

```cpp
#include <unordered_map>
#include <unordered_set>
```

## 与有序关联容器的区别

| 容器 | 保存内容 | 是否自动有序 | 常见实现 |
| --- | --- | --- | --- |
| `set` | 唯一的键 | 是 | 平衡搜索树 |
| `map` | 唯一键对应的值 | 是 | 平衡搜索树 |
| `unordered_set` | 唯一的键 | 否 | 哈希表 |
| `unordered_map` | 唯一键对应的值 | 否 | 哈希表 |

不需要有序遍历，只关心快速插入、删除和查找时，可以考虑无序容器。

## 时间复杂度

哈希分布良好时，`unordered_map` 和 `unordered_set` 的插入、查找与删除平均为常数复杂度；最坏情况下可能退化为线性复杂度。

`map` 和 `set` 的对应操作通常是对数复杂度。因此，在算法题或数据量较大、无需排序的场景中，无序容器有时可以减少运行时间，但仍应结合键类型、哈希质量和实际数据测试。

## unordered_set

`unordered_set` 保存不重复的键。

```cpp
#include <iostream>
#include <unordered_set>

int main()
{
    std::unordered_set<int> values{5, 1, 9, 1};

    values.insert(3);

    if (values.find(9) != values.end()) {
        std::cout << "找到了 9\n";
    }

    values.erase(5);

    for (int value : values) {
        std::cout << value << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

重复的键只保留一份。遍历顺序没有保证，不能依赖输出按插入顺序或数值大小排列。

## unordered_map

`unordered_map` 保存唯一键及其对应的值。

```cpp
#include <iostream>
#include <string>
#include <unordered_map>

int main()
{
    std::unordered_map<std::string, int> scores;

    scores["alice"] = 90;
    scores["bob"] = 85;
    scores.insert_or_assign("alice", 95);

    auto iterator = scores.find("alice");
    if (iterator != scores.end()) {
        std::cout << iterator->first << " : " << iterator->second << '\n';
    }

    return 0;
}
```

它的 `operator[]`、`find`、`erase`、`size` 和 `empty` 等接口与 `map` 的常用接口相似，但元素不保持排序。

## 哈希与相等比较

无序容器通过哈希函数把键分配到不同的桶中，再通过相等比较判断键是否相同。标准库已为许多常用类型提供 `std::hash`。

使用自定义键类型时，通常需要提供哈希函数和相等比较函数，并保证：如果两个键被判定相等，它们的哈希值也必须相同。

## 重新哈希与迭代器失效

元素增加导致桶数量变化时，容器可能进行重新哈希。重新哈希会改变元素所在的桶和遍历顺序，并使迭代器失效。

已知元素数量时，可以提前预留容量：

```cpp
scores.reserve(1000);
```

这可以减少插入大量元素时的重新哈希次数。

## 选择建议

- 需要按键有序遍历、范围查询或稳定的比较顺序：使用 `map`、`set`。
- 不需要排序，主要进行按键查找、插入和删除：考虑 `unordered_map`、`unordered_set`。
- 对运行时间敏感时，应使用具有代表性的数据测试，而不是只根据平均复杂度判断。

<!-- learning-journey:update-history:start -->
## 更新记录

| 日期 | 类型 | 说明 |
| --- | --- | --- |
| 2026-07-20 | 首次发布 | 整理 unordered_map 与 unordered_set 的哈希特性、复杂度、基本用法及与有序容器的选择差异 |
<!-- learning-journey:update-history:end -->
