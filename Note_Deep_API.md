# Deep API

动机：要了解API的用法，需要获取API的使用顺序。

问题：直接将查询语句看作离散的单词的组合，没有对输入语义的整体理解。

其他人给出的解决方案：

- SWIM：
  - 通过word alignment model查询对应的API并且找API序列
  - 问题：不考虑词之间的关系，如：int转string和string转int的区别

语言模型：

- 第一篇文章（A Survey of Machine Learning for Big Code and Naturalness）中提到的naturalness自然性，将代码看成是语言，以及语言模型的概率模型。n-gram表示长度为n的连续的单词，即通过前n-1个推测第n个
- 神经语言模型：单词序列的长度不限（n-gram的参数n是固定的）

模型：RNN。

- 输入层、循环隐藏层、输出层
- RNN Encoder-Decoder模型

  - 两种语言：source&target
  - 给出source的序列，得到target的序列
  - 一个固定长度的上下文向量作为转换的中介，将过程分成两个部分，分别是一个RNN
  - 第二阶段的过程是直接用上下文向量和已经生成的目标序列部分来生成的
  - source：用户输入的查询；target：目标的API序列
- 可以使用词的上下文向量，记录上下文信息以避免单独处理各个单词
- attention-based RNN Encoder-Decoder模型：

  - 用于解决查询的不同部分对于目标序列的不同部分API的重要性问题
    - 如：保存word文件中需要打开和关闭文件，这些操作不是很重要
  - 不是用相同的上下文向量，用所有的隐藏状态加权求和，用权重（隐藏状态和目标词之间的）来解决此问题
- Enhancing RNN Encoder-Decoder Model with API importance
  - 目标序列中API的重要性不同，比如一些经常出现的API不是很重要

Deep API：

- 离线训练&在线翻译两个阶段
- 训练过程的输入：
  - 语言：JAVA
  - 数据筛选：有star，有文档注释并且筛选掉一些不规则的注释
  - API序列获取：用JDT编译器解析成AST，所有API都是记录成对于类的方法调用，包含instance创建、参数构造的函数过程。if和while直接将对应的语句接起来
  - 注释取文档注释第一句
  - 最常用的10000个单词
- 翻译阶段：用Beam search
  - 最后的结果是多个可能的序列
  - 查找序列的时候是一个树状结构，每一个高度中的元素都保留若干个可能的结果（只是一种剪枝策略，在生成的过程中就剪枝，有点类似贪心？）
- 评估
  - BLEU：评估生成的API序列的准确程度
    - 通过对于子序列n-gram的分析得到，看结果（candidate）的长度为n的子序列里面有多少个在正确结果（reference）里面，所以是reference的除以candidate的
    - BP是对reference的长度过长时候的一个惩罚，以避免在candidate比较短的时候使得上面的结果很大（这样的话可能所有的candidate里面的东西都能出现
  - 人类评估：
    - 第一个相关结果的排名
    - 相关结果占到所有给出结果的百分比
- 讨论：
  - 连续的语义空间，语义相似则有相似的向量表示
  - 使用的是序列
  - 通用模式而非特定样本，decoder本身就是语言模型

