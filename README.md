# C语言-指针基本知识
```
#include <stdio.h>
// pointer
int main() {
    int num = 1;
    //过程:找num,num找地址,地址取值
    printf("num's value=%d,num's address=%p\n",num,&num);//输出地址%p, &num = 取出Num的地址

    //指针ptr->num的地址(且类型为int)
    int *ptr = &num; //指针自身也有地址!
    printf("ptr1's address=%p\n",&ptr);//取ptr指针本身的地址
    printf("num's address=%p\n",ptr);//取ptr指针存放的地址.其中ptr可以写成&*ptr

    //综上:
    // num = 1 ; &num = num的地址; &ptr = ptr自身的地址; ptr = num的地址;

    //取出 指针ptr所指向的值.即num的值
    printf("num's address=%d\n",*ptr);

    return 0;
}
```

## 指针 应用案例
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

## 转义字符 应用案例 
- 试编写程序实现如下效果

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
## 计算器 应用案例
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


###### 全局变量使用static修饰
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

###### 函数使用static修饰
1. 函数的使用方式与全局变量类似，在函数的返回类型前加上static，就是静态函数
2. 非静态函数可以在另一个文件中通过extern引用
3. 静态函数只能在声明它的文件中可见，其他文件不能引用该函数
```
file.c

#include <stdio.h>
void fun1(void){//普通函数
    printf("hello from fun1.\n");

}
static void fun2(void){//静态函数
    printf("hello from fun2.\n");

}

file2.c

#include <stdio.h>
extern void fun1(void);
extern void fun2(void);
//报错:因为静态全局变量,只能在本文件中使用，而不能在其它文件使用
void main() {
    fun1();
    fun2(); 
    }

output:
hello from fun1
```
4. 不同的文件可以使用相同名字的静态函数，互不影响
```
file.c

#include <stdio.h>
void fun1(void){//普通函数
    printf("hello from fun1.\n");

}
static void fun2(void){//静态函数
    printf("hello from fun2.\n");

}

file2.c

#include <stdio.h>
extern void fun1(void);
void fun1(){
}           //报错:不同的文件可以使用相同名字的静态函数，互不影响
void fun2(){
};
void main() {
    fun1();
    fun2(); 
    }

output:
hello from fun1
```

### 系统函数
###### 字符串

```
#include <stdio.h>
#include <string.h>

int main(){
    char src [50] = "abcdeff";
    char dest [50] = "abcdeff";
    char *p = src;
    char *q = dest;
    printf("str.len=%d\n", strlen(p));

    // || (上面更容易理解一点)

    /*char src[50], dest[50];//定义了两个字符数组(字符串),大小为50
    char * str = "abcdff";
    printf("str.len=%d", strlen(str));*/

    //表示将"hello"拷贝到src,src本来是abcdeff,拷贝后是Kioo = 4,拷贝字符串会将原来的内容覆盖
    strcpy(src,"Kioo");
    printf("str.len=%d\n", strlen(p));

    //表示将"hello"拷贝到src,src本来是abcdeff,拷贝后是hello world! = 12,拷贝字符串会将原来的内容覆盖
    strcpy(dest, "hello world!");
    printf("str.len=%d\n", strlen(q));

    //llstrcat是将src字符串的内容连接到dest ,但是不会覆盖dest原来的内容，而是连接!!
    strcat(dest, src);
    printf("the last string array:desk = %s", dest);

    return 0;
}
output:
str.len=7
str.len=4
str.len=12
the last string array:hello world!Kioo
```
###### 时间
```
#include <stdio.h>
#include <time.h>
void test() {   //运行test函数所需时间
    int i = 0;
    int sum = 0;
    int j = 0;
    for (i; i < 77777777; i++) {
        sum = 0;
        for (j = 0; j < 10; j++) {
            sum += j;
        }
    }
}
int main(){
    time_t curtime; //time_t是<time.h>中结构体类型
    time(&curtime); //time()完成初始化任务

    // ctime返回一个表示当地时间的字符串，当地时间是基于参数timer
    printf("Current time = %s", ctime(&curtime));

    //先得到执行test前的时间
    time_t start_t, end_t;
    double diff_t; //存放时间差
    printf("Program start...\n");
    time(&start_t);//初始化得到当前时间

    test(); //执行test

    //再得到执行test后的时间
    time(&end_t);
    diff_t = difftime(end_t, start_t);//时间差，按秒ent_t - start_t
    printf("test expend %.2f Second",diff_t);
    //然后得到两个时间差就是耗用的时间
    return 0;
}

output:
Current time = Wed Jan 20 18:20:26 2021
Program start...
test expend 2.00 Second
//如果把j<10改成j<100，test expend 19.00 Second，几乎是2的10倍

```

###### 数学
```
#include <stdio.h>
#include <math.h>

int main(){
    double d1 = pow(2.0,3.0);
    double d2 = sqrt(5.0);
    printf("d1=%.2f\n" , d1);
    printf("d2=%.2f", d2);
    return 0;
}

output:
d1=8.00
d2=2.24
```

#### 基本数据类型和字符串类型的抟换
```
#include <stdio.h>

//基本类型转字符串类型
int main(){
    char str1[20];  //字符数组  即字符串
    char str2[20];
    char str3[20];
    int a=20984,b=48090;
    double d=14.309948;
    sprintf(str1,"%d,%d\n",a,b);
    sprintf(str2,"%.2f\n",d);
    sprintf(str3,"%8.2f\n",d); //8.2% 一共有8位，小数点占2位，不够的用空格补齐
    printf("str1=%s,str2=%s,str3=%s",str1,str2,str3);
}

output:
str1=20984,48090
,str2=14.31
,str3=   14.31      //空格代表不足8位，补足
```

```
#include <stdio.h>
#include <stdlib.h>

//字符串类型转基本数据类型
int main(){
    char str[10] = "123456";
    char str2[10]="12.67423";
    char str3[2]= "ab";
    char str4[4]= "111";

    //说明
    int num1 = atoi(str);       //将str转成整数
    short s1 = atoi(str4);      //将str转成整数

    double d = atof(str2);      //将str转成浮点数
    char c = str3[0];           //获取到str3这个字符串(字符数组)的第一个元素
    printf("num1=%d s1=%d d=%f c=%c",num1,s1,d,c);
}

output:
num1=123456 s1=111 d=12.674230 c=a
```

##### 注意事项
1. 在将char数组类型转成基木数据类型时，要确保能够转成有效的数据，比如我们可以把"123"，转成一个整数，但是不能把"hello”转成一个整数
2. 如果格式不正确，会默认转成0或者0.0
```
#include <stdio.h>
#include <stdlib.h>

//字符串类型转基本数据类型
int main(){
    char str[10] = "hello";
    int num1 = atoi(str);       //将str转成整数
    printf("num1=%d",num1);
}

output:
num1=0
```

#### 预处理命令基本介绍
1. 使用库函数之前，应该用include引入对应的头文件。这种以#号开头的命令称为预处理命令。
2. 这些在编译之前对源文件进行简单加工的过程，就称为预处理（即预先处理、提前处理)
3. 预处理主要是处理以#开头的命令，例如#include <stdio.h>等。预处理命令要放在所有函数之外，而且一般都放在源文件的前面
4. 预处理是C语言的一个重要功能，由预处理程序完成。当对一个源文件进行编译时，系统将自动调用预处理程序对源程序中的预处理部分作处理，处理完毕自动进入对源程序的编译
5. C语言提供了多种预处理功能，如宏定义、文件包含、条件编译等，合理地使用它们会使编写的程序便于阅读、修改、移植和调试，也有利于模块化程序设计


---

```
具体要求:
开发一个c语言程序，让它暂停5秒以后再输出内容"helo,尚硅谷!~"，并且要求跨平台，在Windows和Linux下都能运行，如何处理
提示
1. Windows平台下的暂停函数的原型是void Sleep(DWORD dwMilliseconds)，参数的单位是“毫秒”，位于<windows.h>头文件。
2. Linux平台下暂停函数的原型是unsigned int sleep (unsigned int seconds)，参数的单位是“秒”，位于<unistd.h>头文件
3. #if、#elif、#endif就是预处理命令，它们都是在编译之前由预处理程序来执行

#include <stdio.h>

#if _WIN64//如果是windows平台,就执行#include <windows.h>
#include <windows.h>
#elif _linux_ //否则不是windows平台,就执行#include <unistd.h>
#include <unistd.h>
#endif
int main() {
    //不同的平台下调用不同的函数
    #if _WIN64//识别windows平台
    Sleep(5000); //5000毫秒
    #elif _linux_//识别linux平台
    sleep(5);/5秒
    #endif
    puts("hello,world");
    return 0;
}
```

##### 宏定义


###### #define叫做宏定义命令，它也是c语言预处理命令的一种。所谓宏定义，就是用一个标识符来表示一个字符串，如果在后面的代码中出现了该标识符，那么就全部替换成指定的字符串



