#NSArray
- OC中数组只能用来存储OC对象，不能存储基本数据类型；
- 创建数组：
```
 NSArray *array = [NSArray alloc] init];
 NSArray *array2 = [NSArray arrayWithObject:@"abc"];
 NSArray *array2 = [NSArray arrayWithObject:@"abc", @"123", ... , nil];
 //下面category中生命的方法均为创建数组的方法
 @interface NSArray<ObjectType> (NSArrayCreation)

 + (instancetype)array;
 + (instancetype)arrayWithObject:(ObjectType)anObject;
 + (instancetype)arrayWithObjects:(const ObjectType [])objects count:(NSUInteger)cnt;
 + (instancetype)arrayWithObjects:(ObjectType)firstObj, ... NS_REQUIRES_NIL_TERMINATION;
 + (instancetype)arrayWithArray:(NSArray<ObjectType> *)array;

 - (instancetype)initWithObjects:(ObjectType)firstObj, ... NS_REQUIRES_NIL_TERMINATION;
 - (instancetype)initWithArray:(NSArray<ObjectType> *)array;
 - (instancetype)initWithArray:(NSArray<ObjectType> *)array copyItems:(BOOL)flag;

 + (nullable NSArray<ObjectType> *)arrayWithContentsOfFile:(NSString *)path;
 + (nullable NSArray<ObjectType> *)arrayWithContentsOfURL:(NSURL *)url;
 - (nullable NSArray<ObjectType> *)initWithContentsOfFile:(NSString *)path;
 - (nullable NSArray<ObjectType> *)initWithContentsOfURL:(NSURL *)url;

 @end
```
- 遍历数组：
```
 //1.使用for循环
 for (int i=0; i<[array count]; i++){
    //array[i]
    ...
 }
 //2.增强型for循环
 for (NSObject *objc in array){
    //array[i]
    ...
 }
 //3.使用迭代器
 [array enumerateObjectsUsingBlock:^(id  _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
    //每迭代一次都会执行一次block中的代码
    //obj传入的是当前迭代到的数组中的对象
    //idx为当前迭代到的索引值
    //stop用于控制何时停止迭代
}];
```