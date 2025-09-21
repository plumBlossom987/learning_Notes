Subnormals and Gradual Underflow  
1.The *normalization* causes a gap around zero in the floating-point system  
“零附近的空档”:无法表示比UFL更小的数(0附近的数)
2.If the **leading digits** are allowed to be zero, but only when **the exponent is at its minimum value,** then the gap is "filled in" by *additional subnormal* or *denormalized* floating-point numbers.
3.引入Subnormal 区间的影响  
3.1 Subnormals extend the range of the representable magnitudes   
3.2 the unit roundoff $\varepsilon_{\mathrm{m a c h}}$ is not smaller  
3.2 Augmented system has a gradual underflow.  “渐进下溢”(gradual underflow):当真实结果逐步变小穿过 UFL时，值不会突然从UFL 跳到 0，而是通过一串等步长的次正规数逐级接近 0，最终才到 0。

---
Exceptional Values  
IEEE floating-point standards provide special values to indicate two **exceptional situations**  
1.*Inf* - which stands for "infinity" -- results from *dividing a finite number by zero*, such as 1/0  
2.*NaN* -- which stands for "not a number" -- results from *undefined or indeterminate operations* such as 0/0, 0 · Inf or Inf /Inf.  
Inf and NaN are implemented in the IEEE arithmetic through specia reserved values of the exponent field  

---
Floating-Point Arithmetic
1.Addition or Subtraction ($\oplus$. $\ominus$) *Shifting mantissa to make exponents match* may cause loss of some digits of smaller numbers -- possibly all of them  
1.1要相加/相减两个浮点数，必须先 **“对阶”，即把较小指数的数的尾数右移** ，使得两个数的**指数相同**，然后再对尾数做加减，最后规范化并舍入  
1.2**右移会丢弃低位比特**。这些被移出有效位窗口的比特会影响舍入，但若指数差很大，*小数的所有有效位都可能被移出并完全丢失*，结果等于较大的那个数（称“吸收”或“消失”）
1.3 灾难性抵消：*当两个接近的数相减时*，最高位大量相同，尾数相减后前导位被抵消，只剩下很少的有效位，**显著相对误差放大**。  
加法*非结合*：由于舍入，(a ⊕ b) ⊕ c 与 a ⊕ (b ⊕ c) 可能不同，特别是当量级差别大时。 
2.Multiplication ($\odot$): Product of two p-digit mantissas *contains up to 2p digits*, so the result may not be representable.   
2.1两段 p 位尾数相乘，数学上最多产生 *2p* 位有效数字（进位后规范化大致也是 2p 位量级）
2.2 浮点格式只能保留 p 位，需要对 2p 位结果进行舍入（截断或就近舍入），**因而丢弃低 p 位信息**，带来舍入误差。指数部分则相加，若超出范围可能溢出为 Inf（或下溢进入次正规/零）。  
3.Division ($\oslash$): Quotient of two p-digit mantissas may *contain more than p digits* such as a nonterminating binary expansion of 1/10
3.1 尾数相除往往得到一个无限长的进制展开。例如十进制的 1/3，或二进制的 1/10（0.0001100110011…，循环不终止）。
3.2 由于只能保留 p 位，需要*在第 p 位处舍入*，截断无限展开，产生舍入误差。指数部分相减，可能引发下溢/上溢。
3.3 由于商的展开不终止，像把十进制常数 0.1 转成 binary 时就不可精确表示，随后任何运算都携带微小误差。
4.总结
Results of floating-point arithmetic operations may differ from results of the corresponding real arithmetic operation (on same operands)   

核心要点：
1.浮点加、减、乘、除与实数算术的**差异**来源：*对阶*导致的**丢位**；结果需*舍入*到有限精度；以及某些商的进制展开*不终止*    
2.浮点系统只有有限位的尾数（有效数字，记作 *p* 位）与有限范围的指数，因此每次运算后的“真实结果”通常不能被精确表示，必须**舍入到最近的可表示数**，因而可能偏离实数算术结果  

