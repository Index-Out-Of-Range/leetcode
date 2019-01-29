### 关键在于只写一层循环，降低时间复杂度

## C++
### 使用unordered_map

* 原型
```
template < class Key,                                    // unordered_map::key_type
           class T,                                      // unordered_map::mapped_type
           class Hash = hash<Key>,                       // unordered_map::hasher
           class Pred = equal_to<Key>,                   // unordered_map::key_equal
           class Alloc = allocator< pair<const Key,T> >  // unordered_map::allocator_type
           > class unordered_map;
```

2. 说明
unordered_map 是一种关联容器，用于存储由关键值 (Key Value，以下称为Key 值) 和映射值 (Mapped Value，以下称为映射值) 组成的元素，并且允许根据其 Key 值快速检索各个元素。 
在 unordered_map 容器中，Key 值通常用来唯一标识元素，映射值是与该 Key 值关联内容的对象。Key 值与映射值的类型可能不同。 
在 unordered_map 内部，元素没有按照其 Key 值与映射值的任何顺序进行排序 ，而是根据它们的 Hash 值组织成桶，允许它们通过其 Key 值直接快速访问单个元素（通常具有常数等级的平均时间复杂度）。 
unordered_map 容器与 map 容器相比，通过 Key 值访问各个元素的速度更快，然而通过其元素子集进行范围迭代的效率通常较低。 
unordered_map 实现了直接访问操作符 (operator[])，它允许使用 Key 值作为输入参数，直接访问映射值。 
容器中的迭代器至少是前向迭代器。




## Java


## Python