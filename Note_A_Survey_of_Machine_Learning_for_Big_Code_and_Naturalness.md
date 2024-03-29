# A Survey of Machine Learning for Big Code and Naturalness

在程序验证、错误发现和重构方面，需要软件工具以达到：降低软件复杂性、帮助构建更好的软件 的目的。

借助开源软件的数据（代码&更改&debug&审查）（Big Code），从中发现好的模式（reliable, easy to read, and easy to maintain）。

naturalness hypothesis：

- 自然性假设
- 软件是一种人类交流的形式
- 软件语料库和自然语言语料库的统计特性相似
  - n-gram语言模型展现相似性
- 编码是一种通信行为，大型代码语料库具有丰富的模式
- 因为程序猿更愿意写和读熟悉的代码，所以可以进行预测

用概率，量化得到预测概率。

代码两个渠道：人类&计算机

代码&自然语言不同性：

- 可执行性
  - 互相转换（图灵完备的语言之间）
- 形式化
  - 可重用性
- 跨渠道互动
  - 无法将代码单元映射到文本单元
  - 如变量名函数名的长度也没啥用
  - 自然语言的二义性

概率模型

- Code-generating Models代码生成模型：随机
  - 用训练数据、输出代码表示和上下文训练，得到概率分布，也可以用这个分布来评分
  - 不同级别：token级别、句法层面的树、语义层面的图
  - token级别
    - n-gram模型：用n-1个预测
      - 未出现得到0概率，解决：用平滑方法，用长度更小的字串获得信息
      - 更长的代码，可能丢失信息：解决：从生成的序列提取信息作为辅助信息
      - 局部性：可以添加缓存，近期的token概率更高
    - RNN：按照顺序预测，但不是使用分布式向量表示来表示上下文
      - 隐藏状态针对一个更长的上下文环境
      - 可以学习更丰富的跨上下文信息，如处理不同变量名但同样功能的
  - 句法（树）：
    - 能构造语法正确的代码
    - 上下文中包含已经生成的树
    - 计算成本相对较高
  - 语义（图）：
    - 没有自然的起点或者生成过程，所以是困难的
  - 不同类型（根据上下文的使用）：
    - 语言模型：不使用上下文
      - 交叉熵/字错误率度量误差
    - Code Transducer Models代码转换模型
      - 统计机器学习（SMT）启发，直接映射
    - Multimodal models多模型模型
      - 代码&非代码形式，通过中间表示
- Representational Models of Code代码的表示模型：用上下文的条件概率
  - 分布式表示
  - 结构化预测：给定输入特征向量，预测相互依赖的变量
- Pattern Mining Models模式挖掘模型：无监督推断出代码中的结构
  - 发现可解释的模式

应用

- 推荐系统：代码补全&推荐
- 推断Coding Conventions代码编程风格
- 代码缺陷
  - 从不同的抽象级别入手（如token、api）
- 代码翻译、复制、克隆
- 代码&文本互相转换
- 搜索
- 程序合成
- 程序分析
  - 提取语义属性

挑战&未来

- 引入机器学习处理，应对不确定性、模糊性或者避免硬编码启发式方法
- 新领域：
  - debug
  - 可追溯
  - 代码完成/合成
  - 教育
  - 辅助工具：改进与计算机交互方法