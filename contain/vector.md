# Contain - Vector
---
## 1. API
	template <class _Tp, class _Alloc = __STL_DEFAULT_ALLOCATOR(_Tp) >
	class vector {
		iterator begin();
		iterator end();
		reverse_iterator rbegin();
		reverse_iterator rend();
		const_iterator begin();
		const_iterator end();		
		const_reverse_iterator rbegin();
		const_reverse_iterator rend();

		size_type size();
		size_type max_size();
		size_type capacity();
		bool empty();

		reference operator[](size_type __n);
		const_reference operator[](size_type __n);
		
		explicit vector(const allocator_type& __a = allocator_type());
		vector(size_type __n, const _Tp& __value, const allocator_type& __a = allocator_type());
		explicit vector(size_type __n);
		vector(const vector<_Tp, _Alloc>& __x);
		vector(const _Tp* __first, const _Tp* __last, const allocator_type& __a = allocator_type());
		~vector();
		vector<_Tp, _Alloc>& operator=(const vector<_Tp, _Alloc>& __x);

		vector<_Tp, _Alloc>& operator=(const vector<_Tp, _Alloc>& __x);
		void reserve(size_type __n);
		void assign(size_type __n, const _Tp& __val);
		void _M_fill_assign(size_type __n, const _Tp& __val);

		reference front();
		reference back();
		const_reference front();
		const_reference back();
		void push_back();
		void push_back(const _Tp& __x);
		void pop_back();
		iterator insert(iterator __position);
		iterator insert(iterator __position, const _Tp& __x);
		void insert (iterator __pos, size_type __n, const _Tp& __x);
		void _M_fill_insert (iterator __pos, size_type __n, const _Tp& __x);
		void swap(vector<_Tp, _Alloc>& __x);
		iterator erase(iterator __position);
		iterator erase(iterator __first, iterator __last);
		void resize(size_type __new_size, const _Tp& __x);
		void resize(size_type __new_size);
		void clear();
		// __STL_THROW_RANGE_ERRORS
		_M_range_check, at
		// __STL_MEMBER_TEMPLATES
		vector(), _M_initialize_aux, assign, _M_assign_dispatch ,_M_assign_aux, insert, _M_insert_dispatch
	};
	// operator <, ==, (swap, !=, >, <=, >=)__STL_FUNCTION_TMPL_PARTIAL_ORDER

1. vector构造。
	* 显示说明空间配置器构造
	* 构造包含n个元素的vector，可提供初始值，默认使用无参构造。
	* 使用iterator进行构造，提供begin和end。
2. 元素只能向后增长，可在vector中任意合法位置插入任意数量的元素。
3. vector特有容量capacity属性。

## 2. 宏说明

1. __STL_USE_STD_ALLOCATORS: 使用STD空间配置器
2. __STL_CLASS_PARTIAL_SPECIALIZATION: 类特例化
3. __STL_HAS_NAMESPACES: 如果有命名空间
4. __STL_THROW_RANGE_ERRORS: STL范围越界错误
5. __STL_MEMBER_TEMPLATES 针对5种迭代器的成员模板

## 3. 继承关系
	<class _Tp, class _Alloc = __STL_DEFAULT_ALLOCATOR(_Tp)>
	vector
		-> _Vector_base<_Tp, _Alloc>
			-> _Vector_alloc_base (__STL_USE_STD_ALLOCATORS)

## 4. 数据结构
1. 连续存储空间。
2. 3个和数据结构相关的指针，_M_start，_M_finish，_M_end_of_storage，类型皆是_Tp*。
3. 数据存放于[_M_start, _M_finish)之间，[_M_finish, _M_end_of_storage)段空间保留用于数据的增长。
4. API中的max_size和capacity(vector特有)体现出３中的特点。

## 5. 类_Vector_base接口
	template <class _Tp, class _Alloc> 
	class _Vector_base {
		_Vector_base(const _Alloc&);
		_Vector_base(size_t __n, const _Alloc&);
		~_Vector_base();
		protect:
		_Tp* _M_start;
		_Tp* _M_finish;
		_Tp* _M_end_of_storage;
		//...
	};

## 6. 存储相关
1. 空间配置有２种方式，STD空间配置和自定义空间配置。由空间配置器管理_M_start，_M_finish，_M_end_of_storage这３种指针，初始化默认不分配空间，以n个元素初始化则使用空间大小为n的分配空间。
2. _M_*操作。
	* _M_allocate 针对空间配置器的存储分配
	* _M_deallocate　针对空间配置器的存储释放
	* _M_fill_assign 使用新值填充n个元素的空间
	* _M_fill_insert 填充插入ｎ个元素，可选值
	* _M_allocate_and_copy 分配n个元素空间，并复制n个元素
	* _M_range_check 检查访问元素是否越界
	* **以下针对５种迭代器**
	* _M_range_initialize 初始化[__first, __last)
	* _M_range_insert 把[__first, __last)插入到[..., __pos)
	* _M_initialize_aux 初始化
        * _M_assign_aux 使用[__first, __last)范围元素对vector赋值
        * _M_assign_dispatch
	* _M_insert_aux 超容插入１个元素

## 7. 迭代器iterator
* 迭代器不占用额外空间。
* 迭代器使用类型指针。
