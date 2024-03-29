# C++与C的区别

## C++项目创建

添加的源文件是.cpp

## C++头文件

### 头文件包含

+ C++兼容C语言的头文件
+ C++自己写头文件，依旧按照C语言的头文件方式包含  #include "xxx.h"
+ C++包含C语言头文件方式可以省略.h  在相应头文件前面加个C  
  + #include <stdio.h>
  + #include <cstdio>
+ C++的标准头文件  #include <iostream>

### 综合代码

```c++
#include <stdio.h>
//自己写的不能省略.h
#include "./myHead.h"
//C++可以去掉.h方式包含C语言的标准头文件
#include <cstdio>
#include <cstdlib>
#include <ctime>
#include <cstring>
//C++标准头文件
#include <iostream>
int main() 
{
	printf("C++第01课!\n");
	return 0;
}
```

## C++命令空间

### 创建语法

```c++
namespace 空间名
{
    
}
//空间名随便起
//存放代码的空间
//不同空间可以存在相同名字
```

### 命名空间作用

+ 提高标识符使用率
+ 避免命名污染

### 如何访问

```c++
//直接访问
空间名::变量名;
//省略前置访问
using namespace 空间名;
//这个语法语句有用于域
//使用这个语法时候一定要自己避免二义性问题
```

+ ::   叫做作用分辨符：可以用来区分全局变量

### 命名空间嵌套

空间嵌套大家只需要剥洋葱即可

```c++
namespace A 
{
	int a = 1;
	namespace B 
	{
		int b = 12;
		namespace C 
		{
			int c = 123;
		}
	}
}
void  testNamespace() 
{
	//剥洋葱
	printf("%d\n", A::B::C::c);
	printf("%d\n", A::B::b);
	printf("%d\n", A::a);
	using namespace A::B::C;
	printf("%d\n", c);
}
```

### 标准命名std

C++所有的东西都是在std这个命名空间中，如果写C++程序，大家没加using namespace std; 所有C++的东西都需要加std::前置

```c++
#include <iostream>
using namespace std;	//标准命名空间
int main()
{

    
    
    return 0;
}
```

### 综合代码

```c++
#include <iostream>
#include <cstdio>
#include <string>
using namespace std;		//为了省略前缀
//创建一个MM 空间名
namespace MM 
{
	int  age;
	void print() 
	{
		printf("1");
	}
}
namespace Girl 
{
	int age;
	void print()
	{
		printf("2");
	}
}
namespace A 
{
	int a = 1;
	namespace B 
	{
		int b = 12;
		namespace C 
		{
			int c = 123;
		}
	}
}
void  testNamespace() 
{
	//剥洋葱
	printf("%d\n", A::B::C::c);
	printf("%d\n", A::B::b);
	printf("%d\n", A::a);
	using namespace A::B::C;
	printf("%d\n", c);
	using namespace A::B;
	printf("%d\n", b);
}
int g_num = 111;
int main() 
{
	//No.1 直接访问
	Girl::age = 1199;
	MM::age = 234;
	Girl::print();
	MM::print();
	using namespace MM;
	using namespace Girl;
	//print();			//存在二义性问题
	int g_num = 222;
	printf("%d\n", g_num);
	printf("%d\n", ::g_num);			//访问全局的变量
	std::string str;
	return 0;
}
```

## C++输入输出

首先同学目前学会使用即可，不需要追求为什么这样做，记住就完事

### C++输出

+ C++输出由 cout加上<<完成
+ C++依旧支持C语言的转义字符
+ C++换行可以使用endl

```c++
void testCout() 
{
	//No.1 打印单个常量
	cout << "ILoveyou";
	cout << 1;
	cout << 1.33;
	//No.2 打印多个
	cout << 1 <<"\n" << 1.33 << "\n" << "IMiissyou" << "\n";
	//No.3 打印变量
	int a = 1;
	char b = 'b';
	char str[] = "IMissyou";
	//打印字符串用的数组名
	cout << a << "\t" << b << "\t" << str << "\n";		//字符可以用''
	//No.4 换行可以用endl替换
	cout << "换行" << endl;
}
//精度暂时不用管，流操作符会讲  IO流中会讲
```

### C++输入

+ C++输入由cin加上>>完成
+ C++输入的过程中不需要任何其他的东西，默认用空格充当数据间隔

```c++
void testCin() 
{
	int a;
	double b;
	char str[10] = "";
	cout << "请输入一个整数:";
	cin >> a;
	cout << "请输入double:";
	cin >> b;
	cout << "输入字符串:";
	cin >> str;
	cout << "请输入三个数据：";
	cin >> a >> b >> str;
	//getch();
	cout << a << "\t" << b << "\t" << str << endl;
	//cin.getline(str,199);
}
```

注意点: 如果没有写using namespace std;   cin和cout以及endl 都需要加std::前置

### 综合代码

```c++
#include <iostream>
using namespace std;
void testCout() 
{
	//No.1 打印单个常量
	cout << "ILoveyou";
	cout << 1;
	cout << 1.33;
	//No.2 打印多个
	cout << 1 <<"\n" << 1.33 << "\n" << "IMiissyou" << "\n";
	//No.3 打印变量
	int a = 1;
	char b = 'b';
	char str[] = "IMissyou";
	//打印字符串用的数组名
	cout << a << "\t" << b << "\t" << str << "\n";		//字符可以用''
	//No.4 换行可以用endl替换
	cout << "换行" << endl;
}
void testCin() 
{
	int a;
	double b;
	char str[10] = "";
	cout << "请输入一个整数:";
	cin >> a;
	cout << "请输入double:";
	cin >> b;
	cout << "输入字符串:";
	cin >> str;
	cout << "请输入三个数据：";
	cin >> a >> b >> str;
	//getch();
	cout << a << "\t" << b << "\t" << str << endl;
	//cin.getline(str,199);
	//cin >> a >> " " >> b;     //错误
}
int main() 
{
	testCout();
	testCin();
	std::cout << std::endl;
	return 0;
}
```

## C++函数思想

### 内联函数

#### 什么是内联函数

内联函数就是编译完成函数的存储形式是二进制形式，是一种牺牲空间的方式提升运行效率。

#### 内联函数的特点

+ 短小精悍
+ 重复使用

#### 如何声明为内联函数

```c++
inline int Max(int a,int b)
{
    return a>b?a:b;
}
```

注意点：

+ 在结构体中或者在类中实现的函数默认为内联函数

#### 综合代码

```c++
//内联函数
inline int Max(int a,int b) 
{
	return a > b ? a : b;
}
struct MM 
{
	//默认内联
	void print() 
	{
		cout << "11" << endl;
	}
};
```

### 函数重载

#### 什么是函数重载

C++允许存在相同函数名不同参数的函数存在。(和参数返回值一点关系都没有)

#### 不同参的三个体现

+ 参数的数目不同
+ 参数的类型不同
+ 参数的顺序不同(建立在类型不同的基础上)

```C++
//函数重载
//类型不同
void print(int a, int b) 
{
	cout<<"都是整数:" << a + b << endl;
	
}
void print(char a, char b) 
{
	cout <<"都是字符：" << a + b << endl;
}
//数目不同
void print(int a, int b, int c) 
{
	cout << a + b + c << endl;
}
//顺序不同
void print(int a, double b) 
{
	cout << "顺序不同" << endl;
}
void print(double a, int b) 
{
	cout << "顺序不同" << endl;
}
```

### 函数缺省

#### 什么是函数缺省

函数缺省就是给函数形参默认初始化，就是给形参赋初始值。如果不传参，使用默认参数。

#### 函数缺省原则

+ 只能从右往左缺省，中间不能存在空的。
+ 传参的时候从左往右赋值，没有的使用默认参数
+ 多文件中，.h声明函数缺省即可，实现文件不需要缺省

#### 综合代码

```c++
//函数缺省
int Sum(int a=0, int b=0, int c=0, int d = 0) 
{
	return a + b + c + d;
}
int main() 
{
	//putimage(int x,int y,IMAGE* mm);
	//putimage(int x,int y,IMAGE* mm,int xx,int yy);
	cout << Sum() << endl;		//a=0 b=0 c=0 d=0
	cout << Sum(1) << endl;		//a=1 b=0 c=0 d=0
	cout << Sum(1, 2) << endl;	//a=1 b=2 c=0 d=0
	cout << Sum(1, 2, 3) << endl;	//a=1 b=2 c=3 d=0
	cout << Sum(1, 2, 3, 4) << endl;//a=1 b=2 c=3 d=4
	return 0;
}
```

### 综合代码

```c++
//#include "test.h"
#include <iostream>
using namespace std;
//内联函数
inline int Max(int a,int b) 
{
	return a > b ? a : b;
}
struct MM 
{
	//默认内联
	void print() 
	{
		cout << "11" << endl;
	}
};

//函数重载
//类型不同
void print(int a, int b) 
{
	cout<<"都是整数:" << a + b << endl;
	
}
void print(char a, char b) 
{
	cout <<"都是字符：" << a + b << endl;
}
//数目不同
void print(int a, int b, int c) 
{
	cout << a + b + c << endl;
}
//顺序不同
void print(int a, double b) 
{
	cout << "顺序不同" << endl;
}
void print(double a, int b) 
{
	cout << "顺序不同" << endl;
}

//函数缺省
int Sum(int a=0, int b=0, int c=0, int d = 0) 
{
	return a + b + c + d;
}
int main() 
{
	print(1, 2);
	print('A', 'B');
	//putimage(int x,int y,IMAGE* mm);
	//putimage(int x,int y,IMAGE* mm,int xx,int yy);
	cout << Sum() << endl;		//a=0 b=0 c=0 d=0
	cout << Sum(1) << endl;		//a=1 b=0 c=0 d=0
	cout << Sum(1, 2) << endl;	//a=1 b=2 c=0 d=0
	cout << Sum(1, 2, 3) << endl;	//a=1 b=2 c=3 d=0
	cout << Sum(1, 2, 3, 4) << endl;//a=1 b=2 c=3 d=4

	//testPrint();
	return 0;
}
```

## C++命名空间其他操作

先声明后实现的玩法

```c++
#include <iostream>
using namespace std;
//先声明
namespace MM 
{
	void print();
	struct Girl;
}
//外面需要用空间名做限定
void MM::print() 
{
	cout << "ILoveyou" << endl;
}
struct MM::Girl 
{
	char name[20];
	int age;
};
void printGirl(struct MM::Girl girl) 
{
	cout << girl.name << "\t" << girl.age << endl;
}
void  testMM() 
{
	struct MM::Girl girl = { "girl",18 };
	MM::print();
	cout << girl.name << "\t" << girl.age << endl;
	printGirl(girl);
}

int main() 
{
	testMM();
	return 0;
}
```

## C++起别名与类型转换

### C++起别名

```c++
	//No.1 起别名
	typedef int INT;
	INT a = 1;
	using 整数 = int;
	整数 b = 12;
	cout << b << endl;
	typedef int(*PFUNC)(int, int);
	using FUNC = int(*)(int, int);
	FUNC func = Max;
	cout << func(1, 5) << endl;
```

### 类型转换

```c++
#include <iostream>
using namespace std;

int Max(int a, int b) 
{
	return a > b ? a : b;
}
void test() 
{
	//默认转换依旧不变，支持
	int a = 1.344;
	int b = 'A';			//ASCII

	//强制类型转换
	double result = 1 / (double)2;		//C语言
	cout << result << endl;
	result = 1 / double(2);				//C++写法
	cout << result << endl;

	//专业更为安全的转换
	//static_cast<要转换的类型>(要转的的表达式)  等效强制类型转换
	int data = static_cast<int>(1.33);
	//data = int("Iloveyou");			//老写法不会报错，static_cast会报错
	//C++const类型
}
void print(char* str) 
{
	cout << str << endl;
}
void  printConst(const char* str) 
{
	cout << str << endl;
}
int main() 
{
	test();
	const char* str = "ILoveyou";		//C++对const要求更为严格

	//print("sdfsd");						//函数传参不能传入常量
	printConst("sdf");
	char str2[29] = "sdfsd";
	printConst(str2);
	//static_cast不能用来去掉const属性
	//const_cast专门用来操作const属性
	print(const_cast<char*>("sdfdfd"));
	//dynamic_cast  多态中的转换
	return 0;
}
```

### 综合代码

```c++
#include <iostream>
using namespace std;

int Max(int a, int b) 
{
	return a > b ? a : b;
}
void testType() 
{
	//No.1 起别名
	typedef int INT;
	INT a = 1;
	using 整数 = int;
	整数 b = 12;
	cout << b << endl;
	typedef int(*PFUNC)(int, int);
	using FUNC = int(*)(int, int);
	FUNC func = Max;
	cout << func(1, 5) << endl;
}

void test() 
{
	//默认转换依旧不变，支持
	int a = 1.344;
	int b = 'A';			//ASCII

	//强制类型转换
	double result = 1 / (double)2;		//C语言
	cout << result << endl;
	result = 1 / double(2);				//C++写法
	cout << result << endl;

	//专业更为安全的转换
	//static_cast<要转换的类型>(要转的的表达式)  等效强制类型转换
	int data = static_cast<int>(1.33);
	//data = int("Iloveyou");			//老写法不会报错，static_cast会报错

	//C++const类型


}
void print(char* str) 
{
	cout << str << endl;
}
void  printConst(const char* str) 
{
	cout << str << endl;
}

int main() 
{
	test();
	const char* str = "ILoveyou";		//C++对const要求更为严格

	//print("sdfsd");						//函数传参不能传入常量
	printConst("sdf");
	char str2[29] = "sdfsd";
	printConst(str2);
	//static_cast不能用来去掉const属性
	//const_cast专门用来操作const属性
	print(const_cast<char*>("sdfdfd"));
	//dynamic_cast  多态中的转换
	return 0;
}
```

## C++新数据类型

### C++bool类型

```c++
	//基本用法
	bool bNum = false;
	bNum = true;
	cout << bNum << endl;
	cout << false << endl;
	//计算机非零值表成立
	bNum = 123;
	cout << bNum << endl;

	//占用内存
	cout << sizeof(bNum) << endl;
	//结合流控制字符可以打印false和true
	cout << boolalpha << bNum << endl;
```

### C++指针

空指针的写法，C++新标准引入新的关键字描述：nullptr

```c++
	int* p = nullptr;		//等效C语言的NULL
	void* p2 = nullptr;
```

### C++引用类型

```C++
	//基本用法 --->理解为起别名
	int 女朋友 = 111;
	int& 小可爱 = 女朋友;
	小可爱 = 888;
	cout << 女朋友 << endl;
	//应用场景
	//1.充当函数返回值，增加左值使用
	//注意点: 不能返回局部变量的引用
	//returnValue() = 134;
	returnValue2() = 1222;		//returnValue2()与g_num是一个东西
	cout << g_num << endl;
	//2.充当函数参数，防止拷贝本产生
	int num = 100;
	modify2(num);			//C++引用不是指针，传参传变量即可
	cout << "num:" << num << endl;
	//3.特殊引用类型
	//3.1 常用引用
	const int cNum = 11;
	const int& c = cNum;
	print(num);
	printData(num);
	printData(123);
	//print(123);
	//3.2 右值引用
	int&& girl = 11;     //右值引用--->新语法-->规则
	printData2(1234);
	//4.指针引用
	int number = 123;
	int* p = &number;	//指针类型: 去掉变量名
	int* &pp = p;
	int number2 = 1111;
	pp = &number2;
	cout << *p << endl;
	//5.关于右值引用,C++提供一个可以把左值变成右值的函数
	int data = 1234;
	int&& data2 = move(data);		//转交所有权限
	data2 = 234;
	cout << data << endl;
	data = 1234;
```

### C++auto类型

auto叫做自动推断类型，一定要有数据作为赋值去推断，才可以使用auto

```c++
	//auto data;		//错误，没有推断的依据
	int num = 1;
	auto data = num;		//自动data的类型是int类型
	auto Func = Max;
	cout << Func(1, 4) << endl;
	struct MM mm = { 123 };
	auto pMM = &mm;
	cout << pMM->age << endl;
	auto& pNum = num;
	pNum = 123;
	cout << num << endl;
```

### C++结构体

```c++
//C++类能有的东西C++结构体都可以(构造函数，析构函数，继承)
#include <iostream>
using namespace std;
struct MM 
{
	int age;
	int num;
	//成员函数
	void print() 
	{
		cout << age << "\t" << num << endl;
		cout << "print()" << endl;
	}
	void setData(int Age, int Num) 
	{
		age = Age;
		num = Num;
	}
	int& getAge() 
	{
		return age;
	}
	int& getNum() 
	{
		return num;
	}


	void printData();
};
void MM::printData() 
{
	cout << "printData()" << endl;
}
void testStruct() 
{
	//No.1 类型上的改变， 类型不需要struct ，结构体名即可
	MM mm = {100,1001};
	cout << mm.age << "\t" << mm.num << endl;
	auto p = &mm;
	cout << p->age << "\t" << p->num << endl;
	//No.2 C++结构体中允许存在函数
	mm.print();		//mm.age  mm.num
	p->print();
	MM girl = { 200,200 };
	girl.print();	//girl.age girl.num
	//No.3 如何修改数据
	//直接访问
	mm.age = 111;
	mm.num = 1234;
	mm.print();
	//提供成员访问
	mm.setData(888, 999);
	mm.print();
	//返回引用的方式 --->C++叫做提供访问接口
	mm.getAge() = 66;
	mm.getNum() = 88;
	mm.print();					//每一步打印封装成为行为
	cout << mm.age << "\t" << mm.num << endl;
}
int main() 
{
	testStruct();
	return 0;
}
```

注意点： C++结构体一但写个构造函数，必须要按照类的方式去使用，在没有写构造函数之前和C语言的结构体一样的用法。

### C++动态内存申请

C语言内存是分为四区，C++分为五区，C语言动态内存申请是堆区，C++里面是自由存储区。

C语言是由:malloc,realloc,calloc 和free负责内存是和释放，C++中由new和delete做内存申请释放。

```c++
#include <iostream>
#include <new>
using namespace std;
void testNewOne() 
{
	//申请单个内存
	int* p = new int;	//现在自由存储区创建一个变量，把变量地址返回给p
	*p = 1234;
	cout << *p << endl;
	//申请内存并且做初始化
	int* pp = new int(1243);
	cout << *pp << endl;

	delete p;
	delete pp;
}
void testNewTwo() 
{
	//申请一段内存
	int* p = new int[4];			//申请一段内存 等效 int p[4]

	//申请一段内存并做初始化
	int* pp = new int[4]{ 1,3,4,5 };	//{data}叫做列表数据	
	for (int i = 0; i < 4; i++) 
	{
		cout << pp[i]<<"\t";
	}
	cout << endl;
	delete[] p;						//代表释放一段内存
	delete[]pp;
	//二维数组
	int** pArray = new int* [3];
	for (int i = 0; i < 3; i++) 
	{
		pArray[i] = new int[5];
	}
	for (int i = 0; i < 3; i++) 
	{
		delete[] pArray[i];
	}
	delete[] pArray;

	int(*pArray2D)[4] = new int[3][4];
	auto p2D = new int[3][4];
	delete[] pArray2D;
}
struct MM 
{
	int age;
	int num;
};
void testNewStruct() 
{
	MM* p = new MM;
	p->age = 123;
	p->num = 1234;
}
int main() 
{
	testNewOne();
	testNewTwo();
	return 0;
}
```

### C++string

目前同学掌握string的基本用法即可，不需要过多追求为什么可以。注意点头文件包含问题。

C语言是的char* 包含头文件#include <cstring>或者#include <string.h>,C++的string包含方式是#include <string>

```c++
#include <string.h>		//C语言 char*
#include <string>		//C++string
#include <iostream>
#include <cstdio>
using namespace std;
void testCreateString() 
{
	string  str;
	str = 'A';
	string str1 = "sdfsdf";
	//string str2 = 'A';  //不行
	cout << str << endl;
	cout << str1 << endl;
	string str2;
	cin >> str2;
	cout << str2 << endl;
	string str3(str2);
	cout << str3 << endl;
	string str4="ssdf";
	str4 = str3;
	cout << str4 << endl;
}
void userString() 
{
	//赋值 直接赋值
	//比较，直接用运算符比较即可
	string a = "1234";
	string b = "23";
	cout << (a < b) << endl;		//	a.compare(b);
	cout << (a == b) << endl;
	cout << (a != b) << endl;
	//...等等等其他运算符
	string result = a + b;			//字符串连接
	//a.append(b);					//调用函数的方式
	cout << result << endl;

}
void testStringFunc() 
{
	//支持下标访问
	string str = "ILoveyou";
	for (int i = 0; i < str.size(); i++) 
	{
		//cout << str[i];
		cout << str.at(i);			//等效上面的str[i]
	}
	cout << endl;
	cout << str.front() << endl;	//第一个
	cout << str.back() << endl;		//最后一个
	
	//别致的访问方式
	cout << *str.begin() << endl;
	cout << *(str.begin()+1) << endl;
	//cout << str.end() << endl;   //结尾是最后一个元素的后面不能做取*运算
	for (auto m = str.begin(); m != str.end(); m++) 
	{
		cout << *m;
	}
	cout << endl;
	//C++区间遍历，新版本for循环
	for (char v : str) 
	{
		cout << v;
	}
	cout << endl;
	int array[5] = { 1,2,3,4,5 };
	for (auto v : array) 
	{
		cout << v<<"\t";
	}
	cout << endl;
	string first = "sdfsdfsf";
	string second = "sdf";
	//C++string和C语言的char*有区别
	//把C++string转换为C语言char*
	printf("%s\n", first.data());		
	puts(first.c_str());
	//easyx 要求的都是char*
	//C++把数字转换为相应的字符串
	string test = to_string(12435);
	cout << test << endl;
	first.erase(first.begin(),first.begin()+3);
	cout << first << endl;
	first = "ILoveyousdf";
	first.substr(3);
	cout << first << endl;				//不会改变原字符串
	cout << first.substr(3) << endl;	//截取后的结果当做函数返回值
}
int main() 
{
	//testCreateString();
	userString();
	testStringFunc();
	return 0;
}
```

# C++类和对象

## 什么是类

C++当中类是一个数据类型，封装了数据以及操作。个人理解:C++类就是对事物的抽象，C++万物即可为类，和C语言的结构体一样的，是一系列事物的共同属性和行为。

## 什么是对象

对象就是类的具体化(实例化)。举个栗子:  女朋友类

抽象的过程:类      属性: 年龄 ，身份证号，姓名,三围，身高，体重....   行为:购物，看电影，做你爱做的事 

具体的过程:对象  属性的具体化

## 两个重要的概念

+ 属性:  用的数据描述属性 ，int float ,double ,char,string... 自定类型----->C++类中数据成员
+ 行为：用函数描述行为---->C++类中叫做成员函数

## C++类和对象初识

### 类的创建

```c++
class 类名
{
    public:
    protected:
    private:
};
```

### 类的权限问题

权限限定词:

+ public：公有属性
  + 函数是public属性，通常叫做公有接口
+ protected:保护属性
+ private:私有属性

权限限定是用来限定类外的对象对于类中数据的访问权限，类外只能访问public属性，C++类中默认属性是private属性。

### 对象访问数据

C++类中的一般数据和行为只能通过对象来访问。对象主要是有一下几个形式 

+ 普通对象
+ 对象数组，C++一般很少用到对象数组
+ 对象指针
  + 普通指针指向对象
  + 指针做动态内存申请

综上访问的数据有以下两种访问

+ 对象.成员
+ 对象指针->成员

## C++类中数据访问

+ C++允许在类中直接给数据做初始化
+ C++提供公有接口传参的方式做数据的访问
+ C++提供公有接口返回数据的引用做数据的访问

