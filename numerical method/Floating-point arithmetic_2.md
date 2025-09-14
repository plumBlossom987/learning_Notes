Rounding Rules
1.Def 
lf the real number x is not exactly representable, then it is approximated by a "nearby" floating-point number **fl(x)**.This process is called *rounding*; the error induced by rounding is called *rounding error*.  舍入;舍入误差
2.Two commonly used rounding rules:  
*Chop*: truncate the base-B expansion of x after the (p - 1)st digit; also called *round towards zero*. 截断（Chop，或“向零舍入”）
*Round to nearest*: $\operatorname{f l} ( x )$ is the nearest floating-point number to x using the floating-point number whose last stored digit is even in case of a tie; this is also called *round to even*. 四舍五入到最近(“就近-偶数”规则 Round to even)

比较： 

| Rounding 舍入              | Method             | Rounding Error Analysis 舍入误差分析 | Notes                    |
| ------------------------ | ------------------ | ------------------------------ | ------------------------ |
| Chop 截断                  | round towards zero | 正数会偏小，负数会偏大;容易引入系统性偏差          | /                        |
| Round to nearest 四舍五入到最近 | round to even      | 避免总是向上或向下;能在统计意义上减少系统性偏差       | 在 IEEE 754 浮点标准中是默认的舍入模式 |

---
Machine Precision
The accuracy of a floating-point system is characterized by the *unit roundoff* (or *machine precision* or *machine epsilon*) --denoted by $\varepsilon_{mach}$  
With rounding by chopping: $\varepsilon_{\mathrm{m a c h}}=\beta^{1-p}.$   
With rounding to nearest: $\varepsilon_{\mathrm{m a c h}}=\frac{1} {2} \beta^{1-p}.$   
Alternatively, $\varepsilon_{\mathrm{m a c h}}$ is defined as the smallest number $\varepsilon$ such that  $\mathrm{f l} ( 1+\varepsilon) > 1.$      
Proposition: Rounding  
For every $x \in\mathbb{R}$ in the range of the floating-point system, we have  
$$
| \mathrm{f l} ( x )-x | \leq\varepsilon_{\mathrm{m a c h}} | x |.
$$
0.上式的另一种理解方式：  
This means : For every X in the range of the System there is  $\varepsilon$ with $|\varepsilon|<$$\varepsilon_{mach}$ such that : $f l( x )=( 1+\varepsilon) x$    
1.浮点系统由基数 β（base）和有效位数 p（precision）等参数决定。
2.当把真实数 x 舍入为可表示的 fl(x) 时，舍入误差的相对大小通常与 x 的量级无关（对“规范化”的数）。因此我们用一个统一的上界来刻画最坏情况下的相对舍入误差，这个界就是 $\varepsilon_{mach}$   
3.$\varepsilon_{mach}$约等于“相邻两*可表示*浮点数之间的 *(半)间距*”与*当前量级*相比的相对比例；它反映了“*最糟糕*时相对误差有多大”。\* *半间距与否取决于舍入规则*
4.**ULP(unit in the last place)** 指在某一量级上的相邻浮点数之间的间隔。**就近舍入**的最大误差是 *0.5 ULP*，**截断**的最大误差是 *1 ULP*，因此二者的 $\varepsilon_{mach}$ 相差一倍。 在给定指数 E 的规格化区间内，相邻两个可表示数之间的“步长”（即 1 ULP at exponent E）是 $ULP(E) = β^{E−(p−1)} = β^{E+1−p}$   
\* 这是因为尾数的最后一位（第 p−1 位小数位）加 1 的增量对应的实数增量为 $β^{E} × β^{−(p−1)}$   
5.因此，相对量级下的 1 ULP 与 |x| 的比例大约是 $ULP(E) / |x| ≈ β^{E+1−p} / (m β^{E}) = β^{1−p} / m$， 其中 $m \in [1, β)$，所以这个比例介于 $β^{1−p}/β$ 和 $β^{1−p}$ 之间。取最坏情况的上界（m 取最小的 1），就得到相对误差上界的系数 $β^{1−p}$；就近舍入则再乘以 1/2。 
截断：$|fl(x) − x| ≤ 1 ULP ≤ β^{1−p} |x|$   
就近：$|fl(x) − x| ≤ 0.5 ULP ≤ (1/2) β^{1−p} |x|$  
6.另一种定义（1+$\varepsilon$ 可分辨判据） 
- 定义：$\varepsilon_{\mathrm{m a c h}}$ 是满足 $\mathrm{f l} ( 1+\varepsilon) > 1.$ 的最小正数 $\varepsilon$。 
- 含义：在当前浮点格式和舍入规则下，把 1 加上一个尽可能小的正数 ε，再进行舍入后，结果刚刚能与 1 区分开（即不是被舍回到 1）。这个“临界”大小就是机器精度。 
- 为什么等价：在单位量级（以 1 为代表）处，相邻可表示浮点数之间的间距就是所谓的 ULP(1)。就近舍入时，能把 1 推到下一个可表示数所需的最小加法正量是半个间距；截断时是一个整间距。因此这个最小 ε 与前面给出的 $\varepsilon_{\mathrm{m a c h}}$  公式一致  
  round-to-nearest: ε_mach = $1/2 · β^{1−p}$  
  chopping: ε_mach = $β^{1−p}$  

---
知识补充：  十进制转二进制（二进制转十进制比较简单，直接每一位\*$2^{对应位数}$即可）  
对于**整数**:采用*除以2取余数，逆序排列*的方法，即不断将十进制数除以2，记录余数，直到商为0，再将余数从下往上排列   
对于**小数**，采用*乘以2取整数，顺序排列*的方法，即不断将小数乘以2，记录整数部分，直到小数部分为0或达到所需精度，再将整数部分按顺序排列  

---
7.IEEE标准下的Machine Precision  
For IEEE floating-point systems
$$
\begin{array} {l} {{\varepsilon_{\mathrm{m a c h}}=2^{-2 4} \approx1 0^{-7} \mathrm{~ i n ~ s i n g l e ~ p r e c i s i o n.}}} \\ {{\varepsilon_{\mathrm{m a c h}}=2^{-5 3} \approx1 0^{-1 6} \mathrm{~ i n ~ d o u b l e ~ p r e c i s i o n.}}} \\ {{\varepsilon_{\mathrm{m a c h}}=2^{-1 1 3} \approx1 0^{-3 6} \mathrm{~ i n ~ q u a d r u p l e ~ p r e c i s ion.}}} \end{array}
$$
In IEEE single, double, and quadruple precision systems, we have about *7, 16, and 36* **decimal digits** of precision, respectively

8.性质(UFL,OFL,$\varepsilon_{mach}$)
In practical floating-point systems, we have  
$$
\boxed{0 < \mathrm{U F L} < \varepsilon_{\mathrm{m a c h}} < \mathrm{O F L}}
$$