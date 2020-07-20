# RNA seq数据分析素材

生信技能树的B站资源：https://space.bilibili.com/338686099

## Linux初步

### Linux 基础
一言以蔽之：从Windows的图形界面过渡到Linux的命令行操作！
> * [菜鸟教程：Linux 教程](https://www.runoob.com/linux/linux-tutorial.html)
> * [知乎：Ubuntu学习资源](https://www.zhihu.com/question/19816319)

### Git使用
> * [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
> * [菜鸟教程Git](https://www.runoob.com/git/git-tutorial.html)

### Docker使用（进阶）
> * [菜鸟教程Docker](https://www.runoob.com/docker/docker-tutorial.html)
> * [Docker官方说明](https://docs.docker.com)

### R 语言使用
R 的使用主要分三大块：1.统计分析与数值计算；2.数据可视化；3.生物信息工具使用。下面分享一些有意思的资源：
> [生物信息学R语言入门](https://qiubio.com/new/book/)
> [R的极客理想系列文章](http://blog.fens.me/series-r/)

### Python 使用

## Bulk RNA数据分析

### RNA seq数据分析基础知识

> * [菜鸟入门(一)：RNAseq测序基础简介](http://www.biotrainee.com/thread-984-1-9.html) RNAseq简介，太简略了
> * [Reference-based RNAseq data analysis (long)](https://galaxyproject.github.io/training-material/topics/transcriptomics/tutorials/rb-rnaseq/tutorial.html) 英文版的RNA seq流程解析。讲的比较详细，但未给代码
> * [RNA-seq Tutorial (with Reference Genome)](https://bioinformatics.uconn.edu/resources-and-events/tutorials-2/rna-seq-tutorial-with-reference-genome/#) 也是英文版，给出了部分关键代码

### RNA seq：从分子生物学基础到生物信息学流程理解

这一部分，非常重要的一个知识点，就是让学生们明白，RNA到底是怎么回事：它是怎么被转录的？为何真核生物中的RNA序列向基因组比对的时候是不连续比对？RNA分析工具如何去描述RNA转录的一系列生理过程的？我一直在寻找一些从RNA转录的分子生物学到GTF文件结构解释的文章，但是没找到。考虑这一块我要费点心思自己编写了。
> * [徐洲更简书：转录组入门（4）：了解参考基因组及基因注释](https://www.jianshu.com/p/3e545b9a3c68)
> * [知乎：转录组入门4-参考基因组、注释文件下载及IGV](https://zhuanlan.zhihu.com/p/28126314)

### RNA 基因表达谱后续各种分析

RNA分析一多半分析是围绕表达谱进行的。这部分的资料数不胜数，而这部分由跟R的使用有千丝万缕的联系，这里不再赘述了。

### RNA seq分析全流程

> * http://www.rna-seqblog.com

> 生信技能树资源
> * [PANDA姐的转录组入门（0-6）合辑](http://www.biotrainee.com/thread-1966-1-1.html)
> * [配套视频讲解](https://mp.weixin.qq.com/s/lCMM31GQ6l8aAXFEZKHmcg?)
> 
> 这套讲解有助于了解RNA seq的分析思路，但是里边使用的部分工具已经过时，该升级了。

> GRIFFITH LAB的培训教程
> * [培训主页](https://rnabio.org/course/)
> * [GitHub](https://github.com/griffithlab/rnaseq_tutorial)
>
> 英文版的教程，但是思路也比较清晰

## Single cell RNA数据分析

### scRNA全流程

单细胞分析的关键，主要是理解文库构建的策略，以及在文库构建的基础之上，哪些信息能够获得，哪些信息不易获得

> * [Single-cell RNA-seq analysis workshop](https://github.com/hbctraining/scRNA-seq) 来自哈佛的scRNA教程
> * [Analysis of single cell RNA-seq data](https://scrnaseq-course.cog.sanger.ac.uk/website/index.html) 剑桥桑格中心的scRNA教程
> * [刘小泽的简书](https://www.jianshu.com/u/d7b77c171c15) 单细胞交响乐系列，2020年7月刚刚大规模更新

### scRNA定量基础上的分析

主要围绕scRNA分析的三大R包展开：Seurat，Scater和Monocle。