## C++有头链表

```c++

#include <iostream>
using namespace std;
//误区一: C++里面有类了，不需要结构体了？
//为了访问数据方便，不需要考虑权限问题，那你们可以用结构体
//struct Node 
//{
//	int data;
//	Node* next;
//};
class Node 
{
public:
	void initNode(int data) 
	{
		m_data = data;
		next = nullptr;
	}
	void printNode() 
	{
		cout << m_data << " ";
	}
	Node*& getNext() { return next; }
protected:
	int m_data;
	Node* next;
};

class List 
{
public:
	void createHead()		//创建表头
	{
		headNode = new Node;		//new一个表头节点
		headNode->getNext() = nullptr;	//把表头节点next指针置为空
	}
	void insertNode(int data)	//插入节点
	{
		Node* newNode = new Node;	//new一个新的节点
		newNode->initNode(data);	//初始化新节点数据
		//表头法插入
		newNode->getNext()=headNode->getNext();
		headNode->getNext() = newNode;
	}
	void printList() 
	{
		Node* pmove = headNode->getNext();  //从第二个节点开始
		while (pmove != NULL) 
		{
			pmove->printNode();				//调用打印节点的函数
			pmove = pmove->getNext();		//指针往下走
		}
		cout << endl;
	}
	//其他操作，自行补齐
	//插入 删除

protected:
	Node* headNode;
};

int main() 
{
	List list;
	list.createHead();
	for (int i = 0; i < 3; i++) 
	{
		list.insertNode(i);
	}
	list.printList();
	return 0;
}
```

## C++无头链表

```c++
#include <iostream>
#include <list>
using namespace std;
//记录表头和表尾的方式去写
struct Node 
{
	int data;
	Node* next;
	void print() 
	{
		cout << data << " ";
	}
	void initNode(int Data) 
	{
		data = Data;
		next = nullptr;
	}
};

class List 
{
public:
	void push_front(int data);	//头插法
	void push_back(int data);	//尾插法
	void pop_front();			//头部删除
	void pop_back();			//尾部删除
	//万金油函数
	int  size() { return m_size; }
	bool empty() { return m_size == 0; }
	//访问头节点数据和尾节点数据
	int  front() { return frontNode->data; }
	int back() { return  tailNode->data; }


	void print();
protected:
	//万金油属性
	int m_size=0;						//记录当前链表中的节点个数
	Node* frontNode = nullptr;		//起标识作用，第一个节点
	Node* tailNode = nullptr;		//最后一个节点
};
void  List::push_front(int data) 
{
	//创建节点
	Node* newNode = new Node;
	//初始化节点
	newNode->initNode(data);
	if (m_size == 0)					//当只有一个节点时候，头就是尾巴尾巴就是头		
	{
		tailNode = newNode;
		//frontNode = newNode;
		//m_size++;
	}
	else 
	{
		newNode->next = frontNode;
		//frontNode = newNode;
		//m_size++;
	}
	frontNode = newNode;
	m_size++;
}
void List::push_back(int data)
{	//创建节点
	Node* newNode = new Node;
	//初始化节点
	newNode->initNode(data);
	if (m_size == 0)
	{
		frontNode = newNode;
		//tailNode = newNode;
	}
	else 
	{
		tailNode->next = newNode;
		//tailNode = newNode;
	}
	tailNode = newNode;
	m_size++;
}
void List::pop_front() 
{
	if (m_size == 0)
		return;
	Node* nextNode = frontNode->next;
	delete frontNode;
	if (nextNode == nullptr) 
	{
		tailNode = nullptr;
	}
	frontNode = nextNode;
	m_size--;
}
void List::pop_back() 
{
	if (m_size == 0)
		return;
	if (frontNode == tailNode) 
	{
		pop_front();
	}
	else 
	{
		Node* preNode = frontNode;
		while (preNode->next != tailNode) 
		{
			preNode = preNode->next;
		}
		delete tailNode;
		preNode->next = nullptr;
		tailNode = preNode;
		m_size--;
	}
}
void List::print()
{
	Node* pmove = frontNode;
	while (pmove != NULL) 
	{
		pmove->print();
		pmove = pmove->next;
	}
	cout << endl;
}
//指定删除指定插入，自己补齐代码
int main() 
{
	List list;
	for (int i = 0; i < 3; i++) 
	{
		list.push_front(i);
	}
	list.print();
	for (int i = 0; i < 3; i++)
	{
		list.push_back(i);
	}
	list.print();
	list.pop_front();
	list.print();
	list.pop_back();
	list.print();
	//外面的一种删除的方式打印
	while (!list.empty()) 
	{
		cout << list.front() << " ";
		list.pop_front();
	}
	cout << endl;
	cout << "size:" << list.size() << endl;
	//了解
	std::list<int> mylist;
	mylist.push_back(1);
	mylist.push_back(2);
	mylist.push_front(3);
	while (!mylist.empty()) 
	{
		cout << mylist.front() << " ";
		mylist.pop_front();
	}
	cout << endl;
	cout << "size:" << mylist.size() << endl;
	return 0;
}
```

# C++构造和析构

## 构造函数

### 构造函数特性

+ 构造函数名字和类名相同
+ 构造函数没有返回值
+ 不写构造函数，每一个类中都存在默认的构造函数，默认的构造函数是没有参数
  + default显示使用默认的构造函数
  + delete 删掉默认函数
  + 当我们自己写了构造函数，默认的构造函数就不存在
+ 构造函数不需要自己调用，在构造对象的时候自己调用
  + 构造函数决定的了对象的长相
  + 无参构造函数可以构造无参对象
  + 有参构造函数，对象必须要带有参数
+ 构造函数允许被重载和缺省
+ 构造函数一般情况是公有属性
+ 构造函数一般是用来给数据成员初始化
+ 构造函数允许调用另个构造函数，必须采用初始化参数列表的写法
  + 构造函数的初始化参数列表：  构造函数名(参数1，参数2,...):成员1(参数1)，成员2(参数2)....{}

### 综合代码

```c++
#include <iostream>
#include <string.h>
using namespace std;
class MM 
{
public:
	//构造函数
	//MM() = default;			//使用的函数是默认的构造函数
	//MM() = delete;
	MM()
	{
		cout << "无参构造函数" << endl;
	}
	MM(int a) 
	{
		cout << "具有一个参数的构造函数" << endl;
	}
protected:
};
class Girl 
{
public:
	Girl() = delete;
protected:
};
class Student 
{
public:
	Student() = default;
	Student(string name, int age) 
	{
		//做初始化操作
		m_name = name;
		m_age = age;
	}
	void printStudent() 
	{
		cout << m_name << "\t" << m_age << endl;
	}
protected:
	string m_name;
	int m_age;
};
//初始化参数列表
class Test 
{
public:
	//构造函数特殊写法
	Test(int a, int b) :a(a), b(b) 
	{
	}
	Test():Test(0,0) {}				//无参构造函数调用有参构造函数
	//构造委托
	void print() 
	{
		cout << a << "\t" << b << endl;
	}
protected:
	int a=0;
	int b=0;
};
struct Data 
{
	int a;
	int b;
	int c;
	Data(int a) :a(a) {}
	Data(int a, int b, int c) :a(a), b(b), c(c) 
	{
		cout << "调用三个参数的构造函数" << endl;
	}
	void print() 
	{
		cout << a << "\t" << b << "\t" << c << endl;
	}
};
void testData() 
{
	Data data = { 1,2,3 };   //这个过程也是调用构造函数过程，{}中数据个数要和构造函数参数一致
}
void printData(Data data)    //待会研究
{
	data.print();
}
void printData2(Data& data) 
{
	data.print();
}

int main()
{
#if 0
	MM mm;
	MM girl(1);
	//Girl girl;
	//普通对象
	Student stu("npc", 18);
	stu.printStudent();
	//new一个对象
	Student* pstu = new  Student("执灯", 29);
	pstu->printStudent();

	//对象数组
	Student stuArray[3];			//无参构造函数构造
	Test test;
	test.print();

#endif
	Data data(1,2,3);
	printData(data);
	printData2(data);
	return 0;
}

```

## 析构函数

### 析构函数特性

+ 函数名等于 ~和类名
+ 析构函数没有参数，所以析构函数不能被重载也不能缺省
+ 对象死亡(生命周期结束)的最后一个事情是调用析构函数
+ 析构函数都是公有属性的
+ 什么时候写析构函数?
  + 当类的数据成员new了内存就需要自己手动写析构函数
+ 不写析构函数，也会存在一个析构函数，但是不具有释放new的内存功能

### 综合代码

```c++
#include <iostream>
using namespace std;
class MM 
{
public:
	MM() 
	{
		p = new int;
	}
	void freeMemory() 
	{
		delete p;
		p = nullptr;
	}
	~MM() 
	{
		cout << "我是析构函数" << endl;
		delete p;
		p = nullptr;
	}
protected:
	int* p;

};
int main() 
{
	{
		MM mm;
		//mm.freeMemory();
		MM* p = new MM;
		//p->freeMemory();
		delete p;				//立刻马山调用析构函数
	}
	cout << "......" << endl;
	return 0;
}
```

## 拷贝构造函数

拷贝构造函数也叫做复制构造函数。

### 拷贝构造函数特性

+ 不写拷贝构造函数，存在一个默认拷贝构造函数
+ 拷贝构造函数名和构造函数一样，算是构造函数特殊形态
+ 拷贝构造函数的唯一的一个参数就是对对象引用
  + 普通引用
  + const引用
  + 右值引用--->移动拷贝 
+ 当我们通过一个对象产生另一个对象时候就会调用拷贝构造函数

### 综合代码

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	MM() {}
	MM(MM& object) 
	{
		cout << "调用拷贝构造函数" << endl;
	}
protected:

};

class Girl 
{
public:
	Girl(string name, int age) :name(name), age(age) {}
	Girl():Girl("",0) {}
	Girl(const Girl& object) 
	{
		//构造函数就是通过一个对象赋值另一个对象
		name = object.name;
		age = object.age;
		cout << "调用拷贝构造函数" << endl;
	}
	void print() 
	{
		cout << name << "\t" << age << endl;
	}
protected:
	string name;
	int age;
};
void printGirl(Girl girl)   //Girl girl=实参
{
	girl.print();
}
void printMM(Girl& girl)
{
	girl.print();
}

void testGirl() 
{
	Girl girl("月亮", 18);
	Girl mm(girl);
	mm.print();
	Girl beauty = mm;
	beauty.print();
	cout << "传入普通变量" << endl;
	printGirl(girl);
	cout << "传入引用" << endl;
	printMM(girl);
	//匿名对象的拷贝构造函数
	//匿名对象是右值，右值引用
	Girl test=Girl("匿名", 18);	
}

class Boy 
{
public:
	Boy(string name, int age) :name(name), age(age) {}
	Boy(Boy&& object)		//右值引用
	{
		name = object.name;
		age = object.age;
		cout << "右值引用的拷贝构造" << endl;
	}
	Boy(Boy& object) 
	{
		name = object.name;
		age = object.age;
		cout << "普通拷贝构造" << endl;
	}
protected:
	string name;
	int age;
};
void testBoy() 
{
	cout << ".............." << endl;
	Boy boy("boy", 18);
	Boy gg = boy;						//调用普通的对象
	Boy coolman = Boy("sdfd", 28);		//右值引用的拷贝构造函数
	//没有打印结果，IDE做了优化，看不到
}

int main() 
{
	MM mm;
	MM girl = mm;				//会调用拷贝构造函数
	//string str = "sdfsd";
	//string str2(str);
	//string str3 = str2;
	MM beauty(girl);			//会调用拷贝构造函数
	//误区
	MM  npc;
	npc = girl;					//运算符重载
	testGirl();
	testBoy();
	return 0;
}
```

### 深浅拷贝问题

深浅拷贝只在类中存在指针，并且做了内存申请的，才会存在引发析构问题(内存释放问题)

+ 默认的拷贝构造都是浅拷贝
+ 拷贝构造函数中做普通的赋值操作也是浅拷贝

```c++
#include <iostream>
#include <cstring>
using namespace std;
class MM
{
public:
	MM(const char* str, int num)
	{
		int length = strlen(str) + 1;
		name = new char[length];
		strcpy_s(name, length, str);
		age = num;
	}
	MM(const MM& object) 
	{
		//深拷贝
		int length = strlen(object.name) + 1;	//有一个字符串结束标记\0
		name = new char[length];
		strcpy_s(name, length, object.name);
		age = object.age;
	}
	~MM() 
	{
		if (name != nullptr) 
		{
			delete[] name;
			name = nullptr;
		}
	}
protected:
	char* name;
	int age;
};
void testQuestion()
{
	MM mm("月亮",19);
	MM girl = mm;
}

int main() 
{
	testQuestion();
	return 0;
}
```

## 构造和析构顺序问题

+ 一般情况构造顺序和析构顺序是相反的
+ new对象，调用delete直接被释放
+ static对象，最后释放

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	MM(string info = "A") :info(info)
	{	
		cout << info;
	}
	~MM() 
	{
		cout << info;
	}
protected:
	string info;
};
void testOrder() 
{
	MM mm1("B");			//B
	static MM mm2("C");		//C			//最后释放 C
	MM* p = new MM("D");	//D
	delete p;				//D
	MM arr[3];				//AAA
							//AAABC
}
int main() 
{
	testOrder();
	return 0;
}
```

## C++类的组合

一个类包含另一个类的对象为数据成员叫做类的组合。当多种事物是一个事物的一部分 ，采用组合类来完成描述，C++中组合的使用优先与继承。

注意点: 类不能包含自身的对象。

+ 组合类的构造函数，必须要采用初始化参数列表的方式调用分支类的构造函数
+ 组合类的构造顺序:先构造分支类，分支类的顺序只和声明顺序，和初始化参数列表一点毛线关系。

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	MM() 
	{
		cout << "构造mm" << endl;
	}
	MM(string name) :name(name) {}
	void print() 
	{
		cout <<"MM:" << name << endl;
	}
protected:
	string name;
};
class GG 
{
public:
	GG() 
	{
		cout << "构造gg" << endl;
	}
	GG(int age,string name) 
	{
		m_age = age;
		m_name = name;
	}
	void print() 
	{
		cout <<"gg:" << m_name << " " << m_age << endl;
	}
protected:
	int m_age;
	string m_name;
};
class Family
{
public:
	Family(string mmName,string ggName,int age) : mm(mmName), gg(age, ggName)
	{

	}
	//但是分支类中必须存在无参的构造函数
	Family() 
	{
		cout << "构造组合类" << endl;
	}
	void print() 
	{
		gg.print();
		mm.print();
	}
protected:
	GG gg;
	MM mm;
};
int main() 
{
	Family family("mm","gg",19);
	family.print();
	cout << "................." << endl;
	Family object;
	cout << "................." << endl;
	object.print();

	return 0;
}
```

## C++类中类

类中类的访问问题以及类中类先声明后定义的写法

+ 类中类依旧受权限限定
+ 访问必须要类名::剥洋葱的方式访问

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	MM() 
	{
		cout << "构造mm" << endl;
	}
	MM(string name) :name(name) {}
	void print() 
	{
		cout <<"MM:" << name << endl;
	}
protected:
	string name;
};
class GG 
{
public:
	GG() 
	{
		cout << "构造gg" << endl;
	}
	GG(int age,string name) 
	{
		m_age = age;
		m_name = name;
	}
	void print() 
	{
		cout <<"gg:" << m_name << " " << m_age << endl;
	}
protected:
	int m_age;
	string m_name;
};
class Family
{
public:
	Family(string mmName,string ggName,int age) : mm(mmName), gg(age, ggName)
	{
	}
	//但是分支类中必须存在无参的构造函数
	Family() 
	{
		cout << "构造组合类" << endl;
	}
	void print() 
	{
		gg.print();
		mm.print();
	}
protected:
	GG gg;
	MM mm;
};
class List 
{
public:
	List() 
	{
		cout << "外面的构造函数" << endl;
	}
protected:

public:
	//类中类--->依旧受权限限定
	class iterator 
	{
	public:
		iterator() 
		{
			cout << "类中类构造函数" << endl;
		}
		void print() 
		{
			cout << "类中类函数" << endl;
		}
	protected:

	};
};
void testList() 
{
	List::iterator iter;
	iter.print();
}
int main() 
{
	Family family("mm","gg",19);
	family.print();
	cout << "................." << endl;
	Family object;
	cout << "................." << endl;
	object.print();
	testList();
	return 0;
}
```

# C++特殊成员

## const数据成员

+ 不能被修改const数据成员
+ 初始化必须采用初始化参数列表

## const成员函数

+ 写法上比较特殊的写法， const修饰函数，写在函数的后面
+ const函数和普通函数可以共存
  + 普通对象优先调用普通函数
  + 常对象只能调用常成员函数
+ const函数不能修改数据成员

## const对象

+ 常对象只能调用常成员函数

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	MM(string Name,int Num) :num(Num)
	{
		name = Name;
		//num = Num;		//错误，const数据只能通过初始化参数列表做初始化
	}
	void print() 
	{
		//num = 123;		//错误，const数据不能被修改
		cout << name << "\t" << num << endl;
	}
protected:
	const int num;
	string name;
};
class Girl 
{
public:
	Girl(string name, int age) :name(name), age(age){}
	void print() const					//常成员函数
	{
		//name = "sfsf";				//错误，常成员函数不能修改数据成员
		cout << "常对象只能调用常成员函数" << endl;
		cout << name << "\t" << age << endl;
	}
	void print() 
	{
		cout << "普通对象优先普通函数" << endl;
		cout << name << "\t" << age << endl;
	}
	void printData() 
	{
		cout << "普通函数" << endl;
	}
protected:
	string name;
	int age;
};
int main() 
{
	MM mm("name", 1001);
	mm.print();

	Girl girl("girl", 1002);
	girl.print();
	const Girl beauty("mm", 1003);
	beauty.print();
	//beauty.printData();				//错误   常对象只能调用常成员
	return 0;
}
```

## this指针

+ 用来在类中表示对象本身
+ 避免名字同名问题，用来区分参数和数据成员

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	MM(string name, int age) 
	{
		//this可以区分参数和数据成员
		this->name = name;
		this->age = age;
		//this = nullptr;
	}
	void print() 
	{
		cout << this->name << " " << this->age << endl;
	}
	//函数返回对象
	MM GetMM() 
	{
		return *this;
	}
	//函数返回对象指针
	MM* GetMMPoint() 
	{
		return this;
	}
protected:
	string name;
	int age;
};
int main() 
{
	MM mm("mm",18);
	mm.print();					//this表示mm的地址
	MM girl("girl", 28);
	girl.print();
	//语法上OK 没有实际含义
	mm.GetMM().GetMM().GetMM().GetMM().GetMM().print();
	mm.GetMMPoint()->GetMMPoint()->GetMMPoint()->print();

	return 0;
}
```

## 静态成员

static修饰数据或者函数，叫做静态成员，静态成员不属于对象，属于类，所有对象的公有的。

+ 静态依旧受权限限定
+ 静态成员访问
  + 通过对象访问
  + 直接类名限定访问
+ 静态数据必须在类外做初始化，类初始化不需要static修饰
+ 静态成员函数
  + 不能直接访问非静态数据成员，必须要通过对象去访问。
  + 静态成员函数中没有this指针(不能使用this指针)

```c++
#include <iostream>
#include <string>
using namespace std;
class Login 
{
public:
	Login(string name) :name(name)
	{
		count++;
		cout << "登录成功" << endl;
	}
protected:
	string name;
public:
	//static int count=0			//错误 ，必须在类外做初始化
	static int count;				//静态数据成员
};
int Login::count = 0;				//类外初始化

class Girl 
{
public:
	Girl(string name) :name(name) {}
	static void printData()			//静态成员函数
	{
		//this->name = "dsfd";				//错误写法，静态成员函数没有this指针
		cout << "静态成员函数" << endl;
		//cout << name << endl;				//错误 ，静态成员函数不能直接访问非静态数据成员
		cout << "count:" << count << endl;	//静态成员函数可以直接访问静态数据成员

	}
	static void print(Girl& girl) 
	{
		cout << girl.name << "\t" << girl.count << endl;
		Girl mm("mm");
		cout << mm.name << "\t" << mm.count << endl;
	}

protected:
	string name;
	static int count;
};
int Girl::count = 0;

int main() 
{
	Login login("小美");
	cout << Login::count << endl;
	cout << login.count << endl;
	Login mm("月亮");
	cout << Login::count << endl;
	//静态数据是所有对象共有的
	cout << mm.count << endl;
	cout << login.count << endl;
	cout << "当前游戏人数:" << Login::count << endl;

	Girl girl("girl");
	girl.printData();
	Girl::printData();
	Girl::print(girl);
	static Girl sgirl("static");			//释放是最后释放
	return 0;
}
```

## C++友元

c++友元代表是一种关系，一种无视类的权限限定的关系，C++友元关系用friend关键字描述

+ 友元函数
+ 友元类

友元关系只是单纯提供一个场所，赋予对象具有无视权限的功能。打破类的封装性

### 友元函数

+ 普通函数成为友元
+ 另一个类的成员函数成为友元函数
+ 友元函数不属于类，就是一个外部函数。

```c
#include <iostream>
using namespace std;
class MM 
{
public:
	void print() 
	{
		cout << "见了一个面" << endl;
	}
	friend void hotel();				//用friend修饰的函数叫做友元函数
	friend void house(MM& girl);
protected:
	string name="mm";
private:
	int age=18;
};
//类外实现不需要friend了，不需要类名限定
void hotel() 
{
	MM mm;
	mm.print();
	cout << mm.name << "\t" << mm.age << endl;
}
void house(MM& girl) 
{
	girl.print();
	cout << girl.name << "\t" << girl.age << endl;
}
//另一个类的成员函数成为友元函数  知道有这么回事即可
class B
{
public:
	void printA();
protected:

};
class A 
{
public:
	friend void B::printA();
protected:
	int a=1234;
};

void B::printA()
{
	A aObject;
	cout << aObject.a << endl;
}
int main() 
{
	hotel();
	MM girl;
	girl.print();
	//类外无法访问类中的保护和私有属性
	//cout << girl.name << "\t" << girl.age << endl;
	house(girl);

	B b;
	b.printA();
	return 0;
}
```

### 友元类

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
	friend class Boy;
public:
	void printMM()
	{
		cout << "MM" << endl;
	}
protected:
	string name = "MM";
};

class Boy 
{
public:
	void printBoy() 
	{
		mm.printMM();
		cout << mm.name << endl;			//无视权限
	}
	void printData() 
	{
		MM girl;
		cout << girl.name << endl;			//无视权限
	}
	void print(MM& mm) 
	{
		cout << mm.name << endl;
	}
protected:
	MM mm;
};

