# C++-模板&STL



## 模板

​	许多时候，我们都会对不同的数据类型进行相同的操作，例如两个变量的交换。这两个变量可能是不同的变量类型，但是交换的方法基本是一成不变的，而我们却要为了不同的数据类型分别写几次内容几乎一致的代码，而模板就是为了解决这一类的问题。

​	针对上述问题，我们可以先利用一个变量T来代替我们之后具体的变量类型，从而实现代码的简化，下面将用函数模板举例：

~~~c++
template <class T>
void swap(T &a,T &b)//交换函数模板
{
    T temp = a;
    a = b;
    b = temp;
}

int main()
{
    int t1 = 1;
    int t2 = 2;
    std::cout<<"t1="<<t1<<std::endl<<"t2="<<t2<<std::endl;//打印两变量
    
    swap<int>(t1,t2);//声明交换变量为int类型后，将两变量交换
    
    std::cout<<"t1="<<t1<<std::endl<<"t2="<<t2<<std::endl;//打印交换后结果
}
~~~

### 函数模板

​	函数模板的使用方式就如上述引例，在此不过多赘述。



### 类模板

​	根据模板的使用场景，易得知模板也同样适用于类之中。使用类模板，可以创建内容相似，所传参数类型不相同的类。具体例子如下：

~~~c++
template <class T>			//声明模板类
class test()	
{
    void swap(T &a,T &b);
}

template <class T>
void test<T>::swap(T &a,T &b)//实现模板类中的函数，注意定义函数开头的写法
{
    T temp = a;
    a = b;
    b = temp;
}

int main()
{
    int t1 = 1, t2 = 2;
    
    test<int> t;			//声明模板类的对象，需要提前声明类型
    
    t.swap(t1,t2);
}
~~~





