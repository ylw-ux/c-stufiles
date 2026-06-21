这个基本的扫描输入，然后到输出开始

| 方法/数据类型 | char | int | float | double                                    | long                | string（char[]） | *p（指针） |
| ------- | ---- | --- | ----- | ----------------------------------------- | ------------------- | -------------- | ------ |
| scanf   | %c   | %d  | %f    | ==%lf==                                   | %ld                 | %s             | %p     |
| printf  | %c   | %d  | %f    | %f                                        | %ld                 | %s             | %p     |
|         |      |     |       | ![[Pasted image 20260601223952.png\|191]] | **long long要使用lld** |                |        |


# ⚠️ 重点说明

1. **`scanf` 与 `printf` 对 `double` 的区别**
   - `scanf("%lf", &d)` — 读取 double 必须用 `==%lf==`（`%f` 是给 float 的）
   - `printf("%f", d)` — 输出 double 用 `%f`（或 `%lf`，C99 起两者等效）
   - 原因：`scanf` 需要确切知道变量占用多少字节（float 4 字节，double 8 字节），而 `printf` 中 float 会被自动提升为 double 再传递，所以 `%f` 就够了

2. **`scanf` 必须加 `&` 取地址符**
   ```c
   int n;
   scanf("%d", &n);   // ✅ 正确——传入变量地址
   scanf("%d", n);    // ❌ 错误——n 未初始化，当地址用会崩溃
   ```
   指针变量本身已经是地址，所以不需要 `&`：
   ```c
   char s[100];
   scanf("%c", &s[50]);
   scanf("%s", s);    // ✅ s 是数组名，本身就是首地址
   int *p = &n;
   scanf("%d", p);    // ✅ p 已经是指针=地址
   ```

3. **C 没有内置 `string` 类型**
   - C 中用 `char[]`（字符数组）或 `char*` 来表示字符串
   - `scanf("%s", buf)` 读到空格/换行就停，很危险——超过缓冲区会越界
   - 更安全：`scanf("%99s", buf)` 限制最大读入长度

4. **`%p` 输出指针地址**
   - `printf("%p", (void*)ptr)` — 以十六进制打印指针的值（即地址）
   - 建议先强转为 `(void*)`，否则不同类型指针可能警告

5. **其他常用格式占位符**

   | 占位符 | 含义 |
   | ------ | ---- |
   | `%u`   | 无符号十进制整数（unsigned int） |
   | `%x` / `%X` | 十六进制（小写/大写） |
   | `%o`   | 八进制 |
   | `%e` / `%E` | 科学计数法浮点数 |
   | `%g`   | 自动选 `%f` 或 `%e`，去掉末尾多余的零 |
   | `%%`   | 输出一个百分号 `%` 本身 |
   | `%lld` | `long long` 的读写（scanf/printf 都用） |
   | `%zu`  | `size_t` 类型（如 `sizeof` 返回值） |

```C
if(){

}else if(){

}else{

}

int t;
scanf("%d",&t);
switch ( t){
case 1:
	printf("1");
	break;
case 2:
	printf("2");
	break;
}
default:
	printf("hello world");
```
在 C 语言中，default 是一个关键字，主要用于 switch 语句中作为默认分支。当 switch 语句中的表达式值与所有 case 标签都不匹配时，程序会执行 default 分支的代码块，确保即使没有匹配的 case，程序也能执行预设的逻辑，避免意外错误或遗漏处理。
语法结构：switch (表达式) {
case 值1:
    // 代码块1
    break;
case 值2:
    // 代码块2
    break;
default:
    // 默认代码块（当没有case匹配时执行）
    break;
}


default 分支是可选的，但通常放在 switch 块的末尾，尽管位置灵活。
default 代码块可以不包含 break 语句，因为它通常是最后一个分支，但添加 break 有助于代码可读性和防止意外错误。

示例代码：
```C

#include <stdio.h>

int main() {
    int num = 3;
    switch (num) {
    case 1:
        printf("数字是1\n");
        break;
    case 2:
        printf("数字是2\n");
        break;
    default:
        printf("数字不是1或2\n"); // 当num为3时执行此分支
        break;
    }
    return 0;
}
```
运行此代码，输出将为 "数字不是 1 或 2"，因为 num 的值（3）不匹配任何 case 标签。
作用：

