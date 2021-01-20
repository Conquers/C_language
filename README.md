# C_language
C_language Study
### C语言-指针基本知识
```
#include <stdio.h>
// point
int main() {
    int num = 1;
    //过程:找num,num找地址,地址取值
    printf("num's value=%d,num's address=%p\n",num,&num);//输出地址%p, &num = 取出Num的地址

    //指针ptr->num的地址(且类型为int)
    int *ptr = &num; //指针自身也有地址!
    printf("ptr1's address=%p\n",&ptr);
    printf("num's address=%p\n",ptr);//其中ptr可以写成&*ptr

    //综上:
    // num = 1 ; &num = num的地址; &ptr = ptr自身的地址; ptr = num的地址;

    //取出 指针ptr所指向的值.即num的值
    printf("num's address=%d\n",*ptr);

    return 0;
}
```

### C语言-应用案例
1. 写一个程序，获取一个int变量num的地址，并显示到终端
2. 将num的地址赋给指针ptr,并通过ptr去修改num的值.
3. 并画出案例的内存布局图

```
#include <stdio.h>
int main() {
    int num = 999;
    printf("num's value = %d\n",num);
    printf("num's address = %p\n",&num);
    //用指针修改num的值
    int *ptr = &num;
    *ptr = 1000;
    printf("num's value = %d\n",num);
    printf("num's address = %p\n",&num);
    return 0;
}
```

### 试编写程序实现如下效果

```
姓名  年龄  成绩  性别  爱好
XX    XX    XX    XX    XX
```

要求:
1. 用变量将姓名、年龄、成绩、性别、爱好存储
2. 添加适当的注释
3. 添加转义字符

```
#include <stdio.h>

// point
int main() {
    char name[10] = "Lucy";//字符数组，可以存放字符串
    short age = 23;
    float score = 78.5;
    char gender = 'M';
    char hobby[20] = "Basketball,soccer";
    printf("name\tage\tscore\tgender\thobby\n %s\t%d\t%.2f\t%c\t%s",name,age,score,gender,hobby);
    return 0;
}
```
### 计算器

```
#include <stdio.h>

// point
int main() {
    int num1,num2;
    printf("put num1");
    printf("put num2");
    num1 = 30;
    num2 = 20;
    printf("*****************************\n\tSmall cal\n*****************************\n");
    printf("num1+num2=%d\n",num1+num2);
    printf("num1*num2=%d\n",num1*num2);
    printf("num1/num2=%d\n",num1/num2);
    printf("num1-num2=%d\n",num1-num2);
}
```

### const和#define的区别

1. const定义的常量时，带类型，define不带类型

```
#define 常量名 常量值;
#define Pi 3.14
const 数据类型 常量名=常量值;
const double pi = 3.14;
```

2. const是在编译、运行的时候起作用，而define是在编译的预处理阶段起作用
3. define只是简单的替换，没有类型检查。简单的字符串替换会导致边界效应

```
#include <stdio.h>
#define A 1
#define B A+3     //B=4
#define C A/B*3   //C=1/4*3

int main(){
    //define是一个简单(直接)的替换过程
    // C = A/A+3*3  其中A=1;
    printf("c=%d", C); //问c=?
    // 所以 C = 10;
    return 0;

}
```
注意括号
```
#include <stdio.h>
#define A 1.0       //如果是1，c=0，如果是1.0,c=0.75
#define B (A+3)     //B=4
#define C A/B*3   //C=1/4*3

int main(){
    //define是一个简单的替换过程
    // C = A/A+3*3  其中A=1;
    printf("c=%.2f", C); //问c=?
    // 所以 C = 10;
    return 0;

}
```


4. const常量可以进行调试的，define是不能进行调试的，主要是预编译阶段就已经替换掉了，调试的时候就没它了
5. const不能重定义，不可以定义两个一样的，而define通过undef取消某个符号的定义再重新定义

```
#include <stdio.h>
const double pi = 3.14;
const double pi = 3.145;
×
#define pi2 3.14 
#undef pi2 3.14   //取消pi2的定义
#define pi2 3.145
√
```

