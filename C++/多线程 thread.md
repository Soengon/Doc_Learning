头文件 “ thread ”
创建线程：
```
#include<iostream>
#include<thread>
#include<string>

using namespace std;

void printHello(string msg){
	cout << msg << endl;
	return;
}

int main(){
	// thread 创建线程后，传入的第一个参数是需要开线程的函数，后面就是传入线程的参数。
	thread thread1(printHello, "Hello");

	return 0;
}
```
>运行会报错，因为当主程序运行到 return 时线程还在执行，此时就需要 join 函数。
>thread.join() 函数：join 函数会让主函数等待线程函数运行完成/当线程运行到 return 时再结束主函数。

```
int main(){
	// thread 创建线程后，传入的第一个参数是需要开线程的函数，后面就是传入线程的参数。
	thread thread1(printHello, "Hello");
	thread1.join();

	return 0;
}
```
>此时运行正常，接下来介绍另外一种方法，可以让主程序不报错，那就是 detach 函数。
>thread.detach() 函数：detach 函数会将线程与主函数分离，即当主函数运行完毕，也不会影响线程继续工作，当线程工作完了自动退出。

```
int main(){
	// thread 创建线程后，传入的第一个参数是需要开线程的函数，后面就是传入线程的参数。
	thread thread1(printHello, "Hello");
	thread1.detach();

	return 0;
}
```
>为了防止让无法调用 join 或 detach 的线程被不合法调用，存在一个函数，那就是 joinable 函数。
>thread.joinable()；这个函数会检测该线程可不可以调用 join 或 detach 并返回一个 bool 类型的值。

```
int main(){
	// thread 创建线程后，传入的第一个参数是需要开线程的函数，后面就是传入线程的参数。
	thread thread1(printHello, "Hello");
	bool isJoin = thread1.joinable();
	
	if(isJoin){
		thread.join();
		// thread.detach();
	}

	return 0;
}
```