//互为友元
class A 
{
public:
	friend class B;
	void printA();
protected:
	int a = 1;
};
class B 
{
public:
	friend class A;
	void printB() 
	{
		A aObject;
		cout << aObject.a << endl;
	}
protected:
	int b = 2;
};
void A::printA() 
{
	B bObject;
	cout << bObject.b << endl;
}
int main() 
{
	Boy boy;
	MM mm;
	boy.print(mm);

	B bObject;
	bObject.printB();


	return 0;
}
```

# C++运算符重载

## 运算符重载基础

C++运算符重载是赋予运算符具有操作对象的功能。

```c++
#include <iostream>
using namespace std;
class Data 
{
public:
	Data(int first, int second) :first(first), second(second) {}
	void print() 
	{
		cout << first << ":" << second << endl;
	}
protected:
	int first;
	int second;
};
int main()
{
	Data data1(1, 2);
	Data data2(2, 3);
	//错误，+不能直接操作自定义类型
	//Data result = data1 + data2;
	return 0;
}
```

对于C++运算符重载的本质就是函数调用， 所以运算符重载函数如何编写最为重要

+ 函数返回值: 当前运算符运算结束后产物类型 ,int a,int b, a+b  返回值 int
+ 函数名:  operator和运算符组成函数名
+ 函数参数
  + 运算符重载函数是类中成员函数: 函数参数等于操作数-1
  + 运算符重载函数是友元函数: 函数参数等于操作数
+ 函数体: 写运算符的实际想要的运算即可
+ C++ 每个类中存在一个赋值的重载函数

```c++
#include <iostream>
using namespace std;
class Data 
{
public:
	Data() {}
	Data(int first, int second) :first(first), second(second) {}
	void print() 
	{
		cout << first << ":" << second << endl;
	}
	//运算符重载函数是类成员函数
	Data operator+(Data& data) 
	{
		/*
		Data result = Data(this->first + data.first, this->second + data.second);
		return result;
		*/
		//等效下面四行函数
		/*
		
		Data result;
		result.first = this->first + data.first;
		result.second = this->second + data.second;
		return result;
		
		*/
		return Data(this->first + data.first, this->second + data.second);
	}
	friend Data operator+=(Data& data1, Data& data2);


protected:
	int first;
	int second;
};
Data operator+=(Data& data1, Data& data2) 
{
	data1.first += data2.first;
	data1.second += data2.second;
	return data1;
}
int main()
{
	Data data1(1, 2);
	Data data2(2, 3);
	//错误，+不能直接操作自定义类型
	//重载函数隐式调用
	Data result = data1 + data2;		//拷贝构造函数不写存在默认的
	//类成员函数重载本质是把data1 + data2 解析为 data1.operator+(data2);
	//重载函数显式调用
	Data result2 = data1.operator+(data2);
	result2.print();
	result.print();
	Data data3;
	data3=data3 + data1;
	int a = 1;
	a = a + 3;
	//友元重载
	Data data4(1, 4);
	Data data5(3, 5);
	data4 += data5;		//解析为 operator+=(data4, data5);
	data4.print();
	Data returnObject=operator+=(data4, data5);
	//函数返回值类型:Data 
	//函数名: operator+
	returnObject.print();
	return 0;
}
```

## C++特殊运算符重载

+ . =  () ->  []  只能重载为类成员函数
+ 运算符重载必须存在至少一个自定义类型才能重载
+ .   .*  ?:   ::  不能被重载
+ C++只允许重载已有运算符，不能无中生有
+ 习惯行为: 单目运算符采用类的成员函数重载，双目运算符采用友元重载

### ++ 和--运算符的重载

对于++和--重载 通过增加无用参数(int) 标识为后置运算

```c++
#include <iostream>
#include <string>
using namespace std;
class MM
{
public:
	MM(string name = "", int money = 0) :name(name), money(money) {}
	void print()
	{
		cout << name << "\t" << money << endl;
	}
	MM operator++()				//前置的
	{
		this->money++;
		return *this;
	}
	MM operator++(int)			//int 只有标识作用
	{
		return MM(this->name, this->money++);
	}


protected:
	string name;
	int money;
};

int main() 
{
	MM mm("月亮", 100);
	cout << "前置实现" << endl;
	MM result = ++mm;
	result.print();
	mm.print();
	cout << "后置实现" << endl;
	result = mm++;
	result.print();
	mm.print();

	return 0;
}
```

### C++流对象重载

cout本质是一个类的对象: ostream,cin本质也是一个类对象: istream

+ 流重载必须要用友元方式重载
+ 流重载尽量用引用类型

```c++
#include <iostream>
#include <string>
using namespace std;
class MM
{
public:
	MM(string name = "", int money = 0) :name(name), money(money) {}
	void print()
	{
		cout << name << "\t" << money << endl;
	}
	MM operator++()				//前置的
	{
		this->money++;
		return *this;
	}
	MM operator++(int)			//int 只有标识作用
	{
		return MM(this->name, this->money++);
	}
	//流重载
	//cout << mm;
	friend ostream& operator<<(ostream& out, MM& object);
	//cin >> mm;
	friend istream& operator>>(istream& in, MM& object);
protected:
	string name;
	int money;
};
ostream& operator<<(ostream& out, MM& object) 
{
	out << "美女信息:" << endl;
	out << object.name << "\t" << object.money << endl;
	return out;
}
istream& operator>>(istream& in, MM& object) 
{
	cout << "请输入美女信息:" << endl;
	in >> object.name >> object.money;
	return in;
}
int main() 
{
	MM mm("月亮", 100);
	cin >> mm;
	cout << mm;
	return 0;
}
```

### C++文本重载

所谓的文本重载，就是重载后缀，固定写法 

+ 函数参数:一定是：unsigned long long
+ 函数名: operator "" 要重载的后缀    ---->一般重载后缀采用下换线系列
  + 一个运算符或者一个后缀只能重载被重载

```c++
//文本重载
unsigned long long  operator"" _h(unsigned long long num) 
{
	return num * 3600;
}
unsigned long long  operator"" _s(unsigned long long num)
{
	return num;
}
unsigned long long  operator"" _min(unsigned long long num)
{
	return num*60;
}
int main()
{
    int data = 1_h + 10_min + 50_s;
	cout << data << endl;
	return 0;    
}
```

### C++operator实现隐式转换

所谓是隐式转换就是可以让对象直接赋值给普通数据

```c++
operator 隐式转换的类型 ()
{
    return 数据;
}
```

### 综合代码

```c++
#include <iostream>
#include <string>
#include <chrono>
using namespace std;
class MM
{
public:
	MM(string name = "", int money = 0) :name(name), money(money) {}
	void print()
	{
		cout << name << "\t" << money << endl;
	}
	MM operator++()				//前置的
	{
		this->money++;
		return *this;
	}
	MM operator++(int)			//int 只有标识作用
	{
		return MM(this->name, this->money++);
	}
	//流重载
	//cout << mm;
	friend ostream& operator<<(ostream& out,const MM& object);
	//cin >> mm;
	friend istream& operator>>(istream& in, MM& object);

	//隐式转换--->便捷获取数据成员的接口
	operator int() 
	{
		return this->money;
	}
	operator string() 
	{
		return this->name;
	}
protected:
	string name;
	int money;
};
ostream& operator<<(ostream& out, MM& object) 
{
	out << "美女信息:" << endl;
	out << object.name << "\t" << object.money << endl;
	return out;
}
istream& operator>>(istream& in, MM& object) 
{
	cout << "请输入美女信息:" << endl;
	in >> object.name >> object.money;
	return in;
}

//文本重载
unsigned long long  operator"" _h(unsigned long long num) 
{
	return num * 3600;
}
unsigned long long  operator"" _s(unsigned long long num)
{
	return num;
}
unsigned long long  operator"" _min(unsigned long long num)
{
	return num*60;
}

int main() 
{
	MM mm("月亮", 100);
	cout << "前置实现" << endl;
	MM result = ++mm;
	result.print();
	mm.print();
	cout << "后置实现" << endl;
	result = mm++;
	result.print();
	mm.print();


	string str = "sdfsdf";
	cout << str << endl;			//cout << str
	
	//cin >> mm;
	//cout << mm;

	cout << 1_h << endl;

	int data = 1_h + 10_min + 50_s;
	cout << data << endl;

	int money = mm;
	cout << money << endl;
	string name = mm;
	cout <<name << endl;

	return 0;
}
```

## 运算符的应用场景

+ 迭代器实现：让对象模拟指针的行为
+ 函数包装器：把函数指针包装成为一个对象
+ 智能指针： 可以实现内存的自动申请和释放

```c++
#include <iostream>
#include <string>
#include <list>
#include <new>
#include <functional>
using namespace std;

//No.1 迭代器
struct Node 
{
	int data;
	Node* next;
	Node(int data = 0) :data(data), next(nullptr) {}
};

class List 
{
public:
	List() 
	{
		frontNode = nullptr;
		tailNode = nullptr;
		curSize = 0;
	}
	void push_front(int data) 
	{
		Node* newNode = new Node(data);
		if (curSize == 0)
			tailNode = newNode;
		else
			newNode->next = frontNode;
		frontNode = newNode;
		curSize++;
	}
protected:
	Node* frontNode;
	Node* tailNode;
	int curSize;

public:
	//迭代器部分
	class iterator 
	{
	public:
		iterator(Node* pmove = nullptr) :pmove(pmove) {}
		bool operator!=(const iterator& object) const
		{
			return this->pmove != object.pmove;
		}
		iterator operator++() 
		{
			pmove = pmove->next;
			return iterator(pmove);
		}
		int operator*() 
		{
			return pmove->data;
		}
	protected:
		Node* pmove;
	};
public:
	iterator begin() 
	{
		return iterator(frontNode);
	}
	iterator end() 
	{
		return iterator(nullptr);
	}
};

//No.2 函数包装器
class Func 
{
	using PF = void(*)();
public:
	Func(PF pf) :pf(pf) {}
	void operator()() 
	{
		pf();
	}
protected:
	PF pf;
};
void print() 
{
	cout << "函数包装器的测试代码" << endl;
}

//No.3 智能
//通过对象死亡会自动调用析构函数
class Auto_ptr 
{
public:
	Auto_ptr(int* ptr) :ptr(ptr) {}
	~Auto_ptr() 
	{
		if (ptr != nullptr) 
		{
			delete ptr;
			ptr = nullptr;
		}
	}
	int* operator->() 
	{
		return this->ptr;
	}
	int operator*() 
	{
		return *this->ptr;
	}
protected:
	int* ptr;
};

int main() 
{
#if 0

	string str = "ILoveyou";
	string::iterator iter;
	cout << "第一个元素:" << *str.begin() << endl;
	cout << "最后一个二元素:" << *(str.end()-1) << endl;			//*str.end() 是错误的
	for (iter = str.begin(); iter != str.end(); iter++)
	{
		cout << *iter << " ";
	}
	cout << endl;
	List list;
	list.push_front(1);
	list.push_front(2);
	list.push_front(3);
	List::iterator iterList;
	for (iterList = list.begin(); iterList != list.end(); ++iterList)
	{
		cout << *iterList << " ";
	}
	cout << endl;
#endif


	//模版---->这看不懂没关系，后面会讲
	//std::list<int> my;
	//my.push_front(1);
	//my.push_front(2);
	//my.push_front(3);
	//std::list<int>::iterator stdIter;
	//for (stdIter = my.begin(); stdIter != my.end(); ++stdIter)
	//{
	//	cout << *stdIter << " ";
	//}

	Func object(print);
	object();					//通过对象调用函数


	//模版---->这看不懂没关系，后面会讲
	function<void()> object2(print);
	object2();


	Auto_ptr p(new int(1234));
	cout << *p << endl;

	//模版---->这看不懂没关系，后面会讲
	unique_ptr<int> stdp(new int(1234));
	cout << *stdp << endl;

	return 0;
}
```

# C++继承

C++继承 代表父类属性在子类中会存在一份。理解起来理解为生物学的继承即可，子承父业，传承血脉

继承 子类中不会产生新的属性，派生子类会有新属性产生。继承中分为父类和子类，派生分为基类和派生类。

## C++继承的基本语法

```c++
class 父类{};
class 子类名:继承方式 父类名
{
	
};
//继承方式
//所谓的权限限定词
//public protected private
//公有继承  保护继承  私有继承
```

## C++继承中的两个难点

+ 继承中权限问题： 代表就是继承下来的属性在子类当中的呈现

  | 继承方式  | public继承 | protected继承 | private继承 |
  | --------- | ---------- | :------------ | ----------- |
  | public    | public     | protected     | private     |
  | protected | protected  | protected     | private     |
  | private   | 不可访问   | 不可访问      | 不可访问    |

  + 继承方式只能增强权限
  + 父类当中私有属性，无论采用什么继承方式，子类都可以直接访问

+ 继承中的构造函数

  + 继承下来的属性必须要通过父类的构造函数去初始化
  + 子类的构造函数必须要采用初始化参数列表的方式调用父类的构造函数
  + 构造顺序:优先构造父类，在构造在类

```c++
#include <iostream>
using namespace std;
//权限问题
class MM				//父类
{
public:
	string name;
	void print() {}
protected:
	int age;
private:
	int num;
};
class Girl :public MM	//子类
{
public:
	//	string name;
	//	void print() {}
	void printGirl() 
	{
		cout << name << "\t" << age << endl;
		//cout << num << endl;			//错误的，私有属性不能被访问
	}
protected:
	//	int age;
private:
	//	int num;  不可访问
};

class Boy :protected MM 
{
public:
	void printBoy() 
	{
		cout << name << "\t" << age << endl;
		//cout<<num<<endl;					//错误的
	}
protected:
	//	string name;
	//	void print() {}
	//	int age;
private:
	//	int num;  不可访问
};

class GG :private MM 
{
public:
	void printGG() 
	{
		cout << name << "\t" << age << endl;
	}
protected:

private:
	//	string name;
	//	void print() {}
	//	int age;
	//	int num;				//不可访问的
};
//构造函数写法
class Father 
{
public:
	Father() { cout << "构造father" << endl; }
	Father(string name, int money) :name(name), money(money) {}
	void printFather() 
	{
		cout << name << "\t" << money << endl;
	}
	string GetName() 
	{
		return name;
	}
protected:
	int money;
private:
	string name;
};
class Son :public Father 
{
public:
	Son()					//子类想要这种构造函数，父类必定存在一个无参构造函数
	{
		cout << "构造son" << endl;
	}
	Son(string name, int money, int num) :Father(name, money)
	{
		this->num = num;				//这个东西初始化没有要求
	}
	void printSon() 
	{
		//私有属性不能直接访问，但是可以通过父类的方法访问
		cout << GetName() << "\t" << money << "\t" << num << endl;
	}
protected:
	int num;
};

int main() 
{
	Girl girl1;
	girl1.name = "sdfd";
	girl1.print();
	//girl1.age = 12;					//保护属性
	Boy boy;
	//boy.name = "sdfds";				//继承方式只会增强权限


	Son son;
	Son son2("老汉儿", 100, 1001);
	son2.printSon();

	return 0;
}
```

## C++多继承

### 简单多继承

存在2个或者是2个以上的父类称之为多继承

+ 构造顺序问题： 只和继承顺序有关，和初始化参数列表的顺序一点关系没有

```c++
#include <iostream>
using namespace std;
//欧皇
//阳倩
//欧阳锋
class MM 
{
public:
	MM(string firstMMName, string secondMMName) 
	{
		this->firstMMName = firstMMName;
		this->secondMMName = secondMMName;
	}
protected:
	string firstMMName;
	string secondMMName;
};
class GG 
{
public:
	GG(string firstGGName, string secondGGName) :firstGGName(firstGGName), secondGGName(secondGGName)
	{

	}
protected:
	string firstGGName;
	string secondGGName;
};
class Son :public MM, protected GG 
{
public:
	Son(string firstGGName,string secondGGName,
		string firstMMName,string secondMMName,
		string secondSonName) :GG(firstGGName,secondGGName),MM(firstMMName,secondMMName)
	{
		this->firstSonName = firstGGName + firstMMName;
		this->secondSonName = secondSonName;
	}
	void printName() 
	{
		cout << (firstSonName + secondSonName) << endl;
	}
protected:
	string firstSonName;
	string secondSonName;
};
int main() 
{
	Son son("欧", "皇", "阳", "倩", "锋");
	son.printName();
	return 0;
}
```

### 菱形继承

继承无论被继承多少次，属性一致都在，所以一般类不能被继承很多层。继承太多次数，会导致子类臃肿

```c++
/*
		A
		
	B		 C

		D
D中A的属性，必须调用A的构造函数初始化
*/

#include <iostream>
using namespace std;
class A 
{
public:
	A(int a) :a(a) {}
protected:
	int a;
};
class B :virtual public A 
{
public:
	B(int a, int b) :A(a), b(b) {}
protected:
	int b;
};
class C :virtual public A 
{
public:
	C(int a,int c):A(a),c(c){}
protected:
	int c;
};
class D :public B, public C 
{
public:
	D(int a, int b, int c, int d) :B(a, b), C(a, c), A(a) {}
	D() :B(1, 2), C(3, 4), A(5) {}
	void print() 
	{
		cout << a << endl;
		//虚继承的目的就是为了让孙子类只保留一份爷爷类的属性
		cout << A::a << endl;
		cout << B::a << endl;
		cout << C::a << endl;
	}
protected:
	int d;
};

int main() 
{

	D  d(1, 2, 3, 4);
	d.print();

	D d2;
	d2.print();

	return 0;
}

```

### C++继承中的同名问题

+ 没有用类名限定的基础上，就近原则，在哪个类里面调用那个类的方法
+ 用类名限定，可以访问指定类中的成员
+ 类指针被子类对象初始化
  + 父类没有virtual ，就看指针类型
  + 有virtual ，看对象类型

```c++
#include <iostream>
using namespace std;
class MM 
{
public:
	void print() 
	{
		cout << "MM::print" << endl;
	}
protected:
	string name="MM";
};
class Son :public MM 
{
public:
	void print() 
	{
		cout << "Son::print" << endl;
		cout << name << endl;	//就近原则
		cout << MM::name << endl;
	}
	void printData() 
	{
		print();
	}
protected:
	string name="son";			//就近原则
};
int main() 
{
	//正常调用--->就近原则
	Son son;
	son.print();
	son.printData();
	Son* pSon = new Son;
	pSon->print();				//覆盖 --->正常情况调用，无法访问到父类的同名方法
	pSon->MM::print();			//类名限定调用相应类函数
	//非正常调用
	MM* pFather = new Son;		//C++允许父类指针被子类对象初始化
	pFather->print();			//父类中没有virtual修饰的时候，看指针类型，有virtual看对象类型
	//pFather->printData();		//错误，父类指针不能访问子类中父类没有属性
	//注意点: 子类指针被父类对象初始化，有危险。一般不被允许
	return 0;
}
```

# C++虚函数和多态

## 什么是虚函数

C++类中用virtual修饰函数虚函数,构造函数没有虚构造函数，存在虚析构函数，C++所有函数 都是一个指针去存储的，所以具有虚函数的类，内存会增加一个指针大小的内存。

#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:
	virtual void print() 
	{
		cout << "我是一个虚函数" << endl;
	}
	virtual void printData() 
	{
		cout << "我是第二个虚函数" << endl;
	}
protected:
};
class Boy :public MM 
{
public:
	void print() 
	{

​	}
protected:

};

int main() 
{
	MM mm;
	cout << "MM:" << sizeof(MM) << endl;
	//下面的东西了解可以，不用过于纠结
	long long** p = (long long**) & mm;
	using FUNC = void(*)();
	FUNC pf1 = (FUNC)p[0][0];
	pf1();
	FUNC pf2 = (FUNC)p[0][1];
	pf2();
	return 0;
}

## 纯虚函数

纯虚函数也是虚函数一种，只是没有函数体，怎么表示没有函数体

+ 纯虚函数--->虚函数=0;
+ 具有一个或者多个纯虚函数的类叫做抽象类
  + 抽象类不能构建对象
  + 但是可以构建对象指针

```c++
#include <iostream>
using namespace std;
class MM 
{
public:
	virtual void print() = 0;			//纯虚函数
protected:

};

int main() 
{
	//MM mm;							//抽象类不能构建对象
	MM* pmm = nullptr;
	return 0;
}
```

## C++多态

多态指的是因为指针的不同对象的赋值操作所导致的统一行为的不同结果。多态的这个概念的东西不太重要，重要的是什么样情况调用什么样的行为。

+ 正常指针和正常对象调用行为，就近原则
+ 父类指针被子类对象初始化
  + 函数有virtual 看对象类型
  + 函数没有virtual 看指针类型
+ final关键字 禁止子类重写父类方法
+ override 显示说明当前函数重写函数

```c++
#include <iostream>
using namespace std;
class MM 
{
public:
	virtual void print() 
	{
		cout << "美女上厕所" << endl;
	}
	void printData() 
	{
		cout << "美女" << endl;
	}
	virtual void print2() final 
	{
		cout << "final 禁止重写" << endl;
	}
};
class GG :public MM 
{
public:
	void print() override					//重写
	{
		cout << "帅哥上厕所" << endl;
	}
	void printData()
	{
		cout << "帅哥" << endl;
	}
	//void print2()    //错误，父类禁止重写
	//{

	//}
protected:
};

int main() 
{
	//正常调用，就近原则
	GG gg;
	gg.print();
	gg.printData();
	MM mm;
	mm.print();
	mm.printData();
	GG* pGG = new GG;
	pGG->print();
	pGG->printData();
	MM* pMM = new MM;
	pMM->print();
	pMM->printData();
	//非正常调用
	MM* p = new GG;
	p->print();				//函数有virtual看对象  一号行为
	p->printData();			//函数没有virtual看指针类型
	p = &mm;
	p->print();				//二号行为
	return 0;
}
```

多态的两个必要性条件

+ 父类中存在虚函数
+ 存在不正常指针的引用(不正赋值关系)
+ public继承

## 纯虚函数和ADT过程

ADT: abstract data type  抽象数据类型  主要是通过继承抽象类中，子类必须要实现父类的抽象方法，子类才可以创建对象。

```c++
#include <iostream>
#include <string>
using namespace std;
class MM 
{
public:

protected:
	string name;
	int age;
};

class MMSystem 
{
public:
	virtual void insertData(MM data) = 0;
	virtual void printData() = 0;
	virtual bool empty() const = 0;
	virtual int size() const = 0;
};
class List :public MMSystem
{
public:
	void insertData(MM data) 
	{

	}
	void printData()
	{

	}
	bool empty() const 
	{
		return false;
	}
	int size() const 
	{
		return 0;
	}
protected:

};
class Array :public MMSystem 
{
public:
	void insertData(MM data)
	{

	}
	void printData()
	{

	}
	bool empty() const
	{
		return false;
	}
	int size() const 
	{
		return 0;
	}
protected:

};
int main() 
{
	MMSystem* pmm = new List;
	MM mm;
	pmm->insertData(mm);
	pmm->printData();
	cout << pmm->empty() << endl;

	MMSystem* pmm2 = new Array;
	pmm2->insertData(mm);
	pmm2->printData();
	cout << pmm2->empty() << endl;

	return 0;
}
```

## 虚析构函数

virtual修饰的析构函数就是虚析构函数，当存在子类对象初始化父类指针的时候，父类析构函数就是要虚析构函数。

```c++
#include <iostream>
using namespace std;
class MM 
{
public:
	virtual ~MM() 
	{
		cout << "MM:" << endl;
	}
};
class Girl :public MM 
{
public:
	~Girl() 
	{
		cout << "Girl:" << endl;
	}
};
int main() 
{
	MM* p = new Girl;		//子类对象初始化父类指针的时候，父类的析构函数要用virtual修饰
	delete p;
	return 0;
}
```

## dynamic_cast 类型转换

+ 上行转换  子类到父类   和 static_cast 差不多
+ 下行转换  父类到子类   dynamic_cast 更为安全
+ 交叉交换  多继承

```c++
#include <iostream>
using namespace std;
class MM
{
public:
	 virtual void print() 
	 {
		cout << "MM" << endl;
		cout << name << endl;
	 }
	 //void printMM() 
	 //{
		// cout << "父类有，子类没有的方法" << endl;
		// cout << name << endl;
	 //}
protected:
	string name = "MM";
};
class Girl :public MM 
{
public:
	void print() 
	{
		cout << "Girl" << endl;
		cout << gName << endl;
	}
	//void printData() 
	//{
	//	cout << "子类有父类没有的方法" << endl;
	//	cout << gName << endl;
	//}
protected:
	string gName = "girl";
};
class A 
{
public:
	virtual void print() { cout << "A" << endl; }
};
class B 
{
public:
	virtual void print() { cout << "B" << endl; }
};
class C :public A, public B 
{
public:
	void print() { cout << "C" << endl; }
};