6. define可以配合#ifdef、#ifndef、#endif来使用，可以让代码更加灵活，比如我们可以通过#tdefine来启动或者关闭调试信息。
```
#include <stdio.h>
#define Debug

int main(){
#ifdef Debug    //如果定义过Debug
    printf("defined Debug");
#endif
#ifndef Debug   //如果没有定义过Debug
    printf("undefined Debug");
#endif
}
```
### scanf

```
#include <stdio.h>

// point
int main() {
    char name[10] = "";//字符数组，可以存放字符串
    int age = 0;
    double sal = 0.0;
    char gender = ' ';

    //put information
    printf("Please put name:");
    //scanf("%s",name); 表示接受一个字符串存放到name数组中
    scanf("%s",name);

    printf("Please put age:");
    //因为我们将得到输入存放到age变量指向地址,因此需要加&
    scanf("%d",&age);

    printf("Please put salare:");
    //接收一个double时，格式参数%lf
    scanf("%lf",&sal);
    printf("Please put sex(m/f):");
    scanf("%c",&gender);//有问题 输出sal时按下回车，会将回车作为字符代入gender
    scanf("%c",&gender);//这个是等待用户输入


    printf("\nname %s age %d sal %.2f gender %c", name, age,sal,gender);
    return 0;
}
```

### 枚举

```
#include <stdio.h>

int main(){
    enum DAY{
        MON=1,TUE=2,WED=3,THU=4,FRI=5,SAT=6,SUN=7
    };//这里DAY就是枚举类型,包含了7个枚举元素
    //enum DAY 是枚举类型，day就是枚举变量int a
    enum DAY day; 
    day = WED;      //给枚举变量day赋值，值就是某个枚举元素
    printf("%d" ,day);// 3
    return 0;
}
```


```
//遍历
#include <stdio.h>

enum DAY{
    MON=1,TUE,WED,THU,FRI,SAT,SUN
}day ;//如果没有给赋值编号，就会按照顺序自动赋值

int main() {
    for (day = MON; day <= SUN; day++) {
        printf("Enum element:%d \n", day);
    }
    return 0;
}
```

```
#include <stdio.h>

int main(){
    enum SEASONS {SPRING=1,SUMMER,AUTUMN,WINTER};//定义枚举类型 SEASONS
    enum SEASONS season;//定义了一个枚举变量 SEASON
    printf("Put your favorate season:(1.spring, 2. summer, 3. autumn 4 winter): " );
    scanf("%d",&season);
    switch (season){
        case SPRING:
            printf("your favorate season is spring");break;
        case SUMMER:
            printf("your favorate season is summer");break;
        case AUTUMN:
            printf("your favorate season is autumn");break;
        case WINTER:
            printf("your favorate season is winter");break;
        default:
            printf("你没有选择你喜欢的季节");
    }
}

```


### 函数

```
function.c  //源文件
//内容
定义函数
cal(){
    函数体
    
};
add(){
    函数体
    
};

function.h  //头文件
//内容
声明函数
cal();
add();


//其中.c中含函数
//其中.h只含有函数名

Test.c 源文件
//内容
#include "function.h"   //引入头文件
1.可以使用头文件中声明的函数
2.便于管理和维护
```
1. 引用头文件相当于复制头文件的内容
2. 源文件的名字可以不和头文件一样，但是为了好管理，一般头文件名和源文件名一样.
3. C语言中include <> 与include""的区别

- include<>:引用的是编译器的==类库路径==里面的头文件，用于引用系统头文件。
- include "" :引用的是你==程序目录==的相对路径中的头文件，如果在程序目录没有找到引用的头文件则到编译器的==类库路径==的目录下找该头文件，用于引用用户头文件。
- 所以:==引用系统头文件，两种形式都会可以==，
include <>效率高;引用用户头文件，只能使用include ""
4. 一个#include命令只能包含一个头文件，多个头文件需要多个tinclude命令
5. 同一个头文件如果被多次引入，多次引入的效果和一次引入的效果相同，因为头文件在代码层面有防止重复引入的机制
```
#include "function.h" 
#include "function.h" 
#include "function.h" 
#include "function.h" 
//效果同下
#include "function.h" 
```
6. 在一个被包含的文件(.c)中又可以包含另一个文件头文件(.h)
7. 不管是标准头文件，还是自定义头文件，都只能包含变量和函数的==声明==，不能包含定义，否则在多次引入时会引起重复定义错误

### 函数调用

