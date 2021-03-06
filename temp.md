

# 长安大学第三届“迎新杯”程序设计竞赛题解

---

## 前言

首先感谢各位dalao前来参赛，感谢各位领队帮忙判题发球。

比赛之前我们做了不少准备，为的是能做好命题和评测以及招待外宾的工作，不知道各位是否还觉得满意呢。

很高兴这次比赛没有出什么大问题，尽管有熟悉的`ESA`，熟悉的烂鼠标，以及热身最后崩了一小下。同时赛后我们发现打印的题面并不是最新版本的，但是数据并没有问题，这可能导致一些选手白白花时间多考虑了一些细节上的问题，深表歉意。

我们强行续了一把OJ，尽管它还不是很稳定，目前只放了这次迎新杯的题目，欢迎选手补题，没来现场的也可以在OJ上小玩一下。

题面链接：clw加
比赛链接：clw加

最后，希望各大院校今后都能加强交流与友好往来，祝陕西省的ACM越来越好。

## 热身赛

### 难度分布

热身赛主要让选手熟悉环境与PC^2的使用方法，一共设置了四道题目。其中第一道为测试提交的题，另外三道大概是随便暴力题或比较近期的一些原题简化。由于是热身赛所以难度上也没有去把控，导致有萌新绝望卡题，也有dalao光速AK。

### A.欢迎来到彩虹岛 `签到`
题意：输出“Welcome to CHD”
解析：本题为测试提交题，Hint中写了AC代码。
吐槽：judge真的收到了好多奇怪的东西……

### B.粉刷篱笆 `模拟` `暴力`
题意：n段篱笆，初始为原木色，m次操作，$[l_{i},r_{i}],color_{i}$，表示把区间的篱笆染成该颜色，问篱笆最后有几种颜色。
解析：模拟染色过程，用一个数组维护篱笆的颜色，每次染色操作暴力扫染色区间修改颜色，最后扫一遍统计多少种不同颜色，复杂度O(nm)。

### C.拯救小伙伴 `博弈`
题意：给一个二进制串，每次操作选择一个“1”，将其自身及其左边所有数字进行0/1反转，无法操作者输，问谁胜。
解析：注意到每次操作最左边的数字必然会被翻转，而结束时最左边的数字必然是0，故若初始时最左边的数字是0，则到游戏结束时必然翻了偶数次，即后手胜，反之则先手胜。
吐槽：比较近的原题简化……

### D.魔法少女的数学题 `数学`
题意：给一个正整数k，问存在多少二元组(p, q)使得$p \cdot q = k$且gcd（p， q） = 1。
解析：对于k的每个素因子$Prime_{i}$，它不能同时是p,q的因子，否则不满足pq互质，故只有$Prime_{i}$是p的因子或者$Prime_{i}$是q的因子这2种情况，如果k有n个不同的素因子，那么答案就是$2^n$。统计不同素因子个数暴力O($\sqrt k$)分解即可。
吐槽：依然比较近的原题简化……


## 正式赛

### 难度分布

由于去年题目难度分布不合适，给一些学校的萌新造成了心理阴影，今年花了很长时间来确定题目难度分布，同时想把题面讲的更清楚更有趣些。从结果来看除了G题描述上坑到了不少人，其他题目与我们的期望差不多。

考虑到来参加比赛的选手水平差距较大，有刚上手的萌新，也有在Regional拿了许多牌的dalao，我们今年增加题目数量至12题，让萌新能有题做，dalao也不会觉得很无趣。

其中A，B，C三题的定位是简单题，希望大部分人都能出，考虑到题数较多，萌新不太会找水题，于是特意放在了最前面，但似乎造成了题目是难度递增的假象。

我们认为在这样的个人赛中，CF风的题目是比较合适的，对于新人来说难度与码量不会太大，需要稍微想一些trick，于是便有了DE。结果确实卡了不少人，尤其是E题甚至卡到了dalao，裁判组甚至一度陷入了怀疑数据出错的状态。

为了丰富内容，我们又增加了一个中学知识足以解决的几何F，一个暴力的回文串H，以及一个容易猜结论的构造L。我们认为这几个题目都是不需要前置知识，只要肯想肯算，有一定码力都能出。最后F的出题量比我们预期少很多，而猜出L的人很多。

由于我们之前给自己学校的新人讲过一些算法，于是我们决定出少量套路题给努力做练习的同学，于是有了I题二分与J题BFS，事实证明我们的小朋友果然没有做题呢。: )

最后G题是一个数学递推，K题是一个无趣的LCA，纯粹是怕dalao太快AK闲着无聊，后来发现前面的trick耽误了选手太多时间，而且4小时12题确实是太多了……

