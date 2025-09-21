1.概念：泊松分布适合于描述单位时间内随机事件发生的次数的概率分布  
2.PMF  $P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}$  
参数 $\lambda$ 是随机事件发生次数的数学期望
3.性质  
3.1 $E(X)=Var(X)=\lambda$  
3.2 X~Poission($\lambda_1$), Y~Poisson($\lambda_2$) X+Y~Poisson($\lambda_1+\lambda_2$)  
3.3 泊松分布和二项分布  
在二项分布的伯努利试验中，如果试验次数n很大，二项分布的概率p很小，且乘积 $\lambda=np$ 比较适中，则事件出现的次数的概率可以用泊松分布来逼近。  
二项分布可以看作泊松分布在离散时间上的对应物。  
自然对数e的定义：$\mathop{lim}\limits_{n \rightarrow \infty}(1-\frac{\lambda}{n})^n=e^{-\lambda}$  
二项分布的定义：$P(X=k)={n \choose k}p^k(1-p)^{n-k}$  
![[Poisson&Binomial.png]]  
3.4 泊松分布和指数分布




