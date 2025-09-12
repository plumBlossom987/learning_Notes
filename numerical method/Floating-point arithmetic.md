1.概述
浮点数运算（Floating-point arithmetic）是计算机用来表示和计算实数的一套近似机制与规则。它用有限的比特去表示非常大或非常小的数，并支持加减乘除等运算，但会引入舍入误差和一些非直观现象。 
2.表示方式  
一个实数以 符号 × 尾数（mantissa/significand） × 基数^指数 的形式存储。
常见标准是 IEEE 754，基数通常是 2。比如单精度（float32）和双精度（float64）分别用32位和64位来编码符号位、指数位、尾数位。 
- 单精度：1位符号 + 8位指数 + 23位尾数（隐含首位1），有效精度约7位十进制数字。 
- 双精度：1位符号 + 11位指数 + 52位尾数（隐含首位1），有效精度约16位十进制数字。 
- 指数使用偏移量（bias）存储，以覆盖很宽的数值范围（约10^±38 for float32，10^±308 for float64）。 










Number Representation    
A real number $x$ can be represented as  
$$  x=\pm[ d_{0}+{\frac{d_{1}} {\beta}}+{\frac{d_{2}} {\beta^{2}}}+\cdot+{\frac{d_{p-1}} {\beta^{p-1}}} ] \beta^{E} $$  
where:  
 $\beta$ is the base/radix 基数   
  $\beta$ =2（二进制）, $\beta$ =10（十进制）, $\beta$ =16（十六进制） 
$p$ is the precision 精度  
   指尾数中有效位的个数，即 $d_0$, $d_1$, …, $d_{p-1}$ 共 $p$ 位。$p$ 越大，可区分的数越密，舍入误差越小  
$E$ is the exponent and $L \leq E \leq U$ is the exponent range 指数(及其范围)
  L、U 为指数下界与上界，决定可表示数的量级范围（最小、最大规模）。指数范围越宽，动态范围越大。 
$d_od_1...d_{p-1}$ is the mantissa and $0\leq d_{i} \leq\beta-1, i=0,..., p-1$ 尾数(及其范围)  
 尾数每位是基数 β 下的一位数字。例如 $\beta$=10 时 $d_i\in \{0,…,9\}$；$\beta$=2 时 $d_i\in \{0,1\}$  
$d_1,d_2...d_{p-1}$ is the fraction (也被称为)小数部分  
 因为它们对应  $1/\beta$ , $1/\beta^2$ , … 的系数；而 $d_0$ 是“整数位”（最高位）  
$\beta, p, E, L, U, d_{i}, i=1,..., p-1$ are all nature numbers 为自然数（非负整数） 

理解： 
1.浮点数的一般表示形式：x = sign × mantissa × $β^E$  
2.指数 E 受限于区间 $[L, U]$，共同决定动态范围。 
3.基数 $\beta$ 与精度 $p$ 决定离散格点的密度与舍入误差规模  



