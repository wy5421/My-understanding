转载自 https://www.soso.com/link?url=DOb0bgH2eKg7Sf-koBXrEidQRoztLvNX_4rlk7sEOObtQ4QSGBFbK32j5SA938kQ2Jl73GcKSto.
一、指针是C语言的灵魂
# include   
  
int main(){  
    int *p;  //p是变量名，int *表示p变量存放的是int类型变量的地址，p是一个指针变量  
    int i = 3;  
      
    //p = i; 这样写是错误的  
    //p = 4; 这样写是错误的  
    p = &i;  //将i变量的地址给p变量  
//p保存了i的地址，因此p指向i,修改p的值不影响i的值，修改i的值也不影响p的值  
      
    return 0;  
}  
# include   
  
int main(){  
    int *p; //不表示定义了一个名字叫做 *p的变量  
//应该这样理解：p是变量名，p变量的数据类型是 int *类型  
//int *类型实际就是存放int变量地址的类型  
  
    int i = 3;  
      
    p = &i;  
      
    printf("*P = %d\n", *p);  
    printf("i = %d\n", i);  
    return 0;  
}  
注释：1.如果p是个指针变量，并且p存放了普通变量i的地址，则p指向了普通变量
      2.*P 完全等同于 普通变量i  (有i出现的地方都可以替换成*p)
指针和指针变量的区别：
1.指针就是地址，地址就是指针，地址就是内存单元的编号，所以指针就是内存单元的编号
2.指针变量存放地址的变量，也就是说指针变量是存放内存单元编号的变量
3.指针和指针变量是两个不同的概念，但是要注意通常我们叙述时会把指针变量简称为指针，实际它们的含义不一样
二、指针的重要性：
1.表示一些复杂的数据结构
2.快速的传递数据
3.使函数返回一个以上的值(函数只能返回一个值)
4.能直接访问硬件
5.能够方便的处理字符串
6.是理解面向对象语言中引用的基础
# include   
  
int f(int a, int b);  
void g(int * p ,int * q);  
  
int main(void){  
      
    int a = 100;  
    int b = 200;  
      
//  a = f(a, b);  
    g(&a, &b);  
    printf("a = %d, b = %d\n", a, b);  
      
    return 0;  
}  
//只能修改一个值  
int f(int a, int b){  
      
    return 1;  
}  
//这样被调函数可以修改主调函数一个以上的值  
void g(int * p ,int * q){  
    *p = 1;  
    *q = 2;  
}  
三、指针的定义
1、地址：内存单元的编号，地址是从零开始的非负整数。
2、范围：
      控制总线
CPU <---->    数据总线  <----->  内存条
      地址总线
控制线控制数据传输的方向 
数据线是传输数据
地址线是确定是控制哪个内存单元

cup<----->  数据总线 <-----> 内存条
一根线控制两个 0和1
两根线控制四个
n根线控制2的n次方个单元(字节)(每个单元是8位)

32位机 2x10^32
1G=2X10^30B(字节)
2x10^32 ~= 2X10^30*4  所以内存最大4G
3、指针：指针就是地址，地址就是指针，指针变量就是存放内存单元编号的变量。
指针本质就是一个操作受限(不能运算，只是编号)的非负整数(地址)
四、指针的分类
1、基本类型的指针
常见错误1：
# include   
  
int main(void){  
    int *p;  //p指向一个垃圾值的地址，也就是一个垃圾地址  
    int i = 5;  
      
    *p = i;  // 就是将i的值给了一个不知道的地址，这样写不对  
    printf("%d\n", *p);  
      
    return 0;  
}  
常见错误2：
# include   
  
int main(void){  
    int i = 5;  
    int *p;  
    int *q;  
      
    p = &i  
    //*q = p;  语法编译出错  
    //*q = *p;  error  q指向一个垃圾地址  
    q = p;  // error 可以读 q里面的垃圾地址，但是不能读*q的值,没有控制权限。  
    printf("%d\n", *q);  
      
    return 0;  
}  
一个经典的指针程序：
# include   
  
void huhuan(int i, int j);  
void zhizhenhuhuan(int * a, int * b);  
void huhuan3(int * a, int * b);  
  
