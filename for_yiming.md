## 书名：《深度学习编码指南——from PyTorch Perspective》

### 背景：

tensorflow的API太底层，死掉；keras又封装的太死，死掉。实践证明，往往是对底层内容的有效抽象，并给足了用户自由度的框架，能够活下来。同样的道理，如果把最底层的原理，cudamemcpy，ring-all-reduce都掰开了揉碎了讲出来，没人喜欢。同理，只讲些顶层的resnet，transformer模型结构，只会看个热闹，该不会写，还是不会写。

### 前景：

每年虽然都有算法岗劝退，但是一个事实是，算法岗的人越来越多，现在是一个临界点，正好是大家开始唱衰算法，但又因为惯性原因，在这个领域的学生最多的时候。我们不去和他们卷，而是换个思路，卖他们炼丹的本事，就好比当年旧金山淘金热发财的卖牛仔裤的老兄一样。

另外，pytorch现在的发展很快，远远不再是loss.backward()，然后optimizer.step()一下就完事了。

我调研了一下，目前的书籍大部分没有教你怎样去系统地通过pytorch去写代码，大部分都是浅尝辄止一下，就完事儿了。比较好的书也不过就是陈云之前写过一本，但那也已是2年以前的事了。

### 为什么我们能做这件事：

因为我们都看过大量的代码（这里首推朱俊彦的cycle-gan），知道好代码是怎么一回事。并且也有丰富的经验，包括调参，debug等，好的代码不仅是能跑就行，还包括一系列的问题，比方说yacs/config，optimizer和lr_scheduler的工厂函数，正确的checkpoint，如何resume，等等。这些useful but dirty things正好是我们可以做的。

### 这本书应该包含哪些？

#### 第一部分，Pytorch高级用法指南

- 会不会手写模型？
- 了解dtype，了解device
- gather和scatter的用法
- einsum
- 各种shape的变换，transpose，scatter，view和reshape的区别，stride是什么，什么时候需要加permute？包括我前两天写的[知乎博客](https://zhuanlan.zhihu.com/p/417304042)。
- dataloader的基本原理，collate_fn, sampler, batch_sampler, distributedsampler等等。
- Module里面的modules，还有children的区别
- 中间层hook的使用方式
- detach的使用
- lr_scheduler的使用。

#### 第二部分，正确地写代码 ==> 写正确的代码

- 正确的深度学习项目模板，以及如何阅读别人的项目；
- yacs ==> config，包括如何和argparse配合，freeze和defrost;
- logging的使用方式，stream_handler和file_handler;
- 简单地多级多卡训练方式，应该注意哪些问题，mp.spawn, torch.distributed.launch，各概念的意思，比如world_size，rank这些。
- tensorboard，wandb，visdom，还有netron等等可视化工具的最基本使用方法。
- 如何保存，保存哪些内容，怎么把config也一并保存进来？
- 实验记录管理，commit id，实验结果，保证能够快速回退到某一特定版本的代码。

#### 第三部分，走向实践

- cmake的基本内容教学，能用cmake干活
- cuda的基本内容教学，不要讲太深；
- tensorrt的基本教学，分为两个步骤，第一个步骤，怎么转模型，用ONNX路线？还是c++硬编码？
- 第二个步骤就是简单的，tensorrt代码怎么写，如何在代码中进行部署。
