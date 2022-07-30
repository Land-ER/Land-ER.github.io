## 题意简述
- 给定 $n$ 个十进制整数 $a_1,a_2,...,a_n$，若其转化为十六进制并加上前缀 `0x` 后长度小于或等于原长度，则输出十六进制表示，否则输出十进制表示。
- 保证 $0\leqslant n \leqslant 10^3$，$0\leqslant a_i \leqslant 2^{64}$。

## 解题思路
考虑暴力转换进制后直接比较长度。

但是，手写十进制转十六进制比较麻烦，怎么办？

下面介绍一种简单的、易于使用的 ~~、不会被CCF禁赛的~~方法。

### scanf,printf,sscanf 和 sprintf
首先我们介绍 `scanf` 和 `printf`。这两个是C语言中的函数，用于从标准输入输出中读取或输出数据。首先我们来看这样的一段代码。
```cpp
#include<cstdio>
int main(void){
    int a,b;
    scanf("%d%d",&a,&b);
    printf("%d",a+b);
    return 0;
}
```
这是 A+B Problem 的代码。当你在一开始使用这两个函数时，你有没有思考过，`%d` 是什么意思？

你会得到这样的回答：`%d`代表整数 （更准确的说是 32 位有符号整形）。而且，你还会知道，你可以用 `%lld` 读取 64 位有符号整形，用 `%c` 读取单个字符，用 `%s` 读取字符串。那还有其它的吗？

答案是肯定的。下面给出 C++ Reference 上的一张表格。

| specifier | Output | Example |
| :----: | :----: | :----: |
| `d` or `i` | Signed decimal integer | 392 |
| `u` | Unsigned decimal integer | 7235 |
| `o` | Unsigned octal | 610 |
| `x` | Unsigned hexadecimal integer | 7fa |
| `X` | Unsigned hexadecimal integer (uppercase) | 7FA |
| `f` | Decimal floating point, lowercase | 392.65 |
| `F` | Decimal floating point, uppercase | 392.65 |
| `e` | Scientific notation (mantissa/exponent), lowercase | 3.9265e+2 |
| `E` | Scientific notation (mantissa/exponent), uppercase | 3.9265E+2 |
| `g` | Use the shortest representation: %e or %f | 392.65 |
| `G` | Use the shortest representation: %E or %F | 392.65 |
| `a` | Hexadecimal floating point, lowercase | -0xc.90fep-2 |
| `A` | Hexadecimal floating point, uppercase | -0XC.90FEP-2 |
| `c` | Character | a |
| `s` | String of characters | sample |
| `p` | Pointer address | b8000000 |
| `n` | Nothing printed.The corresponding argument must be a pointer to a signed int.The number of characters written so far is stored in the pointed location. |  |
| `%` | A % followed by another % character will write a single % to the stream. | % |

而这些符号可以组合起来：

|  | `d` `i` | `u` `o` `x` `X` | `f` `F` `e` `E` `g` `G` `a` `A` | `c` | `s` | `p` | `n` |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| (none) | int | unsigned int | double | int | char* | void* | int* |
| `hh` | signed char | unsigned char |  |  |  |  | signed char* |
| `h` | short int | unsigned short int |  |  |  |  | short int* |
| `l` | long int | unsigned long int |  | wint_t | wchar_t* |  | long int* |
| `ll` | long long int | unsigned long long int |  |  |  |  | long long int* |
| `j` | intmax_t | uintmax_t |  |  |  |  | intmax_t* |
| `z` | size_t | size_t |  |  |  |  | size_t* |
| `t` | ptrdiff_t | ptrdiff_t |  |  |  |  | ptrdiff_t* |
| `L` |  |  | long double |  |  |  |  |

其中有一项 `%X` 可以完成题目中要求的转换。

一个简单的程序，输入一个十进制数，输出其十六进制形式：

```cpp
#include<cstdio>
int main(void){
    int n;
    scanf("%d",&n);
    printf("%X",n);
}
```

关于 `sscanf` 和 `sprintf`，它们的功能和上面两个很相似。

```cpp
int printf ( const char * format, ... );
int scanf ( const char * format, ... );
int sprintf ( char * str, const char * format, ... );
int sscanf ( const char * s, const char * format, ...);
```

可以看到后两项多了一个参数 `char * str`（`const char * s`），它是干什么的呢？

其实是十分简单的：它们不再从标准输入输出中读取或向其输出，而是对给定的 `char*` 操作。比如以下的这个程序：

```cpp
#include<cstdio>
int main(void){
    int n;
    char str[20];
    scanf("%d",&n);//假如这里输入的数字为 81522
    sprintf(str,"%X",n);//此时str的内容为 13E72
    return 0;
}
```

那么，这道题目应该也很好解决了。

## 代码实现
注意事项：
- 注意到 $0\leqslant a_i \leqslant 2^{64}$，需要使用 `unsigned long long`。
- `unsigned long long` 的读入可以使用 `llu` 和 `llX`。
- 代码很丑，轻喷。

```cpp
#include<bits/stdc++.h>
char s[5000000];
int tot = 0;
int main(void){
    char a[25],b[25];
    unsigned long long int n;
    char c;
    scanf("%s",s);
    s[strlen(s)-1] = '\0';
    while(true){
        c = s[tot++];
        if(c == '\0')
            break;
        else if(c == '{')
        	printf("{");
        else
            printf(",");
        if(s[tot] == '\0')
            break;
        sscanf(s+tot,"%llu",&n);
        sprintf(a,"%llu",n);
        tot += strlen(a);
        sprintf(b,"%llX",n);
        if(strlen(a) < strlen(b)+2)
            printf("%s",a);
        else
            printf("0x%s",b);
    }
    printf("}");
    return 0;
}
```