```
#include <stdio.h>
void test(int n){
    int n2 = n + 1;
    printf("n2 = %d",n2);
}
int main(){
    int number = 6;
    test(number);
    return 0;
}
```

```
函数调用的规则
1. 当调用(执行)一个函数时，就会开辟一个独立的空间(栈)
2. 每个栈空间是相互独立
3. 当函数执行完毕后，会返回到调用函数位置,继续执行
4. 如果函数有返回值，则将返回值赋给接收的变量
5. 当一个函数返回后，该函数对应的栈空间也就销毁




计算器内存
栈:                   
                      test栈                       <--|
                      n->[6]                          |
                      n2->[n+1=7]                     |
    |--               printff("n2 = %d",n2);          |
    |                                                 |
    |                 main栈                          |
    |                 number->[6]                     |
    |                 test(number)                  --|
    |-->              return 0 ;
                      

```

### 函数递归

```
#include <stdio.h>
void Recursion(int n){
    if(n>2){                //递归出口
        Recursion(n-1);
    }
    printf("n=%d\n",n)；
}

int main(){
    int number = 6;
    Recursion(number);
    return 0;
}

output:
n=2
n=3
n=4
n=5
n=6
```

```
计算器内存
栈:      
  
                      Recursion栈            <----| 
                      n->[2]                      |
                      if(n>2)  //不满足           |
                      printf("n=%d\n",n);//输出2  |     
                                                  |
       |--->          Recursion栈                 | 
       |              n->[3]                      |
       |              if(n>2)                     |
       |              Recursion(2)       ---------|
       |              //printf("n=%d\n",n);等待运行
       |
       |              Recursion栈            <----|    
       |              n->[4]                      |     
       |              if(n>2)                     |
       |------------  Recursion(3)                |            
                      //printf("n=%d\n",n);待运行 |
                                                  |
       |--->          Recursion栈                 | 
       |              n->[5]                      |
       |              if(n>2)                     |
       |              Recursion(4)       ---------| 
       |              //printf("n=%d\n",n);待运行
       |
       |              Recursion栈            <----|    
       |              n->[6]                      |     
       |              if(n>2)                     |
       |------------  Recursion(5)                |  
                      //printf("n=%d\n",n);待运行 |
                                                  |
                      main栈                      |   
                      number->[6]                 |   
                      Recursion(number)  ---------|           
                      return 0 ;
                      
```
#### 函数递归需要遵守的重要原则:
1. 执行一个函数时，就创建一个新的受保护的独立空间(新函数栈)
2. 函数的局部变量是独立的,不会相互影响
3. 递归必须向退出递归的条件逼近，否则就是无限递归，死龟了:)
4. 当一个函数执行完毕，或者遇到return，就会返回，遵守谁调用，就将结果返回给谁

```
void f3(int n){
    n++;        //复制再修改
}
void f3(int*p){
    (*p)++;     //直接对原来的数修改
    //p就是n地址所存的值,*取值符
}
void main(){
    int n = 9;
    //f2(n);                    //9
    f3(&n);
    printf("main函数中 n=%d",n);//10
}

```
### 函数参数的传递方式值传递和引用传递使用特点:
1. 值传递:变量直接存储值，两存通常在栈中分配
2. 默认是值传递的数据类型有1.基本数据类型⒉.结构体3.共用体4.枚举类型
3. 引用传递:变量存储的是一个地址，这个地址对应的空间才真正存储数据(值)。
4. 默认是引用传递的数据类型有:==指针和数组==
5. 如果希望函数内的变量能修改函数外的变量，可以传入变量的地址&，函数内
以指针的方式操作变量。从效果上看类似引用，比如修改结构体的属性.


#### 多个参数
其实，不管是值传递还是引用传递，传递给函数的都是变量的副本，不同的是，值传递的是值的拷贝，引用传递的是地址的拷贝，一般来说，地址拷贝效率高，因为数据量小，而值拷贝决定拷贝的数据天小，数据越大，效率越低。


