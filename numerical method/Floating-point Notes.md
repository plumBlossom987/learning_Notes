机器数(Machine numbers)就是在某一浮点系统中**能被精确表示**的所有数   
$\varepsilon_{\mathrm{m a c h}}$(machine epsilon, 机器精度)是度量这个集合 *“网格密度”的一个标尺*：它刻画在**1附近两个相邻机器数之间的相对间隔大小**，因此直接关联到舍入的相对误差上界。
$\varepsilon_{\mathrm{m a c h}}$ is defined as the smallest number $\varepsilon$ such that $\mathrm{f l} ( 1+\varepsilon) > 1$      
$| \mathrm{f l} ( x )-x | \leq\varepsilon_{\mathrm{m a c h}} | x |$   
截断：$|fl(x) − x| ≤ 1 ULP ≤ β^{1−p} |x| =\varepsilon_{\mathrm{m a c h}}$    
就近：$|fl(x) − x| ≤ 0.5 ULP ≤ (1/2) β^{1−p} |x| =\varepsilon_{\mathrm{m a c h}}$    