提供一个兜底选项，常用于处理无效输入或未覆盖的边缘情况。
增强程序的鲁棒性，防止因遗漏某些情况而导致的错误或异常终止。
即使当前设计已经涵盖了所有预期的可能性，在未来需求变更的情况下，default 也能及时捕获新状况并采取适当措施。

注意事项：

default 不是函数，而是语法结构的一部分。
虽然理论上可以省略 default 分支，但从软件工程的角度来看，建议使用它以遵循防御式编程的原则。


有一个错误的示例，switch, 它的那个控制的变量只能是一个整数
```C
#include<stdio.h>

char r( n );
void main(){
	int t;
	scanf("%d",&t);
	switch(r(t)){
		case Z:
			printf("1");
		case z:
			printf("2");
	}	
} ;
char r (int n ){
	char bb = ('Z' - n);
	return bb;
}
```

for循环
```C
char *str= (char*)malloc(sizeof(char)(10))
for(;;){}  表示无限循环
for(int i =0;i<strlen(str);i++){}字符串长度函数编辑字符串
```
while循环：
```C
while(1){}原生C无限

#include<stdbool.h>
while(true){}用true表示无限循环，需要导入库函数
```
braek与return:
多重嵌套循环中，break只结束当前的这一个嵌套,
而return则直接结束整个循环或者嵌套。如果return在最外面的main函数里面，则会直接整结束整个程序。

/ 整除 10/3= 3.333333 ---->10/3 = 3 省略小数部分

复合运算赋值：
sum += 10；----->sum=sum+10;
减 - 乘 * 除 / 同理 

# 数组

## 数组的定义: int list[100];
## 数组的初始化:一般是采用循环赋值
```C
int list[10];
int a;
//初始化
for(i=0;i<10;i++){
	list[i] = 0; 
}
//循环赋值
for(i=0;i<10;i++){
	scanf("%d",&a)
	list[i] = a; 
}
//数组遍历输出
for(i=0;i<10;i++){
	printf("%d",list[i]);
}
```
总结：我们在定义一个数组时，有哪几种做法
```C
int list[];
int list[10];
int a[3] = {1,2,3};
int a[ ] = {1,2,3,41,2,412,4,1,434,,1,41,4,32,1,3} //自动帮我们填入这个数组的大小
int a[12] = {1,2} //假如没有对这个数组进行初始化的话，那么除了我们给出的这两位，剩下的都是0
```
==C数组没有length方法,计算数组的长度可以用 sizeof(list)/sizeof(list[ 0 ]) 来计算 ==
![[Pasted image 20260601232020.png|364]]

---

## 二维数组

**1. 定义**
```c
int matrix[3][4];  // 3行4列的二维数组，类型为 int

// 类比：matrix 是一个有 3 个元素的数组，
//       每个元素又是一个有 4 个 int 的数组
```

**2. 初始化**
```c
// ① 完整初始化——按行写清楚
int a[2][3] = {{1, 2, 3}, {4, 5, 6}};

// ② 省略内层花括号——编译器按行依次填
int a[2][3] = {1, 2, 3, 4, 5, 6};  // 等价于上面

// ③ 第一维可以省略——编译器根据初始化数据推断
int a[][3] = {{1, 2, 3}, {4, 5, 6}};  // 自动推出 a[2][3]
int a[][3] = {1, 2, 3, 4, 5, 6};      // 同样可以

// ④ 部分初始化——未给的元素自动置 0
int a[3][4] = {{1}, {2}, {3}};
// 结果：第0行 {1,0,0,0}，第1行 {2,0,0,0}，第2行 {3,0,0,0}

// ⑤ 全部置 0
int a[3][4] = {0};  // 所有元素都是 0
```

**3. 内存布局：行优先（Row-Major）**
```c
int a[2][3] = {{1,2,3}, {4,5,6}};

// 内存中的实际排列（连续存放）：
// 地址低 → 高
// | 1 | 2 | 3 | 4 | 5 | 6 |
//   ← 第0行 →  ← 第1行 →

// 所以 a[i][j] 在内存中的位置：
// 地址 = 首地址 + (i × 列数 + j) × sizeof(int)
```