int main() 
{

	MM* parent = new MM;
	Girl* son = new Girl;
	//上行转换
	MM* psUP = static_cast<MM*>(son);
	MM* pdUP = dynamic_cast<MM*>(son);
	MM* p = son;					//隐式转换是成立
	psUP->print();
	psUP->print();
	//下行转换
	//Girl* pp = parent;			//正常是危险的。

	Girl* psDown = static_cast<Girl*>(parent);
	psDown->print();
	//psDown->printData();
	//psDown->printMM();
	cout << "......" << endl;
	Girl* pdDown = dynamic_cast<Girl*>(parent);   //能够检测是否存在virtual，不存在不能转换
	if (pdDown != nullptr) 
	{
		pdDown->print();
		//pdDown->printData();
		//pdDown->printMM();
	}


	A* pA = new C;
	B* pB = dynamic_cast<B*>(pA);
	pB->print();

	return 0;
}
```

## 成员函数指针

```c++
#include <iostream>
#include <functional>
using namespace std;
class MM 
{
public:
	void print() 
	{
		cout << "我是成员函数" << endl;
	}
	static void printData() 
	{
		cout << "静态成员函数" << endl;
	}
};

void printInfo(int a, int b, int c) 
{
	cout << "a:" <<a<< endl;
	cout << "b:" <<b<< endl;
	cout << "c:" <<c<< endl;
}

void testBind() 
{
	//bind:函数适配器，让函数调用形态可以适用于别的形态
	printInfo(1, 2, 3);
	auto func = bind(&printInfo, std::placeholders::_1, std::placeholders::_2, 123);
	func(11,22);
}

int main() 
{
	//创建方式

	//p = &MM::printData;
	//写不明白的同学 一个auto搞定
	auto p2 = &MM::printData;
	p2();
	void(*p3)() = &MM::printData;
	p3();

	//普通函数创建指针
	void (MM:: *p)() = &MM::print;

	//调用形态
	MM mm;
	(mm.*p)();

	//auto func= bind(&MM::print, &mm);
	//func();
	testBind();
	return 0;
}
```

# C++IO流

## 什么是IO流

+ 流是若干个字节组成的字节序列，简单来说指的就是数据从一端到另一端
  + 键盘到程序    标准输入流
  + 程序到屏幕    标准输出流
  + 程序到文件    文件流
+ 流类体系:  一些系列管理输入和输出的流的操作
  + 输入流
  + 输出流
  + 文件流
+ ios类
  + istream
    + ifstream
    + istringstream
  + ostream
    + ofstream
    + ostringstream
+ 所有流操作都可以采用>>  <<运算符完成输入的流动操作

istream和ostream---->iostream

ifstream和ofstream---->fstream

## C++输入输出流

https://cplusplus.com/reference/

No.1 输入输出流对象:

+ cin     标准输入 可以被重定向
+ cout  标准输出 可以被重定向
+ cerr   标准错误  必须要输出到屏幕 不可以被重定向
+ clog   标准  输出到屏幕，被重定向

No.2 输入输出流对象对于字符具有成员函数的调用方式

+ 字符
  + get()：输入字符
  + put(): 输出字符
+ 字符串
  + getline():输入字符串
  + write()：输出字符串

No.3  流控制字符

C++流控制字符类似于C语言的转义字符 控制格式，比较鸡肋

+ 必须包含头文件  #include <iomanip>
+ 流控制字符有两种形态，一个是成员函数的方式，一个是类似关键字的方式
  + setbase():  按照不同的进制输出十进制数
  + setprecision(): 设置有效位数
    + 要控制小数位，要结合fixed
  + setw(): 设置输出数据的宽度
  + setiosflags():设置对其方式
    + ios::left
    + ios::right 
+ put_time 格式时间格式

| specifier | Replaced by                                                  | Example                    |
| --------- | ------------------------------------------------------------ | -------------------------- |
| `%a`      | Abbreviated weekday name *                                   | `Thu`                      |
| `%A`      | Full weekday name *                                          | `Thursday`                 |
| `%b`      | Abbreviated month name *                                     | `Aug`                      |
| `%B`      | Full month name *                                            | `August`                   |
| `%c`      | Date and time representation *                               | `Thu Aug 23 14:55:02 2001` |
| `%C`      | Year divided by 100 and truncated to integer (`00-99`)       | `20`                       |
| `%d`      | Day of the month, zero-padded (`01-31`)                      | `23`                       |
| `%D`      | Short `MM/DD/YY` date, equivalent to `%m/%d/%y`              | `08/23/01`                 |
| `%e`      | Day of the month, space-padded (` 1-31`)                     | `23`                       |
| `%F`      | Short `YYYY-MM-DD` date, equivalent to `%Y-%m-%d`            | `2001-08-23`               |
| `%g`      | Week-based year, last two digits (`00-99`)                   | `01`                       |
| `%G`      | Week-based year                                              | `2001`                     |
| `%h`      | Abbreviated month name * (same as `%b`)                      | `Aug`                      |
| `%H`      | Hour in 24h format (`00-23`)                                 | `14`                       |
| `%I`      | Hour in 12h format (`01-12`)                                 | `02`                       |
| `%j`      | Day of the year (`001-366`)                                  | `235`                      |
| `%m`      | Month as a decimal number (`01-12`)                          | `08`                       |
| `%M`      | Minute (`00-59`)                                             | `55`                       |
| `%n`      | New-line character (`'\n'`)                                  | ``                         |
| `%p`      | AM or PM designation                                         | `PM`                       |
| `%r`      | 12-hour clock time *                                         | `02:55:02 pm`              |
| `%R`      | 24-hour `HH:MM` time, equivalent to `%H:%M`                  | `14:55`                    |
| `%S`      | Second (`00-61`)                                             | `02`                       |
| `%t`      | Horizontal-tab character (`'\t'`)                            | ``                         |
| `%T`      | ISO 8601 time format (`HH:MM:SS`), equivalent to `%H:%M:%S`  | `14:55:02`                 |
| `%u`      | ISO 8601 weekday as number with Monday as `1` (`1-7`)        | `4`                        |
| `%U`      | Week number with the first Sunday as the first day of week one (`00-53`) | `33`                       |
| `%V`      | ISO 8601 week number (`00-53`)                               | `34`                       |
| `%w`      | Weekday as a decimal number with Sunday as `0` (`0-6`)       | `4`                        |
| `%W`      | Week number with the first Monday as the first day of week one (`00-53`) | `34`                       |
| `%x`      | Date representation *                                        | `08/23/01`                 |
| `%X`      | Time representation *                                        | `14:55:02`                 |
| `%y`      | Year, last two digits (`00-99`)                              | `01`                       |
| `%Y`      | Year                                                         | `2001`                     |
| `%z`      | ISO 8601 offset from UTC in timezone (1 minute=1, 1 hour=100) If timezone cannot be termined, no characters | `+100`                     |
| `%Z`      | Timezone name or abbreviation * If timezone cannot be termined, no characters | `CDT`                      |
| `%%`      | A `%` sign                                                   | `%`                        |

```C++
#include <iostream>
#include <iomanip>
#include <ctime>
//#include<istream>
//#include<ostream>
using namespace std;
int main() 
{
#if 0
	cerr << "错误提示" << endl;
	clog << "标准错误" << endl;
	cout << "字符输入:" << endl;
	char key = cin.get();
	cout.put(key);
	setbuf(stdin, nullptr);
	cout << "字符串输入方式:" << endl;
	char buffer[20] = "";
	cin.getline(buffer, 20);
	cout.write(buffer, 20);
#endif
	//设置进制
	cout << setbase(16) << 32 << endl;
	cout  << setbase(8)<<32 << endl;
	//cout << setbase(2) << 32 << endl;			//没有二进制
	cout << hex << 32 << endl;
	cout << oct << 32 << endl;
	cout << dec << 32 << endl;
	//精度控制
	double data = 34.1415661;
	cout << setprecision(4) << data << endl;		//有效位数
	cout << fixed << setprecision(4) << data << endl;		//4位小数位
	cout.unsetf(ios::fixed);
	cout << setprecision(4) << data << endl;		//有效位数

	//制表  输入数据宽度+对其方式
	cout << setiosflags(ios::left);
	cout << setw(10) << "姓名" << setw(6) << "年龄" << setw(10) << "编号" << endl;
	cout << setw(10) << "张三" << setw(6) << 18 << setw(10) << 1001 << endl;
	cout << setw(10) << "欧阳锋" << setw(6) << 99 << setw(10) << 1005 << endl;
	cout.width(10);
	cout << "姓名";
	cout.width(6);
	cout << "年龄";
	cout.width(10);
	cout << "编号";
	//cout.width(10);
	//cout.precision(20);
	//取消格式
	cout << resetiosflags(ios_base::scientific) << endl;
	cout << data << endl;
	time_t num = time(nullptr);
	cout << num << endl;
	tm* tmData = localtime(&num);

	cout << put_time(tmData, "%F %r") << endl;

	return 0;
}
```

## C++字符流

字符流头文件 sstream，都存在一个宽字节版本的格式

+ istringstream
+ ostringstream

一般再处理字符流的是使用的类是stringstream

+ string str():  获取字符流的字符串
+ void str(const string& str)：重置stringstream对象种的数据

应用场景

+ 数据的类型转换
+ 字符串的切割

```c++
#include <sstream>
#include <iostream>
#include <string>
using namespace std;
int main() 
{
#if 0
	stringstream object;
	object << "sdfsdfsd";
	cout << object.str() << endl;
	char buffer[1024] = "";
	object >> buffer;
	cout << buffer << endl;
#endif
	//No.1 数据的类型转换
	stringstream translate;
	int data = 1234;
	string num = to_string(data);
	cout << num << endl;
	string str = "12345";
	translate << str;
	int result = 0;
	translate >> result;
	cout << result << endl;
	//eaayx  不能输出数字 
	//数字转换字符串
	// 计算器
	//No.2  数据分割
	stringstream ip("192.168.1.1");
	int ipnum[4];
	char key;
	ip >> ipnum[0];
	ip >> key;
	ip >> ipnum[1];
	ip >> key;
	ip >> ipnum[2];
	ip >> key;
	ip >> ipnum[3];
	for (int i = 0; i < 4; i++) 
	{
		cout << ipnum[i] << "\t";
	}
	cout << endl;
	//注意点
	//一个流做类型转换，多次一定要clear清除
	result = 0;
	string temp = "9999";
	translate.clear();
	translate << temp;
	translate >> result;
	cout << result << endl;

	stringstream test("sdfsdfsd");
	//test.clear();
	test.str("");
	cout << test.str() << endl;

	return 0;
}
```

## C++文件流

### 文件流类

+ fstream  读写操作
  + ofstream  写操作   ouput:打印   打印东西到文件 就是 写操作
  + ifstream  读操作    input: 把文件当作输入的地方
+ #include  <fstream>
+ 打开文件 ：  void  open(const char* url,ios::openmode mode)
  + ios::in       读
  + ios::out    写    具有创建功能
  + ios::app  追加模式  具有创建功能
  + ios::ate   打开已有文件，文件指针在文件末尾
  + ios::trunc  文件不存在具有创建文件功能
  + ios::binary  二进制
  + ios::nocrate 不创建 
  + ios::replace  不做替换
  + 组合方式  |  
    + ios::in |ios::out 
    + ios::in|ios::trunc 
    + ios::in|ios::binary|ios::trunc
+  文件关闭： void  close()
+ 文件状态函数 
  + 文件为空
    + bool is_open()  : 返回false打开文件失败 ,true是成功呢
    + !文件流对象
  + int eof(): 判定是否到达文件末尾

```c++
#include <iostream>
#include <fstream>
using namespace std;
class MM 
{
public:
	MM(string name = "", int age = 0, int num = 0) :name(name), age(age), num(num) 
	{

	}
	void printMM() 
	{
		cout << name << "\t" << age << "\t" << num << endl;
	}
	void saveFile(const char* filename) 
	{
		fstream  file;
		file.open(filename, ios::in|ios::out|ios::trunc);
		if (!file || !file.is_open())		//两个写一个即可
		{
			cout << "文件打开失败!" << endl;
			return;
		}
		//流方式写数据，尽量写空格和换行，便于作为读出来的格式数据的风格
		file << name << " " << age << " " << num<<endl;
		//C语言 freopen(filename,mode,stdin)
		file.close();
	}
	string& getName() 
	{
		return name;
	}
	int& getAge() 
	{
		return age;
	}
	int& getNum() 
	{
		return num;
	}
	void readFile(const char* filename) 
	{
		//fstream会清空数据
		ifstream  file(filename, ios::out);
		if (!file) 
		{
			cout << "打开文件失败" << endl;
			return;
		}
		file >> this->name >> this->age >> this->num;
		file.close();
	}
protected:
	string name;
	int age;
	int num;
};
class Data 
{
public:
	Data() 
	{
		data[0] = { "月亮",18,1001 };
		data[1] = { "顽石",28,1002 };
		data[2] = { "里奇",38,1003 };
		curSize = 3;
	}
	Data(int a) 
	{

	}
	void saveFile(const char* filename)
	{
		fstream  file;
		file.open(filename, ios::in | ios::out | ios::trunc);
		if (!file || !file.is_open())		//两个写一个即可
		{
			cout << "文件打开失败!" << endl;
			return;
		}
		//流方式写数据，尽量写空格和换行，便于作为读出来的格式数据的风格
		for (int i = 0; i < curSize; i++) 
		{
			file << data[i].getName() << " " << data[i].getAge() << " " << data[i].getNum() << endl;
		}
		//C语言 freopen(filename,mode,stdin)
		file.close();
	}
	void printData() 
	{
		for (int i = 0; i < curSize; i++)
		{
			cout << data[i].getName() << " " << data[i].getAge() << " " << data[i].getNum() << endl;
		}
	}
	void readFile(const char* fileName) 
	{
		ifstream  file(fileName, ios::out);
		if (!file)
		{
			cout << "打开文件失败" << endl;
			return;
		}
		curSize = 0;
		while (!file.eof()) 
		{
			file >> data[curSize].getName() >> data[curSize].getAge() >> data[curSize].getNum();
			curSize++;
		}
		file.close();
	}
protected:
	MM data[3];
	int curSize;
};

void asciiReadWriteFile(const char* readFileName, const char* writeFileName) 
{	
	fstream read(readFileName, ios::in);
	fstream write(writeFileName, ios::out);
	while (!read.eof())
	{
		char key;
		read.get(key);
		write.put(key);
	}
	read.close();
	write.close();
}
void binaryReadWrite(const char* readFileName, const char* writeFileName) 
{
	fstream in(readFileName, ios::in|ios::binary);
	fstream out(writeFileName, ios::out|ios::binary);
	while (!in.eof())
	{
		char str[1024] = "";
		//read.get(key);
		in.read(str, 1024);
		//write.put(key);
		out.write(str, strlen(str) + 1);		//写的是实际长度，如果比实际长度长，会写多余空格
	}
	in.close();
	out.close();
}
int main() 
{
	MM mm = { "张三",18,1001 };
	mm.saveFile("1.txt");
	MM girl;
	girl.readFile("1.txt");
	girl.printMM();

	Data data;
	data.saveFile("2.txt");

	Data data2(1);
	data2.readFile("2.txt");
	data2.printData();
	asciiReadWriteFile("read.txt", "write.txt");
	binaryReadWrite("bRead.txt", "bWrite.txt");

	return 0;
}
```

### C++文件指针

ifstream 对象

ifstream& seekg(long int pos);

ifstream& seekg(long int pos,ios::base::seekdir begin);

ofstream对象

ofstream& seekp(long int pos);

ofstream& seekp(long int pos,ios::base::seekdir begin);

g:get  in

p:put output

seekdir ：

+ ios::beg    开始的位置
+ ios::end 结束的位置
+ ios::cur  当前位置

```c++
void testSeekReadFile(const char* fileName) 
{
	fstream read(fileName, ios::in);
	if (!read) 
	{
		cout << "文件的打开失败!";
		return;
	}
	read.seekg(3);
	char key = read.get();
	cout << key << endl;
	read.seekg(-3, ios::end);
	cout << (char)read.get() << endl;
	read.close();
}
```

# C++异常处理

## 基本的异常处理

异常处理机制是一种延缓问题解决，放到后面去解决。有异常必须要处理，如果不做处理，将调用abort函数终止程序，什么东西都可以当做异常，程序错误可以算是异常的一种。异常处理一般是分为三个步骤

+  抛出异常: throw   一般抛出的是数据
+ 检查异常:try    
+ 处理异常 catch，捕获抛出的数据类型

注意点： try和catch必须成对出现，并且，try语句后面{}不能省略

```c++
#include <iostream>
#include <string>
using namespace std;
int getValue(int a, int b) 
{
	if (b == 0)
		throw string("除数不能为零");				//1.知道抛出什么东西
	return a / b;
}

void print(int a, int b) 
{
	try 
	{
		cout << getValue(a, b) << endl;
	}
	catch (string& str) 
	{
		cout << str << endl;
	}
}
void printData(int a, int b)
{
	cout << getValue(a, b) << endl;
}



int main() 
{
	//基本写法
	try 
	{
		getValue(1, 0);
		cout << "......" << endl;
	}
	catch (string) 
	{
		cout << "除数不能为零" << endl;
	}
	catch (int) 
	{
		cout << "捕获int" << endl;
	}
	catch (double) 
	{
		cout << "捕获double" << endl;
	}
	//传参写法
	try 
	{
		getValue(3, 0);
	}
	catch (string& str)		//存在一个隐藏的传参操作，str=抛出内容
	{
		cout << str << endl;
	}
	//什么叫做延迟处理
	print(4, 0);
	try 
	{
		printData(5, 0);
	}
	catch (string& str) 
	{
		cout << str << endl;
	}
	return 0;
}
```

## 无异常的函数写法

```c++
#include <iostream>
using namespace std;
//老版本写法
int max(int a, int b) throw() 
{
	// warning C4297: “max”: 假定函数不引发异常，但确实发生了
	//if (a == 0)
	//	throw 1;
	return a > b ? a : b;
}
//新版本 noexcept

int min(int a, int b) noexcept 
{
	return a > b ? b : a;
}

int main() 
{
	cout << min(1, 2) << endl;
	return 0;
}
```

## 删减符...

删减符可以捕获任何类型的异常。

```c++
#include <iostream>
using namespace std;
//老版本写法
int max(int a, int b) throw() 
{
	// warning C4297: “max”: 假定函数不引发异常，但确实发生了
	//if (a == 0)
	//	throw 1;
	return a > b ? a : b;
}
//新版本 noexcept
int min(int a, int b) noexcept 
{
	return a > b ? b : a;
}
int getValue(int a, int b) 
{
	if (b == 0)
		throw "除数不能为零";
	return a / b;
}
void deleteList(int size) 
{
	if (size == 0)
		throw 0;
	cout << "假装删除操作" << endl;
}

int main() 
{
	cout << min(1, 2) << endl;
	try 
	{
		getValue(1, 0);
		deleteList(1);
	}
	catch (...) 
	{
		cout << "引发异常" << endl;
	}
	return 0;
}
```

## C++标准库中异常

+ 了解标准库中异常类
+ 继承标准库中异常类

```c++
#include <exception>
#include <iostream>
using namespace std;
class ListEmpty :public exception 
{
public:
    ListEmpty() :exception("ListEmpty") 
    {

    }
protected:
};
void deleteEmpty(int size) 
{
    if (size == 0)
        throw ListEmpty();
    cout << "假装链表删除" << endl;
}
int main() 
{
    try 
    {
        int* p = new int[1024 * 1024*4];
    }
    catch (bad_alloc& object) 
    {
        cout << object.what();
    }
    try 
    {
        deleteEmpty(0);
    }
    catch (ListEmpty& object) 
    {
        cout << object.what() << endl;
    }
	return 0;
}
```

异常处理比较鸡肋，以后基本上很少用到，知道有这么回事即可。了解基本用法就OK了。

# C++模板

## 什么是模板

Template的声明和定义

模板是一种忽略数据一种泛型编程。把数据当做未知量，当使用的传入类型一种编程方式。

```c++
template <typename T1, typename T2, typename T3>    // 模板函数
template <class T1,class T2,class T3>               // 模板类
template <int V>                                    // 整型模板参数
   
// 注意: 其实都可以用
```





**函数模板的调用格式是：**

``` C++
函数模板名 < 模板参数列表 > ( 参数 )
```

模板参数的顺序是有限制的：**先写需要指定的模板参数，再把能推导出来的模板参数放在后面**。

```c++
template <typename DstT, typename SrcT> 
DstT c_style_cast(SrcT v)	// 模板参数 DstT 需要人为指定，放前面。
{
    return (DstT)(v);
}

int v = 0;
float i = c_style_cast<float>(v);  // 形象地说，DstT会先把你指定的参数吃掉，剩下的就交给编译器从函数参数列表中推导啦。
```





**模板类的调用格式(实例化)的语法是：**

```c++
模板名 < 模板实参1 [，模板实参2，...] >  类对象名
```



模板是一种忽略数据一种泛型编程。把数据当做未知量，当使用的传入类型一种编程方式。

语法:

```c++
template <class T1>      //告诉编译器，接下来要用到一个未知类型是T类型
template <typename T>   //等效用class
template <class T1,class T2,class T3>    //三个未知类型
```

```c++
#include <iostream>
#include <string>
using namespace std;
#if 0
int Max(int a, int b) 
{
	return a > b ? a : b;
}
string Max(string a, string b) 
{
	return a > b ? a : b;
}
double Max(double a, double b) 
{
	return a > b ? a : b;
}
#endif
template <class Type> Type Max(Type a, Type b) 
{
	return a > b ? a : b;
}
//两行和一行写没有区别
template<class Type>
void print(Type a) 
{
	cout << a << endl;
}
int main() 
{
	return 0;
}
```

## C++函数模板

+ 函数模板调用
  + 函数模板隐式调用, 可以自动推断:  函数名(函数参数)
  + 显式调用  : 函数名<未知类型>(函数参数)
  
+ 函数模板本质就是函数传参
  + 函数模板也是可以缺省
  
+ 整型模板参数

  + 这里的**整型数比较宽泛，包括布尔型，不同位数、有无符号的整型，甚至包括指针。**

  + 整型模板参数最基本的用途: 定义一个常数。

  + ==这种函数模板必须显示调用==
  + 变量传参只能传入常量

+ 当函数模板和普通函数相遇
  + 优先调用类型一致的普通函数
  + 显式调用一定是调用模板
  
+ 函数模板重载
  + 优先调用传参数目少的函数模板

```c++
#include <iostream>
#include <string>
using namespace std;
template <class Type>
Type  Max(Type a, Type b) 
{
	return a > b ? a : b;
}
template <class _Ty1,class _Ty2,class _Ty3>
void print(_Ty1 one, _Ty2 two, _Ty3 three) 
{
	cout << "1:" << one << endl;
	cout << "2:" << two << endl;
	cout << "3:" << three << endl;
}

//函数模板的缺省
template <class _Ty1, class _Ty2=string, class _Ty3=int>
void printData(_Ty1 one, _Ty2 two, _Ty3 three) 
{
	cout << "1:" << one << endl;
	cout << "2:" << two << endl;
	cout << "3:" << three << endl;
}