```
快速回顾

#define N 100
int main(){
    int sum = 20+ N;    //N->100
    printf("%d\n" , sum); 
    return 0;
}

小结:
1)int sum= 20+N，N被100代替了。
2)#define N 100就是宏定义,N为宏名，100是宏的内容（宏所表示的字符串）。在预处理阶段,对程序中所有出现的“宏名”，预处理器都会用宏定义中的字符串去代换，这称为“宏替换”或“宏展开”。
3)宏定义是由源程序中的宏定义命令#define完成的，宏替换是由预处理程序完成的

```

###### 宏定义的形式
#define 宏名 字符串
1. #表示这是一条预处理命令，所有的预处理命令都以#开头。宏名是标识符的一种，命名规则和变量相同。字符串可以是数字、表达式、if语句、函数等
2. 这里所说的字符串是一般意义上的字符序列，不要和c语言中的字符串等同，它不需要双引号
```
#include <stdio.h>
//宏定义,宏名M，对应的字符串(n*n+3*n)
#define M (n*n+3*n)
int main(){
    int sum, n;
    printf("Input a number: ");
    scanf("%d",&n);
    sum = 3*M+4*M+5*M;//宏展开?    3*(n*n+3*n)+4*(n*n+3*n)+5*(n*n+3*n)
    printf("sum=%d\n", sum);
    return 0;
}
output:
Input a number:3
sum=216
```
3. 程序中反复使用的表达式就可以使用宏定义
4. 宏定义不是说明或语句，在行末不必加分号，如加上分号则连分号也一起替换
5. 宏定义必须写在函数之外，其作用域为宏定义命令起到源程序结束。如要终止其作用域可使用#undef命令
```
#include <stdio.h>
#define PI 3.14159
int main(){
    printf("PI=%f",PI);
    return 0;
}
#undef PI //取消宏定义
void func(){
    //code
    printf("PI=%f",PI);//错误,这里不能使用到PI了,编译器中PI为红色
}
```
6. 代码中的宏名如果被引号包围，那么预处理程序不对其作宏代替

```
#include <stdio.h>
#define OK 100
int main(){
    printf("OK\n");     //"..OK.."不会被宏替换
    return 0;
}
```
7. 宏定义允许嵌套，在宏定义的字符串中可以使用已经定义的宏名，在宏展开时由预处理程序层层代换
```
#define PI 3.1415926
#define S Pl*y*y /* PI是已定义的宏名 */

printf("%f", S);
//在宏替换后变为:
printf("%f,3.1415926*y*y);
```
8. 习惯上宏名用大写字母表示，以便于与变量区别。但也允许用小写字母
9. 可用宏定义表示数据类型，使书写方便
```
#define UINT unsigned int
void main(), {
    UINT a, b;  //宏替换 
}
```

10. 宏定义表示数据类型和用typedef定义数据说明符的区别:
- 宏定义只是简单的字符串替换，由预处理器来处理;
- 而typedef是在编译阶段由编译器处理的，它并不是简单的字符串替换，而给原有的数据类型起一个新的名字，将它作为一种新的数据类型。
 


#### 带参数的宏定义
1. c语言允许宏带有参数。在宏定义中的参数称为“形式参数”，在宏调用中的参数称为“实际参数”，这点和函数有些类似
2. 对带参数的宏，在展开过程中不仅要进行字符串替换，还要用实参去替换形参
3. 带参宏定义的一般形式为#define宏名(形参列表)字符串，在字符串中可以含有各个形参
4. 带参宏调用的一般形式为:宏名(实参列表);
```
#include <stdio.h>
/* 1. MAX就是带参数的宏
2. (a,b)就是形参
3. (a>b) ? a: b是带参数的宏对应字符串，该字符串中可以使用形参
*/
#define MAX(a,b) (a>b)? a : b
int main(){
    int x , y, max;
    printf("input two numbers: ");
    scanf("%d %d" ,&x,&y);
    
    //说明
    //1. MAX(x,y);调用带参数宏定义
    //2.在宏替换时(预处理，由预处理器)，会进行字符串的替换，同时会使用实参，去替换形参
    //3.即MAX(x, y)宏替换后(x>y)? x:y

    max = MAX(x, y);
    printf("max=%d\n" , max);
    return 0;
}
```

注意
1. 带参宏定义中，形参之间可以出现空格，但是宏名和形参列表之间不能有空格出现
#define MAX(a,b) (a>b)?a:b 如果写成了#define MAX (a,b) (a>b)?a:b
将被认为是无参宏定义，宏名MAX代表字符串(a,b) (a>b)?a:b 
而不是:MAX(a,b)代表(a>b) ? a: b 了
2. 在带参宏定义中，不会为形式参数分配内存，因此不必指明数据类型。而在宏调用中，实参包含了具体的数据，要用它们去替换形参，因此实参必须要指明数据类型
3. 在宏定义中，字符串内的形参通常要用括号括起来以避免出错。
```
#include <stdio.h>
#include <stdlib.h>

#define SQ(y)y*y //带参宏定义
int main(){
    int a, sq;
    printf("input a number: ");
    scanf("%d", &a);
    sq = SQ(a+1);//宏替换a+1*a+1 而不是(a+1)*(a+1)
    printf("sq=%d\n", sq);
    system("pause");
    return 0;
}

output:
input a number:30
 sq=61
请按任意键继续. . .
```

#### 带参宏定义和函数的区别
1. 宏展开仅仅是字符串的替换，不会对表达式进行计算;宏在编译之前就被处理掉了，它没有机会参与编译，也不会占用内存。
2. 函数是一段可以重复使用的代码，会被编译，会给它分配内存，每次调用函数，就是执行这块内存中的代码
3. 案例说明:要求使用函数计算平方值，使用宏计算平方值，并总结二者的区别

```
#include <stdio.h>
#include <stdlib.h>
int SQ(int y){ //函数，求y的平方
    return ((y)*(y));
}
int main() {
    int i = 1;
    while (i <= 5) {
        printf("%d^2= %d\n", (i-1), SQ(i++));   //i-1是因为i++先执行,执行完了i就变成了2
        //    ||
        //printf("%d^2= %d\n", i, SQ(i));
        //i=i+1;
    }
    return 0;
}
output:
1^2= 1
2^2= 4
3^2= 9
4^2= 16
5^2= 25

//下面代码有问题
#include <stdio.h>
#define SQ(y) ((y)*(y))
int main(){
    int i=1;
    while(i<=5){            //这里相当于计算了1,3,5的平方
        //讲入循环3次
        //1 * 1 = 1, 3 * 3 = 9, 5 * 5 = 25
        //              SQ(i++)宏调用展开((i++)*(i++))
        printf("%d^2= %d\n",i, SQ(i++));  //1*2 3*4 5*6
    }
    return 0;
}

output:
3^2= 2
5^2= 12
7^2= 30
```

#### 预处理命令

指令 | 说明
---|---
# | 空指令，无任何效果
#include | 包含一个源代码文件
#define | 定义宏
#undef | 取消已定义的宏
#if | 如果给定条件为真，则编译下面代码
#ifdef | 如果宏已经定义，则编译下面代码
#ifndef | 如果宏没有定义，则编译下面代码
#elif | 如果前面的#if给定条件不为真，当前条件为真，则编译下面代码
#endif | 结束一个#if....#else条件编译块

#### 数组
字符数组实际上是一系列字符的集合，也就是字符串(String)。在C语言中，没有专门的字符串变量，没有string类型，通常就用一个字符数组来存放一个字符串.
```


#include <stdio.h>
int main() {
    char array[6] = {'h', 'e', 'l', 'l', 'o'};
    char str[3] =  {'h', 'e', 'l'};//修改版本 char str[4] =  {'h', 'e', 'l','\0'};
    char str2[] = {'a','c','k};//这个后面系统也不会自动添加"\0',即同上str[3],
    
    //\0 表示字符串结束,之后的未知
    //输出array,系统会这样处理
    //从第一个字符开始输出，直到遇到\0,表示该字符串结束
    //printf("%s", array); 不出问题是因为array有六个空间，只使用了5个，默认在最后加上\0 
    printf("%s", str);
    //
}
output:
helhello //这里是因为最后没有\0结尾,所以会继续往后面遍历，直到在o后面检测到了\0

    内存 array:
|----| |----| |----| |----| |----| |----| |------|
|h   | |e   | |l   | |l   | |o   | |\0  | |unkown| 
|----| |----| |----| |----| |----| |----| |------|

    内存 str:
|----| |----| |----| |------| |------| |------|
|h   | |e   | |l   | |unkown| |unkown| |unkown|
|----| |----| |----| |------| |------| |------|


结论:如果在给某个字符数组赋值时，(1)赋给的元素的个数小于该数组的长度，则会自动在后面加'\0',表示字符串结束，(2)赋给的元素的个数等于该数组的长度，则不会自动添加'\0'

```

