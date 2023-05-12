# competitive co-evolutionary differential evolution(CODE) 协同进化差分进化算法

> **本文研究了一种基于混合进化的模拟集成电路自动尺寸设计系统。提出了一种新的竞争协同进化差分进化算法(CODE)来设计具有实际用户定义规格的模拟集成电路。**在HSPICE和MATLAB相结合的基础上，系统将电路性能链接，通过电气仿真评估，在MATLAB环境下优化系统，一旦电路拓扑选择。该系统已经通过了典型的和难以设计的案例，如复杂的模拟模块，具有严格的设计要求。结果表明，即使在高度约束的情况下，设计规范也能得到很好的满足。与遗传算法和差分进化等使用静态惩罚函数处理设计约束的现有方法进行了比较，表明该算法在优化质量和稳健性方面具有重要优势。此外，该算法是有效的。

***

### 模拟设计过程

- 拓扑级设计
- **参数级设计**

本文主要研究参数级设计。即在给定电路拓扑的情况下，通过**参数选择和优化**来提高性能。  

大多数模拟电路尺寸问题可以很自然地表达为一个目标的最小化(例如，功耗)，通常受到一些约束(例如，直流增益大于某一值)。它们可以表述如下:

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512004051885.png" alt="image-20230512004051885" style="zoom: 50%;" />

其中，目标函数f(x)是要最小化的性能函数，h(x)是等式约束。在模拟电路设计中，等式约束主要是指基尔霍夫电流定律(KCL)和基尔霍夫电压定律(KVL)方程。向量x对应设计变量，X_L和X_H分别为设计变量的下界和上界。向量g(x)X0对应于用户定义的约束。

***

### 遗传算法 GA  

##### 常用术语

① 染色体(Chromosome)：染色体又可称为基因型个体(individuals)，一定数量的个体组成了群体(population)，群体中个体的数量叫做群体大小（population size）。

② 位串(Bit String)：个体的表示形式。对应于遗传学中的染色体。

③ 基因(Gene)：基因是染色体中的元素，用于表示个体的特征。例如有一个串（即染色体）S=1011，则其中的1，0，1，1这4个元素分别称为基因。

④ 特征值( Feature)：在用串表示整数时，基因的特征值与二进制数的权一致；例如在串 S=1011 中，基因位置3中的1，它的基因特征值为2；基因位置1中的1，它的基因特征值为8。

⑤ 适应度(Fitness)：各个个体对环境的适应程度叫做适应度(fitness)。为了体现染色体的适应能力，引入了对问题中的每一个染色体都能进行度量的函数，叫适应度函数。这个函数通常会被用来计算个体在群体中被使用的概率。

⑥ 基因型(Genotype)：或称遗传型，是指基因组定义遗传特征和表现。对于于GA中的位串。

⑦ 表现型(Phenotype)：生物体的基因型在特定环境下的表现特征。对应于GA中的位串解码后的参数。  



##### 基本遗传算子(Genetic Operator)

- 选择算子(Selection Operator)

- 交叉算子(Crossover Operator)

- 变异算子(Mutation Operator)



<img src="https://pic1.zhimg.com/80/v2-0d90342ab45097094ab4afe465bb9504_1440w.webp" alt="img" style="zoom:50%;" />