//整型模板参数
template <class _Ty,int size>
_Ty* createArray() 
{
	_Ty* parray = new _Ty[size];
	//_Ty =int  size=5
	//int* parray=new int[5];
	//_Ty=string size=5
	//string* parray=new string[5];
	return parray;
}
template <class _Ty, int size>
void printArray(_Ty array[])
{
	for (int i = 0; i < size; i++) 
	{
		cout << array[i] << "\t";
	}
	cout << endl;
}


template <class _Ty, int size=3>
void printArray2(_Ty array[])
{
	for (int i = 0; i < size; i++)
	{
		cout << array[i] << "\t";
	}
	cout << endl;
}

void test() 
{
	//No.4 函数模板存在变量
	int* pInt = createArray<int, 5>();			//_Ty =int  size=5
	string* pStr = createArray<string, 5>();
	double* pDouble = createArray<double, 5>();
	//整数模板参数,必须要显式调用
	int array[3] = { 1,2,3 };
	printArray<int,3>(array);
	double dNum[3] = { 1.11,2.33,4.44 };
	printArray<double,3>(dNum);
	//变量做了缺省，可以隐式调用
	printArray2(array);
	printArray2(dNum);
	//int length = 5;
	//int* pNum = createArray<int, length>();  //只能传入常量
	//常属性变量ok
	//const int length = 5;
	//int* pNum = createArray<int, length>();
	 
	//错误的
	//int length = 5;
	//int* pNum = createArray<int, static_cast<const int>(length)>();

	//int length = 5;
	//int* pNum = createArray<int,move(length)>();
}

void Func1(int a, string b, double c) 
{
	cout << "普通函数" << endl;
}
//函数模板允许重载
template <class _Ty1,class _Ty2,class _Ty3>
void Func1(_Ty1 a, _Ty2 b, _Ty3 c) 
{
	cout << "三个类型模板" << endl;
}
template <class _Ty1, class _Ty2>
void Func1(_Ty1 a, _Ty2 b, _Ty2 c)
{
	cout << "两个类型模板" << endl;
}
template <class _Ty1>
void Func1(_Ty1 a, _Ty1 b, _Ty1 c)
{
	cout << "一个类型模板" << endl;
}

void test2() 
{
	Func1<int, string, double>(1, "sd", 1.11);
	Func1(1, string("sd"), 1.11);  // 优先推断成char *
	Func1(1, 1, 1);			//一个参数的模板
	Func1("string", 1, 1 );
	Func1("string", 1, "sfsd");
}
int main() 
{
	//No.1 隐式调用法
	cout << Max(string("abc"), string("dbc")) << endl;  //Type=string
	cout << Max(1, 2) << endl;							//Type=int
	cout << Max(1.11, 2.33) << endl;					//Type=double
	//No.2 显示调用
	cout << Max<string>(string("abc"), string("dbc")) << endl;  //Type=string
	cout << Max<int>(1, 2) << endl;							//Type=int
	cout << Max<double>(1.11, 2.33) << endl;					//Type=double
	print<int, string, double>(1, "ILoveyou", 1.11);
	print<string, string, string>("abc", "ILoveyou", "模板");

	//No.3 缺省
	printData<string>("str1","str2",1);		//_Ty1=string _Ty2=string _Ty3=int
	printData<string, double>("str1", 1.11, 1);
	printData<string, double,string>("str1", 1.11, "str3");
	test();
	test2();


	return 0;
}
```

## 函数模板操作自定义类型

操作自定义类型的关键点就是重载。

```c++
#include <iostream>
#include <string>
using namespace std;

template <class _Ty>
void printArray(_Ty array[], int arrayNum) 
{
	for (int i = 0; i < arrayNum; i++)   //_Ty=MM
	{
		cout << array[i];		//array[i] 对象是不能直接打印
	}
	cout << endl;
}
template <class _Ty>
void Sort(_Ty array[], int arrayNum) 
{
	for (int i = 0; i < arrayNum; i++) 
	{
		for (int j = 0; j < arrayNum - i - 1; j++) 
		{
			if (array[j] > array[j + 1])   //_Ty =MM  array[j] 对象与对象比
			{
				_Ty temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;
			}
		}
	}
}

// 操作自定义类型
class MM 
{
public:
	MM(string name = "", int age = 0) :name(name), age(age) {}
    // 重载让cout打印
	friend ostream& operator<<(ostream& out, const MM& object) 
	{
		out << object.name << "\t" << object.age << endl;
		return out;
	}
	bool operator>(const MM& object) 
	{
		return this->name > object.name;
	}
	string getName()const { return name; }
	int getAge()const { return age; }
protected:
	string name;
	int age;
};

// 写的比较准则
bool compareByName(const MM& one, const MM& two)
{
	return one.getName() > two.getName();
}
bool compareByAge(const MM& one, const MM& two)
{
	return one.getAge() > two.getAge();
}

template <class _Ty>
void Sort2(_Ty array[], int arrayNum, bool(*compare)(const _Ty& one,const _Ty& two))
{// 参数3是比较准则
	for (int i = 0; i < arrayNum; i++)
	{
		for (int j = 0; j < arrayNum - i - 1; j++)
		{
			if (compare(array[j],array[j+1]))   //_Ty =MM  array[j] 对象与对象比
			{
				_Ty temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;
			}
		}
	}
}

int main() 
{
	int num[3] = { 1,2,3 };
	printArray(num, 3);
	double dNum[3] = { 1.2,1.1,1.0 };
	Sort(dNum,3);
	printArray(dNum, 3);
    
    // 操作自定义类型
	MM mm[3];
	mm[0] = { "abc",1 };
	mm[1] = { "fc",18 };
	mm[2] = { "de",29 };
	Sort(mm, 3);
	printArray(mm, 3);

	Sort2(mm, 3, compareByName);
	printArray(mm, 3);
	Sort2(mm, 3, compareByAge);
	printArray(mm, 3);
	return 0;
}
```

## C++类模板

+  template修饰的类就是模板类
+ 模板类必须显式实例化，简单来说必须要传参
+ 模板类不是一个真正的类型
  + 声明和实现必须写在一起及同一个文件中, 成员函数直接写成内联函数
  + ==所有用到类型的地方必须要用:    类名<未知类型> 的用法==
+ 类模板特化(特殊情况特殊处理, 理解成类的重载)
  + 局部特化： 特殊化处理，例如两个未知变成一个未知类型 template <class T1, class T2> 变成template < class T> 
  + 完全特化： 具体化类型  template <>

```c++
#include <iostream>
#include <string>
using namespace std;

template <class _Ty1,class _Ty2>
class Data 
{
public:
	void print();
protected:
public:
	static int count;  // 静态变量
};

// 静态变量
template <class _Ty1,class _Ty2>
int Data<_Ty1, _Ty2>::count = 0;


template <class _Ty1,class _Ty2>
void Data<_Ty1, _Ty2>::print() 
{
	cout << "类模板中函数" << endl;
}

// -----------
// 所有用到类型的地方必须要用:    类名<未知类型> 的用法
template <class _Ty1,class _Ty2>
class Son : public Data<_Ty1,_Ty2> 
{
public:

protected:

};

struct MMInfo 
{
	string name;
	int age;
	int num;
};
ostream& operator<<(ostream& out, const MMInfo& object) 
{
	out << object.name << "\t" << object.age << "\t" << object.num;
	return out;
}


struct Score 
{
	int math;
	int english;
	int py;
};

ostream& operator<<(ostream& out, const Score& object)
{
	out << object.math << "\t" << object.english << "\t" << object.py;
	return out;
}


//-----------

template <class _Ty1, class _Ty2>
class MM
{
public:
	MM(_Ty1 one, _Ty2 two) :one(one), two(two)
	{

	}
	void print() 
	{
		cout << one <<"\t" << two << endl;
	}
protected:
	_Ty1  one;
	_Ty2  two;
};
void testMM() 
{
	MM<string, int> mm("月亮", 18);
	mm.print();
	MM<int, int> complex(1, 2);
	complex.print();
	MMInfo  info = { "美女",18,1001 }; 
	Score score = { 88, 99, 100 };
	MM<MMInfo, Score> mmObject(info, score);
	mmObject.print();
}

//----------------------
//类模板特化
template <class _Ty1,class _Ty2,class _Ty3>
class A 
{
public:
	A(_Ty1 one, _Ty2 two, _Ty3 three) :one(one), two(two), three() 
	{
		cout << "三个类型" << endl;
	}
protected:
	_Ty1 one;
	_Ty2 two;
	_Ty3 three;
};

//局部特化
template <class _Ty1, class _Ty2>
class A<_Ty1,_Ty2,_Ty1>
{
public:
	A(_Ty1 one, _Ty2 two, _Ty1 three) :one(one), two(two), three()
	{
		cout << "局部特化" << endl;
	}
protected:
	_Ty1 one;
	_Ty1 two;
	_Ty1 three;
};

//完全特化
template <>
class A<int, int, int>
{
public:
	A(int one, int two, int three) :one(one), two(two), three()
	{
		cout << "完全特化" << endl;
	}
protected:
	int one;
	int two;
	int three;
};
void testA() 
{
	A<int, int, int>  object1(1, 1, 1);
	A<double, double, double>  object2(1.1, 1.1, 1.1);
	A<double, string, double>  object3(1.1, string("模板"), 1.1);
}


int main() 
{
	Data<int, string>  object;
	Data<int, string>* pObject = new Data<int, string>;
	object.print();
	pObject->print();
    
    // 静态变量的访问
	cout << Data<int, int>::count << endl;
	cout << Data<string, int>::count << endl;
    
    
	testMM();
	testA();
	return 0;
}
```

## 稍微复杂一点类模板

学会用别名替换即可

```c++
#include <iostream>
#include <string>
using namespace std;
template <class _Ty1, class _Ty2>
class MM
{
public:
	MM(_Ty1 one, _Ty2 two) :one(one), two(two)
	{

	}
	void print()
	{
		cout << one << "\t" << two << endl;
	}
	template <class _Ty1, class _Ty2>
	friend ostream& operator<<(ostream& out, const MM<_Ty1,_Ty2>& object);
protected:
	_Ty1  one;
	_Ty2  two;
};
template <class _Ty1, class _Ty2> ostream& operator<<(ostream& out, const MM<_Ty1, _Ty2>& object) 
{
	out << object.one << "\t" << object.two;
	return out;
}

template <class _Ty1, class _Ty2>
class Data
{
public:
	Data(_Ty1 one, _Ty2 two) :one(one), two(two)
	{

	}
	void print()
	{
		cout << one << "\t" << two << endl;
	}
protected:
	_Ty1  one;
	_Ty2  two;
};

int main() 
{
	MM<string, int> info("月亮", 18);		//姓名 年龄
	MM<int, int> pos(100, 100);				//位置
	Data<MM<string, int>, MM<int, int>> test(info, pos);
	test.print();
	Data<MM<string, int>, Data<MM<string, int>, MM<int, int>>> test2(info,test);

	using DataType1 = Data<MM<string, int>, MM<int, int>>;
	using DataType2 = MM<string, int>;
	Data<DataType2, DataType1> test3(info, test);

	return 0;
}
```

# C++STL容器

STL是标准模版类库

+ 容器--->存储数据  数据结构
  + array  ：定长数组
  + vector:  动态数组
  + list： 链表
  + stack: 栈
  + queue:队列
  + deque:循环队列
  + priority_queue:优先队列
  + set/multiset :集合 和多重集合
  + map/multimap: 映射和多重映射
  + tuple: 元组
  + initializer_list  列表
+ 迭代器和仿函数
+ 算法

## C++array

array容器就是定长数组，主要掌握的有以下三个点

+ 创建方式
+ 数据存储方式
+ 其他操作(增删改查)
+ 其他一些函数

```c++
#include <array>
#include <iostream>
#include <string>
using namespace std;
//No.1 操作基本数据类型

void printArray(array<double, 3>& arr) 
{
	for (int i = 0; i < arr.size(); i++) 
	{
		cout << arr[i] << " ";
	}
	cout << endl;
}
void testOne() 
{
	//int:存储的数据类型
	//5:数组长度
	array<int, 5> iNum;
	array<double, 3> dNum = { 1.11,2.22,3.33 };

	cout <<"size:" << dNum.size() << endl;
	cout << "isEmpty:" << dNum.empty() << endl;
	printArray(dNum);
	for (int i = 0; i < iNum.size(); i++)
	{
		cin >> iNum[i];
	}
	//直接采用数组的方式遍历
	for (int i = 0; i < iNum.size(); i++)
	{
		cout << iNum[i] << " ";
	}
	cout << endl;
	//采用迭代器的方式遍历
	array<int, 5>::iterator iter;
	for (iter = iNum.begin(); iter != iNum.end(); iter++) 
	{
		cout << *iter << " ";
	}
	cout << endl;
	//采用新版的for循环，区间遍历
	for (auto v : iNum)				//把iNum容器的中数据赋值给v 跑一边循环
	{
		cout << v << " ";
	}
	cout << endl;
	int temp[3] = { 1,2,3 };
	for (auto v : temp) 
	{
		cout << v << " ";
	}
	cout << endl;
	array<int, 5>::iterator result=find(iNum.begin(), iNum.end(), 3);
	if (result == iNum.end()) 
	{
		cout << "未找到" << endl;
	}
	else 
	{
		cout << *result << endl;
	}

}
//操作自定义类型
class MM 
{
public:
	MM(string name = "", int age = 0) :name(name), age(age) {}
	string getName()const { return name; }
	int  getAge()const { return age; }
	friend ostream& operator<<(ostream& out, const MM& object) 
	{
		out << object.name << " " << object.age;
		return out;
	}
protected:
	string name;
	int age;
};
bool searchByName(const MM& object) 
{
	return object.getName() == "西施";
}
bool searchByAge(const MM& object)
{
	return object.getAge() == 38;
}

void testTwo() 
{
	array<MM, 3> mmArray;
	mmArray[0] = MM("月亮", 18);
	mmArray[1] = MM("西施", 28);
	mmArray[2] = MM("貂蝉", 38);
	//操作自定义需要剥洋葱
	for (auto v : mmArray) 
	{
		cout << v.getName() << " " << v.getAge() << endl;
	}
	//才可以采用重载方案
	for (auto v : mmArray) 
	{
		cout << v << endl;
	}
	array<MM, 3>::iterator result = find_if(mmArray.begin(), mmArray.end(), searchByName);
	if(result!=mmArray.end())
		cout << (*result).getName()<<" " << result->getAge() << endl;
	result = find_if(mmArray.begin(), mmArray.end(), searchByAge);
	if (result != mmArray.end())
		cout << (*result).getName() << " " << result->getAge() << endl;
}
int main() 
{
	//testOne();
	testTwo();

	return 0;
}
```

## C++vector

vector容器是动态数组，掌握内容以下这些

- 创建方式
- 数据存储方式
- 其他操作(增删改查)
- 其他一些函数

```c++
#include <vector>
#include <iostream>
#include <string>
using namespace std;
//No.1 操作基本数据类型
bool compareData(int data) 
{
	return data == 666;
}
void  testOne() 
{
	//不带长度的构建方式   不能直接用下标法插入
	//只能采用成员函数操作
	//push_back(type data);
	//这一种写法用的比较多
	vector<int> num;			
	num.push_back(1);
	num.push_back(2);
	for (auto v : num) 
	{
		cout << v << " ";
	}
	cout << endl;

	for (vector<int>::iterator iter = num.begin(); iter != num.end(); iter++) 
	{
		cout << *iter << " ";
	}
	cout << endl;

	for (int i = 0; i < num.size(); i++) 
	{
		cout << num[i] << " ";
	}
	cout << endl;
	//带长度的构建方式,下标法操作不能超过长度-1
	vector<string> str(3);
	str[0] = "我";
	str[1] = "你";
	str[2] = "美女";
	//str[3] = "引发中断";
	str.push_back("才能够增长");
	for (auto v : str) 
	{
		cout << v;
	}
	cout << endl;
	vector<int>  data(3);
	data.push_back(666);	//在已有容器的最后面插入
	for (auto v : data) 
	{
		cout << v << " ";
	}
	cout << endl;
	cout << "size:" << data.size() << endl;
	cout << "isEmpty:" << data.empty() << endl;
	cout << "at:" << data.at(3) << endl;

	cout << "front:" << data.front() << endl;
	cout << "back:" << data.back() << endl;

	vector<int>::iterator result=find_if(data.begin(), data.end(), compareData);
	if (result != data.end()) 
	{
		cout << *result << endl;
	}
}

//No.2 操作自定义类型
class MM 
{
public:
	MM(string name, int age) :name(name), age(age) {}
	friend ostream& operator<<(ostream& out, const MM& object) 
	{
		out << object.name << " " << object.age;
		return out;
	}
	string getName() const { return name; }
	int getAge()const { return age; }
protected:
	string name;
	int age;
};

bool compareByName(const MM& object) 
{
	return object.getName() == "蓝火";
}

void testTwo() 
{
	vector<MM> mm;
	mm.push_back(MM("月亮", 18));
	mm.push_back(MM("西施", 28));
	mm.push_back(MM("蓝火", 38));

	for (auto v : mm) 
	{
		cout << v << endl;
	}
	//删除操作注意点
	//方案一 迭代器
	for (vector<MM>::iterator iter = mm.begin(); iter != mm.end(); ) 
	{
		if (iter->getName() == "西施") 
		{
			//erase
			iter=mm.erase(iter);
		}
		else 
		{
			iter++;
		}
	}
	cout << "删除结果....." << endl;
	for (auto v : mm)
	{
		cout << v << endl;
	}
	vector<MM>::iterator result = find_if(mm.begin(), mm.end(), compareByName);
	if (result != mm.end()) 
	{
		cout << *result << endl;
	}
	vector<int> test = { 0,1,2,3,4,5,6,7,8 };
	test.erase(test.begin() + 2);
	for (auto v : test) 
	{
		cout << v << " ";
	}
	cout << endl;
}

int main() 
{
	testOne();
	testTwo();
	return 0;
}
```

## array与vector嵌套

- array与array嵌套
- vector与vector嵌套
- array与vector嵌套

```c++
#include <vector>
#include <iostream>
#include <string>
using namespace std;
//No.1 操作基本数据类型
bool compareData(int data) 
{
	return data == 666;
}
void  testOne() 
{
	//不带长度的构建方式   不能直接用下标法插入
	//只能采用成员函数操作
	//push_back(type data);
	//这一种写法用的比较多
	vector<int> num;			
	num.push_back(1);
	num.push_back(2);
	for (auto v : num) 
	{
		cout << v << " ";
	}
	cout << endl;

	for (vector<int>::iterator iter = num.begin(); iter != num.end(); iter++) 
	{
		cout << *iter << " ";
	}
	cout << endl;

	for (int i = 0; i < num.size(); i++) 
	{
		cout << num[i] << " ";
	}
	cout << endl;
	//带长度的构建方式,下标法操作不能超过长度-1
	vector<string> str(3);
	str[0] = "我";
	str[1] = "你";
	str[2] = "美女";
	//str[3] = "引发中断";
	str.push_back("才能够增长");
	for (auto v : str) 
	{
		cout << v;
	}
	cout << endl;
	vector<int>  data(3);
	data.push_back(666);	//在已有容器的最后面插入
	for (auto v : data) 
	{
		cout << v << " ";
	}
	cout << endl;
	cout << "size:" << data.size() << endl;
	cout << "isEmpty:" << data.empty() << endl;
	cout << "at:" << data.at(3) << endl;

	cout << "front:" << data.front() << endl;
	cout << "back:" << data.back() << endl;

	vector<int>::iterator result=find_if(data.begin(), data.end(), compareData);
	if (result != data.end()) 
	{
		cout << *result << endl;
	}
}

//No.2 操作自定义类型
class MM 
{
public:
	MM(string name, int age) :name(name), age(age) {}
	friend ostream& operator<<(ostream& out, const MM& object) 
	{
		out << object.name << " " << object.age;
		return out;
	}
	string getName() const { return name; }
	int getAge()const { return age; }
protected:
	string name;
	int age;
};

bool compareByName(const MM& object) 
{
	return object.getName() == "蓝火";
}

void testTwo() 
{
	vector<MM> mm;
	mm.push_back(MM("月亮", 18));
	mm.push_back(MM("西施", 28));
	mm.push_back(MM("蓝火", 38));

	for (auto v : mm) 
	{
		cout << v << endl;
	}
	//删除操作注意点
	//方案一 迭代器
	for (vector<MM>::iterator iter = mm.begin(); iter != mm.end(); ) 
	{
		if (iter->getName() == "西施") 
		{
			//erase
			iter=mm.erase(iter);
		}
		else 
		{
			iter++;
		}
	}
	cout << "删除结果....." << endl;
	for (auto v : mm)
	{
		cout << v << endl;
	}
	vector<MM>::iterator result = find_if(mm.begin(), mm.end(), compareByName);
	if (result != mm.end()) 
	{
		cout << *result << endl;
	}
	vector<int> test = { 0,1,2,3,4,5,6,7,8 };
	test.erase(test.begin() + 2);
	for (auto v : test) 
	{
		cout << v << " ";
	}
	cout << endl;
}

int main() 
{
	testOne();
	testTwo();
	return 0;
}
```

## C++list

list容器就是C语言中学习的链表。

```c++
//插入
void push_back(Type data);
void push_front(Type data);
//删除
void pop_front():
void pop_back();

int size()
bool empty();

type  back();
type  front();
```

```c++
#include <list>
#include <string>
#include <iostream>
#include <functional>
using namespace std;
void testOne()
{
	list<int> iNum = { 1,2,3,4 };
	list<string> str;
	str.push_back("我是帅哥");
	str.push_front("你也是帅哥");
	cout << str.front() << endl;
	cout << str.back() << endl;

	cout << ":区间遍历" << endl;
	for (auto v : str) 
	{
		cout << v << endl;
	}
	cout << ":迭代器遍历" << endl;
	list<string>::iterator iter;
	for (iter = str.begin(); iter != str.end(); iter++) 
	{
		cout << *iter << endl;
	}
	//删除的方式遍历
	while (!str.empty())    //curSize==0
	{
		cout << str.front() << endl;
		str.pop_front();
	}
	cout << "size:" << str.size() << endl;
	while (!iNum.empty()) 
	{
		cout << iNum.back() << " ";
		iNum.pop_back();
	}
	cout << endl;
}
class MM 
{
public:
	MM(string name, int age) :name(name), age(age) {}
	void print() 
	{
		cout << name << "\t" << age << endl;
	}
	string getName()const 
	{
		return name;
	}
	int getAge() const 
	{
		return age;
	}
protected:
	string name;
	int age;
};
void testTwo() 
{
	list<MM> mm;
	mm.push_back(MM("mm", 18));
	mm.push_back(MM("西施", 38));
	for (auto v : mm) 
	{
		v.print();
	}
}
void print(list<int>& test) 
{
	for (auto v : test) 
	{
		cout << v << " ";
	}
	cout << endl;
}
//函数描述比较准则
bool compareByAge(const MM& one, const MM& two) 
{
	return one.getAge() < two.getAge();
}

bool compareByName(const MM& one, const MM& two)
{
	return one.getName() < two.getName();
}
bool findByName(const MM& one, string name) 
{
	return one.getName() == name;
}

