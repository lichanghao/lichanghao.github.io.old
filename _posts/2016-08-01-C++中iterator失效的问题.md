---
layout:     post
title:      "C++中iterator失效的问题"
subtitle:   ""
date:       2016-08-01 10:10:00 +0300
author:     "lichanghao"
header-img: "img/post-bg-js-module.jpg"
header-mask: 0.3
catalog:    true
tags:
    - C++
    - iterator
    - 基础
---


iterator是标准库中大部分容器都支持的一个很好用的机制，它和指针用法很像，作用如它的名字“迭代器”，常用于遍历所有（或一部分）容器
元素。

标准库中的容器类型，例如vector或string，提供了大量方便的接口来直接使用。但是，有一些接口的调用会导致容器元素个数的变化，此时会引起iterator的失效，例如erase()方法。下面是一个例子。

```c++
#include <vector>
#include "stdafx.h"
int _tmain(int argc, _TCHAR* argv[])
{
	vector<int> test ;
	for(int i = 0;i != 10;i++)
		test.push_back(i);
	auto iter = test.begin()+8;
	cout << test[6] << endl;
	test.erase(test.begin()+3); 
	cout << test[6] << endl; //在erase以后建立的iterator都没问题，随便用
	cout << *iter <<endl;    //但是在erase方法之前建立的iter对象，变成了一个野指针，会导致run-time error
	system("pause");
	return 0;
}
```
运行上面的代码，在试图访问*iter时会报错。这里iter已经失效，成为一个类似野指针的存在。

《C++ primer》中的9.3.6章列举了可能会导致iterator失效的情况。

#### insert()方法

1.对于string、vector，如果insert()没有导致它们容量改变，从而在内存中“搬家”，那么insert方法会导致【指向插入元素之后的元素】的迭代器、指针、引用失效。如果搬家，那么所有先前创立的指向该对象的迭代器、指针、引用全部失效。对它们的调用会产生run-time error。

2.对于deque，除了队首和队尾以外，向任何位置插入元素，会导致所有的迭代器、指针、引用失效。如果插入的元素位于队首或者队尾，会导致所有迭代器失效，但是指针和引用没有失效。我认为这是由deque在底层的实现方式导致的。

3.对于list和forward_list，insert方法使用以后对迭代器、指针、引用没有影响。

#### erase()方法

1.对于string、vector，情况和上面相同。

2.对于deque，非队首队尾的情况和上面相同。队首和队尾的情况，只会导致begin()或者end()失效。

3.list和forward_list，情况和上面相同。

insert()和erase()方法都会返回一个新的、合法的iterator，我们可以用例如下面这样的一句话来更新iter，使其合法化。这是一个很好的习惯


```c++
iter = test.erase(iter);  //erase方法返回了【被删除元素后面元素】的迭代器，同时赋值给iter
```

总结一下，迭代器失效的类型：

1.由于容器元素整体“迁移”导致存放原容器元素的空间不再有效，从而使得指向原空间的迭代器失效。

2.由于删除元素使得某些元素次序发生变化使得原本指向某元素的迭代器不再指向希望指向的元素，这样的情况虽然在逻辑上看起来合法，但是会导致一些很奇怪的错误，因此在高版本编译器中也把这种情况归于迭代器失效。上面的例子，就属于这一种。

总而言之，越是灵活的东西，程序员在使用的时候越可能犯错误，而且这种错误往往很难找到并改正。指针就是一个很好的例子。高级程序语言的发展会越来越注重模式化。

