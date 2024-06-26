#### volatile 变量的作用是告诉编译器，该变量是随时可能发生变化的，不要去编译它，在每次使用该变量时重新读取它的地址中的值来使用。
#### 为什么要用 volatile 变量呢？
答：因为当编译器发现两次从同一个变量读数据的代码之间，不存在对该变量的操作，它会自动把上次读到的值赋值给当前的变量，而不是重新从内存中读取该变量的值，这样的话，如果该变量是寄存器变量或者表示端口数据，就容易出错，volatile 可以保证对特殊地质的稳定访问，不会出错。

额外知识获取：编译器有假设的习惯，所以当我们在不经意间会修改某些重要的内容时，应使用 volatile 变量。