```
char arr[]="hello"
    内存 array:
|----| |----| |----| |----| |----| |----| |------|
|h   | |e   | |l   | |l   | |o   | |\0  | |unkown| 
|----| |----| |----| |----| |----| |----| |------| //默认加上'\0'

```

#### 字符数组指针
```
#include <stdio.h>
void main() {
//使用一个指针 p,指向一个字符数组
    char *p="hello";
    printf("pointer p->%s", p);
}
output:
pointer p->hello

    内存 array:
    
指针本身的地址0x1122      数组的地址0x1166 0x1167 0x1168 0x1169 0x116a 0x116b //数组是连续空间
            p ->  0x1166   ------>  |----| |----| |----| |----| |----| |----| 
                                    |h   | |e   | |l   | |l   | |o   | |\0  | 
                                    |----| |----| |----| |----| |----| |----| 
```

###### 使用字符指针变量和字符数组两种方法表示字符串的讨论
1.  字符数组由若干个元素组成，每个元素放一个字符;而字符指针变量中存放的是地址（字符串/字符数组的首地址），绝不是将字符串放到字符指针变量中（是字符串首地址） 上 内存图示
2. 对字符数组只能对各个元素赋值，下能用以下方法对字符数组赋值
```
char str[6]; //str实际是一个常量

str ->   |----| |----| |----| |----| |----| |----| 
         |    | |    | |    | |    | |    | |    | 
         |----| |----| |----| |----| |----| |----| 

str="hello";//错误

str[0] = 'i';//ok
```
3. 对字符指针变量,来用下面方法赋值，是可以的
```
#include <stdio.h>
void main() {
    char *p="hello";            //①
    printf("p's intrinsical address:%p p->%p\n", &p, p);
    p="hello,world";            //②
    printf("p's intrinsical address:%p p->%p\n", &p, p);
    printf("pointer p->%s", p);
}
output:
p's intrinsical address:000000000061FE18 p->0000000000404000
p's intrinsical address:000000000061FE18 p->000000000040402A   
 //即用指针赋值的，所指向的地址不同
 //用指针赋值，也就是开辟另一个内存空间赋值，再把原来的回收销毁
 //p本身的地址不会变
pointer p->hello,world



intrinsical address:000000000061FE18
  |
  | 
  p ->   |----| |----| |----| |----| |----| |----| //p->0000000000404000 = ①
         |    | |    | |    | |    | |    | |    | 
         |----| |----| |----| |----| |----| |----| 
  p ->   |----| |----| |----| |----| |----| |----| //p->000000000040402A = ② 
         |    | |    | |    | |    | |    | |    | 
         |----| |----| |----| |----| |----| |----| 
```

#### 二维数组 n维数组 //本质一维数组
```
#include <stdio.h>
int main() {
    int a[3][4]; //int a[3][3]= {{0,0,1},{1,1,1},{1,1,3}};
    for(int i =0;i<3;i++){
        for(int j = 0;j<4;j++){
            a[i][j] = 0;    //二维数组全部赋值0
        }
    }
    //int a[4][6]={{0,0,0,0},{0,0,0,0},{0,0,0,0}}

    for(int i =0;i<3;i++){  //输出二维数组
        for(int j = 0;j<4;j++){
            printf("%d",a[i][j]);
        }
        printf("\n");
    }
    
    //二维数组的内存布局
    printf("Two-dimensional array a : first element address=%p\n", a);
    printf("Two-dimensional array a : a[0]addres=%p\n", a[0]);
    printf("Two-dimensional array a :[0][0]address=%p\n", &a[0][0]);
    //这三个是一样的
    printf("Two-dimensional array a :[O][1]addres=%p\n", &a[0][1]);
    //这个元素的地址是在前一个加上4个字节，int占四个字节
    
    //将二维数组的各个元素的地址输出及每行第一个元素的地址
    for (int i = 0; i < 3; i++) {
        printf("a[%d]address=%p\n", i, a[i]);
        for (int j = 0; j < 4; j++) {
            printf("a[%d][%d]address=%p\n", i, j, &a[i][j]);
        }
        printf("\n");
    }
    return 0;
}
a   ->   |----| |----| |----| |----|
         |    | |    | |    | |    | 
         |----| |----| |----| |----|
         
         |----| |----| |----| |----| 
         |    | |    | |    | |    | 
         |----| |----| |----| |----| 
         
         |----| |----| |----| |----| 
         |    | |    | |    | |    | 
         |----| |----| |----| |----| 
output:
0000
0000
0000
Two-dimensional array a : first element address=000000000061FDE0
Two-dimensional array a : a[0]addres=000000000061FDE0
Two-dimensional array a :[0][0]address=000000000061FDE0
Two-dimensional array a :[O][1]addres=000000000061FDE4

a[0]address=000000000061FDD0
a[0][0]address=000000000061FDD0
a[0][1]address=000000000061FDD4
a[0][2]address=000000000061FDD8
a[0][3]address=000000000061FDDC
//C + 4 = 12 + 4 = 16 = 0;
a[1]address=000000000061FDE0
a[1][0]address=000000000061FDE0
a[1][1]address=000000000061FDE4
a[1][2]address=000000000061FDE8
a[1][3]address=000000000061FDEC
//C + 4 = 12 + 4 = 16 = 0;
a[2]address=000000000061FDF0
a[2][0]address=000000000061FDF0
a[2][1]address=000000000061FDF4
a[2][2]address=000000000061FDF8
a[2][3]address=000000000061FDFC


Process finished with exit code 0

```
##### 二维数组实例
```
#include <stdio.h>

int main(){
    int map[3][3]= {{0,0,1},{1,1,1},{1,1,3}};

    //sizeof(map) = 整个数组的大小      9*4 = 36
    //sizeof(map[0] = map中第一行的大小 3*4 = 12
    int rows = sizeof(map) / sizeof(map[0]);//整个数组的大小/第一行的大小
    printf("rows=%d\n",rows);

    int cols = sizeof(map[0]) / sizeof(int);//第一行的大小/类型大小
    printf("cols=%d\n",cols);         //12/4=3

    //遍历二维数组
    for(int i = 0;i < rows;i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d ", map[i][j]);
        }
        printf("\n");
    }
    //计算二维数组的和
    for(int i = 0;i < rows;i++) {
        for (int j = 0; j < cols; j++) {
            sum = sum + map[i][j];
        }
    }
    printf("sum = %d",sum);
    return 0;
    }
    
output:
rows=3
cols=3
001
111
113
sum = 9
```
###### 二维数组注意事项

```
1. 可以只对部分元素赋值，未赋值的元素自动取“零”值
#include <stdio.h>
int main(){
    int a[4][5]= {{1},{2},{3},{1}};
    int i,j;
    for (i= 0; i<4; i++){
        for (j = 0; j<5 ; j++){
            printf("%d ",a[i][j]);
        }
        printf("\n");
    }
}
output:
1 0 0 0 0
2 0 0 0 0
3 0 0 0 0
1 0 0 0 0

2. 如果对全部元素赋值，那么第一维的长度可以不给出。比如:
int a[3][3]={1,2,3,4,5,6,7,8,9};
可以写为:
int a[][3]= {1,2,3,4,5,6,7,8,9};
不可以是 int a[3][]= {1,2,3,4,5,6,7,8,9};

3. 二维数组可以看作是由一维数组嵌套而成的;如果一个数组的每个元素又是一个数组，那么它就是二维数组。
二维数组a[3][4]可看成三个一维数组，它们的数组名分别为a[0]、a[1]、a[2]。
这三个一维数组都有4个元素，如，一维数组a[0]的元素为a[0][0]、a[0][1]、a[0][2]、a[0][3]

```
#### 断点调试
```
变量的变化情况
#include <stdio.h>
int main(){
    int sum = 0;
    int i;
    for(i = 0; i < 10; i++) {
        sum += i;
        printf("i=%d\n", i);
        printf("sum=%d\n", sum);
    }
    printf("quit for\n");
}

数组越界异常
#include <stdio.h>
int main(){
    int arr[]={1,2,3,4,5};
    int i = 0;
    int len = sizeof(arr) / sizeof(int);
    for(i = 0; i<= len; i++){ //数组最大小标应该是len-1
        printf("arr[%d]=%d\n", i, arr[i]);
    }
}

output:
arr[0]=1
arr[1]=2
arr[2]=3
arr[3]=4
arr[4]=5
arr[5]=0 //越界 

函数体调用
#include <stdio.h>
double cal(int num1,int num2,char oper){
    double res = 0.0;
    switch(oper) {
        case '+' :
            res = num1 + num2;
            break;
        case '-':
            res = num1 - num2;
            break;
        case '*':
            res = num1 * num2;
            break;
        case '/':
            res = num1 / num2;
            break;
        default :
            printf("你的运算符有误~");
    }
    return res;
}

int main(){
    int n1 = 10;
    int n2 = 40;
    char oper ='+';
    double res = cal(n1,n2,oper);
    printf("res=%.2f", res);
    }


```
#### 指针
1. 指针是c语言的精华，也是c语言的难点。
2. 指针，也就是内存的地址;所谓指针变量，也就是保存了内存地址的变量。
3. 获取变量的地址，用&，比如:int num =10, 获取num的地址:&num
4. 指针类型，指针变量存的是一个地址，这个地址指向的空间存的才是值
比如: int *ptr = & num; ptr就是指向int类型的指针变量，即ptr是int *类型。
5. 获取指针类型所指向的值，使用: * ，比如: int * ptr,使用 * ptr获取ptr指向的值


