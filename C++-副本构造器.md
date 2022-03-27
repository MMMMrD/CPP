# C++-副本构造器



## 为什么需要副本构造器？

​	在C++中，允许将一个类的对象赋值给新创建的一个相同类的对象，被赋值的新对象会将旧的对象中的属性与方法一一复制（包括指针），于是两个不同的对象中的的同名指针，就会指向同一个地址。当我们先删除其中一个指针的内存，此时另一个指针就会指向一个无意义的地址，若再删除该指针，程序就会出错。

​	为了应对这种情况，我们就需要创建一快新的内存，将原内存的值复制到这个新的内存之中，并让新的指针指向这一块新的内存。



## 实现方法

​	为了实现上述的方法，我们将对等于号“=”进行重载，同样的，也需要创建一个副本构造器。代码如下：

~~~c++
class Myclass
{
public:
	Myclass(int *p);
    Myclass(const Myclass &rhs);//副本构造器
	Myclass& operator=(const Myclass &rhs);//对等号进行重载
    void print();
    
private:
    int *ptr;
};

Myclass::Myclass(int *p)
{
    ptr = p;
}

Myclass::Myclass(const Myclass &rhs)
{
    *this = rhs;//该等号是重载之后的等号
}

Myclass& Myclass::operator=(const Myclass &rhs)
{
    if(this != &rhs)
    {
        delete ptr;//删除原来指针指向的内存
        
        ptr = new int;//创建一块新的内存
        *ptr = *(rhs.ptr);//将旧值赋给新的内存中
    }
    
    return *this;
}

void Myclass::print()
{
    std::cout<<*ptr<<std::endl;
}

int main()
{
    Myclass c1(new int(1));//创建一个变量c1
    Myclass c2 = c1;	   //创建一个新的变量c2，并将c1的值赋给c2
    
    c1.print();
    c2.print();
}
~~~





