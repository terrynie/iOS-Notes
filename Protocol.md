#Protocol
- 类似于Java中的Interface，是一系列必须实现和选择实现的方法的声明列表；
- 代码实现：
```
 @protocol 协议名
    ···
 @end
    
 @interface 类名 : 父类名 <协议名1, 协议名2...>
    ···
 @end
```

###使用注意
1. Protocol只能用来声明方法，既不能声明变量，也不能写方法实现；
2. Protocol可以被继承，如果父类遵守了某个Protocol，那么该类的子类也将遵守该协议；
3. OC不允许多继承，但是可以遵守多个协议；
4. 协议也可以遵守协议，一个协议遵守了另一个协议后，将会用用后者所有的方法声明；

##基协议
- 在类中有一个基类NSObject，最基本的类，任何其他类都要继承它；
- 在协议中同样也有一个NSObject协议，它是一个基协议，也是最基本的协议；
- 在NSObject协议中声明了很多最基本的方法：
 - description
 - retain
 - release
 - ···
- 建议每个协议都遵守NSObject协议

##@required和@optional
- 协议中区分哪些方法必须实现哪些方法可以选择实现就是靠`@required`和`@optional`修饰符来区分；
- `@required`修饰符修饰的方法是必须实现的，`@optional`修饰符修饰的方法可以实现也可以不实现；
- 注意：被`@required`修饰的方法即使没有被实现也不会报错，只会报一个警告；(所以，`@required`和`@optional`只是为了方便程序员之间的交流)