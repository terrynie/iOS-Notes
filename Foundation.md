#NSString
###基本概念
- 三种创建方式，第一种是字符串常量创建，第二种是`alloc init`创建，第三种是工厂方法创建：
```
NSString *str1 = @"str1"; //字符串常量创建
NSString *str2 = [[NSString alloc] initWithFormat:@"str2"]; //通过alloc init创建
NSString *str3 = [NSString stringWithFormat:@"str3"]; //工厂方法创建
```
- 如果是通过字符串常量创建，那么字符串常量存储在常量区；
- 通过`alloc init`或者`工厂方法`创建的字符串存储在堆区；
- 不同平台下存储方式不同：Mac平台会对字符串对象进行优化，两个内容相同的字符串对象指向同一个内存空间，但在iOS平台是两个对象；
- 不同编译器存储方式不同：Xcode6以下且是iOS平台，如果内容一样，每次alloc都会创建一个新对象。但如果在Xcode6以上，如果内容相同，多次alloc指向同一块存储空间；
- 由于`initWithString`是通过浅copy返回一个字符串对象，所以在内容相同时，多个对象指向同一个内存空间；

###字符串截取