void testThree() 
{
	
	list<int> test = { 3,1,2,5 };
	test.sort();					//排序 默认从小到大  
	print(test);
	test.reverse();					//反转
	print(test);

	test.sort(greater<int>());
	print(test);
	test.sort(less<int>());			//跟默认的方式是一样的
	print(test);

	list<MM> mm;
	mm.push_back(MM("mm", 18));
	mm.push_back(MM("西施", 38));
	mm.push_back(MM("貂蝉", 28));
	cout << ":年龄排序-->" << endl;
	mm.sort(compareByAge);
	for (auto v : mm)
	{
		v.print();
	}
	cout << ":姓名排序-->" << endl;
	mm.sort(compareByName);
	for (auto v : mm)
	{
		v.print();
	}
	cout << ":删除结果-->" << endl;
	//指定删除
	auto iter = find_if(mm.begin(), mm.end(),bind(findByName,placeholders::_1,"mm"));
	mm.erase(iter);
	for (auto v : mm)
	{
		v.print();
	}

	cout << ":迭代器删除-->" << endl;
	for (auto m = mm.begin(); m != mm.end();) 
	{
		if (m->getName() == "西施") 
		{
			m = mm.erase(m);
		}
		else 
		{
			m++;
		}
	}
	for (auto v : mm)
	{
		v.print();
	}
}
void testDeletAll()
{
	list<int> data = { 1,1,1,2,2,3,4,5,1 };
	for (auto m = data.begin(); m != data.end();)
	{
		if (*m == 1)
		{
			m = data.erase(m);
		}
		else
		{
			m++;
		}
	}
	for (auto v : data)
	{
		cout << v << " ";
	}
	cout << endl;

	list<MM> mm;
	mm.push_back(MM("mm", 18));
	mm.push_back(MM("西施", 38));
	mm.push_back(MM("貂蝉", 28));
	mm.push_back(MM("西施", 38));
	mm.push_back(MM("貂蝉", 28));

	//指定删除
	//auto iter = find_if(mm.begin(), mm.end(), bind(findByName, placeholders::_1, "西施"));
	//mm.erase(iter);
	cout << ":删除所有叫做西施的美女信息-->" << endl;
	list<MM>::iterator iter;
	iter = find_if(mm.begin(), mm.end(), bind(findByName, placeholders::_1, "西施"));

	while (iter!=mm.end())
	{
		iter=mm.erase(iter);
		iter = find_if(iter, mm.end(), bind(findByName, placeholders::_1, "西施"));
	}
	for (auto v : mm)
	{
		v.print();
	}
}
int main() 
{
	testOne();
	testTwo();
	testThree();
	testDeletAll();
	return 0;
}
```

## C++stack

stack叫做栈结构，是一种特殊的存储结构，FILO，栈结构体主要就是回退思想(悔棋，后退，寻路)，因为存储方式固定了，所以没有内置迭代器。

```c
//入栈
void push(Type  data);
void pop();

//获取栈顶元素
Type top()
int size();
bool empty();
```

```c
#include <stack>
#include<iostream>
using namespace std;
void testOne() 
{
	int num = 123;
	stack<int> data;
	while (num != 0) 
	{
		data.push(num % 2);
		num /= 2;
	}
	cout << "123二进制:";
	while (!data.empty()) 
	{
		cout << data.top();
		data.pop();
	}
	cout << endl;
}
class Solution 
{
public :
	bool isValid(string s) 
	{
		stack<char> result;
		for (auto v : s) 
		{
			if (v == '(' || v == '[' || v == '{') 
			{
				result.push(v);
			}
			else 
			{
				if (!result.empty())   //v='}'
				{
					char out = result.top();
					if (v == '}' && out != '{') 
					{
						return false;
					}
					if (v == ']' && out != '[') 
					{
						return false;
					}
					if (v == ')' && out != '(') 
					{
						return false;
					}
					result.pop();
				}
				else 
				{
					return false;
				}
			}
		}
		return result.empty();
	}
};


void testTwo() 
{
	//()[]{}
	//([{   }])
	//([)]
	Solution s;
	cout << s.isValid("()[]{}") << endl;
	cout << s.isValid("([{}])") << endl;
	cout << s.isValid("([)]") << endl;
}

int main() 
{
	testOne();
	testTwo();

	return 0;
}
```

## C++queue

### queue

queue 就是先进先出的一种存储结构，消息队列

```c++
//入栈
void push(Type  data);
void pop();

//获取栈顶元素
Type front()
int size();
bool empty();
```

```c++
#include <queue>
#include <deque>
#include <iostream>
using namespace std;
void testOne() 
{
	queue<int>  data;
	data.push(1);
	data.push(2);
	data.push(3);

	while (!data.empty()) 
	{
		cout << data.front()<< " ";
		data.pop();
	}
	cout << endl;
}



int main() 
{
	testOne();

	return 0;
}
```

### deque

```c++
//插入
void push_back(Type data);
void push_front(Type data);
//删除
void pop_front():
void pop_back();

int size()
bool empty();

type  back();
type  front();
```

```c++
#include <queue>
#include <deque>
#include <iostream>
using namespace std;
class MM 
{
public:
	MM(string name, int age) :name(name), age(age) {}
	void print() 
	{
		cout << name << " " << age << endl;
	}
protected:
	string name;
	int age;
};
void testDeque()
{
	deque<MM> mm;
	mm.push_back(MM("西施", 19));
	mm.push_back(MM("貂蝉", 28));

	//while (!mm.empty()) 
	//{
	//	mm.front().print();
	//	mm.pop_front();
	//}
	while (!mm.empty()) 
	{
		mm.back().print();
		mm.pop_back();
	}
}



int main() 
{
	testDeque();
	return 0;
}
```

### priority_queue

```c++
#include <queue>
#include <deque>
#include <iostream>
using namespace std;
class MM 
{
public:
	MM(string name, int age) :name(name), age(age) {}
	void print() const
	{
		cout << name << " " << age << endl;
	}
	bool operator>(const MM& object) const 
	{
		return this->age > object.age;
	}
	string getName() const 
	{
		return name;
	}
	int getAge() const 
	{
		return age;
	}
protected:
	string name;
	int age;
};
//仿函数
struct compareByAgeLess 
{
	bool operator()(const MM& one, const MM& two) const 
	{
		return one.getAge() < two.getAge();
	}
};

class compareByAgeGreater
{
public:
	bool operator()(const MM& one, const MM& two) const
	{
		return one.getAge() >two.getAge();
	}
};


void testPriorityQueue() 
{
	//偷懒版本
	cout << ":偷懒版本-->" << endl;
	priority_queue<int> q1;		//优先队列默认方式是less方式，出队的结果是从大到小
	q1.push(23);
	q1.push(45);
	q1.push(54);

	while (!q1.empty()) 
	{
		cout << q1.top() << " ";
		q1.pop();
	}
	//完整版本写法
	cout << endl << ":完整版本-->" << endl;
	priority_queue<int,vector<int>,less<int>> q2;		
	q2.push(23);
	q2.push(45);
	q2.push(54);
	while (!q2.empty())
	{
		cout << q2.top() << " ";
		q2.pop();
	}
	cout << endl << "从小到大出队:" << endl;
	priority_queue<int, vector<int>, greater<int>> q3;
	q3.push(23);
	q3.push(45);
	q3.push(54);
	while (!q3.empty())
	{
		cout << q3.top() << " ";
		q3.pop();
	}
	cout << endl << "自定义类型" << endl;
	cout << "不常用的写法，重载比较运算符" << endl;			//greater > less <
	priority_queue<MM, vector<MM>, greater<MM>> mm;
	mm.push(MM("西施", 18));
	mm.push(MM("貂蝉", 29));
	mm.push(MM("圆圆", 27));
	while (!mm.empty()) 
	{
		mm.top().print();			//注意问题，返回一个const对象
		mm.pop();
	}
	cout << endl << "常用方法:" << endl;
	cout << endl << "greater By less:" << endl;
	priority_queue<MM, vector<MM>, compareByAgeLess> mm1;
	mm1.push(MM("西施", 18));
	mm1.push(MM("貂蝉", 29));
	mm1.push(MM("圆圆", 27));
	while (!mm1.empty())
	{
		mm1.top().print();			//注意问题，返回一个const对象
		mm1.pop();
	}
	cout << endl << "greater By age:" << endl;
	priority_queue<MM, vector<MM>, compareByAgeGreater> mm2;
	mm2.push(MM("西施", 18));
	mm2.push(MM("貂蝉", 29));
	mm2.push(MM("圆圆", 27));
	while (!mm2.empty())
	{
		mm2.top().print();			//注意问题，返回一个const对象
		mm2.pop();
	}

}

int main() 
{
	testPriorityQueue();
	return 0;
}
```

## C++ Lambad表达式

Lambad表达式 就是函数指针的一种简单写法，最终Lambda返回的是一个函数指针，并且这个函数指针已经被初始化了。

```c++
//完整版本
[捕获方式](函数参数)->函数返回值{函数体;};
捕获方式:
[=] :用值的方式捕获变量
[&]: 用引用方式捕获外部变量
[this]: 用this指针捕获
[=,&x]: x用引用，其他变量用值的方式
[]: 不捕变量
```

```c++
#include <iostream>
#include <string>
#include <list>
using namespace std;
int Max(int a, int b) 
{
	return a > b ? a : b;
}

class MM 
{
public:
	MM() {}
	MM(string name, int age) :name(name), age(age) {}
	void printData() 
	{
		auto  func = [this]() {cout << name << "\t" << age << endl; };
		func();
	}
	string getName()const  { return name; }
	int getAge() const { return age; }
protected:
	string name="";
	int age=0;
};

int main()
{
	cout << "正常函数指针的操作：" << endl;
	int(*p)(int, int) = Max;
	cout << p(1, 2) << endl;
	cout << "完整版本:" << endl;
	auto pFunc = [](int a, int b)->int {return a > b ? a : b; };
	cout << pFunc(1, 2) << endl;
	cout << "缺省版本" << endl;
	auto func2 = []{cout << "无返回值，无参数的函数"; };
	func2();

	cout << "捕获方式:" << endl;		//所谓的捕获方式就是函数体使用外面的变量的方式
	int a = 1;
	int b = 2;
	//auto func3 = []() {cout << a << endl; cout << b << endl; };	//错误，不捕获不能使用外面的变量
	auto func4 = [=]() { /*a = 123 ;  错误，值方式捕获不能修改外面变量*/cout << a << endl; };
	func4();			//打印1
	auto func5 = [&]() { cout << a << endl; };
	func5();
	cout << a << endl;	//打印123
	//用值的方式捕获，程序的运行结果和第一调用调用的结果都是一样的。不会因为变量的改变，函数的调用结果改变
	a = 123;
	func4();			//打印1
	func5();

	MM mm;
	mm.printData();

	//不太认同写法
	//auto pFunc = [](int a, int b)->int {return a > b ? a : b; };
	//cout << pFunc(1, 2) << endl;
	//两句合成一句话
	cout <<endl<< [](int a, int b)->int {return a > b ? a : b; }(1, 3) << endl;


	list<MM> info;
	info.push_back(MM("西施",19));
	info.push_back(MM("貂蝉", 29));
	string name;
	cin >> name;
	list<MM>::iterator iter = find_if(info.begin(), info.end(),
		[=](const MM& object) {return object.getName() == name; });
	if(iter!=info.end())
		iter->printData();
	return 0;
}
```

## C++ set

set叫做集合，这个容器具有两个特性

+ 自带排序
+ 去重

多重集合 multiset

+ 只具有排序性

```c++
#include <set>
#include <string>
#include <functional>
#include <iostream>
using namespace std;
void testOne() 
{
	set<int> inum;
	set<int, less<int>> test;		//和默认创建一样的，从小到大
	set<int, greater<int>> test2;	//从大到小

	test.insert(1);
	test.insert(1);
	test.insert(444);
	test.insert(3);

	for (auto v : test) 
	{
		cout << v << " ";
	}
	cout << endl;

	for (set<int>::iterator iter = test.begin(); iter != test.end(); iter++) 
	{
		cout << *iter << " ";
	}
	cout << endl;
	cout << "删除操作：" << endl;
	auto result = find_if(test.begin(), test.end(), [](int value) {return value == 444; });
	test.erase(result);
	for (auto v : test)
	{
		cout << v << " ";
	}
	cout << endl;
}

class MM
{
public:
	MM(string name, int age) :name(name), age(age) {}
	void print() 
	{
		cout << name << "\t" << age << endl;
	}
	int getAge()const 
	{
		return age;
	}
protected:
	string name;
	int age;
};
class CmparetByAge 
{
public:
	bool operator()(const MM& one, const MM& two)const 
	{
		return one.getAge() > two.getAge();
	}
};
void testTwo() 
{
	set<MM, CmparetByAge> info;
	info.insert(MM("西施", 18));
	info.insert(MM("貂蝉", 29));
	info.insert(MM("苏小小", 28));

	for (auto v : info) 
	{
		v.print();
	}
}
void testThree() 
{
	multiset<int> data;
	data.insert(1);
	data.insert(1);
	data.insert(2);
	data.insert(3);

	for (auto v : data) 
	{
		cout << v << " ";
	}
	cout << endl;
}

int main() 
{
	testOne();
	testTwo();
	testThree();
	return 0;
}
```

## C++ map

map是映射，映射就是数学的对应关系 ，例如 y=x

+ map中存储的是数对类型: pair<_Ty1,Ty2>
  + first : 键
  + second:值
+ map具有排序性，按照键排序 ，按照first进行的排序
+ map键唯一性

mutimap映射，键不唯一

+ 不存在下标法插入
+ 具有排序

```C++
#include <map>
#include <iostream>
#include <string>
using namespace std;
void testOne() 
{
	map<int, string> data;
	//插入方式
	//直接下标法
	data[0] = string("string");
	data[-1] = string("西施");
	//insert函数插入
	data.insert(pair<int, string>(3, "貂蝉"));
	//make_pair 构建一个pair对象
	data.insert(make_pair<int, string>(5, "苏小小"));
	data.insert(pair<int, string>(3, "星"));					//键相同不做插入
	data[0] = string("npc");								//下表法 保留最新值
	for (auto v : data)			//每一个v都是一个pair类型
	{
		cout << v.first << ":" << v.second << endl;
	}

	for (auto iter = data.begin(); iter != data.end(); iter++) 
	{
		cout << iter->first << ":" << iter->second << endl;
	}
	cout << "删除:" << endl;
	auto iter = find_if(data.begin(), data.end(), [](const pair<int, string>& object) {return object.first == 3; });
	data.erase(iter);
	for (auto v : data)			//每一个v都是一个pair类型
	{
		cout << v.first << ":" << v.second << endl;
	}
}
class MM 
{
public:
	MM(string name, int age) :name(name), age(age) {}
	void printMM() const
	{
		cout << name << "\t" << age<<"配对:\t";
	}
	int getAge()const { return age; }
protected:
	string name;
	int age;
};
class CompareByAge 
{
public:
	bool operator()(const MM& one, const MM& two)const 
	{
		return one.getAge() < two.getAge();
	}
};

class GG
{
public:
	GG() {}
	GG(string name, int age) :name(name), age(age) {}
	void printGG() const
	{
		cout << name << "\t" << age << endl;
	}
protected:
	string name;
	int age;
};


void testTwo() 
{
	map<MM, GG, CompareByAge> test;
	test[MM("西施", 18)] = GG("npc7", 28);
	test[MM("貂蝉", 28)] = GG("星", 38);
	test[MM("苏小小", 16)] = GG("蓝火", 18);

	for (auto v : test) 
	{
		v.first.printMM();
		v.second.printGG();
	}
}
void testThree() 
{
	multimap<int, string,greater<int>> test;
	test.insert(pair<int, string>(1, "西施"));
	test.insert(pair<int, string>(1, "西施"));
	test.insert(pair<int, string>(2, "西施"));
	test.insert(pair<int, string>(1, "貂蝉"));
	test.insert(pair<int, string>(1, "苏小小"));

	for (auto v : test) 
	{
		cout << v.first << ":" << v.second << endl;
	}
}
int main() 
{
	pair<int, string> pairData;
	pairData.first = 123;
	pairData.second = "string";
	testOne();
	testTwo();
	testThree();
	return 0;
}
```

## C++ initializer_list

initializer_list是列表数据，就是{a,b,c....}数据

```c++
#include <iostream>
#include <vector>
#include <initializer_list>
using namespace std;
class MM 
{
public:
	MM() {}
	MM(string name, int age) :name(name), age(age) 
	{
		cout << "调用构造函数" << endl;
	}
protected:
	string name;
	int age;
};

void testOne() 
{
	initializer_list<int> data = { 1,2,3,4,5,6 };
	for (initializer_list<int>::iterator iter = data.begin(); iter != data.end(); iter++)
	{
		cout << *iter << " ";
	}
	cout << endl;

}
template <class _Ty>
class myvector 
{
public:
	myvector(int size) :curSize(0) 
	{
		elem = new _Ty[size];
	}
	myvector(const initializer_list<_Ty>& data) :elem(new _Ty[data.size()])
	{
		for (auto v : data) 
		{
			elem[curSize++] = v;
		}
	}
	void print() 
	{
		for (int i = 0; i < curSize; i++) 
		{
			cout << elem[i] << " ";
		}
		cout << endl;
	}
protected:
	_Ty* elem;
	int curSize;
};


int main() 
{
	vector<int> data1 = { 1,2,3,4,5 };
	vector<int> data2 = { 1};
	vector<int> data3 = { 1,2,3,4,5,3,4,5 };
	MM mm = { "sd",18 };
	testOne();
	myvector<int> myData1 = { 1,2,3,4,5 };
	myvector<int> myData2 = { 1 };
	myvector<int> myData3 = { 1,2,3,4,5,3,4,5 };
	myData1.print();
	myData2.print();
	myData3.print();
	return 0;
}
```

## C++ tuple

tuple就是元组的意思，它是一个可变参模板类，也就是传入的参数随便写，并且数目不定,目前掌握使用即可，原理后面拓展内容讲

```c
#include <tuple>
#include <string>
#include <iostream>
using namespace std;

void testCreate() 
{
	tuple<string, int, int, string> mminfo = {"貂蝉",18,1001,"17718832345"};
	tuple<double, double, double> score = { 87.2,98.9,56.9 };

	tuple<int, string> data = make_tuple(1, "MM");
	tuple<string, string> str = forward_as_tuple("美女", "貂蝉");
	tuple<string, int, int> mm[4];
}
void visitedData()
{
	tuple<string, int, int> data = { "貂蝉",19,1001 };
	//get模板方法
	cout << get<0>(data) << "\t" << get<1>(data) << "\t" << get<2>(data) << endl;
#define Data(index) get<index>(data)
	cout <<Data(0) << "\t" << Data(1) << "\t" << Data(2) << endl;
	//错误代码
	//for (int i = 0; i < 3; i++) 
	//{
	//	cout << get<i>(data) << "\t";
	//}
	//cout << endl;
	//tie访问
	string name;
	int age;
	int num;
	tie(name, age, num) = data;
	cout << name << "\t" << age << "\t" << num << endl;
	//忽略不想要的数据
	tie(name, ignore, ignore) = data;
	cout << "忽略获取值:" << name << endl;

}
void testTuple() 
{
	tuple<string, string> mm = { "小美","艺术学院" };
	tuple<int, int> data = { 18,1001 };
	//tuple<string,stirng,int,int>
	auto info = tuple_cat(mm, data);
	string name;
	string major;
	int age;
	int num;
	tie(name, major, age, num) = info;
	cout << name << "\t" << major << "\t" << age << "\t" << num << endl;
}

int main() 
{
	visitedData();
	testTuple();

	return 0;
}
```

## C++仿函数

仿函数是让类名模仿函数调用的行为---->函数名(参数)  ，让类名能够 : 类名(参数) 方式使用

自己写仿函数关键点在于重载()运算符，所谓的模仿函数的行为，本质先构造一个无名对象，然后通过对象隐式调用重载函数

+ 自己写仿函数
+ 标准库中的仿函数(不需要记，自己会写了，自己创造)

仿函数一般有两个作用:

+ 充当比较准则
+ 充当算法或者容器构建的参数

````c++
#include <iostream>
#include <functional>			//仿函数的头文件
#include <set>
#include <map>
#include <vector>
#include <algorithm>
using namespace std;

class Sum 
{
public:
	int operator()(const int& a, const int& b) 
	{
		return a + b;
	}
};
//No.1 仿函数的调用
void testCallFunctional() 
{
	Sum object;
	cout << object.operator()(1, 2) << endl;
	cout << object(3, 2) << endl;
	cout << Sum{}(3, 2) << endl;	//Sum(3, 2)不知道怎么解析，和调用构造函数产生歧义，用一个{}帮助解析
}



//No.2 充当函数指针和回调函数
template<class _Ty, class _Pr>		//_Pr是一个仿函数
void BubbleSort(_Ty array[], int size) 
{
    bool isok;
    for (int i = size - 1; i > 0; i--)
    {
		isok = false;
        for (int j = 0; j < i; j++)
        {
            if (_Pr{}(array[j], array[j + 1]) == false) 
			{
				_Ty temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;
                isok = true;
			}		
		}
        if (!isok)
			break;
	}
}

template <class _Ty>
struct my_less 
{
	bool operator()(const _Ty& a, const _Ty& b) const
	{
		return a < b;
	}
};

template <class _Ty>
struct my_greater
{
	bool operator()(const _Ty& a, const _Ty& b) const
	{
		return a > b;
	}
};

void testmysort() 
{
	int arr[6] = { 1,2,5,3,4 ,0};
    // 从小到大
	BubbleSort<int, my_less<int>>(arr, 6);
	for (auto v : arr) 
	{
		cout << v << " ";
	}
	cout << endl;
    // 从大到小
	BubbleSort<int, my_greater<int>>(arr, 6);
	for (auto v : arr)
	{
		cout << v << " ";
	}
	cout << endl;
}

//标准库仿函数
void teststdfunctional()
{
	//算术类
	cout << plus<int>{}(1, 2) << endl;
	cout << modulus<int>{}(3, 2) << endl;
	//关系类
	cout << less<int>{}(1, 2) << endl;
	cout << greater<int>{}(1, 2) << endl;
	cout << greater_equal<int>{}(3, 2) << endl;
	//逻辑类
	cout << logical_and<int>{}(1, 2) << endl;
	//位运算类
	cout << bit_and<int>{}(1, 2) << endl;
	//....

}
int main() 
{
	testCallFunctional();
	testmysort();
	teststdfunctional();
	set<int, less<int>> s1;
	set<int, greater<int>> s2;
	map<int, string, greater<int>> m1;

	vector<int> v1 = { 1,2,3,9,0 };
	sort(v1.begin(), v1.end(), greater<int>());
	for (auto v : v1) 
	{
		cout << v << " ";
	}
	cout << endl;
	return 0;
}
````

## C++迭代器

### 分类

迭代器是一个类中类，让类中类对象模仿指针的行为，迭代器通常是用来访问容器的

| 分类         | 迭代器类型                           | 开始位置  | 结束位置 |
| ------------ | ------------------------------------ | --------- | -------- |
| 正向迭代器   | 容器名::iterator iter;               | begin()   | end()    |
| 反向迭代器   | 容器名::reverse_iterator iter;       | rbegin()  | rend()   |
| 常正向迭代器 | 容器名::const_iterator iter;         | cbegin()  | cend()   |
| 常反向迭代器 | 容器名::const_reverse_iterator iter; | crbegin() | crend()  |

按照功能上来说分为三类:

+ 正向迭代器
+ 双向迭代器:list set map
+ 随机访问迭代器： array,vector,deque

注意点： stack与queue以及priority_queue 不支持迭代器访问

### 辅助函数

+ advance(iter,n):移动
+ distance(beginPos ,endPos): 元素个数
+ iter_swap(first,second):交换

### 流型迭代器

输出流型迭代器

+ ostream_iterator<type> object(ostream& out);
+ ostream_iterator<type> object(ostream& out,const char* str);
+ object=value  : 等效  cout<<value

输入流型迭代器

+ istream_iterator<type> object;       //End-of-stream
+ istream_iterator<type> object(istream& in);
+ *object  等效 cin操作

```c++
#include <vector>
#include <array>
#include <map>
#include <set>
#include <list>
#include <string>
#include <iostream>
#include <iterator>
using namespace std;
void testFirst() 
{
	vector<int>::iterator viter;
	array<int, 5>::iterator aiter;
	map<int, string>::iterator miter;

	vector<int> test = { 1,2,3,4,5,6,7,8 };
    // 正向迭代器
	for (vector<int>::reverse_iterator iter = test.rbegin(); iter != test.rend(); iter++)
	{
		cout << *iter << " ";
	}
	cout << endl;
    // 常反向迭代器
	for (vector<int>::const_reverse_iterator iter = test.crbegin(); iter != test.crend(); iter++)
	{
		cout << *iter << " ";
	}
	cout << endl;
}