```
#include <stdio.h>


int main(){
    int var[]={10,20,30};
    int i,*ptr;

    //正向遍历
    ptr = var;
    for(i=0;i<3;i++){
        printf("var[%d] address=%p\n",i,ptr);
        printf("value: var[%d]=%d\n",i,*ptr);
        ptr++;
    }

    //反向遍历
    ptr = &var[2];
    //若这里没有&，则Incompatible integer to pointer conversion assigning to 'int *' from 'int'; take the address with &
    //但是正向遍历是可以的，因为数组名就是首地址，即var代表的是一个地址
    for(i=3;i>0;i--) {
        printf("ptr address %p\n", ptr);
        printf("value:var[%d]=%d\n", i - 1, *ptr);
        ptr--;
    }
    return 0;
}

output:
var[0] address=000000000061FE04
value: var[0]=10
var[1] address=000000000061FE08
value: var[1]=20
var[2] address=000000000061FE0C
value: var[2]=30
//注 var[i]的地址和ptr地址是相同的
ptr address 000000000061FE0C
value:var[2]=30
ptr address 000000000061FE08
value:var[1]=20
ptr address 000000000061FE04
value:var[0]=10
```

#### 指针数组
要让数组的元素指向int或其他数据类型的地址(指针)。可以使用指针数组。
指针数组定义
数据类型*指针数组名[大小];
比如: int *ptr[3];
1. ptr声明为一个指针数组
2. 由3个整数指针组成。因此，ptr中的每个元素，都是一个指向int值的指针。


```
#include <stdio.h>
int main(){
    int var[]={10,20,30};
    int i, *ptr[3];
//    for ( i = 0; i< 3; i++){
//        printf("array address=%p\n",&var[i]);    //数组的地址
//    }
//    for ( i = 0; i< 3; i++){
//        printf("ptr[%d] address=%p\n",i,&ptr[i]);    //指针本身的地址
//    }

    for ( i = 0; i< 3; i++){
        ptr[i] = &var[i];  //把数组的地址分别赋值给数组指针中的地址1，地址2，地址3
    }
    for ( i = 0; i < 3; i++){
        printf("value of var[%d]=%d\n", i, *ptr[i] );//遍历指针数组，再用取值
        printf("array address=%p\n",ptr[i]);         //指针数组存放的地址
        printf("ptr[%d] address=%p\n",i,&ptr[i]);    //指针本身的地址
    }
    return 0;
}
自身地址 0x1133  0x1137  0x113B
var ->   |----| |----| |----| 
         | 10 | | 20 | | 30 | 
         |----| |----| |----| 
         

自身地址 0x1122  0x1126  0x112A
ptr ->   |-----| |-----| |-----| 
         |地址1| |地址2| |地址3| 
         |-----| |-----| |-----| 
赋值后
自身地址 0x1122  0x1126  0x112A
ptr ->   |------| |------| |------| 
         |0x1133| |0x1137| |0x113B| 
         |------| |------| |------| 

output:
value of var[0]=10
array address=000000000061FE10
ptr[0] address=000000000061FDF0
value of var[1]=20
array address=000000000061FE14
ptr[1] address=000000000061FDF8
value of var[2]=30
array address=000000000061FE18
ptr[2] address=000000000061FE00
//数组地址相差4，指针地址相差8?
```


```
#include <stdio.h>
int main(){
    //指针数组
    char *books[] = {
            "one","two","three"
    };
    int i,len =3;
    for(i=0;i<len;i++){
        printf("books[%d] -> %s\n",i,books[i]);
        //注books[i]，而不是*books[i]
        //如果是加*
        //应该是
        //int num = 10;
        //int *ptr = &num;
        //printf("num = %d\n",*num);
    }
    
    //数组
    char book[] = {"onetwothree"};
    for(i=0;i<11;i++){
        printf("book[%d]=%c\n",i,book[i]);
    }
    return 0;
}

output:
books[0] -> one
books[1] -> two
books[2] -> three
book[0]=o
book[1]=n
book[2]=e
book[3]=t
book[4]=w
book[5]=o
book[6]=t
book[7]=h
book[8]=r
book[9]=e
book[10]=e
```

#### 多重指针
基本介绍
指向指针的指针是一种多级间接寻址的形式，或者说是一个指针链。通常，一个指针包含一个变量的地址。当我们定义一个指向指针的指针时，第一个指针包含了第二个指针的地址，第二个指针指向包含实际值的位置(如下图)

```
pointer2         pointer1        Variable
|--------|       |--------|       |-------|
|address2| ----> |address1| ----> | value |
|--------|       |--------|       |-------|
 二级指针        一级指针
 
通过pointer1取值则*pointer1
通过pointer2取值则**pointer2(*pointer2 = address1)
```

1. 一个指向指针的指针变量必须如下声明，即在变量名前放置两个星号。例如，下面声明了一个指向int类型指针的指针: int **ptr;//ptr的类型是int **
2. 当一个目标值被一个指针间接指向到另一个指针时，访问这个值需要使用两个星号运算符,比如 **ptr
3. 案例演示+内存布局图

```
#include <stdio.h>
int main (){
    int var;
    int *ptr;    //一级指针
    int **pptr;  //二级指针
    int ***ppptr;//三级指针
    var = 3000;
    ptr = &var;   //var变量的地址赋值给ptr
    pptr = &ptr;  //把ptr的地址赋值给pptr
    ppptr = &pptr;//把pptr的地址赋值给ppptr
    //var的地址，var存放变量
    printf("var's address =%p,var =%d\n",&var,var);
    
    //ptr指针本身的地址，ptr存放的地址
    printf("ptr's intrinsical address =%p,ptr's address=%p,*ptr = %d\n",&ptr,ptr,*ptr );
    
    //pptr指针本身的地址，pptr存放的地址
    printf("pptr's intrinsical'= %p,pptr's address=%p,**pptr = %d\n",&pptr,pptr,**pptr);
    
    //ppptr指针本身的地址，ppptr存放的地址
    printf("ppptr's intrinsical'= %p,ppptr's address=%p,***pptr = %d\n",&ppptr,ppptr,***ppptr);
    return 0;
}
output:
var's address =000000000061FE1C,var =3000
//var的地址，var存放变量

ptr's intrinsical address =000000000061FE10,ptr's address=000000000061FE1C,*ptr = 3000
//ptr指针本身的地址，ptr存放的地址

pptr's intrinsical'= 000000000061FE08,pptr's address=000000000061FE10,**pptr = 3000
//pptr指针本身的地址，pptr存放的地址

ppptr's intrinsical'= 000000000061FE00,ppptr's address=000000000061FE08,**pptr = 3000
//ppptr指针本身的地址，ppptr存放的地址

pptr 地址:000000000061FE08              ptr 地址:000000000061FE10           var 地址:000000000061FE1C
|----------------|                      |----------------|                  |-------|
|000000000061FE10|          ---->       |000000000061FE1C|         ---->    | 3000  |
|----------------|                      |----------------|                  |-------|
 二级指针                       一级指针
 
        |
        |
        |
 ppptr 地址:000000000061FE00
|----------------|                     
|000000000061FE08|          
|----------------|    
三级指针                      
```

###### 传递指针(地址)给函数
当函数的形参类型是指针类型时，是使用该函数时，需要传递指针，或者地址，或者数组给该形参.


```
//传地址或指针给指针变量
#include <stdio.h>

void test2(int *p); //函数声明,接收int *

int main(){
    int num=90;
    int *p = &num;  //将num的地址赋值给p
    test2(&num);    //传地址  第一种     num----->[90]     自身地址:0x1122 取用num自身地址:0x1122
    printf("\nmain(),num=%d" , num);
    test2(p);       //传指针  第二种     p----->  [0x1122] 自身地址:0x1133 取用p存放的地址
    printf("\nmain(),num=%d" , num);
    return 0;
}

void test2(int *p){ //函数体
    *p += 1;  //*p = num的值,*取值
}

output:

main(),num=91       //调用第一种方法
main(),num=92       //调用第二种方法

内存:


text2栈:
p----->  [0x1122] 自身地址:0x1166


main栈:
num----->[90]     自身地址:0x1122 //调用text2后num----->[91]
p----->  [0x1122] 自身地址:0x1133

```