以上是我们出题时的想法，而最后的Board也不算难看，对于一些不合理的地方，我们今后会吸取经验并改正。

### A. 捍卫彩虹岛 `签到`
题意：给8个整数$Lv_{i}$，输出$\left \lfloor \frac{\sum_{i = 1}^{8}Lv_{i}}{8}  \right \rfloor$。
解析：int直接就向下取整了。


### B.恐高的单身老柴犬 `暴力`
题意：给n级台阶的绝对高度$h_{i}$（递增），以及一个容许高度x，一个人可以走到小于等于x的最高位置，然后用道具飞到楼梯顶端，问飞行最小高度。
解析：扫到小于等于x的最大高度，与最后一级台阶高度做差即可。
吐槽：数据中没有x大于最后一级台阶的情况……有人以为楼梯是相对高差……


### C.彩虹岛电车 `暴力`
题意：给长度为n的数列a[]，问(a[l] + a[r])%5=0的二元组(l, r)对数，其中l$\leq$r。
解析：O（$n^2$）扫一遍即可。


### D.卡片游戏 `贪心`
题意：n张大写字母卡片选k张，使得$\sum_{i = 1}^{k} f_{i}$最大，其中$f_{i}$为k张卡中与第i张卡片字母相同的卡片数目。
解析：统计每个字母的卡片数目，贪心从卡片数目最多的字母开始取k张即可。
吐槽：萌新多是卡排序，不会sort、qsort，然而字母数少可以暴力排。


### E.无尽拼图 `坑人`
题意：给一个部分缺失的整数矩阵，问是否存在一种填数方案使得该矩阵是矩阵$a_{ij} = i + j - 1（i， j \geq 1）$的子矩阵。
解析：若全部为0则必然可以；否则找到第一个非零位置，即可填完所有数，并检查是否是$a_{ij} = i + j - 1（i， j \geq 1）$的子矩阵。坑点在于填完数的矩阵中是不能有0与负数的。
吐槽：毒瘤出题人：“我觉得这道题是出的最好的。”


### F.通往彩虹岛的石头门 `几何`
题意：两个宽W高H的矩形重叠放置，其中一个绕形心顺时针旋转$\alpha$角，问旋转后两个矩形的重叠面积。
解析：为了避免过多的分类，我们可以先去除一些情况。
> * 对于H>W的情况，我们可以将两个矩形旋转90度，即交换W和H，不影响旋转后的相交面积，因此之后仅讨论H$\leq$W的情况。
> * 对于$\alpha > 90^{\circ}$的情况，考虑轴对称，可以将$\alpha$转变为$180^{\circ} - \alpha$，故之后只需要考虑$\alpha \leq 90^{\circ}$的情况。

为了方便叙述，我们令$\beta = arctan(\frac{H}{W})$，即$\beta$为矩形对角线与长边的夹角。
在考虑完上述两点之后，仍然有两种情况需要讨论：

