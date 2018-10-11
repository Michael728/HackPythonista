# 常用三方库

## 队列

### collections

- collections.OrderDict
- collections.defaultdict

## 数据库相关

## itertools

## operator

## functools

Remark，做Python PPT工具。

## six

python2和python3通用性兼容性封装，openstack中使用，强烈推荐

## requests

建议掌握

## eventlet

协程的经典，下层使用的greenlet，建议掌握

## greenlet

非常高效的协程封装，想了解协程机制的话，可以深入学习

## pycrypto 安全

提供了几乎所有的加解密算法，下层使用的是cryptograph，建议做基本了解

## SQLAlchemy

对SQL语句的封装，建议概念了解

## Mock

测打桩，建议掌握

## Unittest

建议掌握

## Multiprocessing

多进程，建议基本了解，工作中不常用

## Threading

多线程，建议掌握，不建议使用thread(thread在python3中变为内部库_thread)

## Queue

多进程/多线程队列按序执行的场景，基本了解

## Subprocess

用于创建新进程，可用于python调用shell/bash等，建议掌握。python调用shell/bash不建议os.system/commands.*（这些方式在python3已经移除）。

- [cookbook-执行外部命令并获取它的输出](https://python3-cookbook.readthedocs.io/zh_CN/latest/c13/p06_executing_external_command_and_get_its_output.html)

## Profile/cProfile

用于性能分析，非常非常好用，和pstat配合食用，建议掌握。

## 时间模块相关

### arrow

- [Python：如何用一行代码获取上个月是几月](https://foofish.net/python-arrow.html)

### pendulum

### Delorean

### REF

- [6 个 Python 的日期时间库](http://python.jobbole.com/89178/)

## 开发工具

### HTTPie

是命令行HTTP客户端。其目标是使与Web服务的CLI交互尽可能人性化。它提供了一个简单的http命令，允许使用简单自然的语法发送任意HTTP请求，并显示彩色输出。HTTPie可用于测试，调试以及通常与HTTP服务器交互。

GitHub：https：//github.com/jakubroztocil/httpie

## Linux

### paramiko

只要是稍微搞过Python与linux的都会熟悉paramiko这个犀利的库。
它完美的契合的用户操作linux机器下的所有操作，ssh ftp等等…

## 运维

### Ansible

是一个极其简单的IT自动化系统。它处理配置管理，应用程序部署，云配置，临时任务执行和多节点编排 – 包括通过负载平衡器轻松实现零停机滚动更新等操作。

GitHub：https：//github.com/ansible/ansible

### Sentry
从根本上讲是一项服务，可以帮助您实时监控和修复崩溃。服务器端使用Python，但它包含一个完整的API，支持在任何应用程序中使用任何语言发送事件。

GitHub：https：//github.com/getsentry/sentry

### Luigi
是一个Python包，可用来创建复杂的批处理作业管道。可用来处理依赖项解析、工作流管理、可视化、处理故障、命令行集成等等。

GitHub：https：//github.com/spotify/luigi

## 好玩的工具

### sh
```
pip install sh
```

### Progressbar

Progressbar 是 Python 中的一个文本进度条程序库，用于展示长时间运行操作的过程，从视觉上提示你程序的处理进度。

### colorama

### YouTube-dl
油管搬运工，可从youtube.com或其他视频平台下载视频。

GitHub：https：//github.com/rg3/youtube-dl

### You-Get
是一个小型命令行实用程序，用于从Web下载媒体内容（视频，音频，图像），尤其是在手边没有合适工具的时候。

GitHub：https：//github.com/soimort/you-get

## 参考

- [哪些 Python 库让你相见恨晚？](https://www.zhihu.com/question/24590883/answer/286407918)
- [8 个用于业余项目的优秀 Python 库](http://python.jobbole.com/89287/)
- [2018年GitHub最流行50大Python开源项目](https://www.ctocio.com/ccnews/27611.html)
- [Python 3 Module of the Week](https://pymotw.com/3/index.html)