```
//传数组给指针变量
//数组名本身就代表该数组首地址,因此传数组的本质就是传地址。
#include <stdio.h>

//函数声明:函数在主函数下面
double getAverage(int *arr,int size);
double getAverage2(int *arr,int size);

int main() {
    /*带有5个元素的整型数组*/
    int balance[5] = {10, 20, 30, 40, 50};
    double avg;
    /*传递一个指向数组的指针作为参数*/
    avg = getAverage2(balance, 5);
    /*输出返回值*/
    printf("Average value is: %f\n", avg);
    return 0;
}

//arr是一个指针
double getAverage(int *arr, int size) {
    int i, sum = 0;
    double avg;
    for (i = 0; i < size; ++i) {
        //arr[0] = arr + 0 int的字节
        //arr[1] = arr + 1 int的字节(4)
        //arr[2] = arr + 2 int的字节(8)
        //....
        
        sum += arr[i];  //数组下标
        //printf("arr 1 address is %p\n",&arr[i]);
        //printf("arr 2 address is %p\n",arr);
    }
    avg = (double) sum / size;
    return avg;
}

//arr是一个指针
double getAverage2(int *arr, int size) {
    int i, sum = 0;
    double avg;
    for (i = 0; i < size; ++i) {
        sum += *arr;    
        arr++;          //指针的自增运算
        //printf("arr 1 address is %p\n",&arr[i]);//错误的，
        //这里的arr是指针，如果这的arr[i] 改成arr[0]正确了
        
        printf("arr 1 address is %p\n",&arr[0]);
        //||
        printf("arr 2 address is %p\n",arr);
    }
    avg = (double) sum / size;
    return avg;
}

output:
两种方式的地址不一样

getAverage 
arr 1 address is 000000000061FE00
arr 1 address is 000000000061FE04
arr 1 address is 000000000061FE08
arr 1 address is 000000000061FE0C
arr 1 address is 000000000061FE10
//&arr[i] 取出每一个的地址

arr 2 address is 000000000061FE00
arr 2 address is 000000000061FE00
arr 2 address is 000000000061FE00
arr 2 address is 000000000061FE00
arr 2 address is 000000000061FE00
//arr全部一样是因为这种方式是通过数组下标来遍历，所以取地址只会取第一个的地址，所以不会改变
Average value is: 30.000000

getAverage2
arr 1 address is 000000000061FE04
arr 1 address is 000000000061FE0C
arr 1 address is 000000000061FE14
arr 1 address is 000000000061FE1C
arr 1 address is 000000000061FE24
//&arr[i] 取出每一个的地址      但是为什么是+8?


arr 2 address is 000000000061FE04
arr 2 address is 000000000061FE08
arr 2 address is 000000000061FE0C
arr 2 address is 000000000061FE10
arr 2 address is 000000000061FE14
//通过指针的自增来取地址
Average value is: 30.000000

改正后:
arr 1 address is 000000000061FE00
arr 2 address is 000000000061FE00
arr 1 address is 000000000061FE04
arr 2 address is 000000000061FE04
arr 1 address is 000000000061FE08
arr 2 address is 000000000061FE08
arr 1 address is 000000000061FE0C
arr 2 address is 000000000061FE0C
arr 1 address is 000000000061FE10
arr 2 address is 000000000061FE10


getAverage2栈
arr----->[0x1122]  自身地址0x1133 //arr指针存放的是数组balance第一个元素的地址


main栈
balance ----> {10[0x1122], 20, 30, 40, 50};
avg = getAverage2(balance, 5);
```
###### 返回指针的函数
c语言允许函数的返回值是一个指针(地址），这样的函数称指针函数

编写一个函数strlong()，返回两个字符串中较长的一个。

```
#include <string.h>
#include <stdio.h>
char *strlong(char *str1, char *str2){
    printf("str1's lenth is %d,str2's lenth is%d\n", strlen(str1), strlen(str2));
    if(strlen(str1) >= strlen(str2)){
        return str1;
    }else{
        return str2;
    }
}
int main(){
    char str1[30], str2[30], *str;
    printf("Please input 1st str:");
    gets(str1); // get = scanf
    printf("Please input 2nd str:");
    gets(str2);
    str = strlong(str1, str2);
    printf("Longest string: %s ", str);
    return 0;
}

output:

Please input 1st str:hello
Please input 2nd str:world
str1's lenth is 5,str2's lenth is5
Longest string: hello
```

注意事项:
1. 用指针作为函教返回值时需要注意，函数运行结束后会销毁在它内部定义的所有局部数据，包括局部变量、局部数组和形式参数，函数返回的指针不能指向这些数据
```
#include <string.h>
#include <stdio.h>
int *func(){
    int n = 100;    //局部变量
    return &n;
}
int main(){
    int *p = func();    //func返回指针
    int n;
    n = *p;
    printf("value = %d\n", n);//不一定能输出100,因为func栈在使用之后会被删除,那么指针p->func栈中n的地址(整个func栈被销毁)无效
    //根据下面第二点，如果没人使用func函数栈这块内存可以访问到n值
    //               但如果有人使用func函数栈这块内存，那么就访问不到n值
    return 0;
}
output:
Process finished with exit code -1073741510 (0xC000013A: interrupted by Ctrl+C)
//报错
```
2. 函数运行结束后会销毁该函数所有的局部数据，这里所谓的销毁并不是将局部数据所占用的内存全部清零,而是==程序放弃对它的使用权限，后面的代码可以使用这块内存==
3. c语言不支持在调用函数时返回局部变量的地址,如果确实有这样的需求，需要定义局部变量为static变量

```
#include <string.h>
#include <stdio.h>
int *func(){
    static int n = 100;    //如果这个局部变量是static性质的，那么n存放数据的空间在静态数据区
    return &n;
}
int main(){
    int *p = func();    //func返回指针
    int n;
    n = *p;
    printf("value = %d\n", n);//输出100
    return 0;
}
output:
value = 100 //解决第一点的问题
```
```
-------------------------------------------------
|    计算机内存                                 |
|                                               |
|    栈区---局部变量                            |
|                                               |
|    堆区---malloc函数动态分配的数据，放在堆    |
|                                               |
|    静态存储区/全局区---全局变量               |
|                     ---静态数据               |
|                                               |
|    代码区---存放代码                          |
-------------------------------------------------
```

####### 编写一个函数，生成10个随机数，并使用表示指针的数组名(即第一个数组元素的地址)来返回他们
```
#include <stdio.h>
#include <stdlib.h>
int *Array(){
    static int arr[10];//存放于静态数据区
    int i = 0;
    for(i=0;i<10;i++){
        arr[i] = rand();
    }
    return arr;
}
int main(){
    int *p = Array();//p 指向Array生成的数组的首地址(即第一个元素的地址)
    int i = 0;
    for (int i = 0; i < 10; ++i) {
        printf("%d\n",p[i]);
        //printf("%d\n",*(p+i));
    }
    printf("array address is %p",p);
    return 0;
}
output:
41
18467
6334
26500
19169
15724
11478
29358
26962
24464
array address is 0000000000407040
``` 
#### 函数指针 (指针函数的指针)
基本介绍
1. 一个函数总是占用一段连续的内存区域，函数名在表达式中有时也会被转换为该函数所在内存区域的首地址，这和数组名非常类似。
2. 把函数的这个首地址（或称入口地址）赋予一个指针变量，使指针变量指向函数所在的内存区域，然后通过指针变量就可以找到并调用该函数。这种指针就是函数指针。


###### 函数指针的定义
简单理解 通过指针指向函数，再通过指针调用函数

```
returnType (*pointerName)(param list);
1) returnType为函数返回值类型
2) pointerName 为指针名称
3) param list为函数参数列表
4)参数列表中可以同时给出参数的类型和名称，也可以只给出参数的类型，省略参数的名称
5)注意( )的优先级高于*，第一个括号不能省略，如果写作returnType *pointerName(param list);就成了函数原型，它表明函数的返回值类型为returnType *(指针类型)
```


```
用函数指针来实现对函数的调用，返回两个整数中的最大值.
#include <stdio.h>

int max(int a, int b);
int main(){
    int x, y, maxVal;

    int (*pmax)(int, int) = max;
    //函数指针:
    //名字 pmax
    //int 表示 该函数指针指向的函数是返回int类型
    //(int, int) 表示 该函数指针指向的函数形参是接受两个int
    //在定义函数指针式，也可以写上形参名。如    int (*pmax)(int a, int b) = max;
    printf("Input two numbers:");
    scanf("%d %d",&x, &y);
    
    maxVal = (*pmax)(x, y);//= maxVal = pmax(x, y);
    //(*pmax)(x, y)通过函数指针调用 函数
    
    printf("Max value: %d\n", maxVal);
    
    printf("function's address is %p",&pmax);
    //函数的地址
    printf("pointer's address is %p",pmax);
    //函数指针的地址
    return 0;
}
int max(int a, int b){
    return a>b ? a : b;
}
output:
Input two numbers:20
30
Max value: 30
function's address is 00000000004015DF
//函数的地址
pointer's address is 000000000061FE08
//函数指针的地址

```


```

-------------------------------------------------
|    计算机内存                                 |
|                                               |
|    栈区---局部变量                            |
|                                               |
|    堆区---malloc函数动态分配的数据，放在堆    |
|                                               |
|    静态存储区/全局区---全局变量               |
|                     ---静态数据               |
|                                               |
|    代码区---存放代码                          |
-------------------------------------------------

代码区:
int max(int a, int b){
    return a>b ? a : b;
}

栈区:
int (*pmax)(int, int) = max;
pmax(指针)->函数(max函数)
```

#### 回调函数(函数指针套娃)--callback
基本介绍
1. 函数指针变量可以作为某个函数的参数来使用的，回调函数就是一个通过函数指针调用的函数。
2. 简单的讲:回调函数是由别人的函数执行时调用你传入的函数(通过函数指针完成)

应用实例
使用回调函数的方式，给一个整型数组int arr[10]赋10个随机数.

```
#include <stdio.h>
#include <stdlib.h>

//回调函数
//int (*f)(void)
//f =  函数指针，它可以接受的函数是：返回int，没有形参
//f 在这里被initarray调用，充当了回调函数的角色
void initArray(int *array, int arraySize, int (*f)(void)) {
    int i;

    for (i = 0; i < arraySize; i++)
        array[i] = f();//通过函数指针调用getNextRandomvalue f() = (*f)()
}
//获取随机值
int getNextRandomvalue(void){
    return rand();//rand 系统函数，返回一个随机整数
    }
int main(){
    int array[10], i; //定义一个int型数组和int
    //调用initArray函数
    //传入一个函数名 getNextRandomvalue(地址)，需要函数指针接受
    initArray(array, 10, getNextRandomvalue);
    //输出复制后的数组
    for (i = 0; i < 10; i++) {
        printf("%d\n", array[i]);
    }
    return 0;
}
output:
41
18467
6334
26500
19169
15724
11478
29358
26962
24464

```

#### 空指针
1. 指针变量存放的是地址，从这个角度看指针的本质就是地址。
2. 变量声明的时候，如果没有确切的地址赋值，为指针变量赋一个NULL值是好的编程习惯
```
int *p = NULL; √
int *p;        ×
```
3. 赋为NULL值的指针被称为空指针NULL指针是一个定义在标准库 <stdio.h>中的
值为零的常量#define NULL 0[案例]
4. 指针使用一览(见后)

## 动态内存分配
c程序中，不同数据在内存中分配说明:
1. 全局变量--内存中的静态存储区
2. 非静态的局部变量--内存中的动态存储区——stack栈
3. 临时使用的数据---建立动态内存分配区域，需要时随时开辟,不需要时及时释放―—heap堆
4. 根据需要向系统申请所需大小的空间，由于未在声明部分定义其为变量或者数组，不能通过变量名或者数组名来引用这些数据，只能通过指针来引用)

