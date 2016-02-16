#Block
- block也是一种数据类型；
- block的形式类似于C语言中指向函数的指针；

###指向函数的指针
- 指向函数的指针保存的是函数；

```
void test() { //定义的函数
    ...
}
void (*pointerTest) (); //定义一个指向函数的指针
pointerTest = test;  //将指针指向函数
pointerTest();  //调用
```
- `void`是返回值类型,`*pointerTest`是指向函数的指针名称，后边的`()`表示没有参数；

###block
- block保存的是代码片段，基本上等同于Swift中的Closures；
- 形式：
```
返回值类型  (^blockName) (参数列表);
```
- 代码实现：
```
void (^blockName) ();  //定义一个block
blockName = ^(){  //初始化block
    ...
}
```
---
##注意事项
1. 在block中可以访问外部变量，如果block内定义有与外部同名变量，访问的是block内部的局部变量；
2. 在block中不能设置外部变量，因为在block内是对外部变量的拷贝，和原来的变量并不一样；
3. 要想在block中设置外部变量，需要在声明变量时使用`__block`修饰，在反编译后，可以发现在使用`__block`修饰后使用的是`引用传递`，在在未使用`__block`修饰时使用的是`值传递`;
4. block默认情况下存储在<b>栈</b>中，但是如果对block进行一个copy操作，block就会转移到堆中；
5. 如果block在栈中，block中访问了外界的对象，不会对对象进行retain操作；但是，如果block在堆中，block中访问了外界的对象，那么会对外界的对象进行一次retain；
6. **如果在block中访问了外界的对象，一定要给对象加上`__block`，只要加上`__block`，即使block在堆中，也不会对外界的对象进行retain；