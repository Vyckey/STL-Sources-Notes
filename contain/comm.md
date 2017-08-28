# Contain Common Features
## 1. Type Definination
    template <class _Tp, class _Alloc = __STL_DEFAULT_ALLOCATOR(_Tp) >
    class __CONTAIN_TYPE {
        typedef _Tp value_type;
        typedef value_type* pointer;
        typedef const value_type* const_pointer;
        typedef value_type& reference;
        typedef const value_type& const_reference;
        typedef size_t size_type;
        typedef ptrdiff_t difference_type;
    };
construct
destroy
copy 复制区间[)到新位置
uninitialized_copy 复制区间[)到新位置
uninitialized_fill_n 在某个位置填充ｎ个元素，值可选
容器元素范围使用左闭右开区间[)，如[begin, end)
