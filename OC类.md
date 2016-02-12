- 点语法实质上就是调用getter和setter方法，是编译器的特性。在调用点语法是，编译器会对点语法进行编译：
```
p.value //会被翻译为 [p value];
p.value = 5 //会被翻译为 [p setValue: 5];
```
- 如果p对象有一个方法`- (void)test;`，那么，使用点语法调用同样是可以的，但是不推荐使用：
```
p.test //等同于[p test];
```
- 多态中，如果想调用子类特有的方法必须强制类型转换为子类才能调用；
- @public可以在其他类和子类中访问；@private不能在其他类和子类中访问；@protect不能在其他类中访问，可以在子类中访问；@package可以再相同包内访问（之后学习打包时学习）；
- 在@implementation中定义的成员变量默认是私有变量，和使用@private修饰的私有变量不太一样，无法在其他类中查看和访问；
- 使用`@property`会默认生成一个私有属性`_name`，这个成员变量是在`@implementation`中生成的而不是在`@interface`中生成的，在其他类中无法查看和访问；
- `@synthesize name = _name`，会实现以下代码：
```
 - (void) setName: (type)name{
    _name = name;    
 }
 - (type) name {
    return _name;
 }
```
`@synthesize name`，会实现一下代码：
```
 - (void) setName: (type)name{
    self.name = name;    
 }
 - (type) name {
    return self.name;
 }
```
- Xcode4.4（好像是这个版本）后，只使用@property即可同时生成setter和getter方法，在没有告诉@property将传入参数传给哪个属性时，默认传递给带有_的属性；
- @property有一个弊端就是不能对setter方法传入数据进行过滤，如果需要对传入参数进行过滤，必须重写setter方法;
- 使用`@property`时，如果只重写setter方法，会自动生成getter方法，同时会生成私有属性`_name`；如果只重写getter方法，会自动生成setter方法，同时也会生成私有属性`_name`；但如果同时重写getter/setter方法，则不再生成私有属性`_name`；
- `readonly`修饰符修饰的property只生成getter方法，readwrite修饰符一般不使用(property默认就是readwrite)，setter=Method修饰符用于自定义setter方法方法名(很少使用)，getter=Method修饰符用于自定义getter方法方法名(经常使用)；
- `retain`修饰符会自动生成set方法内存管理代码；
- `assign`不会帮我们自动生成set方法内存管理代码，仅仅生成普通set方法。默认；
- `atomic`性能低（多线程）默认；
- `nonatomic`性能高（多线程）；
---
- 重写init方法必须按照苹果规定的格式重写，如果不按照规定会引发一些未知错误。
```
 - (instancetype)init
 {
    self = [super init];
    if (self){
        //初始化代码
        ...
    }
    return self;
 }
```
- instancetype和id类似，都是万能指针，但是instancetype只能作为返回值类型，不能声明变量、也不能作为参数类型；
- 通常每自定义一个init方法，就要对应定义一个工厂方法；
- 工厂方法一般都以类名（首字母小写）开头；
- 工厂方法中创建实例时不要使用类名，尽量使用self关键字，否则容易出现未知问题；
- load方法在程序启动时自动调用(无论该类是否被使用)，initial方法在该类第一次被调用时执行；
- load方法和initial方法在继承时要注意顺序，先调用父类的load和initial方法，再调用子类的load和initial方法；
- SEL类型有三种用途：
 1. 配合类/对象检查类/对象中是否实现了某方法，`[class/object respondsToSelector:sel]`；
 2. 配合类/对象调用类/对象中对应的SEL方法；
 3. 配合对象将SEL类型作为形参传入(可以用于将指定传入对象执行传入的SEL方法等...)；
- performSelector方法最多接受两个参数；
- `@class`有两种应用场景，第一是在头文件中使用，以降低代码拷贝频率提高编译速度；第二是放置循环引入头文件；



