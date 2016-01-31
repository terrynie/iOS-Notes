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
- 同时使用`@property type name`和`@synthesize name`会默认生成一个私有属性name，而且在类外部不能通过`->`符号访问，可以使用setter/getter方法访问或者点语法访问；
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
- @property有一个弊端就是不能对传入数据进行过滤，