#Category
- 在不改变原有类的基础上为类添加新功能；
- 代码实现：
```
@interface Classname (categoryname)
     ···
@end
@implementation Classname (categoryname)
     ···
@end
```

###注意：
1. category只能扩充原类的方法，不能添加实例变量；
2. category中的`@property`只会生成setter/getter方法的声明，不会生成实现，也不会生成私有成员变量；
3. 在category中可以访问原有类中的属性；
4. 如果category中有与原有类中重名的方法，会执行category中的方法，忽略原有方法；
5. 如果多个category中有重名方法，调用时会执行最后编译的那个category中的方法；

#匿名分类(类扩展Class Extension)
<b>类扩展可以为原有类添加私有属性和私有方法：</b>
- 写在.m文件中
- 代码实现：
```
@interface Classname ()
      ···
@end
```
