---
title: ARTS第二周（2019年12月23日~29日）
date: 2019-12-29T17:23:08+08:00
slug: week-002
---

## Algorithm

### 隐马尔可夫模型（Hidden Markov Model，HMM）{#algorithm-hmm}

#### 算法简介

在认识这个算法前，我对于序列比对算法和序列相似度搜索算法的理解，只停留在needle/water和blast这几个工具上。也正是在罗静初老师开设的[ABC（应用生物信息学技术）](http://abc.cbi.pku.edu.cn/)课程上，我在掌握前面几个工具后，紧接着接触到了[HMMER](http://hmmer.org/)这个序列搜索工具，也了解了隐马尔可夫模型可以用在序列搜索上，与大名鼎鼎的blast算法起到类似的作用。

如今回过来再看，就能理解隐马尔可夫模型，的确是动态贝叶斯网络的一个简化特例。其概率网络定义了一台状态机在不同状态之间跳转的概率，每个时刻机器只处于其中一个状态，我们需要做的，是根据观察到的某个数据的序列，来推断相应的状态变化的序列。这个模型在一开始看的时候，感觉是非常复杂的，而在理解背后的运行原理和状态机的转移概率矩阵等定义后，就能很直观地理解，所有序列，都是在这个网络上不同路径的游走，只要穷举所有路径，计算相应的概率，最后找到某个概率最大（即最有可能导致目标结果被观察到）的那条路径即可。具体的计算，有前向算法和后向算法等，都是在为了求解这个“穷举”优化的问题。

#### 算法应用

隐马尔可夫模型在生物信息领域里的应用很多。在《An Introduction To Bioinformatics Algorithms》一书中，第11章介绍HMM，给的就是预测（或者说识别）某个序列中的CpG岛（CpG Island）。这是一个很简化但又典型的HMM应用场景。定义两种状态：“在CpG岛中”和“不在CpG岛”。然后整个序列从前往后滑动，就判断其相应的状态是否发生变化。

维基百科上还给出了[更多的应用场景](https://en.wikipedia.org/wiki/Hidden_Markov_model#Applications)，其中与生物信息直接相关的包括：

* Single-molecule kinetic analysis
* Gene prediction
* Alignment of bio-sequences
* Protein folding
* Sequence classification
* Metamorphic virus detection
* DNA motif discovery
* Chromatin state discovery

#### 参考

* <https://en.wikipedia.org/wiki/Hidden_Markov_model>
* <http://hmmer.org/>
* <https://en.wikipedia.org/wiki/HMMER>
* [一文搞懂HMM（隐马尔可夫模型）](https://www.cnblogs.com/skyme/p/4651331.html)
* [隐马尔可夫模型（HMM）攻略](https://blog.csdn.net/likelet/article/details/7056068)
* [HMM——前向算法与后向算法](https://blog.csdn.net/zb1165048017/article/details/48577891)

---

## Resource

### MANE Project {#resource-mane-project}

#### 简介

MANE 是 Matched Annotation from NCBI and EBI 的缩写。

做生物信息的，都会了解，对基因突变/表达等数据结果的功能注释，采用NCBI RefSeq数据库，和采用EBI Ensembl数据库，得到的结果，往往会有很大的差异，不仅数据量差异大，而且两者采用的编号系统都不同。主要原因在于两个数据库的原始数据收集策略上存在差异。NCBI RefSeq会采用人工审核的方式，因此从准确度上会更有保证。而EBI Ensembl有大量计算预测结果，虽然准确度上有所牺牲，但全面性上更有优势。但这两个数据库的差异，导致了使用上普遍存在的困惑。而MANE这个项目，就是要设法解决这个问题，提供一套兼容两者、统一的注释结果。更准确说，该项目主要是针对蛋白编码基因，提供在5'-UTR、CDS、3'-UTR的信息上，RefSeq与Ensembl保持一致的转录本，并给它们分配一个统一的ID（原各自ID也保留）。

我对这个项目的了解，始于2018年12月，NCBI 和 EBI 联合举办的一个专门介绍该项目的网上 Webinar。下面是相应的幻灯片（我一时找不到原始下载链接，就把文件先放到百度网盘，供需要的同学自取；若有侵权，请告知删除）：

* [MANE\_webinar\_1-1\_Aims\_and\_Goals.pdf](https://pan.baidu.com/s/1ijwVuPF-HctPHinKgXJ1kg) *（提取码: ixs6）*
* [MANE\_webinar\_1-2\_Methodology.pdf](https://pan.baidu.com/s/14qTTn0jS_o3fu3b83--Nxw) *（提取码: t1f4）*
* [MANE\_webinar\_2-1\_Deeper\_dive\_methodology.pdf](https://pan.baidu.com/s/1NMypA7OgIfLmWr898k7zxA) *（提取码: gxxn）*
* [MANE\_webinar\_2-2\_Progress\_and\_future.pdf](https://pan.baidu.com/s/11G3XM8_QXaYafknjuW5gLA) *（提取码: qg83）*
* [MANE\_webinar\_2-3\_Sequence.pdf](https://pan.baidu.com/s/1qaSIl_8npKLDn8p36Sa3Zw) *（提取码: hf5v）*
* [MANE\_webinar\_2-4\_LRG.pdf](https://pan.baidu.com/s/1iLVUcBfbBvPgHGgmznsvjw) *（提取码: rg9f）*
* [MANE\_webinar\_2-5\_Access\_and\_Display.pdf](https://pan.baidu.com/s/1LqVXXfo4hvbXwiTzG5oi5w) *（提取码: ry1y）*

#### 当前状态

根据[NCBI网站](https://www.ncbi.nlm.nih.gov/refseq/refseq_select/#relationship-between-refseq-sele)上提供的信息：

> Currently, the MANE Select is a beta set that covers over 60% of the protein-coding genes. NCBI and EBI will add to the set in the next year with the goal of achieving close to 100% coverage of protein-coding genes.

在[MANE主页](https://www.ncbi.nlm.nih.gov/refseq/MANE/)，对这些信息做了详细说明，其MANE转录本集合，会分成三类：

* **MANE Select**: One high-quality representative transcript per protein-coding gene that is well-supported by experimental data and represents the biology of the gene.
* **MANE Plus**: A minimal set of well-supported transcripts that have additional characteristics, such as significant novel exons, which are not included in the MANE Select transcript.
* **MANE**: All other matched transcripts that are not included in the Select and Plus sets.

#### 参考

* <https://www.ncbi.nlm.nih.gov/refseq/MANE/>
* [Ensembl: Our new joint transcript initiative: The Matched Annotation from the NCBI and EBI (MANE) project](http://www.ensembl.info/2018/10/12/our-new-joint-transcript-initiative-the-matched-annotation-from-the-ncbi-and-ebi-mane-project/)
* <http://grch37.ensembl.org/info/genome/genebuild/mane.html>
* [NCBI Insights: Matched Annotation by NCBI and EMBL-EBI (MANE): a new joint venture to define a set of representative transcripts for human protein-coding genes](https://ncbiinsights.ncbi.nlm.nih.gov/2018/10/11/matched-annotation-by-ncbi-and-embl-ebi-mane-a-new-joint-venture-to-define-a-set-of-representative-transcripts-for-human-protein-coding-genes/)
* [NCBI Insights: MANE Select v0.5 is now available!](https://ncbiinsights.ncbi.nlm.nih.gov/2019/03/12/mane-select-v0-5/)
* [NCBI Insights: New human genome annotation release with MANE Select and other improvements!](https://ncbiinsights.ncbi.nlm.nih.gov/2019/07/03/new-human-genome-annotation-release-with-mane-select-and-other-improvements/)
* <https://www.ncbi.nlm.nih.gov/refseq/refseq_select/#The>

---

## Technology

### 免疫细胞治疗中的基因编辑 {#technology-gene-editing-for-immune-cell-therapies}

#### 简介

这一节的学习笔记，主要来自新发表在《[NBT](https://www.nature.com/nbt)》上的一篇综述《[Gene editing for immune cell therapies](https://doi.org/10.1038/s41587-019-0137-8)》。

这是关于近两年比较火热的CAR-T技术的综述。这是一种将免疫T细胞在体外进行遗传改造后，使其能够表达特定的嵌合抗原受体（chimeric antigen receptor，缩写为CAR），重新输回体内，它能靶向B细胞的CD19抗原，从而对于B细胞恶性肿瘤患者有较好的临床疗效。

这篇文章从如下几个方面，对相关领域做了综述：

* CAR-T cells for cancer
* Innovations in antigen receptors and second transgenes
* Innovations in gene transfer and gene editing
* Off-the-shelf engineered T cells
* Engineering natural killer cells and macrophages
* Engineering hematopoietic and non-hematopoietic stem cells
* Immune-cell engineering beyond cancer

#### 参考

* [Nature Biotechnology: Gene editing for immune cell therapies](https://doi.org/10.1038/s41587-019-0137-8)
* <https://baike.baidu.com/item/CAR-T>

---

## Statistics

### 最小二乘法（Least Square Method） {#statistics-least-square-method}

#### 简介

最小二乘法是统计学里很基础的一个方法。我最早对它的理解，仅仅是在做线性回归拟合时的一种计算方法而已。直到后来，在研究生期间，听夏旭华老师来北大上的一门分子进化课程，让我对这个方法有了完全不同的感受。与我此前接触的其他分子演化课程和书籍不同，在这门课程上，夏老师首先从最小二乘法讲起，然后从简单到复杂的一系列分子演化相关计算，竟然都无一例外是从这套方法推演出来的，直观展示了最小二乘法作为一种优化工具的便利和高效。

知乎上看到一段引文：

> 最小平方法是十九世纪统计学的主题曲。  
> 从许多方面来看，它之于统计学就相当于十八世纪的微积分之于数学。
>
> <div style="text-align:right">-- 乔治·斯蒂格勒的《The History of Statistics》</div>

越发感觉这个方法真可谓“神圣”。

#### 我的理解

最小二乘法想要解决的问题，其实是一个最优化的问题：对某种观测进行测量或估算，由于各种随机因素的影响，可能会有很多中不同的估计值，于是要设法从中挑选出一个“最好”的估计值。一个最直接的想法就是，计算估计值与实际值之间的差异（绝对值）的累加，并最小化这个差异和。然而，这种计算方法，对所有数据都“一视同仁”，对于误差较大的取值，惩罚不够大，很容易造成在一段区间内无法区分出优劣。于是，自然而然就可以想到采用平方（即二乘）的方法，从而让误差大的数据具有更大的权重，需要优先去做“优化”，降低其影响。

#### 计算过程

既然是求最小化的参数，那么就可以把方程列出来之后，求偏导数，并解偏导数等于0的参数，就能得到期望估计的参数值。

以下是R语言示范的最小二乘法计算过程（其中数据来自[维基](https://zh.wikipedia.org/zh-hans/%E6%9C%80%E5%B0%8F%E4%BA%8C%E4%B9%98%E6%B3%95)，计算过程代码参考[SegmentFault帖子](https://segmentfault.com/a/1190000019299965)）：

```r
# 输入数据
> x <- 1:4
> y <- c(6,5,7,10)
```

```r
# 基本计算
> mean(x * y)  # xy的均值
[1] 19.25
> mean(x) * mean(y)  # x的均值，乘以y的均值
[1] 17.5
> mean(x^2)  # x的平方的均值
[1] 7.5
> mean(x)^2  # x的均值的平方
[1] 6.25
```

```r
# 参数计算
#   分母：xy的均值，减去x的均值乘以y的均值
#   分子：x平方的均值，减去x均值的平方
> m <- (mean(x*y) - mean(x)*mean(y)) / (mean(x^2) - mean(x)^2)
> c <- mean(y) - m * mean(x)
```

```r
# 拟合结果
> cat("y = ", m, " * x + ", c, "\n", sep = "")
y = 1.4 * x + 3.5
```

#### 参考

* [知乎：最小二乘法的本质是什么？](https://www.zhihu.com/question/37031188/answer/411760828)
* <https://en.wikipedia.org/wiki/Least_squares>
* <https://en.wikipedia.org/wiki/Ordinary_least_squares>
* <https://zh.wikipedia.org/zh-hans/%E6%9C%80%E5%B0%8F%E4%BA%8C%E4%B9%98%E6%B3%95>
* <https://my.oschina.net/keyven/blog/526010>
* <https://www.cnblogs.com/pinard/p/5976811.html>
* <https://baike.baidu.com/item/%E6%9C%80%E5%B0%8F%E4%BA%8C%E4%B9%98%E6%B3%95>