---
4.The real result may fail to be representable because its **exponent is beyond the available range**.  
4.1*Overflow* is a serious problem as there is **no** good approximation to arbitrarily large numbers in floating-point systems.  
4.2*Zero* is often a reasonable approximation for **arbitrarily smal magnitudes**  
4.3On many computer systems **overflow is fatal** but an **underflow may be silently set to zero**.

5.Example: Evaluating a Divergent Series
The infinite series  $\sum_{k=1}^{\infty} \frac{1} {k}$ is divergent, yet has finite value in floating-point arithmetic.  
Possible Explanations:  
5.1The partial sum eventually overflows 
5.2 1/k eventually underflows
5.3 Partial sum ceases to change once $1 / k$ becomes negligible relative to the partial sum:  
$\frac1 k \lesssim\varepsilon_{\mathrm{m a c h}} \cdot\sum_{i=1}^{k-1} \frac1 i.$  

6.ldeally, $x\circledast y=\mathrm{f l} ( x * y )$ , i.e., floating-point arithmetic operations produce correctly rounded results.  
IEEE-Standard 754:  
For any operation $* \in\{+,-, \cdot, / \}$ and any pair of *machine numbers* x,y,we have
$$
x \circledast y=fl( x * y )
$$
This means $x \circledast y=( 1+\varepsilon) \cdot( x * y )$ for some $| \varepsilon| \leq\varepsilon_{\mathrm{m a c h}}.$ 
6.1 *Not all* laws of real arithmetic are valid in the floating-point system
6.2 Floating-point addition and multiplication are *commutative but not associative*.
Example: if $\varepsilon$ is a positive floating-point number that is slightly smaller than $\varepsilon_{\mathrm{m a c h}}$ then $(1 \oplus\varepsilon)\oplus \varepsilon= 1$  but$1\oplus(\varepsilon\oplus\varepsilon) > 1$ 
6.3 理解：  
6.3.1 理想要求(IEEE 754 核心目标): 对任意两台式机数 x, y, 有 $x \circledast y=fl( x * y )$  也就是说，先用实数精度算出 x * y，然后把它按所选舍入模式舍到最近的机器数，硬件给出的结果就是这个值。这就叫 *“正确舍入”*

6.3.2 并非所有实数算术定律在浮点中成立  
原因：每一步都要舍入，**舍入会破坏精确代数恒等式**。特别是涉及三个及以上操作时，中间舍入会让不同的括号次序产生不同误差积累

7.Cancellation
7.1More on $\ominus$ :  
Subtraction of two p-digit numbers having **the same sign** and **similar**
**magnitudes** yields *results with fewer than p digits*, so it is usually exactly representable.
Reason: *the leading digits* of the two numbers *cancel* (i.e., their
difference is zero) 
7.2 Despite the exactness, cancellation often implies serious **loss of information**  
Operands are often uncertain due to rounding or other previous errors -> relative uncertainty in the difference might be large
Example:
lf $\varepsilon$ is a positive floating-point number slightly smaller than $\varepsilon_{mach}$. then
$$
( 1 \oplus\varepsilon) \ominus( 1 \ominus\varepsilon)=1-1=0
$$
in floating-point arithmetic which is correct for the final subtraction operation. The true result of the overall computation ——2e  has been completely lost!  

7.3 Digits lost due to *cancellation* are the most significant, **leading digits**- whereas digits lost in *rounding* are the **least significant digits**   
lt is generally **bad** to compute a small quantity as difference of large quantities since the *rounding error is likely to dominate the result*  

7.4 Evaluating an alternating series such as
$$
e^{x}=1+x+\frac{x^{2}} {2!}+\frac{x^{3}} {3!}+\dots
$$
for $x < 0$ can give a disastrous result due to *catastrophic cancellation*   
当 x < 0，级数的各项交错符号：1（正）、x（负）、x^2/2!（正）、x^3/3!（负）…在数值求和时，正负相间会频繁发生“近数相减”，导致*灾难性抵消*：高位有效数字被相互抵消，只剩下很少的有效位，舍入误差的相对影响被极大放大

