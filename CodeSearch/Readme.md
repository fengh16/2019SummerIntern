# README

## 实验记录

代码来源https://github.com/hamelsmu/code_search

#### 实验环境

- MacOS 10.14.5，8GB RAM
- Python 3.7.3

#### 实验步骤（docker）

1. 安装docker(`brew cask install docker`)，之后打开启动台里面的docker
2. `docker pull hamelsmu/ml-cpu`
3. `docker run -it -p 233:233 hamelsmu/ml-cpu bash`启动（注：之前试了6666端口不行，浏览器不能访问，可能是macos的设置？）
4. 获取代码：在docker中`git clone https://github.com/hamelsmu/code_search`
5. jupyter启动：启动docker之后`jupyter notebook --allow-root --no-browser --port 233 --ip=0.0.0.0`启动，复制网址到自己电脑的网页浏览器后将ip换成127.0.0.1就可以打开
6. 第一个（`1 - Preprocess Data`）：
    1. 减少数据量：手动下载数据集之后缩减，放到了https://raw.githubusercontent.com/fengh16/2019SummerIntern/master/CodeSearch/test_little.csv，可以把对应的获取数据集的代码改掉（改成`df = pd.read_csv(f'https://raw.githubusercontent.com/fengh16/2019SummerIntern/master/CodeSearch/test_little.csv')`）
    2. 运行代码前的操作：新建目录：`data/processed_data`
    3. 直接执行所有代码块就可以跑通第一个
7. 第二个（`2 - Train Function Summarizer With Keras + TF`）
    1. 安装没有的库tensorflow、annoy：直接pip安装（`pip install XXXX -i https://pypi.tuna.tsinghua.edu.cn/simple`）
    2. 调小seq2seq这里的batch_size：（改为100）避免内存不足