```
-------------------------------------------------
|    计算机内存                                 |
|                                               |
|    栈区---局部变量                            |
|                                               |
|    堆区---malloc函数动态分配的数据，放在堆    |
|                                               |
|    静态存储区/全局区---全局变量               |
|                     ---静态数据               |
|                                               |
|    代码区---存放代码                          |
-------------------------------------------------
```

##### 内存动态分配的相关函数

```
1. 头文件#Include <stdlib.h> 声明了四个关于内存动态分配的函数

2. 函数原型void * malloc (usigned int size)     //m emory alloc aiton
                                        malloc =  m + alloc 
                                        
- 作用――在内存的动态存储区(堆区)中分配一个长度为size的连续空间。
- 形参size的类型为无符号整型，函数返回值是所分配区域的第一个字节的地址，即此函数是一个指针型函数，返回的指针指向该分配域的开头位置。
- malloc(100);开辟100字节的临时空间，返回值为其第一个字节的地址

3. 函数原型void *calloc (unsigned n,unsigned size)
- 作用――在内存的动态存储区中分配n个长度为size的连续空间，这个空间一般比较大，足以保存一个数组
- 用calloc函数可以为一维数组开辟动态存储空间，n为数组元素个数，每个元素长度为size.
- 函数返回指向所分配域的起始位置的指针;分配不成功，返回NULL。
- p = calloc(50,4);// 开辟50*4个字节临时空间，把起始地址分配给指针变量p

4. 函数原型: void free (void *p)
- 作用――释放变量p所指向的动态空间，使这部分空间能重新被其他变量使用。
- p是最近一次调用calloc或malloc函数时的函数返回值
- free函数无返回值
- free(p);//释放p所指向的已分配的动态空间

5. 函数原型void *realloc (void *p, unsigned int size)
- 作用――重新分配malloc或calloc函数获得的动态空间大小，将p指向的动态空间大小改变为size(后面直接加空间)，p的值不变，分配失败返回NULL
- realloc(p,50);//将p所指向的已分配的动态空间改为50字节

6. 返回类型说明
C 99标准把以上malloc,calloc,realloc函数的基类型定为void类型,这种指针称为无类型指针(typeiesspointer),即不指向哪一种具体的类型数据,只表示用来指向一个抽象的类型的数据,即仅提供一个纯地址,而不能指向任何具体的对象。

void指针类型(不能用*)
C 99允许使用基类型为void的指针类型。可以定义一个基类型为void的指针变量(即void *型变量),它不指向任何类型的数据。请注意:不要把“指向void类型”理解为能指向“任何的类型”的数据,而应理解为“指向空类型”或“不指向确定的类型”的数据。在将它的值赋给另一指针变量时由系统对它进行类型转换,使之适合于被赋值的变量的类型。例如:

int a = 3;          //定义a为整型变量
int * pl = &a;      //pl指向int型变量
char * p2;          //p2指向char型变量
void * p3;          //p3为无类型指针变量(基类型为void型)
p3=(void * )pl;     //将p1的值转换为void *类型,然后赋值给p3
p2=(char * )p3,     //将p3的值转换为char *类型,然后赋值给p2

printf("%d", * pl); //合法,输出a的值

p3= &a; 
printf("%d", * p3); //错误,p3是无指向的,不能指向a

说明:当把void指针赋值给不同基类型的指针变量(或相反)时,编译系统会自动进行转换,不必用户自己进行强制转换(仅限C99) 。例如:
p3= &a;
相当于“p3=(void * )&a;”,赋值后p3得到a的纯地址,但并不指向a,不能通过*p3输出a的值。

```

###### 实例
动态创建数组，输入5个学生的成绩，另外一个函数检测低于成绩低于60分的，输出不合格的成绩。



```
#include <stdio.h>
#include <stdlib.h>
int main() {
    void check(int *); //函数声明:因为函数在下面
    int *p, i;
    p = (int *) malloc(5 * sizeof(int)); //在堆区开辟20个字节的空间-即5个int
    //C99下等同于p = malloc(5 * sizeof(int));
    for (i = 0; i < 5; i++)
        scanf("%d", p + i);
    check(p);
    free(p);//销毁堆区
    return 0;
}
void check(int *p) {
    int i;
    printf("failing grade:"); //不及格的成绩
    for (i = 0; i < 5; i++) {
        if (p[i] < 60) {
            printf(" %d ", p[i]);
        }
    }
}

栈
check 栈
p----->[0x1122] 本身地址0x1199

mian 栈
p----->[0x1122] 本身地址0x1199
i----->[]

堆
地址:0x1122
20个字节-> 5个int
|----| |----| |----| |----| |----| 
|90  | |80  | | 30 | |20  | |60  | 
|----| |----| |----| |----| |----| 


output:
90
80
30
20
60
failing grade: 30  20
```

###### 动态分配内存注意事项
1. 避免分配大量的小内存块。分配堆上的内存有一些系统开销，所以分配许多小的内存块比分配几个大内存块的系统开销大
2. 仅在需要时分配内存。只要使用完堆上的内存块，就需要及时释放它(谁分配谁释放)，否则可能出现内存泄漏。
3. 总是确保释放以分配的内存。在编写分配内存的代码时，就要确定在代码的什么地方释放内存
4. 在释放内存之前，确保不会无意中覆盖堆上已分配的内存地址，否则程序就出现内存泄漏。在循环中分配内存时，要特别小心