// 辅助函数
void testSecond() 
{
	list<int>  data = { 1,2,3,4,6 };
	list<int>::iterator iter = data.begin();
	//cout << *(iter + 2) << endl;					//链表中没有
	advance(iter, 2);  // 进行移动
	cout << *iter << endl;
	cout<<distance(data.begin(),data.end())<<endl;  //计算元素个数
}

//流型迭代器
void IOIterator()
{
    cout << "输出流型迭代器测试:";
	ostream_iterator<int> object(cout);
	object = 1234;  // 相当于cout << 1234
	//copy
	vector<int> data = { 1,2,3,4,5 };
	cout << endl;
	copy(data.begin(), data.end(), ostream_iterator<int>(cout));  // 等效于打印data的数据
	cout << endl;
	copy(data.begin(), data.end(), ostream_iterator<int>(cout, " "));  // 空格作为间隔
	cout << endl;
    
    // 输入流不常用
	cout << "输入流型迭代器测试:"; 
	vector<int> input;
	istream_iterator<int> end;
	istream_iterator<int> inputIter(cin);
	while (inputIter != end) 
	{
		input.push_back(*inputIter);
		inputIter++;
	}
	for (auto v : input) 
	{
		cout << v << " ";
	}
	cout << endl;

}
int main() 
{
	testFirst();
	testSecond();
	IOIterator();
	return 0;
}
```

## C++函数适配器

函数适配器: 就是bind函数，操作函数指针，让函数指针能够适应回调函数的参数，简单来说就是让函数指针存在不同的调用形态

```c++
#include <functional>
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
void print(int a, int b, int c) 
{
	cout << a <<" "<< b << " " << c << endl;
}

//void printData(void(*pFunc)(int, int, int), int a, int b, int c)
//{
//	pFunc(a，b，c);
//}

template <class _Pr>
void printData(_Pr pr, int a, int b)
{
	pr(a, b);
}


void testFirst() 
{
	auto p = print; // 函数指针
	p(1, 2, 3);
	//printData(p,1,2);			//print不适用于printData
	auto p2 = bind(print, placeholders::_1, placeholders::_2, placeholders::_3);  //绑定普通函数
    //
	auto p3 = bind(print, placeholders::_1, placeholders::_2, 6);  // 这样第三个参数默认是6
	p3(9, 9);
	printData(p3, 2, 3);		//适配完成后适用于这个接口
    //
	auto p4 = bind(print, placeholders::_1, 9, 9);
	p4(6);
	auto p5 = bind(print, 8, 8, 8);
	p5();

	//条件筛选  //count_if条件统计
	vector<int> score = { 98,26,89,54,42,34,87,94 };
	cout << count_if(score.begin(), score.end(), [](int& num) {return num >= 60; }) << endl; // 正常写法
	cout << count_if(score.begin(), score.end(),bind(greater_equal<int>(),placeholders::_1,60)) << endl;  // 仿函数写法
}

class Test 
{
public:
	void printTest(int a, int b, int c) 
	{
		cout << a << " " << b << " " << endl;
	}
};

void testSecond() 
{
	//绑定普通函数
	auto p = bind(print, placeholders::_1, 9, 9);
	p(8);
    
    
	//绑定类中的成员函数
    Test test;
    //方式1:
	auto testFunc = &Test::printTest;
	(test.*testFunc)(1, 2, 3);
    
	// 方式2:
	auto pFunc = bind(&Test::printTest, &test, std::placeholders::_1, std::placeholders::_2, std::placeholders::_3);
	pFunc(1, 2, 3);
    
	auto pFunc2 = bind(&Test::printTest, &test, std::placeholders::_1, std::placeholders::_2, 8);
	printData(pFunc2, 2, 3);
}
int main() 
{
	testFirst();
	testSecond();
	return 0;
}
```

## C++函数包装器

函数包装器就是就是把函数指针包装成为一个对象，function<type>

+ function<type> object(pFunc);
+ function<type> object=pFunc;

type:函数返回值类型(参数类型),  举例包装int sum(int a,int b);   type是: int(int,int)

通过包装后的对象调用函数:   直接把包装器对象当做函数名即可

```c++
#include <iostream>
#include <string>
#include <functional>
#include <string>
using namespace std;
int Max(int a, int b) 
{
	return a > b ? a : b;
}

class Test
{
public:
	void operator()(string info)
	{
		cout << info << endl;
	}
	static void print(int a, int b)
	{
		cout << a + b << endl;
	}
    //包装operator隐式对象转换的指针
	using _Pr = void(*)(int, int);  //起别名
	operator _Pr()
	{
		return print;
	}
};

void testFirst() 
{
	//包装普通函数
	function<int(int, int)> pMax = &Max;   // 把函数(指针)包装成对象
	cout << pMax(1, 2) << endl;
	//包装仿函数
	//function<void(string)> func = Test();
	Test test;
	function<void(string)> func = test;
	func("仿函数");
	//包装operator隐式对象转换的指针
	function<void(int,int)> func2 = test;
	func2(1, 2);
}

void printData(int a, double b, string c) 
{
	cout << c << endl;
}
void testSecond()
{
	//包装器和适配器
	//直接包装
	function<void(int, double, string)> func1 = printData;
	func1(1, 1.1, "正常包装普通函数");

	function<void(int, double)> func2 = bind(printData, std::placeholders::_1, placeholders::_2, "正常适配");
	func2(1, 1.2);

	function<void(double, int)> func3 = bind(printData, std::placeholders::_2, placeholders::_1, "不正常适配");
	func3(1.2, 1);
    
	//void printData(int a, double b, string c) 
	function<void(string, int, double)>  func4 = bind(printData,
		std::placeholders::_2,				//包装器的第二个参数要是原函数的第一个参数
		placeholders::_3,					//包装器的第三个参数要是原函数的第二个参数
		placeholders::_1);					//包装器的第一个参数要是原函数的第三个参数

	func4("调整参数", 1, 1.2);
}

int main() 
{
	testFirst();
	testSecond();

	return 0;
}
```

# C++STL算法

## 查找算法

- adjacent_find : 查重复数，返回首个元素iter

- `binary_search`: 二分查找

- count: 区间统计

- count_if: 范围查找统计个数

  equal: 比较

- equal_range :区间元素比较

- find:区间查找元素

- find_first_of:区间查找第一次出现值

- find_if : 条件查找

- upper_bound:查找最后一个大于等于val的位置

- lower_bound: 查找第一个大于等于val的位置

- search:子序列查找位置

- search_n:子序列查找出现次数

## 排序和通用算法

排序和通用算法就是用来给容器排序，主要的排序算法主要是有以下14个：

- merge: 归并排序，存于新容器

- inpace_merge: 归并排序，覆盖原区间

- sort: 排序，更改原容器顺序

- stable_sort: 排序，保存原容器数据顺序

  nth_element: 关键字排序

- partition:范围排序

- partial_sort:范围排序

- partial_sort_copy:范围排序外加复制操作

- stable_partition: 范围排序，保存原容器顺序

- random_shuffle: 随机排序

- reverse:逆序原容器

- reverse_copy: 逆序容器保存到新容器

- rotate:移动元素到容器末尾

- rotate_copy:移动元素到新容器

## 删除和替换算法

删除和替换算法一般都会修改容器的存储现状，一般处理删除和替换的算法主要有以下的15种：

- copy: 拷贝函数

- copy_backward: 逆序拷贝

- iter_swap: 交换

- remove: 删除

  remove_copy: 删除元素复制到新容器

- remove_if:条件删除

- remove_copy_if:条件删除拷贝到新容器

- replace:替换

- replace_copy: 替换，结果放到新容器

- replace_if: 条件替换

- replace_copy_if:条件替换，结果另存

- swap: 交换

- swap_range:区间交换

- unique:去重

  unique_copy:去重，结果另存

## 排列组合算法

**提供计算给定集合按一定顺序的所有可能排列组合 ，主要有以下两个:**

next_permutation:下一个排序序列的组合

prev_permutation:上一个排序序列的组合

**算术运算算法主要用来做容器的算术运算，使用的时候加上numeric头文件，主要有以下4个：**

accumulate:区间求和

partial_sum:相邻元素的和

inner_product:序列内积运算

adjacent_difference:相邻元素的差

## 生成和异变算法

生成和一遍算法总共有以下6个下，相对于来说for_each用的相对于来说更多一些:

for_each:迭代访问

fill:填充方式初始容器

fill_n:指定长度填充容器

generate_n:填充前n个位置

transform:一元转换和二元转换

## 关系算法

关系算法类似与条件表达式一样的作用，主要用来判断容器中元素是否相等等运算，主要有以下8个：

equal:两容器元素是否都相同

includes:是否是包含关系

lexicographical_compare:比较两个序列

max:求最大值

max_element:返回最大值的iterator

min:求最小值

min_element:求最小值的iterator

mismatch:找到第一个不同的位置

## 集合算法

集合算法主要是集合上的一些运算，例如集合加法：并集，集合的减法：差集，还有交集。主要有以下4个：

set_union:并集

set_intersection:交集

set_difference:差集

set_symmetric_difference:对称差集

## 堆算法

堆算法，就是把容器当做堆去操作，主要算法函数只有以下4个：

make_heap:生成一个堆

pop_heap:出堆

push_heap:入堆

sort_heap:堆排序

## 综合代码

```c++
#include <iostream>
#include <vector>
#include <list>
#include <ctime>
#include <array>
#include <cstdlib>
#include <string>
#include <numeric>
#include <functional>
#include <algorithm>
#include <iterator>
using namespace std;
void test() 
{
	vector<int> data = { 1,2,3,4,5,6,7,8,9 };
	int num = count_if(data.begin(), data.end(), [](int data) {return data > 5; });
	cout << num << endl;
	auto result = find_if(data.begin(), data.end(), [](int data) {return data == 5; });
	if (result != data.end()) 
	{
		cout << *result << endl;
	}
	bool bresult = binary_search(data.begin(), data.end(), 5);
	if (bresult)
	{
		cout << "找到" << endl;
	}
	int arr[10] = { 1,2,3,4,0,9,8,7,6,5 };
	sort(arr, arr + 10);
	for (auto v : arr) 
	{
		cout << v << " ";
	}
	cout << endl;
	//list 内置排序算法
	list<int> listData = { 3,1,2 };
	listData.sort(greater<int>());
	for (auto v : listData) 
	{
		cout << v << " ";
	}
	cout << endl;
	reverse(listData.begin(), listData.end());
	for (auto v : listData)
	{
		cout << v << " ";
	}
	cout << endl;
	string  str = "ILoveyou";					//汉子有问题
	reverse(str.begin(), str.end());
	cout << str << endl;
	
	random_shuffle(str.begin(), str.end());		//voLyuoIe
	cout << str << endl;
	//"sdf"
	//--->密钥 "123"
	vector<int> first = { 1,3,5 };
	vector<int> second = { 2,4 };
	vector<int> three(first.size()+second.size());
	merge(first.begin(), first.end(), second.begin(), second.end(), three.begin());
	for (auto v : three)
	{
		cout << v << " ";
	}
	cout << endl;
	vector<int> vec(4);
	int arr2[4] = { 1,2,3,4 };
	copy(arr2, arr2 + 4, vec.begin());
	for (auto v : vec) 
	{
		cout << v << " ";
	}
	cout << endl;
	copy(vec.begin(), vec.end(), ostream_iterator<int>(cout, " "));
	cout << endl;
	list<int> rev = { 1,2,3,4,5,6,8 };
	//不会影响元素的总个数，后面的往前移动
	remove_if(rev.begin(), rev.end(), [](int data) {return data == 6; });
	copy(rev.begin(), rev.end(), ostream_iterator<int>(cout, " "));
	cout << endl;
	string str3 = "abcde****dsf******fd*********";
	string str4;
	str4.resize(str3.size());
	unique_copy(str3.begin(), str3.end(),str4.begin());
	cout << str3 << endl;
	cout << str4 << endl;
	//{a,b,c}  a<b<c   1 2 3
	//上一个: 1 3 2 ---> 1 2 3
	//下一个: 1 2 3 ---> 1 3 2

	array<int, 3> value = { 1,2,3 };
	int index = 1;
	do 
	{
		cout << index << ":";
		for (auto v : value) 
		{
			cout << v;
		}
		cout << endl;
		index++;
	} while (next_permutation(value.begin(), value.end()));

	int sum = 0;
	cout << accumulate(value.begin(), value.end(), sum) << endl;

	vector<int> row = { 10,2,3 };
	vector<int> cols = { 10,5,6 };
	cout << inner_product(row.begin(), row.end(), cols.begin(),0) << endl;

	for_each(row.begin(), row.end(), [](int data) {cout << data << " "; });
	cout << endl;

	for_each(row.begin(), row.end(), [](int& data) {data += 5; cout << data << " "; });
	cout << endl;

	cout << *max(row.begin(), row.end()-1) << endl;
	vector<int> one = { 1,2,3,4,5 };
	vector<int> two = { 4,5,6,7,8 };
	vector<int> snum(one.size() + two.size());
	set_union(one.begin(), one.end(), two.begin(), two.end(), snum.begin());
	for (auto v : snum) 
	{
		cout << v << " ";
	}
	cout << endl;

}
void testHeap() 
{
	vector<int>  data = { 1,9,2,8,4,6,0 };
	make_heap(data.begin(), data.end());
	for (auto v : data) 
	{
		cout <<v<<" ";
	}
	cout << endl;
	//pop_heap(data.begin(), data.end());
	//for (auto v : data)
	//{
	//	cout << v << " ";
	//}
	//cout << endl;
	while (!data.empty()) 
	{
		pop_heap(data.begin(), data.end());	//不会删除
		cout << data.back()<<" ";
		data.pop_back();				//真正的删除操作
	}
	cout << endl;

	vector<int> value = { 1,3,4,5,6,7,9,0 };
	make_heap(value.begin(), value.end(),greater<int>());
	for (auto v : value)
	{
		cout << v << " ";
	}
	cout << endl;
	sort_heap(value.begin(), value.end(), greater<int>());//sort_heap和make_heap一定要一致
	for (auto v : value)
	{
		cout << v << " ";
	}
	cout << endl;

}

int main() 
{
	srand((unsigned int)time(nullptr));
	//test();
	testHeap();
	return 0;
}
```

# C++智能指针

智能指针是用对象的方式管理指针,所谓的智能体现在不需要认为释放new的内存,实质是通过析构函数自动调用的特性实现的,在使用智能指针的时候一般都是构建对象 ,不是new一个对象.

## 共享型智能指针

```c++
#include <memory>
#include <string>
#include <iostream>
#include <vector>
#include <cstdio>
using namespace std;
/*

*/
void testOne() 
{
	shared_ptr<int> p1;			//无参构造
	if (!p1) 
	{
		cout << "空的智能指针对象" << endl;
		//return;
	}
	shared_ptr<int> p2(new int(123));		//new 一个int内存 并且做初始化
	//shared_ptr<int> p2 = new int(123); 错误
	shared_ptr<int> p3 = make_shared<int>(1234);
	//怎么访问数据
	//直接把智能指针对象当做指针即可
	cout << *p3 << endl;
	//cout << p3[0] << endl;  //错误,没有下标法使用方式
	//获取管理对象原生指针
	int* pNum = p3.get();
	cout << *pNum << endl;
	cout << pNum[0] << endl;
	//获取到原生指针的时候千万不要自己手动方式
	//delete pNum;
	//成员函数: use_count()
	cout <<"管理对象数:" << p3.use_count() << endl;
	shared_ptr<int> p4(p3);
	cout << "管理对象数:" << p3.use_count() << endl;
}
class MM 
{
public:
	MM(string name,int age):name(name),age(age) {}
	MM(string name) :name(name), age(0) {}
	MM() :name(""), age(0) {}
	void print() 
	{
		cout << name << "\t" << age << endl;
	}
	~MM() 
	{
		cout << "释放成功!" << endl;
	}
protected:
	string name;
	int age;
};
void testTwo() 
{
	shared_ptr<MM> pMM(new MM("name1", 18));
	pMM->print();
	vector<MM*> arr;
	arr.push_back(new MM("name1", 20));
	arr.pop_back();
	arr.clear();
	//实际应用比较多写法
	vector<shared_ptr<MM>> arr2;
	shared_ptr<MM> p(new MM("name2", 20));
	arr2.push_back(p);
	shared_ptr<MM> pMM2 = make_shared<MM>("name3");
	pMM2->print();
}

void testThree() 
{
	shared_ptr<int>  p(new int[4]{1,2,3,4});
	int* pnum = p.get();
	for (int i = 0; i < 4; i++) 
	{
		cout << pnum[i] << "\t";
	}
	cout << endl;
	//手动写删除器的情况,
	//特殊内存
	//delete [] pMM;
	//C语言文件指针  fopen搞内存  free释放
	shared_ptr<MM>  pMM(new MM[4], [](MM*& pMM) {delete[] pMM; });
	shared_ptr<FILE> pfile(fopen("1.txt", "w+"), [](FILE*& file) {free(file); });
}
void printMM(shared_ptr<MM>& pMM) 
{
	pMM->print();
}
shared_ptr<int> returnPoint(int num) 
{
	return shared_ptr<int>(new int(num));
}

int main() 
{
	testOne();
	testTwo();
	testThree();
	return 0;
}
```

## 弱引用型智能指针

weak_ptr 弱引用型智能指针,不会累计计数,存在意义是为了解决shared_ptr导致的循环引用问题

```C++
#include <iostream>
#include <memory>
using namespace std;
class B;
class A
{
public:
	~A() 
	{
		cout << "A" << endl;
	}
	weak_ptr<B> a;
};
class B 
{
public:
	~B()
	{
		cout << "B" << endl;
	}
	weak_ptr<A> b;
};
void testLoopUse() 
{
	shared_ptr<A> ao(new A);
	shared_ptr<B> bo(new B);
	ao->a = bo;
	bo->b = ao;
}

void test_weak_ptr() 
{
	//1.weak_ptr只能从shared_ptr或者已有的weak_ptr 去构造,不能直接管理对象
	//2.不能直接访问管理的对象 (*或者->访问)
	//3.访问数据方式只能通过lock函数访问shared_ptr 然后再去访问数据
	shared_ptr<int> p(new int(123));
	cout << "count:" << p.use_count() << endl;
	weak_ptr<int> w(p);
	cout << "count:" << w.use_count() << endl;
	weak_ptr<int> w2(w);
	cout << "count:" << w2.use_count() << endl;
	//访问数据
	cout << *w.lock() << endl;
	shared_ptr<int> object = w.lock();
	cout << *object << endl;
}
int main() 
{

	testLoopUse();
	test_weak_ptr();
	return 0;
}
```

## 独享型智能指针

unique_ptr 独享型就是一个对象永远都只有一个智能对象管理,实现本质是禁止拷贝,禁止复制

+ move函数转交所有权
+ 通过reset函数 结合release函数转交所有权

```c++
#include <iostream>
#include <memory>
using namespace std;
void testOne() 
{
	unique_ptr<int> p1(new int(1234));
	cout << *p1 << endl;
	unique_ptr<int> p2;
	//p2 = p1;						//错误
	//unique_ptr<int> p3(p2);		//错误
	p2 = move(p1);
	cout << *p2 << endl;
	//cout << *p1 << endl;			//错误,p1 失去了管理对象

	unique_ptr<int> p3(new int(435));
	p3.reset(p2.release());
	cout << *p3 << endl;
}
class MM 
{
public:
	MM() {}
	void print() 
	{
		cout << "打印测试" << endl;
	}
	~MM() { cout << "析构完成..." << endl; }
protected:
};
void testTwo() 
{
	//unique_ptr 删除器写法,需要手动写入删除器的类型
	unique_ptr<MM,void(*)(MM*&)> pMM(new MM[4], [](MM*& pMM) {delete[] pMM; });
    
	using FUNC = void(*)(MM*&);  // 起别名
	unique_ptr<MM, FUNC> pMM2(new MM[4], [](MM*& pMM) {delete[] pMM; });
}

// 当作参数使用,必须用引用
void printUnique(unique_ptr<MM>& pMM) 
{
	pMM->print();
}

int main() 
{
	testOne();
	testTwo();
	unique_ptr<MM> pMM(new MM);
	printUnique(pMM);
	pMM->print();
	return 0;
}
```

# C++折叠参数

折叠参数就是一个参数包, 代表是多个未知,tuple元组就是一个折叠参数的使用

折叠参数类型:

+ typename  ...Args  ,   Args参数包的包名 ,  本质是声明一个Args折叠参数类型
+ Args ...arg ,   折叠参数包类型的变量
+ ...  理解为多个意思

## 函数模板中使用折叠参数

+ 递归方式展开
+ 列表数据展开
+ 完美转发的方式展开

```c++
#include <iostream>
#include <string>
#include <functional>
#include <initializer_list>
using namespace std;

//递归的方式剥离参数展开
template <typename _Ty>
void print(_Ty  data) 
{
	cout << data << endl;
}
template <typename _Ty, typename ...Args>
void print(_Ty head, Args ...args)		//{1, 2, "string", "sdg", 1.3}
{
	cout << head << "\t";	//head=1  args...={2, "string", "sdg", 1.3} ....  {1.3}
	print(args...);
}
//列表的方式展开
template <typename _Ty>
void printData(_Ty  data)
{
	cout << data << "\t";
}
template <typename ...Args>
void printArgs(Args ...args) 
{
	//int array[] = { (printData(args),0)... };
	initializer_list<int>{ (printData(args), 0)...};
	cout << endl;
}

class Test 
{
public:

	void testFunc() 
	{
		if (func) 
		{
			func();		//统一调用接口
		}
	}
	template <typename Func, typename ...Args>
	void connect(Func&& f, Args&& ...args)
	{
		func = bind(forward<Func>(f), forward<Args>(args)...);
	}
protected:
	function<void()> func;
};

void  sum(int a, int b) 
{
	cout << a + b << endl;
}
void printTest() 
{
	cout << "提示信息" << endl;
}

int main() 
{
	print(1, 2, "string", "sdg", 1.3);
	print(1, 2, "string", "sdg", 1.3, 1, 2, "string", "sdg", 1.3, 1, 2, "string", "sdg", 1.3);
	printArgs(1, 2, "string", "sdg", 1.3);
	printArgs(1, 2, "string", "sdg", 1.3, 1, 2, "string", "sdg", 1.3, 1, 2, "string", "sdg", 1.3);
	Test test;
	test.connect(sum, 1, 2);
	test.testFunc();
	test.connect(printTest);
	test.testFunc();

	test.connect([](int a, int b) {cout << a + b << endl; },3,4);
	test.testFunc();
	return 0;
}
```

## 类模板中使用折叠参数

展开方式:

+ 继承+模板特化的方式展开
+ 递归的方式展开

```c++
#include <iostream>
#include <string>
#include <tuple>
using namespace std;

