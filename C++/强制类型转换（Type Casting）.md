强制类型转换共有四个类型，分别是 static_cast | dynamic_cast | const_cast | reinterpret_cast 四种。
1. static_cast ：
- 它主要用于隐式类型转换，比如说 int 转换 double ：
```
int i = 10;
double d = static_cast<double>(i); // 等价于 double d = (double)i;
```
- 还用于基类和派生类之间指针或引用的转换，但是前提要确保转换是安全的：
```
Base *b = new Derived();
Derived *d = static_cast<Derived*>(b);
```
- 它还可以去掉const、volatile属性(但是不能增加这些属性)。
2. dynamic_cast :
- 主要用于处理多态类型，需要基类有至少一个虚函数。
- 在运行时执行类型检查并且只有在转换是安全的时候才会进行转换。失败时返回 nullptr (对于指针) 或抛出 std::bad_cast 异常(对于引用)
3. const_cast :
- 用于去掉或增加对象的 const 或 volatile 属性。
- 主要用于与遗留代码或API交互时改变 constness 。
```
const int *p = &i;
int *modifiableP = const_cast<int*>(p);
```
4. reinterpret_cast :
- 用于进行完全无关类型之间的转换。例如指针类型之间的转换，或者将指针转换为证书类型。
- 非常强力和危险的操作，通常会破坏类型安全性，需要特别小心使用。
```
long p = reinterpret_cast<long>(intptr);
void* ptr = reinterpret_cast<void*>(intPtr);
```