> **一维 vs 二维的访问本质**：`a[i][j]` 等价于 `*(*(a + i) + j)`。`a` 是一个「指向数组的指针」——`a + i` 跳过一整行。

**4. 遍历**
```c
int a[3][4];

// 双层循环遍历——外层管行，内层管列
for (int i = 0; i < 3; i++) {          // 行
    for (int j = 0; j < 4; j++) {      // 列
        scanf("%d", &a[i][j]);          // 读入
    }
}

// 输出时换行——看起来像矩阵
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 4; j++) {
        printf("%4d", a[i][j]);         // %4d 对齐输出
    }
    printf("\n");                       // 每行结束换行
}
```

**5. 二维数组做函数参数——第二维必须写死**

```c
// ✅ 正确——第二维大小必须指定
void printMatrix(int a[][4], int rows) { // 列数 4 必须写
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < 4; j++) {
            printf("%4d", a[i][j]);
        }
        printf("\n");
    }
}

// ✅ 也可以用指针形式（两者等价）
void printMatrix(int (*a)[4], int rows) { ... }

// ❌ 错误——编译器不知道一行多大，无法定位 a[i][j]
void printMatrix(int a[][], int rows, int cols) { ... }  // 不能省略第二维！
void printMatrix(int **a, int rows, int cols) { ... }    // 二级指针≠二维数组！
```

> **为什么第二维必须写死？** 编译器计算 `a[i][j]` 时需要知道一行有多少个元素：`地址偏移 = i × 列数 + j`。列数未知就无法定位。

**6. 变长数组（VLA，C99 起）**
```c
// 如果行列在运行时才确定，可以用 VLA（Variable-Length Array）
int rows, cols;
scanf("%d %d", &rows, &cols);
int a[rows][cols];  // 运行时决定大小（栈上分配，大数组小心爆栈）
```


## malloc请求一块空间

### **2维正常写可能不会，但是用malloc写会范致命逻辑漏洞：只分配了外层「行指针」，没分配内层「列数据空间」**
 比如下面的`arr2[0] ~ arr2[9]` 全是野指针，直接写 `arr2[i][j]` 会内存越界、程序直接崩溃。
```C
#include<stdlib.h>
#include<stdio.h>

int main(){
	//请一块能存10个数的int 数组
	int * arr = (int*)malloc(sizeof(int)*10);
	//数组定义一个字符串
	char * arrstr = (char*)malloc(sizeof(char)*3);
	arrstr[0] = 'h';
	arrstr[1] = 'i';
	arrstr[2] = 0;
	
	
	//二维数组
	int ** arr2 = (int**)malloc(sizeof(int*)*10);
	//int**,一个指向一个指向int型的一块内存地址的指针，也就是指向一个指针的指针
	//还没有给每一行初始化
	// 假设每行存 5 个 int
	for(int i =0;i<10<i++){
		arr2[i] = (int*)malloc(sizeof(int)*5);
	}
	//2维字符串数组  长度为10的数组，数组的每一个位置存一个字符串
	char ** chararr =(char**)malloc(sizeof(char*)*10);
	
	//初始化
	for(int i=0;i<10;i++){
		chararr[i] = malloc(sizeof(char)*10);
		//scanf("%s",chararr[i]);
		//安全写法：
		scanf("%9s", chararr[i]);//限制最大输入长度。
	}
	
```
	
### 别忘了free和NULL
```C
	
	free(arr);
	free(arrstr);
	
	//!!!free(arr2);
	//!!!free(chararr);
	//但是二维的或者更高维的malo释放就不能这样单纯的释放，
	//因为这只是把最外层的那10个malloc指针给释放掉了，
	//但是这10个指针又都各自指向了一块你malloc的区域，所以这10个区也都要free
	
	//完整的写法
	1.先释放内层的
	for(int i =0;i<10;i++){
		free(arr2[i]);
	}
	2.释放外层的
	free(arr2);
	3.arr2 = NULL;
	//第三步是保护性写法
	return 0;
}

```
## 字符串数组
给你一个整数 `n` ，返回一个字符串数组 `answer`（**下标从 1 开始**），其中：
- `answer[i] == "FizzBuzz"` 如果 `i` 同时是 `3` 和 `5` 的倍数。
- `answer[i] == "Fizz"` 如果 `i` 是 `3` 的倍数。
- `answer[i] == "Buzz"` 如果 `i` 是 `5` 的倍数。
- `answer[i] == i` （以字符串形式）如果上述条件全不满足。

