# 面向对象编程

> [!TIP]
>
> 错题集：<br />[https://k5ms77k0o1.feishu.cn/wiki/wikcnH7YKB6KFCwCXgRdXk2MZAf](https://k5ms77k0o1.feishu.cn/wiki/wikcnH7YKB6KFCwCXgRdXk2MZAf)<br />笔记：<br />[https://note.hobbitqia.cc/OOP/](https://note.hobbitqia.cc/OOP/) 

## 函数
函数声明可以不写参数名，也可以设置参数默认值 default arguments

调用函数时，若一个参数值未给出，那么之后所有的参数值也不能给出

- Never new something and return the pointer  

### 默认参数 default arguments
A default argument is a value given in the declaration that the compiler automatically inserts if you donʼt provide a value in the function call.<br />默认参数必须**从右到左**写，没有默认参数的在最左边。eg,`int harpo(int n, int m = 4, int j = 5);`<br />默认值只能出现在函数原型中，不会在函数代码里出现

### 引用 reference
From GPT: <br />A reference to an object in C++ is an alternative name for an object. It's similar to a pointer,  but with a few key differences.

1. **Definition and Declaration**:
   - A reference is declared using the `&` symbol. For example, `A& ref = obj;`, where **obj** is an existing object of class **A**.
   - Once a reference is initialized to an object, it cannot be made to refer to another object; it remains an alias to that specific object throughout its scope. 初始化后，它在整个范围内仍然是该特定对象的别名，不可以再成为别的对象的引用（不可改变）
2. **Behavior and Usage**:
   - A reference must be initialized when it is declared. There is no such thing as a "null reference" in C++, unlike pointers which can be null. 必须初始化且不能为 NULL
   - A reference, when used in code, behaves exactly as if you used the original object. That is, using the reference is syntactically identical to using the object itself. 引用在语法上与使用对象本身相同
   - Since a reference is just another name for an existing object, it doesn't occupy any additional memory (unlike pointers, which require memory for storing the address of the object they point to). 引用只是对象的另一个名字，没有分配新的地址（占内存）
3. **References vs Pointers**:
   - Unlike pointers, references are less powerful but safer. They are safer because they must refer to an object (they **cannot be null**) and they **don't involve explicit memory address manipulation**. 
   - 引用通常用在函数参数和返回类型中，以确保传递实际对象并避免复制大对象（按引用传递）的开销。
4. **Example in Function Arguments**:
   - If a function takes an object reference as an argument, it can modify the original object.  如果函数将对象引用作为参数，则它可以修改原始对象（共享内存） For instance, a function `void foo(A& a)` can modify the **A** object passed to it.

**_注意：_**

- 当使用引用传递时，实际参数必须是一个**变量**
- no reference/pointer to reference 
- reference to pointer is ok
- No arrays of references
- **万能引用：**`auto &&`
```c
char c = 'A';
char &r = c;
r = 'B';
cout << "c: " << c << endl;
cout << "b: " << r << endl;
//此时我们发现两行的输出都是 B.
```
## 对象和类 object and class
类就是用于创建对象的模板

- 在 C++的一个类中，用变量定义_数据域_，用_函数_定义行为（_构造函数_用来初始化，每创建新对象都会调用）
- 类定义末尾要加分号
- 定义一个类时，应把类名_每个单词首字母大写_
- 关键字`public`表示所有数据域、构造函数和普通成员都可通过类对象来访问
- 作为类成员，数据域不能在声明时进行初始化
- 类内 const 变量只能通过初始化列表初始化
- 在类内只有 `static const i = 1` 常量在后使用（eg，`int array[i]`） 才能通过编译（去掉 static 不行
- class中的变量和函数默认`private`，struct中的函数默认为`public`

类中：

- `**this**` is a **pointer** to the current object. 当前对象的指针
- `**that**` is a **reference** to another object of the same type. 引用
- `->` is used to access members of an object through a pointer. 指针指向对象的某个成员
- `.` is used to access members of an object directly. 直接获取某个对象的成员，对象.成员

域解析器 `::`<br />`type <Class Name>::<function name>`

### 友元函数
In C++, a **friend** function is a function that is not a member of a class but is allowed to access its private and protected members.
### 构造函数 constructor

- 构造函数名称必须与类名一致
- 没有返回类型（void 也不可以）
- 在创建对象时，构造函数会被调用，它的作用就是**初始化对象**
- 可以重载，但它们函数签名不同？
- 构造函数可以由参数
- 默认构造函数可以无参数调用
- If (and only if) there are no constructors for a class (struct or class), the compiler will automatically create one for you 没有构造函数时编译器会默认构造一个无参数构造函数
- 在外调用 `public`

一个类通常有一个_无参数构造函数_，当类的声明中不包含构造函数的声明时，此时隐含声明了_缺省构造函数 _（无参数的构造函数）
#### 初始化
##### 初始化列表 initializer list

- To define a function with an argument list, defaults must be added _**from right to left**_. 初始化参数表时有初值（默认值）的在最右边；
- 默认值只能出现在函数原型。（声明和定义一起是可以的）
- 默认参数值不会在函数代码里出现，只是编译器把编译时会把默认值放进堆栈调用里。因此可能会被其他原型声明改变默认值。
```cpp
ClassNme(parameterlist):datafield(value1), datafiled2(value2)
{
    //additional statements if needed
}
class Point {
private:
    const float x, y;
public:
    Point(float xa = 0.0, float ya = 0.0) : y(ya), x(xa) {}
};
```

- 这里的 const 变量不能被赋值，只能被初始化。成员 const 变量的初始化，可以`const float x = 1.0;` 但这样所有类的对象的值都是一样的。
- `: `后是初始化列表，只有在构造函数中使用。会在构造函数执行之前，调用 Initializer list 的构造
- 根据定义顺序来初始化变量（实例化子类，先调用父类，再初始化自己）
- 对象的数据域和函数（总称为对象成员）可用对象名通过`.`来访问
- 如果我们需要创建一个对象但只使用一次，则无需给对象命名，成为_匿名对象_
- 在 C++中，如果使用**无参的构造函数**来创建**匿名**对象，必须在构造函数之名后加上括号；而使用无参的构造函数来创建一个**命名**对象，在对象名之后是不能使用括号的

eg, `Student::Student(string s):name(s) {}`在构造函数执行之前，将 s 初始化为 name<br />**_不同于赋值 _**`Student::Student(string s) {name=s;}`在构造函数执行时，string 必须有一个默认构造函数（要先构造出 string 的对象 name 再赋值）

符号`：：`称为二元作用域解析运算符，指明了类成员的作用范围
### 析构函数 deconstructor
析构函数是当对象超出范围或通过调用显式销毁时自动调用的成员函数`delete`。析构函数与类同名，前面有波浪号 ( `~`)。

- Don't accept arguments. 没有参数
- Don't return a value (or `**void**`) 没有返回值
- Can't be declared as `const`, `volatile`, or `static`. However, they can be invoked for the destruction of objects declared as const, volatile, or static.
- Can be declared as `virtual.` Using virtual destructors, you can destroy objects without knowing their type —the correct destructor for the object is invoked using the virtual function mechanism. Destructors can also be declared as pure virtual functions for abstract classes.
- 先析构自己（子类），再析构父类，与构造函数顺序相反

当发生以下事件之一时，将调用析构函数：

- 具有块作用域的本地（自动）对象超出作用域，析构会被自动调用
- 使用 运算符 分配的对象**new**可以使用 显式释放**delete**。
- 临时对象的生命周期结束。
- 程序结束，全局或静态对象存在。
- 使用析构函数的完全限定名称显式调用析构函数。

析构函数可以自由调用类成员函数并访问类成员数据。<br />析构函数的使用有两个限制：

- 你无法获取它的地址。
- 派生类不继承其基类的析构函数。
### 内联函数 inline
在类定义内实现的函数自动成为内联函数<br />用关键字`inline`在类实现文件中指明成员函数是内联函数；如果将成员函数的定义写在声明内，就会自动变成内联函数<br />`inline`不会真正编译函数，而是在调用函数时_直接替换代码_，不需要调用步骤&时间， 比函数调用所花的时间少，**增加空间以减少时间**<br />一般是简单的成员函数或者在循环中多次使用的函数<br />允许多次定义（allow multiple definitions<br />空间太大的函数或者递归函数不适合变成内联函数<br />inline 函数的 body 不是定义，只是一个声明。即如果有 inline 函数，我们应该把它放在头文件里<br />inline 比宏定义要好，因为它有类型检查
### 复制构造 copy constructor
定义 `T::T(const T&)`

- Create a new object from an existing one. 从已有对象构造
- Copying is implemented by the copy constructor 由拷贝函数实现
- C++ builds a copy ctor for you if you don't provide one. 如果没有给拷贝构造, C++ 会自动创造一个
- 如果有成员是一个对象，会调用对象自己的拷贝函数。
- 如果有成员变量是指针，会和原来对象一样指向同一块内存。如果有一个对象被析构，那么这块内存就被 delete, 这就变成了无效内存。因此我们不一定要有拷贝构造函数，有指针时必须要有。

Copies each member variable

- Good for numbers, objects, arrays
- Copies each pointer
- Data may become shared!

create  a new object from an existing one 使用函数调用进行值传递
#### 什么时候拷贝构造会被调用？ 

- 只有对象本身才会有拷贝构造（指针、引用不会）
- 定义变量时做的是初始化，其他时候是赋值。**初始化是要拷贝构造**，赋值要重载赋值运算符。

`Personbaby_a("Fred");// these use the copyctor`<br />私有的拷贝构造函数使得对象不能被拷贝构造


### 移动构造 move constructor
移动构造函数是可以使用相同类类型的参数调用的构造函数，并复制参数的内容，可能会改变参数，参数为右值引用。<br />如果有一个对象，里面有指针指向一块内存。拷贝构造就是重新申请一块内存并将原内存的数据拷贝过来。而移动构造就是让新对象的指针指向内存，但原指针不再指向这个内存(nullptr).<br />左值引用`&`，右值引用`&&`<br />如果函数返回了一个对象，我们可以用右值引用，避免拷贝构造。

什么时候需要移动构造？

- 类内有指针，而且对象会在函数内传进传出。

`std::move()`
```cpp
vector<int> v1{1, 2, 3, 4};
vector<int> v2 = v1;
vector<int> v3 = std::move(v1);// 此时调用用移动构造函数  
此时调用复制构造函数，v2是v1的副本 通过 std::move 将 v1 转化为右值，
从⽽激发 v3 的移动构造函数，实现移动语义
```

### 数据域封装
`private`关键字使类之外的程序无法直接引用类对象来访问，为了使私有数据可被访问，可定义一个 get 函数返回数据域的值，为了使私有数据可被修改，可提供一个 set 函数为数据域设置新值

### 封装 encapsulation
#### 可见性 public，private，protected

- **Public**: visible to all clients
- **Protected**: visible to classes derived from self (and to friends) 不让外界访问，但可以让继承者访问
- **Private**: visible only to self and to friends 只对自己和友元可见

class defaults to private<br />struct defaults to public
#### Encapsulation

- Data hiding
- Separation of interface and implementation
- Use of access specifiers
### 继承 inheritance
#### Composition
construct new objects with existing objects（reusing the implementation<br />Embedded objects
#### Inheritance
从已有的类（称为基类、父类）派生出新的类称为继承(inheritance)，派生类又称子类derived/child 

- 继承可以避免代码重复，重复利用
- 易于维护和拓展 easier maintenance and extendibility
- **子类可以调用父类的函数**，反之不行
- 父类的指针可以指向子类
- 子类不能访问父类的私有变量 All types of inheritance **do not inherit private members**，

但私有变量存在于这个类中

- 当调用构造函数时，我们不能调用父类的私有变量，只能用初始化列表的方式调用父类的构造函数。我们不能也不应该在子类对父类的变量做初始化 (code duplication)

Suppose class B is derived from A. Then:<br />Base class member access specifier

有什么是没有继承得到：<br />构造函数没有被继承，但父类的构造会被自动调用。析构同理。赋值的运算符不会被继承。

Type ( B is )

| Inheritance Type ( B is ) | public | protected | private |
| --- | --- | --- | --- |
| public A | public in B | protected in B | hidden |
| private A | private in B | private in B | hidden |
| protected A | protected in B | protected in B | hidden |

```cpp
Employee::Employee( const string& name, const string& ssn )
	: m_name(name), m_ssn( ssn) {
    // initializer list sets up the values!
}
class Manager : public Employee {
    public:
        Manager(const std::string& name, const std::string& ssn, const std::string& title);
        const std::string title_name() const;
        const std::string& get_title() const;
        void print(std::ostream& out) const;
    private:
        std::string m_title;
};
Manager::Manager( const string& name, const string& ssn, const string& title = "" )
	:Employee(name, ssn), m_title( title ) {
        
}
```
The Manager class is defined as a subclass of Employee. 父类 Employee，子类 Manager<br />父类的构造是在子类的构造之前。<br />要调用父类的成员函数，要 `Employee::print()`.
#### multiple inheritance 多重继承
diamond inheritance 菱形继承（孙子体内有两个爷爷<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1704265986004-9d198e27-c785-4646-a1d9-12f6f268792c.png#averageHue=%23f8f8f8&clientId=u0aef905c-55cb-4&from=paste&height=300&id=u7d3b591b&originHeight=1053&originWidth=1011&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=106879&status=done&style=none&taskId=u0bb0289d-f39c-4b7c-b558-a4762ec8b71&title=&width=288)
### 多态 polymrphism

- 被基类定义的变量可以引用一个子类类型的对象
- 父类的指针或引用指向基类
- 只有 upcast 和 virtual function 时才会发生
- 把子类复制给父类，没有多态发生
- 构造函数不会发生多态

**Upcast**: take an object of the derived class as an object of the base one.<br />e.g. Ellipse can be treated as a Shape<br />**Polymorphic variables 多态变量**<br />Pointers or reference variables of objects are polymorphic variables<br />They can hold objects of the declared type, or of subtypes of the declared type.<br />只写了一句代码，但实际执行中可能会有多种执行方式，这就是多态。
#### 虚函数 virtual function
`virtual` 定义了虚函数，意味着子类可能出现这个函数的新版本。告诉编译器通过指针访问这个函数时，要如何编译。

- 基类定义了`virtual`
- can be transparently overridden in a derived class 可以在派生类中透明地重写
- 对象携带其虚拟函数包
- 编译器检查包并动态调用正确的函数
- 如果编译器在编译时就知道函数，则可以生成静态调用
```cpp
class Ellipse : public Shape {
public:
    Ellipse(float maj, float minr);
    virtual void render(); // will define own
protected:
    float major_axis, minor_axis;
};
class Circle : public Ellipse {//Class derived from Ellipse
public:
    Circle(float radius) : Ellipse(radius, radius){}
    virtual void render();
};
void render(Shape* p) {
    p->render(); // calls correct render function
} // for given Shape! void func() {

我们认为 p 这个指针是一个 polymorphic variable 多态变量，
有静态（声明）类型 Shape 又有动态类型。

Ellipse ell(10, 20);
ell.render(); // static -- Ellipse::render();
Circle circ(40);
circ.render(); // static -- Circle::render();
render(&ell); // dynamic -- Ellipse::render();
render(&circ); // dynamic -- Circle::render()
```
##### 静态、动态绑定 binding

- The declared type of a variable is its static type.
- The type of the object a variable refers to is its dynamic type.
- The compilerʼs job is to check for static-type violations.
- 因此在编译时，如果我们去掉 `Shape()` 里的 `render` 函数，编译就会报错。这样无法通过静态检查，尽管我们知道我们并不会使用 Shape 的 render 函数。

**Binding**: which function to be called 

- _Static binding_：在声明的时候决定编译的时候匹配哪个函数，C++默认静态绑定
- _Dynamic binding_：在运行时判断调用哪个函数
   - 在基类中，函数需要被声明为虚函数
   - 虚函数中，引用对象的变量必须以引用或指针的形式传递（如果通过传值传递，不会出现动态绑定，即输出和不用虚函数是一样的

virtual 关键词是在告诉编译器，这个函数使用动态绑定。否则即使用指针，也是静态绑定。<br />e.g. `g();` `Student a; a.f()` 是静态; `Student &a; a.f(); p->f();` 不一定是静态。

| **call** | **type** |
| --- | --- |
| free function | static |
| `object.fun()` | static |
| `ref.func()` | static |
| `p->func()` | static |
| `ref.vfunc()` | dynamic |
| `p->vfunc()` | dynamic |

```cpp
class A {
    int i;
    void f() {}
};
class B: public A {
    int j;
};
```
这时 `sizeof(A) == 4`，但如果将 f 声明为虚函数，`sizeof(A)` 就变为 16. 如果去掉`int i`; 后 `sizeof(A)` 变为 8<br />一旦有虚函数声明，这里会在开头放一个指针 `VPTR`, 指向一个表，里面放的是函数指针。（对象里面没有函数指针，只放表的指针）`VPTR` 只会在构造函数执行的时候对其进行赋值。

##### Overriding 函数覆盖
在派生类中重定义一个虚函数<br />如果希望在调用对象是子类的情况下，仍调用基类定义的函数，应使用基类名和作用域运算符`::`，eg: `child.father::function()`

- If you override an overloaded function, you must override all of the variants
- 不要重新定义父类的默认参数值。
#### Abstract classes 抽象类
类中一旦有一个虚函数=0(纯虚函数), 那么这个类就不能被制造出对象，这样的类叫做抽象类。<br />类抽象就是将类的实现和使用分离开来

- 抽象基类具有纯虚拟函数 pure virtual
   - 只定义了接口
   - 未给出函数体
- 抽象基类不能实例化
   - 必须派生一个（或多个）新类
   - 在类实例化之前，必须提供所有纯虚函数的定义
##### pure virtual 纯虚函数
`virtual void render() = 0; // mark render() pure`
### 函数重载 function overloading
两个或多个函数可以具 To define 同的参数。当一个函数名被不同的作业重载时，称为函数重载。在函数重载中，“函数”名称应该相同，**参数应该不同**。<br />只有返回类型不同不算重载<br />![1704704908527.jpg](https://cdn.nlark.com/yuque/0/2024/jpeg/34417153/1704704909730-07e488f4-8031-441f-af30-867168335103.jpeg#averageHue=%23fcfbfb&clientId=u22814c3e-773a-4&from=paste&height=133&id=u0eb1ac95&originHeight=199&originWidth=1124&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=44931&status=done&style=none&taskId=u7dc783a8-a51c-486e-b8ed-7b64368e4dc&title=&width=749.3333333333334)
### Const and Static

![output.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1704703805539-e26c4581-0809-4368-a89f-f7e588696a31.png#averageHue=%23f6f5f4&clientId=u22814c3e-773a-4&from=ui&id=u10963060&originHeight=761&originWidth=983&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=145939&status=done&style=none&taskId=u1573e3e2-1b4c-41e9-94c2-2747e264b8b&title=)
#### const
`const`声明一个常量
```cpp
char * const q = "abc"; // q is const
*q = 'c'; // ERROR
// char a[] = "abc"; *q = 'c' is ok.
q++; // ERROR
const char *p = "ABCD"; // (*p) is a const char
*p = 'b'; // ERROR! (*p) is the const
```
`char * const q` 表示 q 指向 abc 的地址，则 q 不能再指向其他地方。<br />`const char * p` p 指向的地址可以修改，但不能通过 p 修改 p 指向的值。<br />`*` 的位置：<br />`* const`  不能修改指针（地址），但可以修改指针指向的对象的内容；指向的数据不是常量，可以更改<br />`const *`不能修改指针指向的对象的内容，但可以修改（地址）成为另一个对象；指针不是常量，但指向的数据是常量
```cpp
string p1("Fred");
const string* p = &p1;
/*p is a pointer that can point to strings, 
but you cannot modify the string that p points to through this pointer. 
However, you can change p to point to another string
*/
string const* p = &p1;//same as const string* p = &p1;
string *const p = &p1;
/*
you can change the string that p points to (i.e., modify p1 through p), 
but you cannot change the pointer p to point to another string. 
p will always point to p1 for its lifetime.
*/
```

1. 函数声明末尾 `const` :
- This const qualifies the member function, indicating that it does not modify the object's state on which it's called. **不会更改调用对象的成员变量的值**
- 在函数内不会调用其他非 const 的成员函数
- const 和非 const 函数可构成重载关系
2. 函数参数中有 const `(const A &that)`:
- This const indicates that the function will not modify the object passed by reference. It ensures that the state of that object remains unchanged throughout the function. 该 const 表示该函数**不会修改通过引用传递的对象**。 它确保该对象的状态在整个函数中保持不变。
3. 如果成员变量中有 const，需要在构造函数中用初始化列表初始化

在同时存在 const 函数和 非 const 重载函数的前提下，若 非const 对象想调用 const 成员函数，则需要显示的转化，例如`(const Student&)obj.getAge();`若const对象想调用非const成员函数，同理进行强制类型转换`const_cast < Student&>(constObj).getAge();`(注意`constObj`一定要加括号)<br />                <br />当类中只有一种函数存在的情况，非const对象可以调用const成员函数或者非const成员函数，const对象只能调用const成员函数，若直接调用非const成员函数编译器会报错。
#### static
静态本地变量实际上是全局变量，被存储在静态内存中。<br />出现在全局变量/函数前，表示访问限制，只有当前文件可以访问。<br />Initialization occurs only once. 对象、构造函数都只初始化一次<br />**静态成员变量**<br />静态成员变量和静态本地变量是一样的。访问受限，限于类内部，实际上是全局变量（在这个类内所有的对象都维持相同的值，对象 A 修改了，那么对象 B 的这个变量的值也会改变）<br />静态成员函数没有 this, 不能调用非静态成员变量，也不能访问非静态函数。可以在没有创建类的对象的时候就能调用静态成员函数。

### Namespace 命名空间
Namespace is a scope just like a class. `namespace X {type function1;type function2;}`<br />避免不同 h 文件里的函数名称有重复<br />`using namespace xx;`（可以放在某个函数里，不一定要在全局）或者`using xx::function()`（明确指出哪个命名空间的函数）<br />可以给某个命名空间取别名`namespace simple = complicated;`<br />命名空间是开放的，可以分开在不同 h 文件定义

### 重载运算符 Overloading operators 
[C++运算符重载-CSDN博客](https://blog.csdn.net/weixin_45673283/article/details/105654281)
#### 不可重载的运算符
`.`,`.*`,`::`,`?:`,`sizeof`,`typeid`,`static_cast`(xxx_cast)<br />//运算符`[]`
```cpp
class A {
public:
    A(int a):i(a){}
    int get() {return i;}
    /* 返回的一定是 A 的一个新的对象 */
    const A operator+(const A &that) const {
        A c(this->i+that.i); /* 这里可以访问 that. 私有是针对类的，不是针对对象的。 */
        return c;
    }
private:
    int i;
}
int main() {
    A a = 6;
    A b = 7;
    A c = a + b;    /* a + 9 也是可以的（编译器会用 9 帮我们构造一个对象）；但 9 + a 不行 */
    cout << c.get() << endl;    /* 输出 13 */
}
```
#### 
Private Member Access: 在类内 private 成员可以被函数访问<br />全局函数是不能访问类的私有变量的，要声明友元 `friend`<br />加减乘除只能作为右值，因此要 const.；而 `[]` 可以作为左值，就不能 const.
#### 运算符类型 prototypes of operator

- **两元运算：**`**+ - * / % ^ & | ~**`

`const T operator X(const T&l, const T&r);`<br />这里返回的必须是一个新的对象。如果这里返回引用，那必须返回一个全局的地址，但函数只有本地空间。

- **两元关系运算 relation operator：**`**! && || < <= == >= >**`

`bool operator X(const T&l, const T&r);`

- `**[]**` 认为是一个容器

`E & T::operator[](int index);`<br />`int& operator[](int index)`<br />返回的是左值（不能为 const），而且不能是一个新对象（否则 `a[6]=7` 执行后就被丢掉了）

- **自增、自减 **`**++ --**`
```cpp
class Integer { 
 public: 
 ... 
 const Integer& operator++(); //prefix++ 
 const Integer operator++(int); //postfix++ 
 const Integer& operator--(); //prefix-- 
 const Integer operator--(int); //postfix-- 
 ... 
 };
// 
const Integer& Integer::operator++() { 
*this += 1; // increment 
return *this; // fetch 
} 
// int argument not used so leave unnamed so 
// won't get compiler warnings 
const Integer Integer::operator++( int ){ 
Integer old( *this ); // fetch 
++(*this); // increment 调用了刚刚的函数
return old; // return 

++x; // calls x.operator++(); 
x++; // calls x.operator++(0); 
--x; // calls x.operator--(); 
x--; // calls x.operator--(0);
```
`a++`后缀++ 要参数 int（编译器设为 0）<br />Postfix is generally less efficient than the prefix version because it involves creating a copy of the object. 前缀比后缀效率更高

- **赋值运算符 assignment operator **`**=**`

 需要自检是不是自己给自己赋值
```cpp
T & T::operator=( const T& rhs ) {
// check for self assignment
	if ( this != &rhs ) {//Protect against self-assignment
	// perform assignment
	...
	}
	return *this;
}
//This checks address, not value (*this != rhs)

```
对于动态分配的类，内存声明一个赋值运算符（和一个复制构造函数）,可以声明`operator=` 为 private 类，或使用`=delete`. eg, `MyClass& operator=(const MyClass& other) = delete;`

**functor**： A functor, which overloads the function calloperator, is an object that acts like a function
```cpp
struct F {
	void operator()(int x) const {
		std::cout << x << "\n";
	}
}; // F is a functor
F f;
f(2); // calls f.operator()
```
### 类型转换 User-defined type conversions
可以在函数前声明`explicit`来避免隐性类型转换 implicit
```cpp
class Rational {
public:
 ...
 operator double() const; // Rational to double
}
Rational::operator double() const { 
 return numerator_/(double)denominator_;
}
Rational r(1,3); 
double d = r; // r=>double
```
不需要写返回类型。 如果有声明`explicit`, 那么我们就必须写作 `double d = (double)r`;
#### C++类型转换
![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1702800137727-65d91b31-e22d-48dc-a370-5bb69e732576.png#averageHue=%23f6f6f5&clientId=u7b86ce3f-b7e0-4&from=paste&height=465&id=u6dce5b0f&originHeight=697&originWidth=1217&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=72653&status=done&style=none&taskId=u704f79cd-c232-4c1b-a423-c49fa587292&title=&width=811.3333333333334)<br />但是不能同时有两个对同一个对象的类型转换，例如一个构造函数和另一个定义的函数（上图）<br />需要一个 `C(T)` 的不加 `explicit`的构造函数，或者 `operator C()` 的重载；如果两个都有，编译器会出错

---

- `**static_cast**<type>(expression)`
   - is not safe when it is used to cast object pointer
- `**dynamic_cast**<type>(expression)`checks whether a downcast（向下类型转换） of object pointer is safe；If not safe, will return a NULL pointer
- `**const_cast**<type>(expression)` is used to modify the const or volatile property
   - modify a variable that was initially declared as `const`
   - [const_cast examples](https://www.geeksforgeeks.org/const_cast-in-c-type-casting-operators/)
- `**reinterperet**_cast<type>(expression`) is used to convert pointers or reference into integer or backforth
- <br />
#### named casts
```cpp
int a=7;
double *q;
q=(double*) &a;//error


```
重载和类型转换的 best match<br />Exact match is cost-free<br />– Matches involving built-in conversions<br />– User-defined type conversions

## STL 标准模板库
STL = Standard Template Library<br /> Containers

- Sequence Containers (vector, deque, list, forward_list,array, string)
- Associative Containers (set, multiset, map, multimap)
- Unordered Associative Containers (unordered_set,unordered_multiset, unordered_map, unordered_multimap)
- Algorithms（sort, search, etc)
#### Iterators
`for(auto i : arr)`<br />写起来简单，不需要预先初始化迭代器。<br />缺点是不能获得下标，也不能逆序遍历，也不能跳过某个单元，不能修改容器的值。
### 向量 vector
`sort(array[0],array[n])`将向量或数组中的元素排序
```cpp
#include <iostream>
#include <vector>
using namespace std;
int main( ) {
	vector<int> x;
	for (int a=0; a<1000; a++)
		x.push_back(a);
	vector<int>::iterator p;
	for (p=x.begin(); p<x.end(); p++)
		cout << *p << " ";
	return 0;
}
```
`vector.pushback()` 需要拓展时 capacity 按倍数增长一次（到不够了再*2）；size 就+1<br /> `reserve`分配空间(capacity)<br />`clear`size 变成 0；capacity 不变<br />`shrink.fit()`size 和 capacity 一起变//和空 vector 进行 swap()

- It is able to _increase its internal capacity_ as required: as more items are added, it simply makes enough room for them.
- It keeps its own private count of how many items it is currently storing. Its _size_ method returns _the number of objects_ currently stored in it.
- It _maintains the order_ of items you insert into it. You can later retrieve them in the same order.

注意
:::danger
`vector<int> v; v[100]=1; // Whoops!`<br />`if (foo["bob"]==1)//silently created entry “bob”`正确的写法：`if(foo.count("bob"))`
:::
### 链表 list
list 不用 小于<br />`x.push_back(item)`<br />`x.push_front(item)`<br />`x.pop_back()`<br />`x.pop_front()`<br />`x.remove(item)`
```cpp
list<int> L;
for(int i=1; i<=5; ++i)
L.push_back(i);
//delete second item.
L.erase( ++L.begin() );
copy( L.begin(), L.end(),ostream_iterator<int>(cout,",")); //Prints: 1,3,4,5,
```
## Streams 流
![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1702452917243-f78c693a-efe9-410b-98b9-4a22dce60e73.png#averageHue=%23c0c0c0&clientId=u463d58be-9850-4&from=paste&height=329&id=ua121c4a0&originHeight=494&originWidth=1397&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=69905&status=done&style=none&taskId=udc36711c-e790-45b9-96e6-e8e2edc9a32&title=&width=931.3333333333334)<br />Defining a stream extractor，可定义重载的`>>`
```cpp
istream& operator>>(istream& is, T& obj) {
// specific code to read obj
	return is;
}
```
## Templates 模板
重复使用源代码<br />函数模板<br />类模板
```cpp
tempalte <class T>
void swap(T &x, T &y){
    T tmp =y;
    y=x;
    x=tmp;
}
```
the template keyword introduces the template

- The class `T`specifies a parameterized type name
- class means any built-in type or user-defined type
- Inside the template, use T as a type name
```cpp
template <class T>
void foo() { /* ... */ }
foo<int>(); // type T is int
foo<float>(); // type T is float
```
模板不允许隐式类型转换，但可以由不同种类<br />模板参数可以是`const`类型，可以不声明参数类型

- Templates can inherit from non-template classes/template classes
-  Non-template classes can inherit from temp
```cpp
template <class T>
Vector<T>::Vector(int size): m_size(size) {
	m_elements = new T[m_size];
}
template <class T>
T& Vector<T>::operator[](int index)
{
	if(index < m_size && index >= 0) {
	return m_elements[index];
	} else {
	...
	}
}
...

```
## Iterators
visit the elements **in order**, without knowing the details of the container
## Exceptions 异常
异常使程序终止时，下面的语句不执行，但开辟的栈空间会自动释放（析构函数）<br />析构函数中不要抛异常<br />函数后面加`throw()`会不抛出异常<br />In C++, throwing an exception makes a copy of the exception object. 
### try
```cpp
try{
    A;
    B;
}
catch{do something;}//form1
catch(){do something;}//form2
……
```

- try后可以跟任意数量的catch
- throw 可以抛的任意类型, int/double/... 也是可以的。一般不会抛原始数据类型，因为表达的信息有限。通常会做一个类，抛类的对象
### new
`new` does NOT returned 0 on failure, new raises a `bad_alloc()` exception.

## Smart Pointers
在头文件`memory`中<br />`unique_ptr`<br />`shared_ptr`<br />`weak_ptr`<br />ucObject
```cpp
#include <assert.h> 
class UCObject { 
public: 
    UCObject() : m_refCount(0) { } 
    virtual ~UCObject() { assert(m_refCount == 0);};   // 这里 assert, 因为不是对象的问题，是外部的问题。
    UCObject(const UCObject&) : m_refCount(0) { }      // 不拷贝 refcount
    void incr() { m_refCount++; } 
    void decr(); 
    int references() { return m_refCount; } 
private: 
    int m_refCount; 
};
inline void UCObject::decr() { 
    m_refCount -= 1; 
    if (m_refCount == 0) { 
    delete this; 
    } 
} 
```

# Q

1. 关于动态绑定的下列描述中，（ ）是错误的。 (2分)
   1. 动态绑定是以虚函数为基础的
   2. 动态绑定在运行时确定所调用的函数代码
   3. 动态绑定调用函数操作是通过指向对象的指针或对象引用来实现的
   4. 动态绑定是在编译时确定操作函数的

_动态绑定在运行时确定所调用的函数代码，重载函数是在编译时确定操作函数的。_

2.  关于虚函数的描述中，（ ）是正确的。
   1. 虚函数是一个static类型的成员函数
   2. 虚函数是一个非成员函数
   3. 基类中说明了虚函数后，派生类中将其对应的函数可不必说明为虚函数
   4. 派生类的虚函数与基类的虚函数具有不同的参数个数和类型

_A答案：静态成员函数，可以不通过对象来调用，即没有隐藏的this指针。virtual函数一定要通过对象来调用，即有隐藏的this指针。所以虚函数不可以是static的；_<br />_B答案：这很明显吧，怎么不叫成员函数呢orz；_<br />_C答案：这个就是虚函数的特性，只要派生类的函数与基类的同原型（函数返回类型、函数名和形参列表），自动转为虚函数，不需要声明virtual； _<br />_D答案：参考C答案，如果不同的话就叫作函数重载了。_

3.  关于纯虚函数和抽象类的描述中，(  )是错误的。 
   1. 纯虚函数是一种特殊的虚函数，它没有具体的实现；
   2. 抽象类是指具有纯虚函数的类；
   3. 一个基类声明有纯虚函数，该基类的派生类一定不再是抽象类;
   4. 抽象类只能作为基类来使用，其纯虚函数的实现由派生类给出

_带有纯虚函数的类称为抽象类。抽象类是一种特殊的类，它是为了抽象和设计的目的而建立的，它处于继承层次结构的较上层。__抽象类是不能定义对象的__，在实际中为了强调一个类是抽象类，可将该类的构造函数说明为保护的访问控制权限。<br />    抽象类的主要作用是将有关的组织在一个继承层次结构中，由它来为它们提供一个公共的根，相关的子类是从这个根派生出来的。<br />    抽象类刻画了一组子类的操作接口的通用语义，这些语义也传给子类。一般而言，抽象类只描述这组子类共同的操作接口，而完整的实现留给子类。<br />    __抽象类只能作为基类来使用，其纯虚函数的实现由派生类给出__。如果派生类没有重新定义纯虚函数，只是继承基类的纯虚函数，则这个派生类仍然还是一个抽象类。如果派生类中给出了基类纯虚函数的实现，则该派生类就不再是抽象类了，它是一个可以建立对象的具体类了。_

4. <br />
```cpp
#include <iostream>
#include <string.h>
using namespace std;
class A
{
public:
    A() { cout << "A( )" << endl; }
    ~A() { cout << "~A()" << endl; }
};
class B : public A
{
public:
    B() { cout << "B( )" << endl; }
    ~B() { cout << "~B()" << endl; }
};
int main()
{
    A *ap = new B[2];
    delete []ap;
}
```
输出：`A( ) B( ) A( ) B( ) ~A() ~A()` (不想换行了）<br />由于没有虚函数，所以不会析构 B

5. <br />
# Warning

- 两个浮点数之间的相等性测试是不可靠的，应写为`abs(x-y)<1E-14`double (`1E-7`float)
- 赋值运算是右结合的，其他二元运算均为左结合
- 当一个整数被转换成一个字符时，只有低8位能被使用
- 只有声明可以放在.h 文件里面
