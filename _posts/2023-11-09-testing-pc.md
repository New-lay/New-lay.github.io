---
layout: post
title: Model Error
date: 2023-11-09 11:38 +0800
last_modified_at: 2023-11-09 11:38 +0800
tags: [Model, Error]
toc:  true
---

模型错误类型很多，如下：

1） 包含不可微分运算操作的模型

在深度学习模型中，一切都必须是端到端可微分的，以支持反向计算。因此，你可能希望不可微分操作能够在 TensorFlow 等深度学习框架中被明确标识出来。这是不对的，正如 Berker 曾经对 Keras Lambda 层感到特别困惑，因为它可以破坏反向计算。一个解决办法是使用 model.summary() 进行检查，以验证大多数参数是可训练的，如果发现有不可训练参数的 layer，则可能是破坏了自动微分能力。





2）在测试时没有成功关闭 dropout

我们都知道，在测试数据时需要关闭 dropout，否则可能获得的是随机结果。这可能非常令人困惑，尤其是对于正在部署模型并开始跑测试集的人而言。

这一问题可以通过 eval() 来解决。另外需要注意的是，在训练模型时 dropout 可能会导致一个奇怪现象——模型在验证集上的准确性高过比训练集上的准确性。这是因为在验证集上用到了 dropout，这看起来可能是欠拟合了，而且可以会造成一些让你头疼的问题。


-----
