# Contain Common Features
## 1. Type Definination
    template <class _Tp, class _Alloc = __STL_DEFAULT_ALLOCATOR(_Tp) >
    class __CONTAIN_TYPE {
        typedef _Tp value_type;
        typedef value_type* pointer;
        typedef const value_type* const_pointer;
        typedef value_type* iterator;
        typedef const value_type* const_iterator;
        typedef value_type& reference;
        typedef const value_type& const_reference;
        typedef size_t size_type;
        typedef ptrdiff_t difference_type;
    };
construct
destroy
copy
uninitialized_copy
容器元素范围使用左闭右开区间[)，如[begin, end)
