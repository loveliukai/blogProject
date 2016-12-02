当我们写一个空类而不添加任何代码时，却可以用它来创建对象，拷贝、赋值等操作。例如：

```
#include<iostream>
using namespace std;

class Empty{};

int main(int argc,char *args[])
{
    Empty a; //default construct
    Empty b(a); //copy construct
    b = a;      //copy assigment
    return 0;
}
```
执行上述程序发现并么有报错
![这里写图片描述](http://img.blog.csdn.net/20160904005447609)
这是因为编译器给我们自动的生成了一些函数，包括，默认构造函数，拷贝构造函数，重载赋值操作符等。添加了这些函数的类如下

```
class Empty{
public:
    Empty();  
    ~Empty();
    Empty(const Empty &rhs);
    Empty & operator = (const Empty &rhs);
};

```
如果我们不想这个类有赋值与拷贝功能应当怎么做，按照思维如果我们不想这个函数的功能，我们不应该去定义它，但是在这里如果我们不去定义，编译器会自动帮我们创建出来，那么该如何做呢，很简单，只需要把这两个函数显示的设为私有的就行了，例如：

```
class Empty{
public:
    Empty();  
    ~Empty();
private:
    Empty(const Empty &rhs);
    Empty & operator = (onst Empty &rhs);
};
int main(int argc,char *args[])
{
    Empty a; //default construct
    Empty b(a); //copy construct
    b = a;      //copy assigment
    return 0;
}
```
当我们将这两个函数显示的设为私有的时候，我们在类外面调用拷贝构造和赋值操作"="时，编译器就会提示一个编译错误
![这里写图片描述](http://img.blog.csdn.net/20160904010915772)

虽然这样做保证了我们在类外调用赋值操作会被显示的拒绝，可是如果是在类的里面，或者是类的friend函数呢？很简单，此时我们只需声明
Empty(const Empty &rhs);
    Empty & operator = (onst Empty &rhs);
    这两个函数，而不用去实现它，这样在frind函数或是类的成员函数里进行拷贝、赋值时就回报错。
```
#include<iostream>
using namespace std;

class Empty{
public:
Empty(){} //在我们提供了拷贝构造函数之后，编译器不会生成默认构造函数
friend void copy(Empty &a);
private:
    Empty(const Empty &rhs);
    Empty & operator = (const Empty &rhs);
};

void copy(Empty &a)
{
    Empty b(a); //copy construct
    b = a;      //copy assigment
}

```
我们只编译不运行，结果如下
![这里写图片描述](http://img.blog.csdn.net/20160904013253982)
由上图所示编译成功并生成了.o文件，现在我们链接
![这里写图片描述](http://img.blog.csdn.net/20160904013507730)
报错了，提示函数未定义（我们确实没有定义），但是通常我们希望这个错误能在编译期间就显现出来。很简单

```
class Child : private Empty{};
```
只需如此，当Child的成员函数或者友元函数试图拷贝Child对象时，Child类会生成一个copy construct来构造，但是子类的拷贝构造函数会先调用Empty的构造函数，而Empty的构造函数是未定义的、私有的不允许被调用，因此早便宜期间就会直接报错。