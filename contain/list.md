# Contain - List
---
## 1. API

	template <class _Tp, class _Alloc = __STL_DEFAULT_ALLOCATOR(_Tp) >
	class list {
	public:
		explicit list(const allocator_type& __a = allocator_type());
		explicit list(size_type __n);
		list(size_type __n, const _Tp& __value,const allocator_type& __a = allocator_type());
		list(const list<_Tp, _Alloc>& __x);
		list<_Tp, _Alloc>& operator=(const list<_Tp, _Alloc>& __x);
		~list();

		iterator begin();
		iterator end();
		reverse_iterator rbegin();
		reverse_iterator rend();
		const_iterator begin();
		const_iterator end();
		const_reverse_iterator rbegin();
		const_reverse_iterator rend();

		bool empty();
		size_type size();
		size_type max_size();
		reference front();
		reference back();
		const_reference front();
		const_reference back();

		void swap(list<_Tp, _Alloc>& __x);
		iterator insert(iterator __position);
		iterator insert(iterator __position, const _Tp& __x);
		void insert(iterator __position, const _Tp* __first, const _Tp* __last);
		void insert(iterator __position,const_iterator __first, const_iterator __last);
		void insert(iterator __pos, size_type __n, const _Tp& __x);
		void _M_fill_insert(iterator __pos, size_type __n, const _Tp& __x);

		void push_front();
		void push_back();
		void push_front(const _Tp& __x);
		void push_back(const _Tp& __x);
		void pop_front();
		void pop_back();

		iterator erase(iterator __position);
		iterator erase(iterator __first, iterator __last);
		void clear();
		void resize(size_type __new_size);
		void resize(size_type __new_size, const _Tp& __x);
		// __STL_MEMBER_TEMPLATES
		// list(), insert, _M_insert_dispatch, assign, _M_assign_dispatch
		void assign(size_type __n, const _Tp& __val);
		void _M_fill_assign(size_type __n, const _Tp& __val);
		void splice(iterator __position, list& __x);
		void splice(iterator __position, list&, iterator __i);
		void splice(iterator __position, list&, iterator __first, iterator __last);
		void remove(const _Tp& __value);
		void unique();
		void merge(list& __x);
		void reverse();
		void sort();
	};
	// operator <, ==, (swap, !=, >, <=, >=)__STL_FUNCTION_TMPL_PARTIAL_ORDER

1. list构造。
	* 无元素，指定空间配置器。
	* 构造ｎ个元素，可选值。
	* 使用新list赋值构造，支持＝操作。
2. 增加push_front和pop_front，splice，remove，unique，merge和sort等操作。

## 2. 继承关系
