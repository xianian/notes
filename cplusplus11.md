* delete 
四个作用:

1.删除编译器默认生成的函数，如拷贝构造，赋值操作，移动赋值操作，默认构造函数等

2.删除由数据转换损失的成员函数

3.针对一个类限制该对象通过new操作在堆中创建

4.删除特征的模版特化

* std::bind

一个函数作为输入，返回一个新的函数对象，新函数的参数可以包含原函数的一个或者多个参数（通常小于等于原函数的参数），并且参数顺序可以重新排列。

* Variadic Template Function

c++11 支持参数数目可变的模版函数

实现机制:
Declaring a vardiac template function is easy but its definition is little tricky. We cann’t access the the passed variable number of arguments directly. We need to use the c++ type **deduction mechanism & recursion** to achieve this

* std::shared_ptr, std::weak_ptr, std::unique_ptr

shared_ptr要防止内存泄漏问题（通常是对象互相shared形成环，导致引用计数无法变为0，此时可考虑weak_ptr或者unique_ptr代替）

* std::all_of() / std::any_of()

std::all_of:检查一组元素是否都满足给定条件，与std::any_of()相反。

std::any_of:检查一组元素中如果任意一个满足条件即可。

`bool all_of (<Start of Range>, <End of Range>, UnaryPredicate pred);`

`bool any_of (InputIterator start, InputIterator end, UnaryPredicate callback);`
eg:

 `bool result = std::all_of(wordList.begin(), wordList.end(), [](const std::string & str) {		return str.size() == 4;});`

* std::initialzer_list\<T>
初始化列表的原型实现，可利用此结构实现自定义结构的初始化列表初始化，只要传过去的参数是这个就行了。

* std::unordered_map
How unordered_map store elements?

The reason because unordered_map does the hashing i.e. whenever we try to insert an element in a unordered_map, it internally does the following steps,

First hash of key is calculated using Hasher function and then on the basis of that hash an appropriate bucket is choose.

Once bucket is identified then it compares the key with key of each element inside the bucket using Comparator function to identify if given element is a duplicate or not.

If its not a duplicate then only it stores the element in that bucket
以上描述说明unordered_map使用了hash function和comparator function来决定key的位置以及是否重复，如果重复就覆盖，如果没有就插入同一个bucket中。

三种方式初始化unordered_map
1.用初始化列表初始化。
2.使用一组std::pair初始化。
3.使用另一个unordered_map初始化。

std::map 与 std::unordered_map比较
1.内部实现上，map基于平衡BST，unordered_map基于hash表
2.内存消耗上，unordered_map通常比map多
3.查询时间上，每次查询map复杂度O(log n),unordered_map不考虑hash冲突复杂度是O(1)
4.自定义key对象时，map需要重载operator <用于key的比较，unordered_map需要提供std::hash<K>并且重载==operator