#### 指针一览
变量定义 | 类型表示 | 含义
---|---|---
int i; | int |定义整型变量i
int *P; | int * | 定义p为指向整型数据的指针变量
int a[5]; | int [5] | 定义整型数组a,它有5个元素
int *p[4]; | int * [4] |定义指针数组p,它由4个指向整型数据的指针元素组成
int ( * p)[4]; | int( * )[4] |p为指向包含4个元素的一维数组的指针变量
int f(); | int () | f为返回整型函数值的函数
int * p(); | int *() |p为返回一个指针的函数,该指针指向整型数据
int (* p)(); | int (*)() | p为指向函数的指针,该函数返回一个整型值
int **p;|int **|p是一个指针变量,它指向一个指向整型数据的指针变量
void * p;|void *|p是一个指针变量,基类型为void(空类型),不指向具体的对象



#### 结构体
张老太养了两只猫猫:一只名字叫小白,今年3岁,白色。还有一只叫小花,今年100岁,花色。请编写一个程序，当用户输入小猫的名字时，就显示该猫的名字，年龄，颜色。如果用户输入的小猫名错误，则显示张老太没有这只猫猫。

```
传统方法:不利于数据的管理和维护，猫的三种属性是一个整体，传统方法拆开了这种联系。
//单变量
void main(){
    char cat1Name[10] = "小白"；
    int car1Age = 3;
    char car1Colar[10] = "白色；
    //....
}
//数组
void main(){
    char *catsName[2] = {
        "小白",
        "小花"
    }
    int *catsAge[2] = {
        3,
        100
    }
}
//结构体
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Cat{ //结构体
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
};
int main() {
    //使用结构体创建变量
    struct Cat cat1; // 类型于 struct Cat = int, cat1 = num
    struct Cat cat2;

    //给结构体的各个成员赋值
    cat1.name = "lucy";
    cat1.age = 3;
    cat1.color = "white";

    cat2.name = "lily";
    cat2.age = 100;
    cat2.color = "black";

    //输出两只猫的信息
    printf("the frist cat:name = %s,age = %d, color = %s\n",cat1.name,cat1.age,cat1.color);
    printf("the twice cat:name = %s,age = %d, color = %s\n",cat1.name,cat1.age,cat1.color);

    //输入名字，输出其他信息 含部分错误->已调试完成
    char Name[] = "";
    scanf("%s",Name);
    printf("%s\n",Name);
    //比较字符串是否相等，不能直接使用==
//    if(Name == cat1.name)
//        printf("lucy :name = %s,age = %d, color = %s\n",cat1.name,cat1.age,cat1.color);

    if(strcmp(Name, cat1.name) == 0)
        printf("cat: \nname = %s,age = %d, color = %s\n",cat1.name,cat1.age,cat1.color);
    else if(strcmp(Name, cat2.name) == 0)
        printf("cat: \nname = %s,age = %d, color = %s\n",cat2.name,cat2.age,cat2.color);
    else
        printf("no this cat");
    return 0;
}
```
###### 结构体和结构体变量的区别和联系
通过上面的案例和讲解我们可以看出:
1. 结构体是自定义的数据类型，表示的是一种数据类型.
2. 结构体变量代表一个具体变量，好比

```
int num1 ; //int 是数据类型，而num1 是一个具体的int变量 
struct Cat cat1;//struct Cat 是结构体数据类型，而cat1 是一个struct Cat变量 
```

3. Cat就像一个“模板”，定义出来的结构体变量都含有相同的成员。也可以将结构体比作“图纸”，将结构体变量比作“零件”，根据同一张图纸生产出来的零件的特性都是一样的

###### 结构体内存布局
```
struct Cat cat1;
cat1.name = "lucy";
cat1.age = 3;
cat1.color = "white";

计算机内存
cat1 ----->|-------|
           |char * | name
           |-------|
           |int 3  | age
           |-------| 
           |char * | color
           |-------|

```
###### 声明结构体

```
struct 结构体名称 {
    成员列表;
};
如
struct Cat{ //结构体
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
    //..
    //成员可以是结构体(套娃)
};
1)从叫法上看:有些书上称为成员，有些书说结构体包含的变量
2)成员是结构体的一个组成部分，一般是基本数据类型、也可以是数组、指针、结构体等。比如我们前面定义Cat结构体的int，age就是一个成员。

```

###### 注意事项细节说明
1. 成员声明语法同变量，示例:数据类型 成员名;
2. 字段的类型可以为:基本类型、数组或指针、结构体等
3. 在创建一个结构体变量后，需要给成员赋值，如果没有赋值就使用可能导致程序异常终止。
```
#include <stdio.h>
struct Cat{ //结构体
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
};
int main() {
    struct Cat cat1;
    printf("the frist cat:name = %s,age = %d, color = %s\n",cat1.name,cat1.age,cat1.color);
    return 0;
}

output:
Process finished with exit code -1073741819 (0xC0000005)//异常
```

4. 不同结构体变量的成员是独立，互不影响,一个结构体变量的成员更改，不影响另外一个。//修改cat1中信息不影响cat2信息

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Cat{ //结构体
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
};
int main() {
    struct Cat cat1; // 类型于 struct Cat = int, cat1 = num
    struct Cat cat2;
    
    cat1.name = "lucy";
    cat1.age = 3;
    cat1.color = "white";

    cat2.name = "lily";
    cat2.age = 100;
    cat2.color = "black";
    //修改cat1中信息不影响cat2信息
    return 0;
}
```
###### 创建结构体和结构体变量
1. 方式1-先定义结构体，然后再创建结构体变量

```
struct Cat{ //结构体
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
};
struct Cat cat1, cat2;
//定义了两个变量cat1和cat2，它们都是cat类型，都由3个成员组成
//注意关键字struct不能少
```
2. 方式2-在定义结构体的同时定义结构体变量
```
struct Cat{ //结构体
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
}cat1,cat2;
//在定义结构体Cat的同时,创建了两个结构体变量cat1,cat2
```
3. 方式3-如果只需cat1,cat2两个变量，后面不需要再使用结构体名定义其他变量，在定义时也可以不给出结构体名 = 匿名结构体
```
struct { //没有写Cat
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
}cat1,cat2;
cat1.name = "lucy";
cat1.age = 3;
.....

//该结构体数据类型，没有名。即匿名结构体
//cat1，cat2就是该结构体的两个变量
//但只能使用cat1，cat2这两个变量
```
###### 成员的获取和赋值
结构体和数组类似，也是一组数据的集合，整体使用没有太大的意义。数组使用下标[]获取单个元素，结构体使用点号.获取单个成员。获取结构体成员的一般格式为 
- 结构体变量名.成员名;

```

struct Cat{ 
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
}cat1,cat2;
//分别赋值
cat1.name = "lucy";
cat1.age = 3;
cat1.color = "white";

//统一整体赋值
//1.创建结构体的时候直接赋值
struct Cat{ 
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
}cat1 = {"lucy",3,"black"};
//2.在main函数里创建并赋值
struct Cat{ 
    char * name;  //名字 指针->字符串
    int age;      //年龄
    char * color; //颜色
};
void main(){
    //在定义结构体变量时，需要一一对应。
    struct Cat cat1 = {"lucy",3,"black"};//√
    struct Cat cat2;
    cat2 = {"lucy",3,"black"};//×
    
}
```
###### 实例
步骤
1. 声明(定义)结构体，确定结构体名
2. 编写结构体的成员
3. 编写处理结构体的函数
- 小狗案例:
1. 编写一个Dog结构体，包含name(char[10])、age(int)、weight(double)属性
2. 编写一个information函数，返回字符串，方法返回信息中包含所有成员值。
3. 在main方法中，创建Dog结构体变量，调用information函数，将调用结果打印输出。  


```
#include <stdio.h>
struct Dog{ //结构体
    char * name;//char name[10]
    int age;
    double weight;
};
char * information(struct Dog dog){
    static char info[50];//局部静态变量，如果不使用static，将会在information函数栈销毁时，找不到所对应的变量
    sprintf(info,"name=%s,age=%d,weight=%.2f\n",dog.name,dog.age,dog.weight);
    //sprintf 发送格式化输出到 str 所指向的字符串。
    dog.name = "lucy";  //由于是值传递，不会对主函数中小狗的名字产生影响
    return info;
}
int main() {
    struct Dog dog= {"jack",3,20};            //创建结构体变量
    char * info = NULL;
    info = information(dog);   //结构体默认是值传递
    printf("dog's information = %s",info);
    printf("dog's name = %s",dog.name); //名字依然是jack，不是lucy
    return 0;
}
```
###### 盒子案例
1. 编程创建一个Box结构体，在其中定义三个成员表示一个立方体的长、宽和高，长宽高可以通过控制台输入。
2. 定义一个函数获取立方体的体积(volume)。
3. 创建一个结构体，打印给定尺寸的立方体的体积。


```
#include <stdio.h>
struct Box{ //结构体
    int length;
    int weight;
    int height;
    int volume;
};
void Volume(struct Box box){
    int volume = box.weight*box.length*box.height;
    box.volume = volume;
    printf("this box's volume = %d",box.volume);
}

int main(){
    //struct Box box = {2,3,4};
    struct Box box;
    scanf("%d",&box.length);
    scanf("%d",&box.weight);
    scanf("%d",&box.height);
    Volume(box);
    //printf("this box's volume = %d",box.volume);
    return 0;
}