**示例 1：**
**输入：** n = 3
**输出：** ["1","2","Fizz"]
**示例 2：**
**输入** n   = 5
**输出:** ["1","2","Fizz","4","Buzz"]
**示例 3：**
**输入:** n = 15
**输出：**["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]


## [[#1. 结构体数组（Array of Structures, AoS）—— 传统 C 语言思维|结构体数组]]


# 函数：

![[Pasted image 20260601225906.png|507]]
函数的这个声明很容易忽略的一点是，这个要写参数，而且参数的类型和名称都要写，然后要标明这个函数返回值的类型

## 第一节---如何通过一个函数来操控更改函数外面的实参

典型的一个例子就是通过一个函数来交换两个数的值；
通过往函数传那个实参的指针，然后在函数内部通过指针的解引用去操纵实际的值，虽然传进来的指针地址在函数类里是用一个形参来表示的，但是它的地址值与真实的那个地址值所指向的都是同一个东西，可以通过这个来更改。

```C
```C
#include <stdio.h>
// 形参是指针，接收变量的地址
void swap(int *x, int *y)
{
    int t = *x;  // *解引用：通过地址找到原变量
    *x = *y;
    *y = t;
}

int main()
{
    int a = 1, b = 2;
    swap(&a, &b); // 传 a、b 的地址
    printf("%d %d", a, b); // 输出 2 1，交换成功
    return 0;
}
```


## ！指针与高维数组---数组名地址退化



### 1. 什么是「数组名地址退化」？

定义：
在 **函数传参、数组名赋值给指针、数组名做加减运算** 时，
**数组名 不再代表「整个数组」，自动退化为 指向数组首元素的常量指针**。

**简单理解**：
`int arr[5] = {1,2,3,4,5};`
正常：`arr` 代表整个数组；
传参时：`arr` → 等价于 `&arr[0]`（首元素地址）。

`int arr[3][5];`
正常语境下：`arr` 代表**整个二维数组**（本质是一个包含 3 个元素的数组，每个元素又是一个包含 5 个 int 的一维数组）；其中 `arr[0]`、`arr[1]`、`arr[2]` 才分别代表每一行的一维数组。

传参时：`arr` → 等价于 `&arr[0]`（首行的地址，也就是第一个一维数组的地址），会退化为指向「长度为 5 的 int 数组」的指针，类型为 `int(*)[5]`（数组指针）。

**硬件理解**
`int arr[3][5];` 在内存里是==**一整块连续的纯数据空间**==，里面没有任何指针变量。

它的真实定义是：一个长度为 3 的数组，数组的**每个元素本身就是一个长度为 5 的 int 一维数组**。
- `arr[0]` 不是指针，它就是第一行那个长度为 5 的一维数组本身；
- 只是在表达式、传参场景下，`arr[0]` 才会像普通一维数组名一样，退化成指向首元素的指针 `&arr[0][0]`。

打个比方：

- 一维数组：一排 5 个盒子
- 二维数组：3 排盒子，每排 5 个，整整齐齐连在一起，没有额外的 “指向每排的指针”
- 指针数组：先放 3 个箭头，每个箭头各自指向一排盒子，这几排盒子可以不连在一起



二维数组传参：合法写法
```C
// 写法1：形似二维数组（推荐，矩阵题首选）
void printMatrix(int a[][4], int row);

// 写法2：指针形式（揭露本质：指向 含4个int 的一维数组）
void printMatrix(int (*a)[4], int row);

// 写法3：行列都写死（灵活性差，不推荐）
void printMatrix(int a[3][4]);
```

![[Pasted image 20260616225051.png]]

==指针在传参的时候会退化，或者说它的维度会变成更内部的一层==
```C

printarr(int**arr);

int main(){
	int arr2[10][5];
	int ** arr2 = (int**)malloc(sizeof(int*)*10);
	for(int i =0;i<10;i++){
		arr2[i] = (int*)malloc(sizeof(int)*5);
	}
}

inputarr(int**arr 或者 int arr[][5] 或者 int (*arr) [5]){
	for(int i =0;i<10;i++){
		for(int j=0;j<5;j++){
			scanf("%d", &arr[i][j]);或者
			scanf("%d", *(arr+i)+j  );
		}	
	}
}
printarr( I: int arr[][5] 或者 II: int**arr 或者 III: int (*arr) [5])
{	for(int i =0;i<10;i++){
		for(int j=0;j<5;j++){
			printf("%d", arr[i][j]); I 或者
			printf("%d", *(*(arr+i)+j)  ); II III 
		}	
	}
}
```
`  int (*arr) [5]  和 *(*(arr+i)+j)`
- arr是一个指向存了五个整数的数组的地址指针，`int (*arr) [5] = &arr2`
- arr+1 : 指向下存了五个整数的数组的的地址，
- `*(arr+1)` : 对地址解引用，变为一个存了五个整数的数组
- 解引用得到的是**第 1 行的一维数组本身**；这个数组名参与后续运算时，会自动退化为指向该行首元素的`int*`指针，所以才能继续做`+j`的元素级偏移。
- `*(arr+i)+j` : 一个存了五个整数的数组的下一（j）个元素的地址
- `*(*(arr+i)+j)` : 一个存了五个整数的数组的下一（j）个元素的值
 
[[#指针退化的本质，在表达式中| 理解本质]]





# 结构
### 1. 结构体数组（Array of Structures, AoS）—— 传统 C 语言思维

```
struct Patient {
    char name[20];
    int age;
    bool has_tumor;
    float ct_mean_val;
};
struct Patient database[10000]; // 连续内存中，结构体一个接一个存放
```

在物理内存中，`database` 是这样布局的： `[Name0, Age0, Tumor0, CT0][Name1, Age1, Tumor1, CT1]...`


# 指针
[[#函数：|指针和函数]]
[[#数组|还有数组相结合，就会形成一个巧妙的点]]
[[#！指针与高维数组---数组名地址退化]]
## NULL与 '\0'
在创建一个新指针时通常把他赋值为 NULL防止野指针
,NULL(0)在内存里为禁区，也防止调用，会直接编译错误
`int *p = NULL;`

==区分==
`NULL` 是空指针宏（本质是 `(void*)0`），用来判断**指针地址是否为空**；而 `'\0'` 是字符常量（值为 0），用来判断**字符内容是否为结束符**。二者数值上都是 0，但类型、用途完全不同。

你在循环里写 `p[i] != NULL`，编译器会把 NULL 隐式转成数值 0，最终效果和 `p[i] != '\0'` 完全一样，还是遇到第一个 0 就停，**根本解决不了中间有 0 的问题**，还会造成严重的概念混淆。

判断字符结尾永远用 `'\0'`，判断指针是否为空才用 `NULL`，绝对不要混用。



# 指针退化的本质，在表达式中

## 初始化
`int a = 1;`
第一天就会写的代码，到底有没有理解它的本质？
这是一个初始化表达式，左边是变量定义的语法，右边是初始化的值。
这里的等号并不充当使它成为一个表达式的作用，这只是一个变量的定义。同时它不是表达式，它也不会有返回值。
## 表达式
再写下`a = 100;`
就是一个表达式，它在编译时会发生两个事情。
第一：使a被赋值为100，
第二：有一个返回值，等于赋值完成后左操作数（也就是 `a`）的值，即 100。
所以
```C
int a=1;
a=100;
if(a=0){
	printf("hello");
}
int b = 99;
while(a = b = 1){
	printf("hello");
}
```
if的语句会不会执行？答案是不会
等于0是一个表达式，它的返回值是0
相当于if( 0 )
while?
会相当于while( 1 )
从右往左读，先发生了 b = 1,它的返回值为1
然后发生了a = (b = 1的返回值) 。最终得到a = 1;
即为1

同样的表示还有比如函数 逻辑运算符 ，我们有一个函数int nember（），它的return值是1，那
```C
int a = 1;
while( a = number()) --> while( 1 )
while( a != number())--> while( 0 )
a和函数的返回值都是1，它们不等于吗？他们不是，所以这个表达式返回0
```

这样子就可以很顺理其然地推断出数组名在表达式中的时候，它会退化吧
eg：
 ```C
 int array1[3] = {1,2,3};
 这里array1表示为 一个 int[3];
 
 int array2[3] = {1.2.3};  对
 int array2[3] = array1; 不对
 这里array表示为 &array1[0];
 ```
## 统一规则（一 / 二维通用）

1. **定义 / 声明语境下**：数组名就是数组本身，类型是完整的数组类型
    
    - 一维 `int arr[3];` → arr 类型是 `int[3]`，表示整个长度为 3 的 int 数组
    - 二维 `int arr[3][4];` → arr 类型是 `int[3][4]`，表示整个 3 行 4 列的二维数组
    
2. **绝大多数表达式语境下**：数组名会发生「数组 → 指向首元素的指针」的隐式转换（退化），且**只退一层**
3. **三个例外不退化**：`sizeof(数组名)`、`&数组名`、字符串字面量初始化字符数组

这是最容易搞错的核心点，也是和一维的唯一区别：

- 一维数组的首元素是 `int` 类型的单个变量 → 退化后是 `int*`（指向 int 的指针）
- 二维数组的首元素是 `int[4]` 类型的**一整行一维数组** → 退化后是 `int (*)[4]`（指向长度为 4 的 int 数组的指针，简称「数组指针」）
- 一个简单的程序便于理解
```C
#include<stdio.h>
void pr (int *p);
int main (){
	int num[3] = {1,22,333}; 
	pr(num);
	return 0;
}

void pr (int *p){
	int i;
	for(i = 0;i<3;i++){
		printf("%d\n",*(p+i));
	}
}
```
# 数组查找算法

## 顺序查找（无序数组通用）
```C
# include<stdio.h>

int check(int arr[10],int size,int key);

int main ( ){
	int size =10;
	int number[10]= {3,4,1,2,1,33,5,677,8,9};
	int key = 2;
	int rul = check(number,size,key);
	if(number[rul] == key)
		printf("%d",rul);
	else
		printf("worse");
	return 0;
}


int check(int arr[10],int size,int key){
	int i ;
	arr[0] = key;
	for(i = size-1;arr[i] != key;i--);
	return i;

} 
```

## 二分查找必须是有序数组
```C
# include<stdio.h>

typedef struct arr{
	int arrey [10];
	int length ;
} A;
typedef A* Arr;
int check(Arr p,int key);

int main(){
	A array = { {1,2,3,4,5,6,7,8,9,10}, 10 };
	int rul = check(&array,8);
	printf("%d",rul);
	return 0;
}
  
int check(Arr p,int key){
	int l,r,Notfound;
	Notfound = -1;
	l=0;
	r=p->length;
	int n;
	int nn;
	while(l<=r){
		//C语言里的数据初始化之后，不会随着后面的改变而改变
		//C 语言里变量没有 “联动” 效果。你改了下标n，必须手动重新写一句 nn = p->arrey[n];，nn的值才会更新。 
		n= (l+r)/2;
		nn = p->arrey[n];
		if(key == nn ){
			return n;
		}
		if(key<nn){
			r= n-1;
		}
		if(key >nn){
			l= n+1;
		}
	}
	return Notfound;
}
```


# 基础排序

```C
# include<stdio.h>


int main(){
	int size =10;
	int number[10]= {0,199,0,3,4,1,2,1,199,-1};


//冒泡排序
//	for(int i=0;i<size-1;i++ ){
//		for(int j = 0;j<size-1-i;j++){
//			if(number[j]>number[j+1]){
//				int temp;
//				temp = number[j+1];
//				number[j+1] = number[j];
//				number[j] = temp;
//			}
//		}
//	}

//选择排序
//	for(int i=0;i<size-1;i++){
//		for(int j=i+1;j<size;j++){
//			if(number[j] < number[i]){
//				int temp;
//				temp = number[j];
//				number[j] = number[i];
//				number[i] = temp;
//			}
//		}
//	} 


//插入排序
//	for(int i = 1;i<size;i++){
//		int j =i-1;
//		int key = number[i];
//		while( j>=0 && number[j]>key){
//			number[j+1] = number[j];
//			j--;
//		}
//	 	number[j+1]  =key;
//	} 

	for(int k = 0;k<size;k++){
		printf("%d\n",number[k]);
	}
	return 0;
}
```