7.5 The two solutions of the quadratic equation $a x^{2}+b x+c=0$ are given by
$$
x_{1 / 2}=\frac{-b \pm\sqrt{b^{2}-4 a c}} {2 a}
$$
A naive use of this formula can suffer from overflow, underflow, or severe cancellation.  
*Rescaling the coefficients* avoids overflow or harmful underflow. 对系数进行*重缩放*  
*Cancellation* between $- b$ and the square root can be avoided by computing one root using the alternative formula
$$
x_{1 / 2}=\frac{2 c} {-b \mp\sqrt{b^{2}-4 a c}}
$$
Cancellation inside the square root cannot be easily avoided without using higher precision.  
上溢/下溢：当 |b|、|a|、|c| 很大或很小，计算 b^2、4ac、以及 $\sqrt{(b^2−4ac)}$ 可能超出浮点范围（上溢）或落入次正规区甚至为 0（下溢），导致无意义结果
如果 b 的符号与 $\sqrt{(b^2−4ac)}$ 使得 −b 与 $\pm\sqrt{(b^2−4ac)}$接近，分子是两个几乎相等的大数之差，保留下来的有效位数很少，根的相对误差可能很大。典型地，当 b > 0 时，取 “+” 号将产生 −b + √(...) 的抵消；当 b < 0 时，取 “−” 号将产生 −b − √(...) 的抵消。

7.6 The mean and standard deviation of sequence $\{x_{i} \}_{i=1}^{n}$ are given by
$$
\bar{x}=\frac{1} {n} \sum_{i=1}^{n} x_{i} \quad\mathrm{a n d} \quad\sigma^{2}=\frac{1} {n-1} \sum_{i=1}^{n} ( x_{i}-\bar{x} )^{2}.
$$
 The mathematically equivalent formula  
$$
\sigma^{2}=\frac1 {n-1} \left( \sum_{i=1}^{n} x_{i}^{2}-n \bar{x}^{2} \right)
$$
avoids making *two passes through the data*.  
*Single cancellation* **at the end of the one-pass formula** is more damaging numerically than *all cancellations* **in the two-pass formula combined**.  
7.6.1两种计算方式  
两遍法（稳定）: 先一遍求和得到均值 x̄；再第二遍累加 (x_i − x̄)^2 并求平均。这在数值上较稳定，*因为每个 (x_i − x̄) 都是局部小量，平方后累加，抵消效应分散在许多小项中*，相对误差有限。 
一遍法（等价但不稳定）: 在一次遍历中同时累加 S1 = ∑ x_i 与 S2 = ∑ x_i^2，最后用 σ^2 = (S2 − S1^2/n)/(n−1)。表面省时，但**最后一步要做 S2 − S1^2/n**，这经常是 *“两大数之差得到一个小数”*，会发生**灾难性抵消**。  
7.6.2 为什么一遍法更脆弱:   
若数据方差不大，则 S2 ≈ S1^2/n。两者本身可非常大（规模随 n 和数值大小增长），但它们的差恰是方差量级，远小得多。浮点中 S2 和 S1^2/n 各自包含舍入误差；**相减时高位相互抵消，导致有效位数骤减**，最终的 σ^2 相对误差被放大。
两遍法中的“抵消”发生在 (x_i − x̄) 这一级：每一项规模就与标准差同量级，累加的是“小量的平方”。即使有舍入，也不会把两个巨大的量相减，因而不会放大到灾难性程度。

---

Summary: Floating-Point Arithmetic  
1.On computers, the infinite *continuum* of real numbers is approximated by *finite and discrete* floating-point number systems with sign, exponent, and mantissa   fields with each floating-point word.  
2.The **exponent field** determines *the range of representable magnitudes* characterized by underflow and overflow levels.  
3.**Mantissa field** determines *precision* of the floating-point approximation -- characterized by the unit roundoff $\varepsilon_{mach}$.  
4.**Rounding error** is the loss of *least significant trailing digits* when approximating a true real number by nearby floating-point numbers
5.**Cancellation** is the loss of the *most significant, leading digits* when numbers of similar magnitude are subtracted -- resulting in *fewer significant digits* in finite precision.