```
###### 景区门票案例
1. 一个景区根据游人的年龄收取不同价格的门票。
2. 请编写游人结构体(Visitor)，根据年龄段决定能够购买的门票价格并输出
3. 规则:年龄>18,门票为20元，其它情况免费。
4. 可以循环从控制台输入名字和年龄，打印门票收费情况，如果名字输入n ,则退出程序。

```
#include <stdio.h>
#include <string.h>
struct Visitor{ //结构体
    char name [10];
    int age;
    int price;
};

//因为结构体默认是值传递，会拷贝一份完整数据，效率较低因此，
//为了提高效率，我们直接接收地址(指针)
void Price(struct Visitor * visitor){
    // 以下visitor-> = (*visitor)
    if( visitor->age > 18){
        (*visitor).price = 20;
    }
    else{
        (*visitor).price = 0;
    }
    printf("name:%s\n",(*visitor).name);
    printf("Price:%d\n",(*visitor).price);
}

int main(){
    struct Visitor visitor;
    while (1){
        printf("input visitor's name\n");
        //其中name不加&是因为name定义的是一个字符数组，地址传递。
        //其中age加&是因为age定义的是int，值传递。
        scanf("%s",visitor.name);
        if(strcmp("n",visitor.name)==0){
            break;
        };
        printf("input visitor's age\n");
        scanf("%d",&visitor.age);
        printf("this visitor price is\n");
        //取地址是因为Price函数参数是指针
        Price(&visitor);
        return 0;
    }
    printf("quit process");
}
    
output:
input visitor's name
jack
input visitor's age
20
this visitor price is
name:jack
Price:20

input visitor's name
n
quit process
```

#### 共用体
- 现有一张关于学生信息和教师信息的表格。
- 学生信息包括姓名、编号、性别、职业、分数
- 教师信息包括姓名、编号、性别、职业、教学科目

```
传统方式
定义结构体，根据人员的职业，使用对应的成员变量。
struct Person {
char name[20];
int num;
char sex;
char profession;
float score;    //学生使用score
char course[20];//老师使用course
};
传统方式的问题分析:会造成空间的浪费，比如学生只使用score,但是也占用了course成员的20个字节.
解决方案:
1. 做struct Stu和struct Teacher但如果职业很多，就会对应多个结构体类型,不利于管理
2. 使用共用体
```
###### 共用体
1. 共用体(Union)属于构造类型，它可以包含多个类型不同的成员。和结构体非常类似,但是也有不同的地方.
2. 共用体有时也被称为联合或者联合体，定义格式为
```
union 共用体名 {
    成员列表
};
```
3. 结构体和共用体的区别在于:结构体的各个成员会占用不同的内存，互相之间没
有影响;而共用体的所有成员占用同一段内存，修改一个成员会影响其余所有成员

###### 定义共同体类型和共同体变量的三种方式(类似于结构体)

```
1. 先定义共用体，再定义共同体变量
union union1{ //共同体
    int n;
    char ch;
    double f;
};
int main(){
    union union1 a,b,c;
}
2.定义共用体的同时，定义共同体变量
union union1{ //共同体
    int n;
    char ch;
    double f;
}a,b,c;
3.只使用一次共同体 
union { //共同体
    int n;
    char ch;
    double f;
}a,b,c;
```

###### 快速入门

```
#include <stdio.h>
union information{ //共同体:三个成员
    int age;      //4个字节
    char name;    //1个字节
    short salary; //2个字节  7个字节，但是输出字节大小为4，这说明三个成员不是占用不同的空间
                  //实则是共享数据空间，以最大的数据类型为准，如果删除int age。那么占用空间为2个字节
};
int main(){
    union information info;//定义了一个共同体变量 info
    printf("%d,%d\n", sizeof(info), sizeof(union information)); //输出info和information占用空间

    info.age = 0x40;        //16进制 0x40=64
    printf("%d, %c,%d\n", info.age, info.name, info.salary);//输出结果为64, @,64。由于共享空间，可能会导致其他成员的值改变
    //但是在结构体中，如果只赋值一个会报错。

    info.name= '9';
    printf("%d, %c,%d\n", info.age, info.name, info.salary);
    info.salary = 0x2059;
    printf("%d, %c,%d\n", info.age, info.name, info.salary);
    info.age = 0x3E25AD54;
    printf("%d, %c,%d\n", info.age, info.name, info.salary);
    return 0;
}

output:
4,4
64, @,64
57, 9,57
8281, Y,8281
1042656596, T,-21164


内存:
int占四个字节，一个字节占8bit即8位
info(四个字节:因为int是四个字节占用最大)--------> __0000 0000__ __0000 0000__ __0000 0000__ __0100 0000__
int age;      //4个字节 即占用4个格子(从右往左)
char name;    //1个字节 即占用1个格子
short salary; //2个字节 即占用2个格子

当执行info.age = 0x40; 0x40(16进制)即0100 0000(2进制).(其中0x代表找个数是16进制)
输出info.age = 0100 0000转10进制就变成了64.
输出info.name = 0100 0000转ASCII码就变成了@.
输出info.short = 0100 0000转10进制就变成了64.

info(四个字节:因为int是四个字节占用最大)--------> __0000 0000__ __0000 0000__ __0000 0000__ __0011 1001__
当执行info.name= '9'; 字符9对应的十进制为57 即0011 1001
输出info.age = 0011 1001转10进制就变成了57.
输出info.name = 0011 1001转ASCII码就变成了9.
输出info.short = 0011 1001转10进制就变成了57.

info(四个字节:因为int是四个字节占用最大)--------> __0000 0000__ __0000 0000__ __0010 0000__ __0101 1001__
当执行info.salary = 0x2059; 0x2059(16进制)即0010 0000 0101 1001 (2进制).(一位数=4bit即4位)
输出info.age = 0011 1001转10进制就变成了8281.
输出info.name = 0011 1001转ASCII码就变成了Y.
输出info.short = 0011 1001转10进制就变成了8281.

info(四个字节:因为int是四个字节占用最大)--------> __0011 1110__ __0010 0101__ __1010 1101__ __0101 0100__
当执行info.age = 0x3E25AD54;; 0x2059(16进制)即0011 1110 0010 0101 1010 1101 0101 0100(2进制).(一位数=4bit即4位)
输出info.age = 0011 1110 0010 0101 1010 1101 0101 0100转10进制就变成了1042656596.
输出info.name = 0011 1110 0010 0101 1010 1101 0101 0100转ASCII码就变成了T.
输出info.short = --short只占两个字节-- 1010 1101 0101 0100转10进制就变成了44372.
//实际上不是直接去掉前面两位，当两个字节占满后，读取前面的之后会溢出
//short的范围 为-32768~32767
//实际输出为-21164

```

```
#include <stdio.h>
#define Total 2 //人员总数
union Sc {
    float score;
    char course[20];
};
struct Person{
    char name[20];  //姓名
    int num;        //编号
    char sex;       //性别 f->女性,m->男性
    char profession;//职业 s->学生.t->老师
//    union{
//        float score;//得分
//        char course[20]
//    }sc;//sc是一个共同体变量
    union Sc sc;
};
int main(){
    int i;
    struct Person persons[Total];//定义了一个结构体数组
    //输入人员信息
    for(i=0;i<Total;i++){
        printf("input information:name,num,sex,profession(f->female,m->male.s->student.t->teacher):\n");
        //对于数字和字符要用&
        //输出时使用空格
        scanf("%s %d %c %c",persons[i].name,&(persons[i].num),&(persons[i].sex),&(persons[i].profession));
        if(persons[i].profession == 's'){   //如果是学生
            printf("input score\n");
            scanf("%f",&persons[i].sc.score);
        }
        else{
            printf("input course\n");//如果是老师
            scanf("%f",&persons[i].sc.course);
            }
        }
        fflush((stdin));
    //输出人员信息
    printf("name\tnum\tsex\tprofession\tscore/course\n");
    for (int i = 0; i < Total; i++) {
        if(persons[i].profession == 's'){   //如果是学生
            printf("%s\t%d\t%c\t%c\t\t%f\n",persons[i].name,persons[i].num,persons[i].sex,persons[i].profession,persons[i].sc.score);
        }
        else{//如果是老师
            printf("%s\t%d\t%c\t%c\t\t%f\n",persons[i].name,persons[i].num,persons[i].sex,persons[i].profession,persons[i].sc.course);
        }
    }
    return 0;
}

input information:name,num,sex,profession(f->female,m->male.s->student.t->teacher):
jack 10 f s
input score
90
input information:name,num,sex,profession(f->female,m->male.s->student.t->teacher):
lucy 20 f t
input course
chinese
name    num     sex     profession      score/course
jack    10      f       s               90.000000
lucy    20      f       t               0.000000


```
