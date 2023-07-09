## WoChat, help you build your owned IM software.

我聊项目，是基于[MatterMost](https://mattermost.com)为基本内核进行开发的。MatterMost是一款集中式架构的开源的优秀IM。我聊项目第一阶段是对其进行汉化和界面的调整，使其更符合中国人的口味，在这个过程中熟悉其核心技术，并丰富其中文文档，方便后面的加入者进行上手。目前（2023年7月）开始，我们的任务是学习搭建独立的MatterMost环境，学习其基本使用，开始撰写原创性的文档，方便后来者的学习和加入。所以我们目前还是暂时依托mattermost的代码库，不会独立出来。

整个系统包括服务器端和客户端。客户端又分为桌面版和手机版，列表如下：
 - [Server](https://github.com/mattermost/mattermost)，运行在Linux服务器上
 - [Desktop](https://github.com/mattermost/desktop)，包括Windows/MacOS/Linux
 - [Mobile](https://github.com/mattermost/mattermost-mobile)，包括安卓和iOS


本项目(wochat)集中在文档和零基础培训视频教程的开发方面。本项目所列的文档全部为我们原创，都是经过实践检验过的。

文档列表如下：
- 概述
- 服务器端的编译方法
- 桌面版的编译方法
- 安卓的编译方法
- iOS的编译方法
- 零基础培训视频

联系方式；wochatyou@gmail.com

## 体验MatterMost

我们已经在AWS上搭建了一套独立的MatterMost聊天系统，供第一次接触它的用户体验之用。下面是体验的方法。

1. 貌似MatterMost只能在桌面版注册账号。手机版只能登录，不能注册。所以我们已经注册了如下用户：
   * 用户名：david / 口令：Welcome2023
   * 用户名：peter / 口令：Welcome2023

2. 请下载手机版MatterMost。你可以在安卓或者苹果的应用商店里面搜索MatterMost进行下载安装。
3. 如果你想体验桌面版，请到：https://mattermost.com/download 在此页面的底部有客户端下载。
4. 登录MatterMost后，需要输入服务器的地址，请输入： https://im.wochat.org
5. 用户名和口令请见第一步。如果是桌面版，你可以自行注册账号。
6. 登录后可以自行聊天。目前支持语音通话和屏幕分享。你可以和好友进行测试。

在体验过程中有任何问题，请致信：wochatyou@gmail.com

##  日志
- 2023/07/06 - 新增服务器端搭建文档： https://github.com/wochatyou/wochat/blob/main/ubuntu-server-installation.md
- 2023/07/06 - 新增后台PostgreSQL数据库结构文档： https://github.com/wochatyou/wochat/blob/main/mm.sql
- 2023/07/08 - 新增如何体验的文档： https://github.com/wochatyou/wochat/blob/main/feel.md
- 2023/07/08 - 新增文档：MatterMost的协议分析： https://github.com/wochatyou/wochat/blob/main/protocol.md
- 2023/07/09 - 开设了[client](https://github.com/wochatyou/client)和[server](https://github.com/wochatyou/client)两个项目。Client采用纯Native的开发方式，服务器端尽量不开发，采用成熟的MQTT和Web服务器软件进行搭建。



  
  
