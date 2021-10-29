# using的用法

## 1、概述
我们用到的库函数基本上都属于命名空间std的，在程序使用的过程中要显示的将这一点标示出来，如std::cout。这个方法比较烦琐，而我们都知道使用using声明则更方便更安全。

这个我们程序员肯定都知道了，今天突发奇想就想对using整理一下。

## 2、命令空间的using声明
我们在书写模块功能时，为了防止命名冲突会对模块取命名空间，这样子在使用时就需要指定是哪个命名空间，使用using声明，则后面使用就无须前缀了。例如：

```
using std::cin;	//using声明，当我们使用cin时，从命名空间std中获取它
int main()
{
	int i;
	cin >> i;	//正确：cin和std::cin含义相同
	cout << i;	//错误：没有对应的using声明，必须使用完整的名字
	return 0;
}
```

```cpp
//main.cpp

#include <iostream>
using namespace std;
#define DString std::string    //! 不建议使用！
typedef std::string TString;   //! 使用typedef的方式
using Ustring = std::string;   //！使用 using typeName_self = stdtypename;
typedef void (tFunc*)(void);using uFunc = void(*)(void); //更直观
int main(int argc, char *argv[])
{

    TString ts("String!");
    Ustring us("Ustring!");    
    string s("sdfdfsd");　　 cout<<ts<<endl;
    cout<<us<<endl;
    cout<<s<<endl;
    return 0;
}
```

需要注意的是每个名字需要独立的using声明。例如：

```
using std::cin;	//必须每一个都有独立的using声明
using std::cout;  using std::endl;	//写在同一行也需要独立声明
```

位于头文件的代码一般来说不应该使用using声明。因为头文件的内容会拷贝到所有引用它的文件中去，如果头文件里有某个using声明，那么每个使用了该头文件的文件就都会有这个声明，有可能产生名字冲突。

## 3、在子类中引用基类成员
在子类中对基类成员进行声明，可恢复基类的防控级别。有三点规则：

- 在基类中的private成员，不能在派生类中任何地方用using声明。
- 在基类中的protected成员，可以在派生类中任何地方用using声明。当在public下声明时，在类定义体外部，可以用派生类对象访问该成员，但不能用基类对象访问该成员；当在protected下声明时，该成员可以被继续派生下去；当在private下声明时，对派生类定义体外部来说，该成员是派生类的私有成员。
- 在基类中的public成员，可以在派生类中任何地方用using声明。具体声明后的效果同基类中的protected成员。

例如：

```
class Base 
{
protected:
    void test1() { cout << "test1" << endl; }
    void test1(int a) {cout << "test2" << endl; }

    int value = 55;
};
 
class Derived : Base 	//使用默认继承
{
public:
    //using Base::test1;	//using只是声明，不参与形参的指定
    //using Base::value;
    void test2() { cout << "value is " << value << endl; }
};
```

我们知道class的默认继承是private，这样子类中是无法访问基类成员的，即test2会编译出错。但是如果我们把上面注释的声明给放开，则没有问题。

注意：using::test1只是声明，不需要形参指定，所以test1的两个重载版本在子类中都可使用。
但是在往下派生，则只能使用无参函数，具体什么原因就不知道了…

## 4、使用using起别名
相当于传统的typedef起别名。
```
typedef 	std::vector<int> intvec;
using 	intvec	= std::vector<int>;	//这两个写法是等价的
```

这个还不是很明显的优势，在来看一个列子：

```
typedef void (*FP) (int, const std::string&);
```

若不是特别熟悉函数指针与typedef，第一眼还是很难指出FP其实是一个别名，代表着的是一个函数指针，而指向的这个函数返回类型是void，接受参数是int, const std::string&。
```
using FP = void (*) (int, const std::string&);
```

这样就很明显了，一看FP就是一个别名。using的写法把别名的名字强制分离到了左边，而把别名指向的放在了右边，比较清晰，可读性比较好。比如：

```
typedef std::string (* fooMemFnPtr) (const std::string&);
    
using fooMemFnPtr = std::string (*) (const std::string&);
```

来看一下模板别名。

```
template <typename T>
using Vec = MyVector<T, MyAlloc<T>>;
 
// usage
Vec<int> vec;
```

若使用typedef

```
template <typename T>
typedef MyVector<T, MyAlloc<T>> Vec;
 
// usage
Vec<int> vec;
```

当进行编译的时候，编译器会给出error: a typedef cannot be a template的错误信息。

那么，如果我们想要用typedef做到这一点，需要进行包装一层，如:

```
template <typename T>
struct Vec
{
  typedef MyVector<T, MyAlloc<T>> type;
};

// usage
Vec<int>::type vec;
```

正如你所看到的，这样是非常不漂亮的。而更糟糕的是，如果你想要把这样的类型用在模板类或者进行参数传递的时候，你需要使用typename强制指定这样的成员为类型，而不是说这样的::type是一个静态成员亦或者其它情况可以满足这样的语法，如：
```
template <typename T>
class Widget
{
  typename Vec<T>::type vec;
};
```

然而，如果是使用using语法的模板别名，你则完全避免了因为::type引起的问题，也就完全不需要typename来指定了。

```
template <typename T>
class Widget
{
  Vec<T> vec;
};
```

一切都会非常的自然，所以于此，模板起别名时推荐using，而非typedef。

感谢大家，我是假装很努力的 [@Charmve(益达)](https://github.com/Charmve)。

----

参考资料：
https://zhuanlan.zhihu.com/p/21264013
https://blog.csdn.net/shift_wwx/article/details/78742459
