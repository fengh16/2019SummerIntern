# Maybe Deep Neural Networks are the Best Choice for Modeling Source Code

OOV：out of vocabulary，对代码预测生成代码token，如果原本没有这个token，就不能生成

subword unit：将方法名分开成不同的词

方法：

- RNN模型变体GRU，需要处理输入（分割成subword unit）
  - 先在输入解析出的token中间加上`</t>`进行分隔，之后将token全部拆成一个个字母，作为最初始的输入
  - 可能有一些非单词的结果，如把setter分开成为set和ter
  - 生成subword unit的过程：考虑相邻连续字符在整个序列中出现的次数->出现次数最多的符号对则说明是在同一个单词内部的->合并
    - 终止条件：设定的merge次数
  - 预测：前k个最好的token（不是unit）
    - candidate：最好的subword unit
    - 拿出最好的candidate之后进行extend
  - 新的project：Dynamic adaptation：
    - 在原来（一个global的）的基础上，新的project作为输入，进行训练

