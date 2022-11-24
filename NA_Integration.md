### numerical integration method 

#### chapter 1

* 与微分一样，数值分析里面是用离散的点积分，而利用离散点积分的方法便是用拉格朗日插值将这些点还原成函数再积分。

* **Trapezoidal Rule**：用两个点，线性拉格朗日插值再积分

  $\int_a^b{f(x)dx}=\frac{h}{2}(f(x_0)+f(x_1))$

  $|R(n)|=\frac{h^3}{2}f''(\xi)$

* **Simpson rule**:用三个点，拉格朗日插值成二次多项式再积分

  $\int_a^b{f(x)dx}=\frac{h}{3}(f(x_0)+4f(x_1)+f(x_2))$

  $|R(n)|=\frac{h^5}{90}f^{4}(\xi)$

(还有其他类似的拓展到3-4次的，在书本192页，此处不详列。Todo：有空补)

#### chapter 2

* 遇到更多的点，如果还是直接还原出拉格朗日公式的话，由于拉插的荣格现象会出现较大误差，于是我们选择对其进行分段的二次，三次插值

* **Composite Trapezoidal rule** 将函数分成n段，每段长度为h，每段当线性积分再累加

  ​	$[a,b]内,x_k=a+kh,k\in[0,n]$

​			$\int_a^b{f(x)dx}=\frac{h}{2}(f(a)+2\sum_{k=1}^{n-1}f(x_k)+f(b))$

​			$|R(n)|=\frac{h^2}{12}(b-a)f^{2}(\xi)$

* **Composite Simpson rule** 将函数分成n段，每段长度为h，算上边界每段有3个点（所以点总数为$2n-1$)，对每段进行Simpson rule

  * 课本上公式把点总数设为n，此处公式随它

  ​	$\int_a^b{f(x)dx}=\frac{h}{3}(f(x_0)+2\sum_{j=1}^{(n/2)-1}f(x_{2j})+4\sum_{j=1}^{(n/2)}f(x_{2j-1})+f(b))$

![image-20221124151037785](C:\Users\andres\AppData\Roaming\Typora\typora-user-images\image-20221124151037785.png)

​			$|R(n)|=\frac{h^4}{16}\frac{(b-a)}{180}f^{2}(\xi)$

#### chapter 3

* **Romberg sequence**

​	以Composite Trapezoidal rule为例子，我们可以发现

​	R(n)与h为平方关系，h变成1/2(h为段长度，即更加细分），R(n)变为1/4

即$\frac{I-T_{2n}}{I-T_{n}}=\frac{1}{4}$($T_n$为把函数分成n段然后求积分)

​	故我们可以从上式解$I=\frac{4T_{2n}-T_{n}}{4-1}$这个相当于把二次项的误差消掉了，（称为$S_n$）递减速度更快。

​	同时对于$S_n$，我们可以用类似的方法进一步递推下去，消掉三次，四次的误差。

![image-20221124152532277](C:\Users\andres\AppData\Roaming\Typora\typora-user-images\image-20221124152532277.png)



* 这种方法可以适用于所有精度可以用多项式表达的式子里，被称为$Richardson's Extrapolation$

  ![image-20221124152713144](C:\Users\andres\AppData\Roaming\Typora\typora-user-images\image-20221124152713144.png)

