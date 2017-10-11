## tmux

## 说明

    tmux是一个优秀的终端复用软件，类似GNU Screen，但来自于OpenBSD，采用BSD授权。使用它最直观的好处就是，通过一个终端登录远程主机并运行tmux后，在其中可以开启多个控制台而无需再使用更多的SSH会话来连接这台远程主机；其功能远不止于此。

## 地址

- https://github.com/mxgnene01/m-tmux

## 安装

###  基础组件

```shell
# mac
$ brew install tmux
$ brew install reattach-to-user-namespace

# ubuntu
$ sudo apt-get install tmux
```

#### 配置

```shell
$ curl 'https://raw.githubusercontent.com/mxgnene01/m-tmux/master/tmux.conf' > ~/.tmux.conf

or

$ git clone git@github.com:mxgnene01/m-tmux.git
$ ln -s $PWD/m-tmux/tmux.conf $HOME/.tmux.conf
```

## 使用

> tmux -> session -> window -> pane

### 设置新前缀

```
PREFIX = Ctrl-x
```

### session

#### 创建session

```
$ tmux new -s session_name
```

#### 在tmux 中创建一个新的session

```
[PREFIX-:] new -s session_name
```

#### 退出tmux

```
[PREFIX-d]
```

#### 查看已有的session list

```
$ tmux ls
```

#### 连接已有的session

```
$ tmux a
```

#### 切换多个session

```
[PREFIX-s]
```

#### 重命名session

```
[PREFIX-$]
```

### window

#### 创建window

```shell
$ tmux new-window -n code -t session_name
```

```
[PREFIX-c]
```

#### 关闭一个window

```
[PREFIX-x]
```

#### 切换下一个window/下一个

```
[PREFIX-n] or [PREFIX-ctrl+l] / [PREFIX-ctrl+n]
```

#### 快速切换到上一个使用的窗口

```
[ctrl-x+x] ctrl 接两次的x键位
```

#### 切换到对应的窗口

```
[PREFIX-1/2/3]
```

#### 可视化选择切换窗口

```
[PREFIX-w]
```

### pane - 面板

#### 创建pane

```
# 原始 [PREFIX-%]和[PREFIX-"]
# 修改之后 垂直/水平分割窗口
[PREFIX-|] / [PREFIX--]
```

#### 切换pane

```
[PREFIX-hjkl] pane之间移动
```

#### 关闭pane

```
# 关闭一个面板, 要确认
[PREFIX-x]

# 或者
$ exit [面板里执行]
```

#### 调整大小

```
[Ctrl-<>JK] < -左移， > - 右移，J - 向下，K - 向上
```

#### 当前pane在新的window中打开

```
[PREFIX-!]
```

#### 切换pane布局

```
[PREFIX-space]
```

#### 多pane 命令同步

```
[PREFIX-:] set synchronize-panes on
```

### 复制粘贴

#### 基本操作

```
# 进入复制模式
[PREFIX-[]
[PREFIX-PgUp]

=> 可以进行的操作
space/v    开始选择
hjkl       方向键移动
w/b        向前向后移动一个单词
fx/Fx      行内移动到下一个字符位置
ctrl-b/f   在缓冲区里面翻页
g/G        到缓冲区最顶/底端
/ ?        向下, 向上查找
n/N        查找后下一个, 上一个
Enter/y    复制
[PREFIX-]] 粘贴
```

#### 自定义 for mac

```
# 安装 工具包，为了在tmux 中复制到系统剪切板
$ brew install reattach-to-user-namespace

# 进入复制模式
[PREFIX-[]
v  			开始选择
y			复制到系统剪切板
```

### 其他

#### 修改.tmux.conf 之后reload

```
[PREFIX-r]
```

### 快速启动小脚本

```shell
#!/bin/bash

export HOSTNAME='MacBook-Pro'
tmux has-session -t local
if [ $? != 0 ]; then
    # local session
    tmux new-session -s local -n "~" -d
    tmux new-window -n code -t local
    tmux send-keys -t local:2 'j app_php' C-m
    tmux new-window -n jenkins -t local
    tmux send-keys -t local:3 'j python' C-m
fi

# tmux has-session -t f12
# if [ $? != 0 ]; then
#     tmux new-session -s f12 -n python -d
# fi

```

------

mxgnene01

Email: mxgnene01@gmail.com

Github: https://github.com/mxgnene01

2017-10-10 BeiJing