int main(void){  
    int a = 3;  
    int b = 5;  
      
//  huhuan(a, b);  
//  zhizhenhuhuan(&a, &b);  
    huhuan3(&a, &b);  
  
    printf("a = %d,b = %d\n", a, b);  
      
      
    return 0;  
}  
  
void huhuan(int a, int b){  //不能完成互换，a,b是形参，单独分配内存  
    int t;  
      
    t = a;  
    a = b;  
    b = t;  
}  
  
void zhizhenhuhuan(int * a, int * b){ //不能完成互换，互换了指针的指向  
    int * t;  
  
    t = a;  
    a = b;  
    b = t;  
}  
  
void huhuan3(int * a, int * b){  //可以完成互换，传递的是地址，交换的是地址指向的值  
    int t;  
  
    t = *a;  
    *a = *b;  
    *b = t;  
}  
*的含义：
♥乘法   c = a*b;
♥定义指针变量 int * p;
♥取值运算符 *p
2、指针和数组的关系
一维数组名是个指针常量，它存放的是数组第一个元素地址
int a[5];  
int b[5];  
//a = b 是错误的  a,b都是常量  
# include   
  
int main(void){  
    int a[5];  
      
    printf("%#x\n", &a[0]);  
    printf("%#x\n", a);  
  
    return 0;  
}  
输出结果：0x12ff6c
0x12ff6c
如果p是个指针变量，则p[i]永远等价于 *(p+i)
确定一个一维数组需要两个参数:
数组第一个元素的地址
数组的长度
//f函数可以输出任何一个一维数组的内容  
# include   
  
void f(int * pArr, int len){  
    int i;  
    for (i=0; i
        printf("%d  ", *(pArr+i));  
    printf("\n");  
}  
int main(void){  
    int a[5] = {1, 2, 3, 4, 5};  
    int b[6] = {-1, -2, -3, 4, 5, -6};  
    int c[100] = {1, 99, 22, 33};  
      
    f(a, 5); //确定一个数组：数组首地址和长度  
    f(b, 6);  
    f(c, 100);  
      
    return 0;  
}  
# include   
  
void f(int * pArr, int len){  
    pArr[3] = 88;  //pArr[3]等价于a[3]也等价于*(a+3)和*(pArr+3)   
                   // *a==a[0]  
}  
  
int main(void){  
    int a[6] = {1, 2, 3, 4, 5, 6};  
      
    printf("%d\n", a[3]);  
    f(a, 6);  // a和pArr都指向数组的第一个元素  
    printf("%d\n", *(a+3));  
      
    return 0;  
}  
五、指针变量的运算
指针变量不能相加，不能相乘，也不能相除(这些运算没有意义)
如果两个指针变量指向的是同一块连续空间中得不同的存储单元，则这两个指针才可以相减(这样减才有意义)
萝卜家园win7系统下载http://blog.china.com/u/140307/737330/
 
# include   
  
int main(void){  
    int i = 5;  
    int j = 10;  
    int * p = &i;  
    int * q = &j;  
    //此时p和q不能相减  
    int a[5];  
    p = &a[2];  
    q = &a[4];  
  
    printf("相减的结果为:%d\n", p-q);  
    //此时p和q可以相减，相减的值指p和q单元相隔的个数  
  
    return 0;  
}  
结果为：相减的结果为:-2
 
六、指针变量长度
预备知识：
sizeof(数据类型)；或者 sizeof(变量名);返回该数据类型所占的字节数
例如： sizeof(int) = 4 sizeof(char) = 1
# include   
  
int main(void){  
    char ch = 'A';  
    int i = 90;  
    double x = 66.6;  
    char * p = &ch;  
    int *q = &i;  
    double *r = &x;  
      
    printf("%d  %d  %d\n", sizeof(p), sizeof(q), sizeof(r));  
}  
输出的结果：4  4  4
七、多级指针
# include   
  
int main(void){  
    int i = 10;  
    int * p = &i;  
    int ** q = &p;  
    int *** r = &q;  
      
    printf("i = %d\n", ***r);  
  
    return 0;  
}  
结果： i = 10
