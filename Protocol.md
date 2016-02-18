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

##应用场景
1. 如果想让某个对象必须遵守某个协议，可以将协议写在数据类型的右边：
```
ClassName<protocolName> *objc = [[ClassName alloc] init];
//ClassName是数据类型，protocolName是要遵守的协议
```
2. 使用协议对对象进行类型限定后，并不意味着该对象一定实现了协议中的方法，所以在调用协议声明的方法前一定要进行安全性检查：
```
if ([objc respondsToSelector:@selector(methodName)]){ //methodName就是协议中声明的方法
      [objc methodName];
}
```

##规范
1. 一般情况下，当前协议属于谁，我们就将协议定义到谁的头文件中；
2. 协议的名称一般以它属于的类名开头，后面跟上protocol或者delegate；
3. 协议中的方法名称一般以协议的名称中protocol之前的部分作为开头；
4. 一般情况下协议中的方法会将触发该协议的对象传递进去；
5. 一般情况下类中的代理属性命名为delegate；
6. 当某一个类要成为另外一个类的代理时，一般在头文件中使用`@protocol 协议名`，告诉当前类这是一个协议，而在实现文件中才使用`#import`导入；
