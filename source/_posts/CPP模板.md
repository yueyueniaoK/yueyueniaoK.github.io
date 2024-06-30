---

title: C++模板

date: 2023-11-21 16:57:28

tags: C++

categories: C++学习

---
## 模板定义

### 1函数模板定义

##### 1.1函数模板

```C++
template<typename T,typename U>
```

**模板定义**以关键字**template**开始，后面跟着一个**模板参数列表（template parameter list**），**模板参数（template parameter）**用逗号分隔开，用小于号**<**和大于号**>**包围起来。

**<font color = red>Note：模板参数列表不能为空</font>**

##### 1.2实例化函数模板

当我们调用一个函数模板时，编译器会根据函数实参推断出模板实参，用推断出的模板参数为我们**实例化（instantiate）**一个特定版本的函数，编译器生成的版本通常被称为**模板的实例（instantiation）**。

```C++
//compare的函数模板
template<typename T>
int compare(const T&v1,const T&v2)
{
	if(v1 < v2) return 1;
	if(v2 < v1) return -1;
	return 0;
}

//当我们使用compare函数模板时
cout<<compare(1,0)<<endl;

//编译器实例化compare的实例
int compare(const int &v1,const int &v2)
{
	if(v1 < v2) return 1;
	if(v2 < v1) return -1;
	return 0;
}
```

##### 1.3模板类型参数和非模板类型参数

模板类型参数

```C++
template<typename T,class U>
```

模板类型参数前面必须使用关键字**typename**或者**class**，**模板类型参数（template parameter)**可以看作为类型说明符，像内置类型和类类型一样使用。

<font color = gree>非模板类型参数</font>

<font color= gree>非模板类型参数可以是一个整型、指向对象或函数类型的指针或者引用，绑定到非类型整型参数必须是一个常量表达式，绑定到指针或引用非类型参数的实参必须具有静态的生存期,不能用一个普通的局部变量或动态对象作为指针或引用类型模板参数的实参。在需要常量表达式的地方，可以使用非类型参数，比如数组的大小</font>

<font color  = red>Note：非模板类型参数必须是常量表达式</font>

函数模板可以声明**inline**和**constexpr**，放在模板参数列表之后，返回类型之前。

```C++
template<typename T> inline int compare(const T &v1,const T &v2)
```

##### 1.4尽量编写类型无关的代码

如上面compare函数例子，编写泛型编程代码的两个重要原则：

1. 模板中的函数参数是const的引用；（可以保证函数可以用不能拷贝的类型）
2. 函数体中的条件判断仅使用<比较运算；（可以降低对要处理的类型的要求）

<font color = red>Best Practices:模板程序应该尽量减少对实参类型的要求</font>

![](https://hexoimagebed.oss-cn-shanghai.aliyuncs.com/images/Snipaste_2023-11-21_15-23-04%E6%A8%A1%E6%9D%BF%E7%BC%96%E8%AF%91.png))

![img](https://hexoimagebed.oss-cn-shanghai.aliyuncs.com/images/Snipaste_2023-11-21_15-24-05.png)

![img](https://hexoimagebed.oss-cn-shanghai.aliyuncs.com/images/Snipaste_2023-11-21_15-24-50.png)

### 2类模板定义

##### 2.1类模板

```C++
template<typename T>
类的定义
```

```C++
template <typename T>
class Blob
{
public:
    typedef T value_type:
    typedef typename std::vector<T>::size_type size_type;
    //构造函数
    Blob();
    Blob(std::initializer_list<T> il);
    //Blob中的元素数目
    size_type size() const {return data->size();}
	bool  empty() const {return data->empty();}
    //添加和删除元素
    void pysh_back(const T &t) {data->push_back(t);}
    //移动版本
    void push_back(T &&t) {data->push_back(std::move(t));
    void pop_back()
  	//元素访问
    T& back();
    T& operator[](size_type i);
private:
    std::shared_ptr<std::vector<T>> data;
    //若data[i]无效，则抛出msg
    void check(size_)
        
}
```

<font color = red>size_type是string和vector类类型定义的类型，用来保存string和vector对象的长度，标准库类型将size_type定义为unsigned类型。</font>