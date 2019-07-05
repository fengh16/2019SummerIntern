# README

## 实验记录

代码来源https://github.com/hamelsmu/code_search

#### 实验环境

- MacOS 10.14.5，8GB RAM
- Python 3.7.3

#### 实验步骤

1. 安装docker(`brew cask install docker`)，之后打开启动台里面的docker
2. `docker pull hamelsmu/ml-cpu`
3. `docker run -it -p 233:233 hamelsmu/ml-cpu bash`启动
4. jupyter启动：启动docker之后`jupyter notebook --allow-root --no-browser --port 233 --ip=0.0.0.0`启动，复制网址到自己电脑的网页浏览器后将ip换成127.0.0.1就可以打开

