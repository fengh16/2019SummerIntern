# When deep learning met code search

综述

- NCS（无监督，只用code）、CODEnn、SCS、UNIF等（后面几个有监督，UNIF基于NCS）的描述
- 自然语言输入，返回片段
- 找到映射的方法（描述&代码）
- 无监督不好，不是越深越好，人工描述比docstring有时要好

NCS：

- fastText得到嵌入矩阵
- code：token的average

SCS：

- code训练一个encoder
- GRU：code到docstring
- LSTM得到encoder和decoder