```
#include <stdio.h>
#include <stdarg.h>

//num表示传递的参数个数
//...表示可以传递多个参数,和num一致对应

int MultiParemeter(int num,...){    //可变函数,即参数的个数可以不确定,使用...表示
    int i, totalSum=0;              //totalSum一定要初始化
    int val = 0;
    va_list v1;                     //v1实际是一个字符指针，从头文件里可以找到
    va_start(v1, num);              //使v1指向可变列表中第一个值，即num后的第一个参数
    printf("*v(first parameter) = %d\n",*v1);
    for(i = 0; i < num; i++){       //num 减一是为了防止下标超限
    val = va_arg(v1, int);          //该函数返回v1指向的值，并使v1向下移动一个int的距离，使其指向下一个int
    printf("val = %d\n", val);
    totalSum += val;
    }
    va_end(v1);                     //关闭v1指针，使其指向null
    return totalSum;
}

void main(){
    int totalSum = MultiParemeter(4,10,60,30,-10);
    printf("%d",totalSum);
}

output:
*v(first parameter) = 10
val = 10
val = 60
val = 30
val = -10
90

```

### 交换值
```
#include <stdio.h>
//请编写一个函数swap(int *n1, int *n2)可以交换n1和n2的值
//说明
1.函数名为swap
2.形参是两个指针类型int*
void swap(int *n1, int *n2){
    int temp =*n1;  //表示将n1这个指针指向的变量的值赋给temp
    *n1 = *n2;      //表示将n这个指针指向的变量的值赋给n1这个指针指向的变量
    *n2 = temp;     //表示将temp值赋给n2这个指针指向的变量
}
void main(){
    int n1 = 1;
    int n2 = 2;
    swap(&n1,&n2);
    printf("main n1 = %d n2 = %d",n1,n2);
}

```
```
swap栈  //*代表取值
n1      -------------------->  [0x1122]   0x1144
n2      -------------------->  [0x1133]   0x1155

//int temp =*n1;
-----> temp = 1

//*n1 = *n2; 
-----> n1 = 2;

//*n2 = temp;
-----> n2 = 1;

main栈
n1 ==================== [1]  0x1122
n2 ==================== [2]  0x1133
swap(&n1,&n2)
```
### Static
static关键字在c语言中比较常用，使用恰当能够大大提高程序的模块化特性，有利于扩展和维护。
###### 局部变量使用static修饰
1. 局部变量被static修饰后，我们称为静态局部变量
2. 对应静态局部变量在声明时未赋初值，编译器也会把它初始化为0。
3. 静态局部变量存储于进程的静态存储区(全局性质)，只会被初始一次，即使函数返回，它的值也会保持不变
```
#include <stdio.h>
void fn(){
    int n = 10;//普通变量,每次执行都会初始化，n在栈区
    printf("n=%d", n);
    n++;
    printf("\nn++=%d\n", n);
}

void fn_static(){
    static int n = 10;//静态局部变量,放在静态存储区，全局性质空间

    printf("static n=%d", n);
    n++;
    printf("\nn++=%d\n", n);
}
int main() {
    fn_static();
    fn_static();
    return 0;
}

output:
static n=10
n++=11      
//因为static定义的变量只会初始化一次，第一次10，第二次并不会重新定义为10，而是使用上一次计算后的11
static n=11
n++=12

```


#### 全局变量使用static修饰
1. 普通全局变量对整个工程可见，其他文件可以使用extern外部声明后直接使用。也就是说其他文件不能再定义一个与其相同名字的变量了（否则编译器会认为它们是同一个变量)，静态全局变量仅对当前文件可见，其他文件不可访问，其他文件可以定义与其同名的变量，两者互不影响
```
file.c

int num = 10;//普通全局变量
static int num2= 20;//静态全局变量,只能在本文件中使用，而不能在其它文件使用

file2.c

#include <stdio.h>
//在一个文件中，使用另外—个文件的全局变量,使用extern引入即可
extern int num;
extern int num2;        //报错:因为静态全局变量,只能在本文件中使用，而不能在其它文件使用
void main() {
printf("num=%d num2=%d", num, num2);
}
```
2. 定义不需要与其他文件共享的全局变量时，加上static关键字能够有效地降低程序模块之间的耦合，避免不同文件同名变量的冲突，且不会误使用

#### 函数使用static修饰
1. 函数的使用方式与全局变量类似，在函数的返回类型前加上static，就是静态函数
2. 非静态函数可以在另一个文件中通过extern引用【案例】
3. 静态函数只能在声明它的文件中可见，其他文件不能引用该函数[案例]
4. 不同的文件可以使用相同名字的静态函数，互不影响[案例]
