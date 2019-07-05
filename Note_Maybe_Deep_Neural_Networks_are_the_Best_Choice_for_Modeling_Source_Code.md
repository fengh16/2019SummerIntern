# Maybe Deep Neural Networks are the Best Choice for Modeling Source Code

OOV：out of vocabulary，对代码预测生成代码token，如果原本没有这个方法名，就不能生成

subword unit：将方法名分开成不同的词

方法：

- RNN模型变体GRU，需要处理输入（分割成subword unit）
  - 可能有一些非单词的，如把setter分开
  - 生成subword unit的过程：考虑相邻连续字符在整个序列中出现的次数->合并
    - 终止条件：不同的merge次数
  - 预测：前k个最好的token（不是unit）
    - candidate：最好的subword unit
    - 对于常数类型的token（比如可以考虑只对函数进行预测）？
  - 新的project：Dynamic adaptation：
    - 在原来（一个global的）的基础上，新的project作为输入，进行训练