template <typename ...Args>
class Test;

// 特化
template <>
class Test<> {};

template <class _Ty,class ...Args>
class Test<_Ty, Args...> :public Test<Args...> 
{
public:
	Test() {}
	Test(_Ty data, Args ...args) :data(data), Test<Args...>(args...) {}
	Test<Args...>& getObject() 
	{
		return *this;
	}
	_Ty& getData() 
	{
		return data;
	}
protected:
	_Ty data;
};
void testFirst() 
{
	Test<string, int, double>  test("str", 1, 1.1);
	cout << test.getData() << "\t" << test.getObject().getData() << "\t" << test.getObject().getObject().getData() << endl;
    
	Test<string, string>  test1("str1", "str2");
	cout << test1.getData() << "\t" << test1.getObject().getData() << endl;
}


// 第二种方案 
template <class ...Args>
class my_tuple;

template <>
class my_tuple<> {};

template <typename _Ty, typename ...Args>
class my_tuple<_Ty, Args...> 
{
public:
	my_tuple() {}
	my_tuple(_Ty data, Args ...args) :data(data), args(args...) {}

	_Ty& getData() { return data; }
	my_tuple<Args...>& getObject() { return args; }
protected:
	_Ty data;
	my_tuple<Args...> args;  //自身
};

void testSecond() 
{
	my_tuple<string, int, double>  test("str", 1, 1.1);
	cout << test.getData() << "\t" << test.getObject().getData() << "\t" << test.getObject().getObject().getData() << endl;
    
	my_tuple<string, string>  test1("str1", "str2");
	cout << test1.getData() << "\t" << test1.getObject().getData() << endl;
}

int main() 
{
	testFirst();
	testSecond();
	tuple<string, int> tup;

	return 0;
}
```

# C++正则库

## 正则表达式语法

正则是一种规则，它用来匹配（进而捕获、替换）字符串。这种规则需要“模式”、“字符串”这两样东西，“模式”根据正则规则，来处理“字符串”。这种规则被许多语言支持，C++11以后才支持正则。

**常用元字符**

| 代码/语法 | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| .         | 匹配除换行符以外的任意字符                                   |
| \w        | 匹配字母、数字、下划线, 等价于[a-zA-Z0-9_]                   |
| \W        | 匹配不是字母、数字、下划线的其他字符                         |
| \s        | 匹配任意空白字符, 等价于(\t\n\r\f)                           |
| \S        | 匹配任意非空字符                                             |
| \d        | 匹配数字,  等价于[0-9]                                       |
| \D        | 匹配不是数字的字符                                           |
| \b        | 匹配单词的开始或结束指示字符串的边界（头/尾/空格左/空格右），字符\b要求边界的左边是字符，\b字符要求边界的右边是字符。 |
| \A        | 匹配字符串开头                                               |
| \Z        | 匹配字符串结尾的,如果存在换行,只匹配到换行前的结束字符串     |
| \z        | 匹配字符串结尾的,如果存在换行,匹配到换行符\n                 |
| \G        | 最好完成匹配的位置                                           |
| \n        | 匹配一个换行符                                               |
| \t        | 匹配一个制表符(tab)                                          |
| ^         | 匹配字符串的开始,且要求字符串以字符开头                      |
| $         | 匹配字符串的结束, 且要求字符串以字符结尾                     |
| [ x ]     | 用来表示一组字符,  比如[a-z0-9]表示小写和数字之中的,   [abc]表示abc之中的任意一个 |
| [^x]      | 匹配除了x以外的任意字符,   比如\[^abc]表示  abc之外的        |
| a\|b      | 匹配a或者b                                                   |
| (…)       | 匹配括号里的表达式,也可以表示一个组                          |

**常用限定符**

| 代码/语法 | 使用      | 说明                                       |
| :-------- | :-------- | ------------------------------------------ |
| *         | 字符*     | 要求字符出现0到多次   {0,}                 |
| +         | 字符+     | 要求字符出现1到多次     (\w)  {1,}         |
| ?         | 字符?     | 要求字符出现0次或1次    {0,1}              |
| {n}       | 字符{n}   | 要求字符出现n次,  比如\d{5}表示匹配5个数字 |
| {n,}      | 字符{n,}  | 要求字符出现n到多次  {0,}                  |
| {n,m}     | 字符{n,m} | 要求字符出现n到m次、                       |

==含有`\`的元字符，在C++定义时，都要写成`\\`==

## 常用正则表达式大全

**一、校验数字的表达式**

```
 1 数字：^[0-9]*$
 2 n位的数字：^\d{n}$
 3 至少n位的数字：^\d{n,}$
 4 m-n位的数字：^\d{m,n}$
 5 零和非零开头的数字：^(0|[1-9][0-9]*)$
 6 非零开头的最多带两位小数的数字：^([1-9][0-9]*)+(.[0-9]{1,2})?$
 7 带1-2位小数的正数或负数：^(\-)?\d+(\.\d{1,2})?$
 8 正数、负数、和小数：^(\-|\+)?\d+(\.\d+)?$
 9 有两位小数的正实数：^[0-9]+(.[0-9]{2})?$
10 有1~3位小数的正实数：^[0-9]+(.[0-9]{1,3})?$
11 非零的正整数：^[1-9]\d*$ 或 ^([1-9][0-9]*){1,3}$ 或 ^\+?[1-9][0-9]*$
12 非零的负整数：^\-[1-9][]0-9"*$ 或 ^-[1-9]\d*$
13 非负整数：^\d+$ 或 ^[1-9]\d*|0$
14 非正整数：^-[1-9]\d*|0$ 或 ^((-\d+)|(0+))$
15 非负浮点数：^\d+(\.\d+)?$ 或 ^[1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0$
16 非正浮点数：^((-\d+(\.\d+)?)|(0+(\.0+)?))$ 或 ^(-([1-9]\d*\.\d*|0\.\d*[1-9]\d*))|0?\.0+|0$
17 正浮点数：^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$ 或 ^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$
18 负浮点数：^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$ 或 ^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$
19 浮点数：^(-?\d+)(\.\d+)?$ 或 ^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$
```

**二、校验字符的表达式**

```
 1 汉字：^[\u4e00-\u9fa5]{0,}$
 2 英文和数字：^[A-Za-z0-9]+$ 或 ^[A-Za-z0-9]{4,40}$
 3 长度为3-20的所有字符：^.{3,20}$
 4 由26个英文字母组成的字符串：^[A-Za-z]+$
 5 由26个大写英文字母组成的字符串：^[A-Z]+$
 6 由26个小写英文字母组成的字符串：^[a-z]+$
 7 由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$
 8 由数字、26个英文字母或者下划线组成的字符串：^\w+$ 或 ^\w{3,20}$
 9 中文、英文、数字包括下划线：^[\u4E00-\u9FA5A-Za-z0-9_]+$
10 中文、英文、数字但不包括下划线等符号：^[\u4E00-\u9FA5A-Za-z0-9]+$ 或 ^[\u4E00-\u9FA5A-Za-z0-9]{2,20}$
11 可以输入含有^%&',;=?$\"等字符：[^%&',;=?$\x22]+
12 禁止输入含有~的字符：[^~\x22]+
```

**三、特殊需求表达式**

```
 1 Email地址：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
 2 域名：[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(/.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+/.?
 3 InternetURL：[a-zA-z]+://[^\s]* 或 ^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$
 4 手机号码：^(13[0-9]|14[0-9]|15[0-9]|16[0-9]|17[0-9]|18[0-9]|19[0-9])\d{8}$ (由于工信部放号段不定时，所以建议使用泛解析 ^([1][3,4,5,6,7,8,9])\d{9}$)
 5 电话号码("XXX-XXXXXXX"、"XXXX-XXXXXXXX"、"XXX-XXXXXXX"、"XXX-XXXXXXXX"、"XXXXXXX"和"XXXXXXXX)：^(\(\d{3,4}-)|\d{3.4}-)?\d{7,8}$ 
 6 国内电话号码(0511-4405222、021-87888822)：\d{3}-\d{8}|\d{4}-\d{7} 
 7 18位身份证号码(数字、字母x结尾)：^((\d{18})|([0-9x]{18})|([0-9X]{18}))$
 8 帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$
 9 密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：^[a-zA-Z]\w{5,17}$
10 强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在8-10之间)：^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$  
11 日期格式：^\d{4}-\d{1,2}-\d{1,2}
12 一年的12个月(01～09和1～12)：^(0?[1-9]|1[0-2])$
13 一个月的31天(01～09和1～31)：^((0?[1-9])|((1|2)[0-9])|30|31)$ 
14 钱的输入格式：
15    1.有四种钱的表示形式我们可以接受:"10000.00" 和 "10,000.00", 和没有 "分" 的 "10000" 和 "10,000"：^[1-9][0-9]*$ 
16    2.这表示任意一个不以0开头的数字,但是,这也意味着一个字符"0"不通过,所以我们采用下面的形式：^(0|[1-9][0-9]*)$ 
17    3.一个0或者一个不以0开头的数字.我们还可以允许开头有一个负号：^(0|-?[1-9][0-9]*)$ 
18    4.这表示一个0或者一个可能为负的开头不为0的数字.让用户以0开头好了.把负号的也去掉,因为钱总不能是负的吧.下面我们要加的是说明可能的小数部分：^[0-9]+(.[0-9]+)?$ 
19    5.必须说明的是,小数点后面至少应该有1位数,所以"10."是不通过的,但是 "10" 和 "10.2" 是通过的：^[0-9]+(.[0-9]{2})?$ 
20    6.这样我们规定小数点后面必须有两位,如果你认为太苛刻了,可以这样：^[0-9]+(.[0-9]{1,2})?$ 
21    7.这样就允许用户只写一位小数.下面我们该考虑数字中的逗号了,我们可以这样：^[0-9]{1,3}(,[0-9]{3})*(.[0-9]{1,2})?$ 
22    8.1到3个数字,后面跟着任意个 逗号+3个数字,逗号成为可选,而不是必须：^([0-9]+|[0-9]{1,3}(,[0-9]{3})*)(.[0-9]{1,2})?$ 
23    备注：这就是最终结果了,别忘了"+"可以用"*"替代如果你觉得空字符串也可以接受的话(奇怪,为什么?)最后,别忘了在用函数时去掉去掉那个反斜杠,一般的错误都在这里
24 xml文件：^([a-zA-Z]+-?)+[a-zA-Z0-9]+\\.[x|X][m|M][l|L]$
25 中文字符的正则表达式：[\u4e00-\u9fa5]
26 双字节字符：[^\x00-\xff]    (包括汉字在内，可以用来计算字符串的长度(一个双字节字符长度计2，ASCII字符计1))
27 空白行的正则表达式：\n\s*\r    (可以用来删除空白行)
28 HTML标记的正则表达式：<(\S*?)[^>]*>.*?</\1>|<.*? />    (网上流传的版本太糟糕，上面这个也仅仅能部分，对于复杂的嵌套标记依旧无能为力)
29 首尾空白字符的正则表达式：^\s*|\s*$或(^\s*)|(\s*$)    (可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式)
30 腾讯QQ号：[1-9][0-9]{4,}    (腾讯QQ号从10000开始)
31 中国邮政编码：[1-9]\d{5}(?!\d)    (中国邮政编码为6位数字)
32 IP地址：\d+\.\d+\.\d+\.\d+    (提取IP地址时有用)
33 IP地址：((?:(?:25[0-5]|2[0-4]\\d|[01]?\\d?\\d)\\.){3}(?:25[0-5]|2[0-4]\\d|[01]?\\d?\\d)) 
```

## 正则操作

```c++
#include<regex>   ///头文件
```

基本操作

1. 构建正则对象(准则)
2. 调用正则函数 
3. 传入相应参数即可，分析结果

处理问题:

+ 字符串匹配问题  regex_match()
+ 字符串截取(获取)问题  regex_search() 或者 sregex_token_iterator类
+ 字符串替换问题 regex_replace()

```c++
#include <regex>
#include <string>
#include <iostream>
using namespace std;
void test_regex_match() 
{
	//1.正则做匹配时候一定是完全匹配
	string str = "ILoveyou1314";
	regex reg("[a-z0-9]+");		//1个或者多个小写字母或者数字
	if (regex_match(str, reg)) 
	{
		cout << "匹配" << endl;
	}
	else 
	{
		cout << "不匹配" << endl;
	}
	//2.正则对象附加参数的构造方式
	regex reg2("[a-z0-9]+", regex_constants::icase); // regex_constants::icase忽略大写小写
	if (regex_match(str, reg2))
	{
		cout << "匹配" << endl;
	}
	else
	{
		cout << "不匹配" << endl;
	}
    
	regex reg3("[a-z0-9A-Z]+");
	if (regex_match(str, reg3))
	{
		cout << "匹配" << endl;
	}
	else
	{
		cout << "不匹配" << endl;
	}
    
	//3.原生字符串充当正则对象
	//	string str = "ILoveyou1314";
	regex reg4("ILoveyou[0-9]+");
	if (regex_match(str, reg4))
	{
		cout << "匹配" << endl;
	}
	else
	{
		cout << "不匹配" << endl;
	}
}

//字符串截取问题regex_search()
void test_regex_search()
{
	smatch result;
	//prefix(): 获取前缀
	//suffix(): 获取后缀
	//str(): 获取匹配到字符串
	//只做操作第一次匹配的
	string str = "ILoveyou1314IMiisyou520Iwantyou";
	bool flag = regex_search(str, result, regex("\\d+"));	//\d+多个数字
	if (flag == true) 
	{
		cout << "size:" << result.size() << endl;
		cout << "匹配:" << result.str() << endl;      // 1314 
		cout << "前缀:" << result.prefix() << endl;  // ILoveyou
		cout << "后缀:" << result.suffix() << endl;  // IMiisyou520Iwantyou
	}
    
	//怎么获取所有匹配到的字符串
	//sregex_iterator类
	//1.带惨构造: 正常区间描述匹配正则
	//2.无参构造: 结束标记  --->istream_iterator   end of 
	sregex_iterator end;
	regex reg("\\d+");
	sregex_iterator pos(str.begin(), str.end(), reg);
	while (pos != end) 
	{
		cout << pos->str() << " "; // 1314  520
		pos++;
	}
    
    // 推荐
	//怎么获取不匹配的
	//sregex_token_iterator 这个类相对于sregex_iterator来说多了一个可选项(就是多了附加参数,0:找的就是匹配，-1找的就是不匹配)
	regex reg2("\\d+");
	sregex_token_iterator endToken;
	sregex_token_iterator posToken(str.begin(), str.end(), reg2, -1);
	while (posToken != endToken) 
	{
		cout << posToken->str() << endl;
		posToken++;
	}

}

// 字符串替换问题 regex_replace()
void test_regex_replace() 
{
	//替换所有满足规则的内容
    // 例子1
	string str = "I妈sdfdsdf妈Ilikeyou妈";
	regex reg("妈");
	cout << "屏蔽结果:" << regex_replace(str, reg, "**") << endl;
    // 例子2
	string str2 = "臭 sb,我太会sb sssb";
	regex reg2("sb");
	cout << "屏蔽结果:" << regex_replace(str2, reg2, "**") << endl; // 臭 **,我太会** ss**
    // 例子3
    string str = " 123  45 6 78  9  ";
	regex reg("  ");
	cout << str << endl;
	cout << regex_replace(str, reg, " "); // 123 45 6 78 9
    
	//附加参数替换模式
	cout << "only one:" << regex_replace(str2, reg2, "**",regex_constants::format_first_only) << endl; //臭 **,我太会sb sssb // 只替换第一次匹配的  
	cout << "format_no_copy" << regex_replace(str2, reg2, "**", regex_constants::format_no_copy) << endl;  //****** //只保留匹配的替换 
}
int main() 
{

	test_regex_match();
	test_regex_search();
	test_regex_replace();
	return 0;
}
```

# C++时间

C++时间管理是放在chrono头文件中,C++时间管理分为三个内容

+ 时间描述
+ 时钟
  + system_clock
  + steady_clock
  + high_resolution_clock
+ 类型转换
  + to_time_t
  + from_time_t

```c++
#include<iostream>
#include <chrono>
#include <ctime>
#include <iomanip>
#include <thread>
using namespace std;
void  GetTime() 
{
	std::chrono::system_clock::time_point curTime = chrono::system_clock::now();
	//auto curTime = chrono::system_clock::now()
	//to_time_t  : 把time_point 转换为time_t
	time_t  tm_time = chrono::system_clock::to_time_t(curTime);
	cout << "date:" << ctime(&tm_time) << endl;
	tm* pTime = localtime(&tm_time);
	cout << put_time(pTime, "%F %X") << endl;  //put_time()打印格式
	cout << "时间戳:" << curTime.time_since_epoch().count() << endl;  //time(NULL)的返回值
}

void CountTime() 
{
	//clock() 函数完成
	chrono::steady_clock::time_point start = chrono::steady_clock::now();
	for (int i = 0; i < 10000; i++) 
	{
		int a = 1;
		a++;
	}
	chrono::steady_clock::time_point end = chrono::steady_clock::now();
	//auto dt = end - start;	//纳秒
	chrono::duration<double, ratio<1, 1000>> dt = end - start;			//定义一个秒对象
	cout << "耗时:" << dt.count() << endl;
}

// 高精度
void  HighClock() 
{
	//clock() 函数完成
	chrono::high_resolution_clock::time_point start = chrono::high_resolution_clock::now();
	for (int i = 0; i < 10000; i++)
	{
		int a = 1;
		a++;
	}
	chrono::high_resolution_clock::time_point end = chrono::high_resolution_clock::now();
	//auto dt = end - start;	//纳秒
	chrono::duration<double, ratio<1, 1000>> dt = end - start;			//定义一个秒对象
	cout << "耗时:" << dt.count() << endl;
}

// 时间的描述
void showTime() 
{
    // 参数可以直接写时间单位
	this_thread::sleep_for(1s);
	//this_thread::sleep_for(2min);
	//this_thread::sleep_for(1h);
	//this_thread::sleep_for(1ms);
	//this_thread::sleep_for(10000ns);
	cout << "休眠1秒钟" << endl;
	this_thread::sleep_for(chrono::seconds(1));		//等效上面这种写法
}
int main() 
{
	GetTime();
	CountTime();
	HighClock();
	showTime();
	return 0;
}
```

# C++文件路径

```c++
#include <filesystem>  // 头文件,   c++17支持
```

核心:

+ 路径操作
+ 文件状态
+ 遍历文件

```c++
#include <filesystem>
#include <iostream>
#include <fstream>   // 文件操作
#include <set>
using namespace std;


/********************************* 路径操作 **************************************/
void testPath() 
{
	//创建单层目录
	error_code temp;
	filesystem::create_directory("xxx", temp);
	cout << temp.message() << endl;   //输出 操作成功完成
	//创建多级目录
	filesystem::create_directories("YYY/小电影", temp);
	cout << temp.message() << endl;
}

void testpathClass() 
{
	//path类,路径管理
	filesystem::path url = filesystem::current_path();			//获取当前路径
	cout << url / "某某某" << endl;									//路径直接/作为路径的组合
	cout <<"当前路径:" << url << endl;
	cout << "当前路径:" << url.string() << endl;
	cout << "根目录:" << url.root_directory() << endl;
	cout << "相对路径:" << url.relative_path() << endl;
	cout << "根名:" << url.root_name() << endl;
	cout << "根路径:" << url.root_path() << endl;

}

/********************************* 文件类型 **************************************/
void getStatus(filesystem::file_status object) 
{
	switch (object.type()) 
	{
	case filesystem::file_type::regular:
		cout << "磁盘文件" << endl;
		break;
	case filesystem::file_type::directory:
		cout << "目录" << endl;
		break;
	case filesystem::file_type::unknown:
		cout << "无法识别" << endl;
		break;
	}
}
void testStatus() 
{
	//file_status类  文件状态管理
	filesystem::create_directory("Box");
	getStatus(filesystem::status("Box"));
	fstream file("Box/file", ios::out | ios::trunc); // 创建文件
	getStatus(filesystem::status("Box/file"));
}


/********************************* 遍历文件 **************************************/
//遍历文件
//directory_entry
//directory_iterator: 遍历文件
//recursive_directory_iterator:递归遍历

//遍历当前路径下的 所有目录(仅限一层)
void tarverseDirectroyFirst()
{
	filesystem::path  url("C:\\Users\\16658\\Desktop\\Project_temp\\文件路径");
	if (!filesystem::exists(url))		//判断当前路是否存在
	{
		cout << "目录不存在" << endl;
		return;
	}
	filesystem::directory_iterator object(url);
	for (auto v : object)
	{
		cout << v.path() << endl;
		//cout << v.path().filename() << endl;
	}
}

//遍历当前目录下的 所有文件
void travserDirectorySecond()
{
	filesystem::path url("C:\\Users\\16658\\Desktop\\Project_temp\\文件路径");
	set<string> dir;
	for (filesystem::directory_iterator end, begin(url); begin != end; ++begin)
	{
		if (!filesystem::is_directory(begin->path()))
		{
			dir.insert(begin->path().filename().string());
		}
	}
	for (auto v : dir)
	{
		cout << v << endl;
	}
}

//遍历路径下面的所有文件(包括不同目录)
void travserDirectoryThird()
{
	filesystem::path url("C:\\Users\\16658\\Desktop\\Project_temp\\文件路径");
	multiset<string>  dir;
	for (filesystem::recursive_directory_iterator end, begin(url); begin != end; ++begin)
	{
		if (!filesystem::is_directory(begin->path()))
		{
			dir.insert(begin->path().filename().string());
		}
	}
	for (auto v : dir)
	{
		cout << v << endl;
	}
}

int main() 
{
	//testPath();
	//testpathClass();
	//testStatus();
	//tarverseDirectroyFirst();
	//travserDirectorySecond();
	travserDirectoryThird();
	return 0;
}
```

# C++随机数

C++随机数是放在random头文件,C++随机数是由以下两部分组成

+ 随机引擎(相关数学算法)
+ 随机数种子

```c++
#include <random>
#include <iostream>
#include <chrono>
#include <functional>
using namespace std;
int main() 
{
	//生成随机数
	default_random_engine e;
	e.seed(chrono::high_resolution_clock::now().time_since_epoch().count()); // c++
	//e.seed(time(NULL));
	for (int i = 0; i < 3; i++) 
	{
		cout << "随机生成:" << e() % 10 << endl;		//e() 生成随机数
	}
	cout << "max:" << e.max() << endl;
	cout << "min:" << e.min() << endl;
	//引擎结合分布方式生成随机数
	uniform_int_distribution<int>  durtaion(1, 6);
	cout << "uniform:" << durtaion(e) << endl;
    //  随机数
	auto rand = bind(durtaion, e);
	cout << "bind:" << rand() << endl;
	cout << "bind:" << rand() << endl;
	cout << "bind:" << rand() << endl;
    
    
	//适配器实例化产生随机数
	//线性同余:  //y=(x*a+c)%m;
	linear_congruential_engine<unsigned int, 1, 2, 10>  ee; // 1 2 10 a c m
	ee.seed((size_t)time(nullptr));
	cout << "线性同余:" << ee() << endl;
	cout << "线性同余:" << ee() << endl;

	//梅森旋转
	mt19937_64 eee;
	cout << "梅森旋转:" << eee() << endl; // 产生格很大的随机数
	mersenne_twister_engine<unsigned int, 10, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1> eeee;
	eeee.seed((size_t)time(nullptr));
	cout << "梅森旋转:" << eeee() << endl;

	return 0;
}
```

# C++设计模式



# C++新标准多线程



































































































