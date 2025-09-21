**Taylor Expansion**. Let $f : \mathbb{R} \rightarrow\mathbb{R}$ be $k$ -times diff. at $a \in\mathbb{R}.$ We have  
$$
f ( x )=\sum_{i=0}^{k} \frac{f^{( i )} ( a )} {i!} ( x-a )^{i}+R_{k} ( x ),
$$
where $R_{k} ( x )=o ( | x-a |^{k} )$ (for $x \to a$ ) and $f^{( i )} ( a )$ denotes the i-th deri-vative of $f$ at a.
Taylor's theorem allows to approximate a function by a polynomia expansion close to the *reference point a*.

---
**Landau Notation: big-O and small-o**
A full stability $/$ error analysis of a given algorithm or problem can quickly become lengthy and difficult  
In practice, the big-O and small-o calculus and other tools, such as e.g., Taylor expansion, are used to simplify the analysis  
Definition: big-O. For $f, g : \mathbb{R} \to\mathbb{R}$ and $a \in\mathbb{R},$ we write
$$
f ( x )={\mathcal O} ( \mathrm{g} ( x ) ) \quad\mathrm{f o r} \quad x \to a
$$
if there exist $\varepsilon> 0$ and $C \geq0$ such that $| f ( x ) | \leq C \cdot| g ( x ) |$ for all x satisfying $\left| x-a \right| < \varepsilon.$ 
Definition: small-o. For $f, g : \mathbb{R} \to\mathbb{R}$ and $a \in\mathbb{R},$ we write
$$
f ( x )=o ( g ( x ) ) \quad\mathrm{f o r} \quad x \to a
$$
if  $\operatorname* {l i m}_{x \to a} | f ( x ) | / | g ( x ) |=0.$  

Comments
1.Typical choices: a = 0 or $a=\infty.$  
2.Asymptotic relationship between $f$ and $g$ :  $g$  is often much simpler than $f$ and captures *main growth behavior* of $f$   
3.We are often only interested in the **leading order** (${\mathcal{O}} ( \varepsilon_{\mathrm{m a c h}} ) )$ or in the order of the **complexity**.  
4.Examples  
4.1 $\sin( x )={\cal O} ( 1 )$ for all $X$ 
$sin(x)=\mathcal{O}(x)$ for $x \to0$, 
$log(1+x)=\mathcal{O}(x)$ for $x \to0$
4.2 $(1 +\mathcal{O}(x)(1+ \mathcal{O}(x))=1+\mathcal{O}(x)$ for $x \to 0$

---