[遗传算法](https://zhuanlan.zhihu.com/p/100337680)

***


### 差分进化算法 DE

> 差分进化是一种基于种群的进化计算技术，它使用一个简单的微分算子来创建新的候选解，并使用一对一的竞争方案来贪婪地选择新的候选解。该算法利用解在搜索空间中的分布和解对之间的**差值**作为搜索方向，试图找到全局最优解。  

GA：根据适应度来控制父代杂交

DE：变异向量由父代差分向量生成，与父代个体向量交叉生成新个体向量，直接与其父代个体进行选择

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512165432417.png" alt="image-20230512165432417" style="zoom:50%;" />


第t代，d维，第i个个体：

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512185334117.png" alt="image-20230512185334117" style="zoom: 67%;" />

NP：种群个体数量  



对于每一个目标个体i，有一个突变向量：

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512185421196.png" alt="image-20230512185421196" style="zoom: 67%;" />

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512190627386.png" alt="image-20230512190627386" style="zoom:67%;" />

r1,r2为{1,2,...,NP}中的随机数

F一般取自(0,2]  

Xr0(t)是



试验向量

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512190745027.png" alt="image-20230512190745027" style="zoom:67%;" />

在交叉操作之后，进行选择，以决定试验向量Ui(t)是否为下一代t+1总体的成员。对于最小化问题，将Ui(t)与初始目标个体进行比较，根据以下基于一对一的贪婪选择准则:

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512190759635.png" alt="image-20230512190759635" style="zoom:67%;" />




[遗传算法、差分进化算法、协同进化算法、分布估计算法](https://zhuanlan.zhihu.com/p/442270629)

***

### 约束模拟电路优化问题

尽管DE非常有效和高效，但对于模拟电路的尺寸来说还不够。所有EC算法本身都缺乏**处理问题约束**的机制，这仍然是一个开放的研究领域。然而，大多数模拟电路设计问题都存在用户自定义规范，必须适当处理这些约束。

使用罚函数是最常用的方法，但它对罚系数非常敏感，没有适当的罚系数很难得到满意的结果。此外，Michalewicz和Schoenauer得出结论，没有任何复杂性的静态惩罚函数方法更健壮，因为一种这样的复杂方法可能在某些问题上工作得很好，但在另一个问题上可能不太好。

本文使用**增广拉格朗日方法处理约束**，将约束优化问题转化为可适用于第3节中描述的DE算法的问题。**增广拉格朗日公式中的惩罚参数在算法执行过程中自动更新以达到最优点，从而避免了惩罚参数设置不当的问题。参数是基于协同进化方法更新的。**

本文将竞争协同进化概念与基于增广拉格朗日方法的改进DE算法相结合，提出了一种用于模拟集成电路合成中约束优化问题的混合算法CODE。



#### 增广拉格朗日

> 更新拉格朗日乘子，使其收敛到鞍点，从而避免局部寻优

约束非线性优化问题可以表示为

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512183911682.png" alt="image-20230512183911682" style="zoom: 67%;" />

这些函数可以组合成一个变换函数U，称为增广拉格朗日量。

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512184005876.png" alt="image-20230512184005876" style="zoom: 67%;" />

在模拟电路设计中，相等约束仅限于基尔霍夫定律所施加的电流和电压关系:KCL和KVL。基尔霍夫定律自动包含在电子模拟器的电路方程中，因此在优化过程中只需要考虑设计规范定义的不等式约束。因此，**增广拉格朗日公式化简为:**

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512184020131.png" alt="image-20230512184020131" style="zoom: 67%;" />

x：决策变量的向量

r：惩罚参数的向量

u_i=θ_i*r_i是与第i个约束相关的拉格朗日乘子。

这个过程不断重复，直到收敛。优化目标是找到鞍点(x', u')  



#### 共同进化方法与增广拉格朗日量的结合

> 增广拉格朗日方法的主要问题是如何更新拉格朗日乘子，使其收敛到鞍点，从而避免局部寻优。预先确定的更新方案可能在某些问题上工作得很好，但在另一个问题上可能不工作得很好。协同进化方法依靠决策变量的当前进化结果解决了这一问题。
>
> 竞争协同进化方法的灵感来自于对捕食者-猎物关系的观察，即生物在动态环境中相互适应。如果团体击败了与他们竞争的个体，他们就会得到奖励。竞争性协同进化策略可以看作是两个群体之间的军备竞赛。为了引起竞争，必须**产生两个适应度函数值相反的种群**。

<img src="C:\Users\caiyujie\AppData\Roaming\Typora\typora-user-images\image-20230512184650415.png" alt="image-20230512184650415" style="zoom:50%;" />