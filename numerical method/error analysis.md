Data error 输入数据的误差  
Computational error 计算时产生的误差  
Computational error = truncation error + rounding error    
truncation error  截断误差：误差来源于算法本身：比如只取无穷级数的前两项作为结果   
rounding error 舍入误差：误差来源于运用算法时数据采用了有限的精度(p);以及基于这种精度运行的运算规则(操作)(**本质**：有限精度、经过舍入的算术运算, *finite-precision, rounded* arithmetic)  

---
1.Conditioning(Sensitivity)  
1.1 概述： 输入**数据**的变化能引发多少输出数据的变化  
1.2 指标(定性分析) ： 
1.2.1 A problem is *insensitive* or *well-conditioned* if the relative change in input causes **similar relative change** in the solution.  
1.2.2 A problem is *sensitive* or *ill-conditioned* if the relative change in the solution is **much larger** than that in the input data.  
1.3 指标(定量)：Condition number  
cond=$\frac{|relative change in solution|}{|relative change in input data|}=\frac{|(f(\hat{x})-f(x))/f(x)|}{|(\hat{x}-x)/x|}=\frac{|\Delta y /y|}{|\Delta x/x|}$  

 The problem is *sensitive* or *ill-conditioned* if cond ≫ 1  
1.4 Condition number 的理解与近似
1.4.1 The condition number is an **amplification factor** relating the *forward error* to the *relative backward error*
|relative forward error| = cond · |relative backward error|.  
1.4.2 In practice:    
|relative forward error| ⪅ cond · |relative backward error|   
*Relative forward error*, *Absolute forward error*  and *Condition number*:  
$$
\begin{array} {l} {f ( x+\Delta x )-f ( x ) \approx f^{\prime} ( x ) \Delta x} \\ {\frac{f ( x+\Delta x )-f ( x )} {f ( x )} \approx\frac{f^{\prime} ( x ) \Delta x} {f ( x )}} \\ {\mathrm{c o n d} \approx\left| \frac{f^{\prime} ( x ) \Delta x / f ( x )} {\Delta x / x} \right|=\left| \frac{x f^{\prime} ( x )} {f ( x )} \right|} \end{array}
$$
1.4.3 关于反函数的cond:  
$cond(f^{−1}) = 1/cond(f)$

---

2.Stability  
2.1 概述：**计算过程**中的扰动能引发多少输出数据的变化
2.2 定性分析：Analgorithm $\hat{f}$ for a problem $f$ is called **stable** if the produced result is *relatively insensitive* to perturbations during computation.
2.3 定量指标  An algorithm ${\hat{f}} \ : \ \mathbb{R}^{n} \to\ \mathbb{R}^{m}$ for a problem $f \, : \, \mathbb{R}^{n} \, \to\, \mathbb{R}^{m}$ is called  $s t a b l e$ if for all ${\boldsymbol{x}} \in\mathbb{R}^{n},$ we have  
$$
\frac{\| {\hat{\boldsymbol{f}}} ( \mathbf{x} )-f ( {\hat{\mathbf{x}}} ) \|} {\| f ( \mathbf{x} ) \|}={\mathcal{O}} ( \varepsilon_{\mathrm{n a c h}} ) \quad{\mathrm{f o r ~ s o m e ~}} {\hat{\boldsymbol{x}}} {\mathrm{~ w i t h ~}} \quad{\frac{\| {\hat{\mathbf{x}}}-\mathbf{x} \|} {\| \mathbf{x} \|}}={\mathcal{O}} ( \varepsilon_{\mathrm{n a c h}} ).
$$

---

3.Accuracy  
3.1 概述：描述**计算的结果**相对**真实结果**是否接近
3.2 定性描述： *Accuracy* generally expresses the **closeness** of a *computed solution* to the *true solution*(i.e., the *relative forward error*)
3.3 定量分析： An algorithm ${\hat{f \,}} : \, \mathbb{R}^{n} \, \to\, \mathbb{R}^{m}$ for a problem $f \, : \, \, \mathbb{R}^{n} \, \to\, \, \mathbb{R}^{m}$ is called accurate if for all $x \in\mathbb{R}^{n},$ ,we have
$$
\frac{\| {\hat{f}} ( \mathbf{x} )-f ( \mathbf{x} ) \|} {\| f ( \mathbf{x} ) \|}={\mathcal{O}} ( \varepsilon_{\mathrm{m a c h}} ) \quad( \mathrm{f o r} \ \varepsilon_{\mathrm{m a c h}} \to0 ).
$$
3.4 *Accuracy* depends on the *conditioning* of the problem as well as on the *stability* of the algorithm.

