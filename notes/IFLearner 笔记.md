---
attachments: [Clipboard_2022-06-16-14-29-23.png, Clipboard_2022-06-17-10-40-01.png]
tags: [实习笔记/iflearner框架]
title: IFLearner 笔记
created: '2022-06-16T06:18:54.934Z'
modified: '2022-06-17T02:40:01.758Z'
---

# IFLearner 笔记

## PRC (remote procedure call)
[gPRC通信：](https://www.jianshu.com/p/9c947d98e192)
- gRPC可以通过protobuf来定义接口，从而可以有更加严格的接口约束条件。
- 通过protobuf可以将数据序列化为二进制编码，这会大幅减少需要传输的数据量，从而大幅提高性能。
- gRPC可以方便地支持流式通信
![](@attachment/Clipboard_2022-06-16-14-29-23.png)
AggregateServer 和 各个client之间通过PRC进行通信

## Controller
### 同质化客户端

首先初始化一个Trainer，其中包含了数据、模型、训练、评估等方法。
1. client向AggregateServer发送注册信息
2. client建立监听sever的notice进程
3. report client ready
4. client 的trainer fit、evaluate
5. server 等待所有client fit、evaluate完毕
6. server handler_upload_param
7. client handler_aggregate_result


## I.I.D data

## SCAFFOLD
SCAFFOLD算法相比FedAvg只是加了一个修正项$c-c_i$，有了这个修正项可以有效的解决本地更新时的client-drift，让每个客户端在本地更新的时候“看到”其他客户端更新的信息，这里不是指真的看到，而是一种guess。

也就说我不再是每次只在自己的数据上训练，我还去猜测别人这一步可能在做什么。 有了这个猜测我就好像用所有的数据在本地训练模型一样。
![](@attachment/Clipboard_2022-06-17-10-40-01.png)



