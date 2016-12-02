最近在学习C++时突发奇想，一个空类的大小是多少呢？
即

```
#include<iostream>
using namespace std;
class X
{
};
class Y : public virtual X{};
class Z : public virtual X{};
class A : public Y,public Z{};

int main(int argc,char *args[])
{
  cout<<"X的大小："<<sizeof(X)<<endl;
  cout<<"Y的大小："<<sizeof(Y)<<endl;
  cout<<"Z的大小："<<sizeof(Z)<<endl;
  cout<<"A的大小："<<sizeof(A)<<endl;
  return 0;  
}
```
按照之前的想法，因为X是一个空类，其中不包含任何的数据，那么它的大小必然是为0，但是让我们大吃一惊的是，得到的结果并不是如同所想象的那样。得出的结果为：
X的大小：1
Y的大小：4
Z的大小：4
A的大小：8
![这里写图片描述](http://img.blog.csdn.net/20160819133744004)
注：采用的编译器为vs2005。
《深入理解C++对象模型》这本书是这样解释的：一个空类事实上并不是空的，它有一个隐晦的 1byte ，那是呗编译器安插进去的一个char。这使得这个 class 的两个不同的对象得以在内存中配置独一无二的地址。
	简而言之一个类的实例化对象有着它自己的独一无二的地址，而地址是代表着一段内存大小，假如一个空类的空间大小也为0，则我们不能为它分配内存，不能得到它的地址，因此编译器会为空类添加一个隐晦的char用以来标识空类的实例化对象。
	同时《深入理解C++对象模型》也解释到影响Y,Z类的大小有如下三个因素：
	1.语言本身所造成的额外负担，当语言支持虚基类的时候，就会导致一些额外的负担，在派生类中，这个额外的负担反映在某种形式的指针上，它或者指向virtual base class subobject(虚基类子对象)，或者指向一个相关表格，表格中存放的若不是virtual base class subobject(虚基类子对象)的地址，就是其偏移量(offset)
	2.编译器对特殊情况所提供的优化处理，virtual base class X subobject的1 byte 大小也出现在class Y和Z身上。传统上它被放在派生类的固定的部分的尾端。某些编译器会对empty virtual base class提供特殊的支持，（这种特殊的支持会使得派生类的1byte被取代）
	3.Alignment(内存对齐)的限制，Class Y和Z的大小目前是5byte，在大部分机器上，群聚的结构体大小会受到alignment的限制，使它们能更有效率的存取，假如上述第二点的编译器没有提供empty virtual base class的支持，那么大部分aliment是4byte（32位），会补齐3byte，最终得到的结果会是8byte。d当然很明显vs2005为我们提供了上述支持，因此只有4byte。
	![这里写图片描述](http://img.blog.csdn.net/20160819140637242)

![这里写图片描述](http://img.blog.csdn.net/20160819141251788)
	越是深入学习C++，越会发现编译器的细节以及语言的实质，让我们理解的越发深刻