## 如何光明正大地学习KISS？当然是用这个DL接吻检测器了

[机器之心](javascript:void(0);) *今天*

选自 arXiv

**作者：Amir Ziai**

**机器之心编译**

> 情人节的时候，机器之心向大家推荐了一个鉴黄数据集，结果大家反应热烈，纷纷留言。还有一些有「大胆想法」的朋友在问有没有视频的数据集，这不，福利来了 [贼笑]←←

不要误会。作为一个严肃的公众号，我们才不会收集什么奇怪的视频呢！我们批判了大量电影，造访了众多 GitHub，这次推荐给大家的内容的确包含大量视频数据，这些视频的确有那么点少儿不宜，大家看完还可以借鉴一下里面的姿势呢。

诶，想什么呢？这些只是接吻的视频而已😗。这些接吻视频片段来自 100 部电影，看完这些，你可能就学会了十八式或者一百零八式接吻姿势了？

这个项目是斯坦福的 Amir Ziai 做的，至于他到底在斯坦福念的是什么学位，小编还没搞明白。但略查了查，这人还挺厉害：

![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicEaZXlmOwuibxiaFcq42JxHk6H23WOPFK3bgNj5sGtSxia1hMumeHu06GJUCcOm3BE1q4HKsYIYjR9g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

本科毕业于有「伊朗麻省理工」之称的谢里夫理工大学，念的是机械工程；然后在加拿大名校西蒙弗雷泽大学读了硕士学位，接着又在 UC Berkeley 拿到了数据科学的硕士学位，然后是佐治亚理工大学的计算机科学、机器学习硕士学位。最后，这两年在斯坦福进修 AI。

貌似跑题了，重点是他做的项目：深度学习电影镜头接吻检测器。一看就好有内涵哦……

**这个系统到底是干嘛用的？**

不要以为作者这么无聊，就为了集中看一下电影中的接吻镜头顺便观摩学习一下。其实，电影中的场景类型对于视频编辑、分类和个性化等应用来说，都非常重要。

精确的场景探测器可以丰富特定场景类型的视频元数据，用户也可以轻松搜索和检索目标片段。

但是，大多数现有系统都只是对静止帧进行分类，或者识别整个视频中是否存在某个动作。所以，在这项研究中，作者提出了一个检测和提取电影中接吻片段的系统。

本着学习的精神，小编为广大读者朋友们推荐了这个系统，大家可以试试这个检测系统好不好用，好用的话用来干点别的也是可以的。当然，你想集中观看一下这些电影中的接吻片段，顺便观摩学习一下也是可以的。

**激动人心接吻检测器**

看到这里，大家一定急着想用这个工具来「学习」了。作者在 Github 上提供了使用代码的方法，可以通过提供的 API 从视频中获得接吻镜头。

调用代码的方式如下：

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

使用作者提供的 segmentor 和 unpickle 两个 API，然后使用 seg.visualize_segments

提取本地 mp4 文件中的接吻镜头：

![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicEaZXlmOwuibxiaFcq42JxHkUfUHqYbTVHSOzcPgCe1GfOoOx7NMsrn3Yciamib1SWIE1ckHLZbzaCwg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

从 Youtube 网站的视频获取接吻镜头：

![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicEaZXlmOwuibxiaFcq42JxHkaW5bMuPeX1z1jextSyJQfb8wytXavNWbRp8t2jVTWnK7xOC4T7EicUw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

代码可以在 Github 的 examples 文件夹中找到。

- Github 地址：https://github.com/amirziai/kissing-detector

**这个检测系统是怎么做的？**

这个系统输入的是单个视频（电影），输出的是视频中检测到的一个或多个不重叠的接吻片段。比如说一部 60 分钟的电影 M 中有两个时长为 1 分钟的接吻场景，分别在第 5 分钟和第 55 分钟时出现。这时系统应该输出 K1 和 K2，其中 K1 表示第一个接吻片段，K2 表示第二个接吻片段。

它需要两个组件来实现这一点：二元分类模型和聚合算法（aggregation algorithm）。作者小哥哥还制作了一个小视频，他简要介绍了这篇论文的最主要思想与做法：



首先，二元分类模型获取连续且不重叠的 1 秒钟视频片段，然后为每个片段预测一个二进制标签（即该片段是否为接吻片段）。接着，聚合算法把对这些片段的预测聚集到一组接吻场景中。图 1 描述了这个过程，如下所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicEaZXlmOwuibxiaFcq42JxHk4XEZhPWUXr5NicpMgled1oBJ2uTwiaFbPsnm3MQbDiauibk38SqBVkGpbg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**二元分类模型**

二元分类模型由两个架构组成：一个 18 层的 ResNet CNN 和一种类似 VGG 的架构 VGGish。如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicEaZXlmOwuibxiaFcq42JxHktiaH0HcEuicxCcOST5mzbjh5qCtibBZM3mXZ1pVkzTkslHEsHAocag9IA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

ResNet 以 3 通道 224x224 张量的形式在 1 秒钟视频片段的最后一帧上运行。作者已经分离了最后一个全连接的层，并使用了前一层的 512 维输出。

而 VGGish 对 1 秒钟视频片段最后 960 毫秒的音频波进行转换。这种转换是以单通道 96x64 张量的方式完成的。VGGish 是一种卷积网络，它有效地将转换后的音频视为图像，并生成语义上有意义的 128 维嵌入。

**聚合算法**

聚合算法结合了来自二元分类器的预测标签列表 P，并生成了一组接吻片段。例如，有一部 60 分钟的电影中包含一个两分钟长的接吻场景，从第 30 分钟开始。

分类器将输出 3600 个预测结果，作者再将这些预测放在列表 P 中。假如有一个完美的分类器，那分割器的预期输出将是包含单个视频片段的列表，该片段从第 30 分钟开始，在第 32 分钟时结束。

算法 1 详细描述了聚合算法的逻辑：

![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicEaZXlmOwuibxiaFcq42JxHkceS9LqOfZr0rJCdy8EI5XiaD6ARRsbQIp27vEIevVRguEXfGKIAHvhA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**数据集来自哪里？**

作者使用的数据是一个 2.3TB 大小的数据库，里面包含了从 1915 年到 2016 年的 600 部好莱坞电影。这些电影的题材范围很广，分辨率也各不相同，大小在 200MB 到 12GB 之间。

作者从中手动选择了 100 部电影，然后对这些电影中的接吻片段进行了注释。未注释的片段被视为非接吻片段并被如此标记，如图 4 所示。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

最后，作者总共标注了 263 个接吻片段和 363 个非接吻片段，时长从 10 秒到 120 秒不等。数据集分为训练、验证和测试集，比例分别为 80%、10%、10%。

对于每个带注释的视频片段，作者会提取两组特征，分别是图像特征和音频特征。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**这个接吻镜头检测系统好用吗？**

作者使用了 F1 得分来评估二元分类器的质量。F1 被计算为精确度和召回率的调和平均数，并在二者之间达到平衡，这使得系统很难作弊。

作者对二元分类器训练了 10 个 epoch 后，评估 F1 得分为 0.95。也就是说，这个系统的准确率高达 95%。对于这个初始实验，他训练了网络中的所有权重。此外，使用的批大小是 64，ResNet-18 作为图像特征提取器，VGGish 作为音频特征提取器，Adam 优化器的学习率为 0.001。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

并且，作者通过实验发现，ResNet 是这一任务和训练配置的最佳架构。因此，他还对 3D ResNet-34 训练了 10 个 epoch，但使用该架构的 F1 得分为 0.88，低于 ResNet-18。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

对于这一差异，作者认为可能有两个原因：首先，ResNet-18 受益于在 ImageNet 上进行的预训练，而 3D ResNet-34 是从头开始训练的；其次，模型在 16 帧的时间深度上可能不足以捕捉相关上下文。

如果对这个系统感兴趣，可以戳下面的链接了解更多信息哦~

- https://arxiv.org/pdf/1906.01843.pdf



**深度****Pro**

**理论详解 | 工程实践 | 产业分析 | 行研报告**



机器之心最新上线深度内容栏目，汇总AI深度好文，详解理论、工程、产业与应用。这里的每一篇文章，都需要深度阅读15分钟。





**今日深度推荐**

[中文和英文NLP自然语言处理异同点分析](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650763742&idx=2&sn=5270f3d692e9724e70553eca23e5d4c2&chksm=871ab5a0b06d3cb662048cdca6a7e0253a0495ad1a17dfcff3a200f6c43400a15d8666e87460&mpshare=1&scene=1&srcid=&key=90581f21d61583cc29beea1ceb3dfcd7ccabbc74c6921464b827b067730df9e6001d789c33f01c0a568c1fc79a442d33fa56d5020ae5ba9139395bb1aea7ebb67671fd95e6053e36ea4ee4a511a3d677&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=BUWUYnKfJ56vNqQot1aK1RyBMuUIKZVt8%2BLodOvPcOenM5CSUrKLMK7C%2FjdIemJw)

[SysML 2019论文解读：视频分析系统的提升](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650763742&idx=2&sn=5270f3d692e9724e70553eca23e5d4c2&chksm=871ab5a0b06d3cb662048cdca6a7e0253a0495ad1a17dfcff3a200f6c43400a15d8666e87460&mpshare=1&scene=1&srcid=&key=90581f21d61583cc29beea1ceb3dfcd7ccabbc74c6921464b827b067730df9e6001d789c33f01c0a568c1fc79a442d33fa56d5020ae5ba9139395bb1aea7ebb67671fd95e6053e36ea4ee4a511a3d677&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=BUWUYnKfJ56vNqQot1aK1RyBMuUIKZVt8%2BLodOvPcOenM5CSUrKLMK7C%2FjdIemJw)

[基于人工智能的三维传感网空间定位技术](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650763742&idx=2&sn=5270f3d692e9724e70553eca23e5d4c2&chksm=871ab5a0b06d3cb662048cdca6a7e0253a0495ad1a17dfcff3a200f6c43400a15d8666e87460&mpshare=1&scene=1&srcid=&key=90581f21d61583cc29beea1ceb3dfcd7ccabbc74c6921464b827b067730df9e6001d789c33f01c0a568c1fc79a442d33fa56d5020ae5ba9139395bb1aea7ebb67671fd95e6053e36ea4ee4a511a3d677&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=BUWUYnKfJ56vNqQot1aK1RyBMuUIKZVt8%2BLodOvPcOenM5CSUrKLMK7C%2FjdIemJw)





[![img](https://mmbiz.qpic.cn/mmbiz_jpg/KmXPKA19gW9gF0pcodHXyjR2CkTmXiafpzu7mwsuZMmWSJFf7odaB0Rug12hWIshXTmw2ZQ398SY6vZMP1aWIuA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650763742&idx=2&sn=5270f3d692e9724e70553eca23e5d4c2&chksm=871ab5a0b06d3cb662048cdca6a7e0253a0495ad1a17dfcff3a200f6c43400a15d8666e87460&mpshare=1&scene=1&srcid=&key=90581f21d61583cc29beea1ceb3dfcd7ccabbc74c6921464b827b067730df9e6001d789c33f01c0a568c1fc79a442d33fa56d5020ae5ba9139395bb1aea7ebb67671fd95e6053e36ea4ee4a511a3d677&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=BUWUYnKfJ56vNqQot1aK1RyBMuUIKZVt8%2BLodOvPcOenM5CSUrKLMK7C%2FjdIemJw)

点击图片，进入小程序深度Pro栏目





PC点击阅读原文，访问官网

更适合深度阅读

www.jiqizhixin.com/insight





每日重要论文、教程、资讯、报告也不想错过？

[点击订阅每日精选](https://mp.weixin.qq.com/s?__biz=MzIyMjE2ODk5NQ==&mid=2247483701&idx=1&sn=f6f5c2f1ef750490595b03f8650aff72&scene=21#wechat_redirect)



[阅读原文](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650763742&idx=2&sn=5270f3d692e9724e70553eca23e5d4c2&chksm=871ab5a0b06d3cb662048cdca6a7e0253a0495ad1a17dfcff3a200f6c43400a15d8666e87460&mpshare=1&scene=1&srcid=&key=90581f21d61583cc29beea1ceb3dfcd7ccabbc74c6921464b827b067730df9e6001d789c33f01c0a568c1fc79a442d33fa56d5020ae5ba9139395bb1aea7ebb67671fd95e6053e36ea4ee4a511a3d677&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=BUWUYnKfJ56vNqQot1aK1RyBMuUIKZVt8%2BLodOvPcOenM5CSUrKLMK7C%2FjdIemJw##)







微信扫一扫
关注该公众号