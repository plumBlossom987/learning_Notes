1.概述
浮点数运算（Floating-point arithmetic）是计算机用来表示和计算实数的一套近似机制与规则。它用有限的比特去表示非常大或非常小的数，并支持加减乘除等运算，但会引入舍入误差和一些非直观现象。  

2.Number Representation    
A real number $x$ can be represented as   
$x=\pm[ d_{0}+{\frac{d_{1}} {\beta}}+{\frac{d_{2}} {\beta^{2}}}+\cdot+{\frac{d_{p-1}} {\beta^{p-1}}} ] \beta^{E}$  
$x=sign*mantissa*\beta^{E}$
where:   
 $\beta$ is the base/radix 基数   
  $\beta$ =2（二进制）, $\beta$ =10（十进制）, $\beta$ =16（十六进制） 
$p$ is the precision 精度  
   指尾数中有效位的个数，即 $d_0$, $d_1$, …, $d_{p-1}$ 共$p$ 位。$p$ 越大，可区分的数越密，舍入误差越小  
$E$ is the **exponent** and $L \leq E \leq U$ is the **exponent range** 指数(及其范围)
  L、U 为指数下界与上界，决定可表示数的量级范围（最小、最大规模）。指数范围越宽，动态范围越大。  
$d_o.d_1...d_{p-1}$ is the **mantissa** and $0\leq d_{i} \leq\beta-1, i=0,..., p-1$ 尾数(及其范围)  
 尾数每位是基数 β 下的一位数字。例如 $\beta$=10 时 $d_i\in \{0,…,9\}$；$\beta$=2 时 $d_i\in \{0,1\}$  
$d_1,d_2...d_{p-1}$ is the fraction 小数部分  
 因为它们对应  $1/\beta$ , $1/\beta^2$ , … 的系数；而 $d_0$ 是“整数位”（最高位） 
$\beta, p, E, L, U, d_{i}, i=1,..., p-1$ are all nature numbers 为自然数（非负整数） 

---
3.Normalization   
The floating-point system is said to be normalized if the leading digit do is always **nonzero** unless the represented number is zero  
In a normalized system, the mantissa $m$ of a nonzero floating-point number always satisfies $1 \leq m < \beta.$  
In such case:  
- representation of each number is unique  
- no digits are wasted on leading zeros
- leading bit does not need to be stored (in a binary system, $\beta$=2)    

---

4.实际操作标准
一个实数以 符号 × 尾数（mantissa/significand） × 基数^指数 的形式存储。
常见标准是 IEEE 754，基数通常是 2。比如单精度(float32)和双精度(float64)分别用32位和64位来编码符号位、指数位、尾数位。 
- 单精度：1位符号 + 8位指数(偏置 bias = 127) + 23位尾数(隐含首位1)，有效精度约7位十进制数字。 
- 双精度：1位符号 + 11位指数(bias = 1023) + 52位尾数(隐含首位1)，有效精度约16位十进制数字。 
- 指数使用偏移量（bias）存储，以覆盖很宽的数值范围（约10^±38 for float32，10^±308 for float64）。  

解释隐含首位1(hidden leading 1):   
1.p 表示二进制有效位数（precision，位数），也就是尾数有效比特的总数。 
2.在单精度里，内存里尾数字段有 23 个比特，但有效位数(p)是 24，这是因为还有一个不存储但默认为 1 的“隐含首位”（hidden leading 1）。 
3.之所以有这个隐含首位1，是因为在基数($beta$) 为2 的情况下，经过规范化(Normalization) ,尾数m满足$1\leq m<\beta$ ,即m的第一位只能为1  
4.既然这个最高位在规范化数中必定是 1，就没有必要把它占一个存储位；硬件在解码时自动把它补回来.(所以在尾数字段只有23个比特的情况下，默认第一位是1，故精度是24)   

| System  | $\beta$ | p   | L      | U     | Notes               |
| ------- | ------- | --- | ------ | ----- | ------------------- |
| IEEE SP | 2       | 24  | -126   | 127   | singe precision     |
| IEEE DP | 2       | 53  | -1022  | 1023  | double precision    |
| IEEE QP | 2       | 113 | -16382 | 16383 | quadruple precision |

---
5.性质  
5.1 The floating-point number system is **finite and discrete**  
5.2 Total number of normalized floating-point numbers in a system is:  
$2(\beta-1)\beta^{p-1}(U-L+1)+1$  
*+1*是因为*0*的表示（在规范化之后，$1 \leq m < \beta$ 无法表示0） 
5.3 Smallest positive normalized number
$UFL =underflow \; level=\beta^L$
5.4 Largest floating-point number  
$OFL =overflow \; level = \beta^{U+1}(1-\beta^{-p})$
5.5 Floating-point numbers are equally spaced only between successive powers of $\beta$   (Space=$\beta^{1-p+E}$,p为总有效位数，E是指数部分)
5.6 Not all real numbers are exactly representable; those that are are called machine numbers.   









