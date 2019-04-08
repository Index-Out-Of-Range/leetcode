# unordered\_map

## 原型

```text
template < class Key,                                    // unordered_map::key_type
           class T,                                      // unordered_map::mapped_type
           class Hash = hash<Key>,                       // unordered_map::hasher
           class Pred = equal_to<Key>,                   // unordered_map::key_equal
           class Alloc = allocator< pair<const Key,T> >  // unordered_map::allocator_type
           > class unordered_map;
```

## 说明

* unordered\_map 是一种关联容器，用于存储由关键值 \(Key Value\) 和映射值 \(Mapped Value\) 组成的元素，并且允许根据其 **Key** 值快速检索各个元素。 
* 在 unordered\_map 容器中，Key 值通常用来**唯一标识元素**，映射值是与该 Key 值关联内容的对象。Key 值与映射值的类型可能不同。 
* 在 unordered\_map 内部，**元素没有按照其 Key 值与映射值的任何顺序进行排序** ，而是**根据它们的 Hash 值组织成桶**，允许它们通过其 Key 值直接快速访问单个元素（通常具有常数等级的平均时间复杂度）。 
* unordered\_map 容器与 map 容器相比，通过 Key 值访问各个元素的速度更快，然而通过其元素子集进行范围迭代的效率通常较低。 
* unordered\_map 实现了**直接访问操作符** \(operator\[\]\)，它允许**使用 Key 值作为输入参数，直接访问映射值**。 
* 容器中的迭代器至少是前向迭代器。

## 容器属性

* 关联性 
  * 关联容器中的元素的参考地址指的是其 Key 值，而不是他们在容器中的绝对地址；
* 无序性 
  * 无序容器使用 Hash 表来组织元素，这些 Hash 表允许无序容器通过 Key 值快速访问元素；
* 映射 
  * 每个元素将一个 Key 值与映射值关联起来，Key 值用于标识其主要内容是映射值的元素；
* 唯一关键值 
  * 容器中不存在同时拥有相同 Key 值的两个元素；
* 分配器感知 
  * map 容器使用分配器对象动态处理其存储需求。

## 模板参数

* Key
  * Key 值的类型。在 unordered\_map 中的每个元素都是由其 Key 值唯一指定的。
  * 别名为成员类型 unordered\_map::key\_type
* T
  * 映射值的类型。在 unordered\_map 中的每个元素，都存储了一些数据作为其映射值。
  * 别名为成员类型 unordered\_map::mapped\_type（注：不同于 unordered\_map::value\_type，详细见下面）
* Hash
  * 一个一元函数对象类型，它将**与 Key 值同类型的对象作为参数**，并以此为基础**返回类型为 size\_t 的唯一值**。它可以实现函数调用符的类，或是指向函数的指针。它的**默认值是 hash** ，它返回一个碰撞概率接近于1.0/std::numeric\_limits::max\(\)1.0/std::numeric\_limits::max\(\)的 Hash 值。
  * unordered\_map 对象使用该函数返回的散列值，并在内部组织元素，加速了定位各个元素的过程。
  * 别名为成员类型 unordered\_map::hasher
* Pred
  * 一个二元值，它接受两个 Key 类型的参数，并返回一个布尔值。表达式 pred\(a, b\) 中，pred 是该类型的对象，a, b 是 Key 值，如果 a 被认为与 b 等价，则返回 true。它可以使实现了函数调用运算符的类，或者指向函数的指针（具体请详细参阅示例的构造函数）。它的默认值是 equal\_to ，它返回与等号运算符 operator\(a==b\) 相同的值。
  * unordered\_map 对象使用该表达式，来确定两个元素的 Key 值是否等价。在 unordered\_map 容器中，没有任何两个元素可以使用该断定产生 true 值（原句：No two elements in an unordered\_map container can have keys that yield true using this predicate. ，也许翻译的不对）。
  * 别名为成员类型 unordered\_map::key\_equal
* Alloc（通常使用默认值）
  * 用于定义存储分配模型的分类器对象的类型。默认情况下，使用分配器类模板，它定义了最简单的内存分配模型，并且与值无关。
  * 别名为成员类型 unordered\_map::allocator\_type

在 unordered\_map 成员函数的参考中，模板函数假定了相同的名称：**Key, T, Hash, Pred, Alloc**。 unordered\_map 容器元素的迭代器可以访问 Key 值与映射值。为此 unordered\_map 定义了一个对应的类 value\_type，它的第一个值对应于 Key 值类型的常量版本，第二个值对应于映射值（即模板参数 T）：

`typedef pair<const Key, T> value_type;`

unordered\_map 容器的迭代器指向该 value\_type 的元素。因此对于一个调用 value\_type 的迭代器而言，迭代器指向 unordered\_map 的一个元素，它的 Key 值与映射值可以分别用下面的方式进行访问：

```text
unordered_map<Key,T>::iterator it;
(*it).first;             // the key value (of type Key)
(*it).second;            // the mapped value (of type T)
(*it);                   // the "element value" (of type pair<const Key,T>)
```

当然可以用任何其他的直接访问运算符，如 -&gt; 或 \[\]。例程如下：

```text
it->first;               // same as (*it).first   (the key value)
it->second;              // same as (*it).second  (the mapped value)
```

## 常用函数

* bucket

  > 原型 size\_type bucket \( const key\_type& k \) const；
  >
  > 说明 定位元素所在的桶，**返回 Key 值为输入参数 k 的元素的所在桶号。**  桶是容器内部 Hash 表中的一个槽，槽中的元素根据 Key 值分配元素。桶号的编号从 0 到 \(bucket\_count - 1\)。 桶中单个元素可以通过 unordered\_map::begin 和 unordered\_map::end 返回的范围迭代器进行访问。

* count

  > 原型 size\_type count \( const key\_type& k \) const;
  >
  > 说明 使用给定的 Key 值计算元素。 搜索容器中 Key 值为输入参数 k 的元素，并返回找到元素的数量。由于 unordered\_map 容器不允许存在重复的 Key 值，这说明如果容器中存在具有该 Key 值的元素，则该函数返回 1，否则返回 0。

* 其他

  > clear 清除 map 中所有元素；
  >
  > erase 删除 map 中指定位置的元素；
  >
  > insert 在 map 指定位置添加 pair 类型的元素；
  >
  > find 获取 map 中元素的迭代器；
  >
  > begin, end map 的正向迭代器的起始位置与终点位置；

