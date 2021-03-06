#MagicMolecule
> 来源：TC SRM 571 Div1 500
> 
> 作者：孙耀峰
> 
> 修改：
> 
> 关键词：带权最大团，搜索，剪枝

##题目简介
给出$$N$$个点的无向图，每一个点有权值$$A_i$$。要求找出一个$$M$$个点的团，满足$$3M \geq 2N$$，使得权值和最大。

团的定义为，一个点集，使得两两点对之间都有边。

范围：$$N \leq 50$$，$$A_i \le 100000$$。
##解题思路
因为最大团问题是$$NP$$问题，而这道题的$$N$$又比较大，不能用一些暴力的通用方案解决，所以考虑利用题目的性质来解题。
###算法一
这道题比较奇怪的限制就是$$M \geq \frac{2}{3} N$$。容易发现，如果一个点的度数不足$$\frac{2}{3}N$$，则这个点不可能在答案里，这也就意味着度数满足要求的点构成的图，必然是非常稠密的。

所以有一个朴素的想法，就是暴搜+剪枝。我们可以把所有点按照权值从大到小排序，然后依次枚举每个点是否选择。加入一些剪枝就可以通过此题，具体剪枝如下：

- 用一个bitset记录剩下哪些点与之前已经选择的点之间都有边。如果bitset中所有点全部选上，还不足以构成一个可行解，则剪枝；
- 令$$s$$表示bitset中合法的点数，因为按照权值从大到小排序，所以如果令$$s$$个点权值全为剩下的权值最大的点，还是没有当前答案大，则剪枝；
- 还有一些无足轻重的剪枝，诸如DFS时优化搜索的顺序，以及一些更加宽泛的限制来判断是否有解，可以详见我的代码。

###算法二

看了TC的官方题解后发现一种另外的方法，主要思路还是搜索。

容易发现，对于每一条原图中不存在的边，这条边的两个端点必然至少有一个点不被选择。基于贪心的想法，在处理这条边的时候，两个点都不选是不优的。

当$$N=50$$时，最多不选$$17$$个点，所以搜索的分治是非常少的。这种方法似乎不用加什么剪枝就可以通过此题了。具体的复杂度我不会证，有感兴趣的老司机可以帮我证证。