> * $\alpha > 2 \beta$，这种情况较为容易，此时相交部分为一平行四边形，面积即为底乘高，结果即为$\frac{H^{2}}{\sin\alpha}$。
> * $\alpha \leq 2\beta$，即题目附图的情况，按下图设变量解二元一次方程组：
$$
\left\{
\begin{aligned}
\frac{y}{\tan\alpha} + \frac{y}{\sin\alpha} + x & =  W \\
\frac{x}{\tan\alpha} + \frac{x}{\sin\alpha} + y & =  H 
\end{aligned}
\right.
$$
解完方程用矩形减去三角形面积即可。

![Door](http://p1.bpimg.com/1949/d9f7752270d9009a.png)

### G.兔兔的纠纷 `数学` `题意杀`
题意：记斐波那契数列为f[],其中f[0]=f[1]=1,对于i>1有f[i]=f[i-1]+f[i-2]。已知在第k年，年龄为i的兔子数目为2f[k-i]，若两只兔子年龄和为k，会发生一次纠纷。T次询问，第k年兔子间共发生多少次纠纷（$T, k \leq 200000$）。
解析：记$g[k] = \sum_{i = 0}^{k} f[i] \cdot f[k-i]$，则答案即为：
$$ans[k] =
\left\{
\begin{aligned}
2g[k] & , & odd \\
2g[k] - f[k/2] & , &even 
\end{aligned}
\right.
$$
问题转化为求$g[]$数组，
$$
g[k] - g[k-1] = \sum_{i = 0}^{k-1} f[i] \cdot (f[k-i] - f[k-1-i]) + f[k]\\
= \sum_{i = 0}^{k-2} f[i] \cdot f[k-2-i] + f[k]\\
= g[k-2] + f[k]
$$
即$g[k] = g[k-1] + g[k-2] + f[k]$，先预处理递推$f[]$再递推$g[]$即可，时间复杂度$O(T+k)$。
吐槽：全没看到只生两年……斐波那契数列不叫兔子数列吗？


### H.七彩原石 `回文串` `暴力`
题意：求压缩串的最长回文子串。
解析：类似于求普通串最长回文子串的枚举回文中心并向左右扩展的方法，在扩展的时候分三种情况：
> * 颜色相同，且长度相同，继续向两边扩展。
> * 颜色相同，但长度不同，两端取min切断，并停止扩展。
> * 颜色不相同，直接停止扩展。

单组时间复杂度$O(n^2)$。
吐槽：命题的时候想了要不要卡$O(n^3)$的做法，但是发现比$O(n^2)$还难写，大家也可以想想马拉车什么的怎么写。

### I.机器人小队 `二分`
题意：将一个长度为n的序列划分成连续且非空的m段，设第$i$段的和为$S_i$，求使得max{$S_i$}最小的划分方案，多种情况时要求越靠前的段数字尽量少。
解析：先求解最小的max{$S_i$}，可以假设max{$S_i$}$\leq x$，来判断这种情况是否成立：对于一个x，我们可以求出在每段和不超过x的情况下所需要的最少划分数k，如果k＞m，肯定不成立，反之成立。显然x与k满足单调性，故可以用二分求解最小的x。
之后考虑方案输出，只需从后往前依次给每一段放总和小于等于max{$S_i$}的数即可，但需要注意的是每一段非空这一条件。
吐槽：输出略鬼畜，场上似乎出现了PE判WA的情况，致歉。

### J.藏宝图 `BFS` `RoyYuan`
题意：给一个有障碍的$m \times n$迷宫，起点S，终点T，地图上障碍每间隔k秒会打开一次，问S能否到达T以及所需最短时间。
解析：普通的迷宫题直接用二维状态(x, y)表示位置来BFS即可。本题不同的是，障碍每隔k秒会开一次，故需多标记一维时间状态。对于同一个点(x,y)来说，t秒和t+k秒表示的状态是相同的，所以新加的维度只需要k的大小就足够，转移的时候按时间的不同讨论能否经过障碍即可。当然也可以从分层图角度来理解。
吐槽：不能因为RoyYuan超可爱就欺负他呀。

### K.书人 `LCA`
题意：一个栈支持三种操作：
> * 1 push（x） 
> * 2 pop（） 
> * 3 退回第t次操作结束后的版本

对于每个操作3回答本次操作最少可以看成是由多少次操作1/2组成的。
解析：栈要可持久，建树即可：维护一个当前位置指针pos，push把pos移向儿子（没有这个儿子则需加叶子），pop把pos移向父亲。先做完所有操作把树建完，每个操作3询问的即为树上距离，故离线LCA即可。
吐槽：因为是先想好做法再套题，所以可能会被什么简单做法艹掉，欢迎dalao讨论。

### L.大魔王的魔咒 `构造` `猜结论`
题意：给L个左括号与R个右括号，构造一个串使得合法括号子串最多，输出个数。
解析：显然括号要成对，故取x = min（L,R）对括号即可，多余的没有用处。最优的构造方案为（）（）（）……即x对括号并排放，答案即为$\frac{x \cdot (x + 1)}{2}$。
> 证明：
> 1.合法括号子串的上界是$\frac{x \cdot (x + 1)}{2}$
    合法括号子串的长度必然是偶数，对于长度为2x的串，将其长度为偶数的子串一共有$x^2$个，可以将其分为三类：

> * 左端点l为奇数，且右端点为2x，有$x$个。

> * 左端点l为奇数，且右端点不为2x，有$\frac{x \cdot (x-1)}{2}$个。

> * 左端点l为偶数，有$\frac{x \cdot (x-1)}{2}$个。

> 注意到对于一个子串[l, r]如果它是合法括号序列，则其最左端必然是“（”，最右端必然是“）”，故[l+1, r+1]必然不是合法括号序列。在上述的3类子串中，第2类与第3类可以建立一个[l, r] $\leftrightarrow $[l+1, r+1]的双射关系。也即是说，只要第2类中有一个子串是合法括号序列，对应的第3类中有一个子串必然不是合法括号序列，故这两类中的合法括号序列之和不会超过$\frac{x \cdot (x-1)}{2}$，因此所有合法括号序列总和不会超过$\frac{x \cdot (x+1)}{2}$

> 2.存在一种构造使得合法括号子串数目为$\frac{x \cdot (x+1)}{2}$。
显然并排放（）（）（）（）……即是。
证毕。

吐槽：欢迎其他证明，可以思考对应的子序列的问题。
