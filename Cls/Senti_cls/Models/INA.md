
<span id='title' ></span>

# Interactive Network Attention

## 简介


&#8195; 本文认为Aspect-level的情感分类任务中，target与context应该具有交互性，即context应该是target-specific的，target也应该是context-specific的，传统模型中将二者分开建模或只针对其一，本文利用attention实现二者交互。我关注的更多的应该就是这里面的attetion机制是如何将上述target和context结合的。Itroduction里面有些传统的做法，比如词袋，情感词库，SVM...这些方法都很容易遇到瓶颈，现在的做法一般都是利用深度学习进行多层次语义分析。2011年的一篇论文解释了为何传统的方法会遇到很大的瓶颈（40% errors）,主要是因为之前的方法都没有有效的利用target信息。之后就有大量论文关注target的作用，但是这些论文都忽视了target与context的关系。多层次语义情感分类的解释是，如：

> a group of friendly staff, the pizza is not bad, but the beef cubes are not worth the money !

这句话里，对staff，pizza, beef的情感是不同的，一句话里面的情感是多层次的。上面的三个名词都是target,这段话上下文就是是指context.本文认为Aspect-level的情感分类任务中，target与context应该具有交互性，即context应该是target-specific的，target也应该是context-specific的，传统模型中将二者分开建模或只针对其一，本文利用attention实现二者交互。我关注的更多的应该就是这里面的attetion机制是如何将上述target和context结合的。Itroduction里面有些传统的做法，比如词袋，情感词库，SVM...这些方法都很容易遇到瓶颈，现在的做法一般都是利用深度学习进行多层次语义分析。2011年的一篇论文解释了为何传统的方法会遇到很大的瓶颈（40% errors）,主要是因为之前的方法都没有有效的利用target信息。之后就有大量论文关注target的作用，但是这些论文都忽视了target与context的关系。

### 结构
&#8195;模型的结构是基于一下两点假设。

1. target和形容它的context其实是可以互相推理的，所以两种虽然建模可以分开，但是模型学习的时候是通过两者之间的交互关系来学习的。

2. target和context不止一个单词，比如target:'picture quality'和context:'clear-cut'。这里的picture的重要度比quality重要，涉及到不同权重，自然而然就引入了attention机制。这篇论文也是第一个提出要将target与context分别计算attention weights的。
基于上述两种思想，作者提出了一种interactive attention network(IAN)模型，该模型基于LSTM，与attention机制.框架图结构如下：
<p align="center">
<img src = "https://www.zdnet.com/a/hub/i/r/2019/05/07/fb5e6782-24c1-424b-af2d-2a942cc97346/resize/1200xauto/8e7b82926590d7ec3a8a7288d7813252/gpt-model-open-ai-2018.png" class="center" width=600 height=300>
</p>





### 输入/输出
&#8195;论文使用了两种模型： BERT_BERT BASE​ : L=12, H=768, A=12, Total Parameters=110M BERT LARGE: L=24, H=1024, A=16, Total Parameters=340M 这里L是layers层数(即Transformer blocks个数)，H是hidden vector size, A是self-attention的“头数”。 在NLP领域，10层以上的layer还是比较“惊人”的，印象中当年Attention is All You Need第一次提出transformer的时候，在MT任务中用到了6层。当然从结构上来讲，transformers之间用的是residual connection，并且有batch normarlization这种“常规”操作，多层不是什么问题。有意思的是在于这么多层的结构究竟学到了什么？NLP不能和CV做简单的类比，网络层数并不是“多多益善”；有论点认为低层偏向于语法特征学习，高层偏向于语义特征学习。希望将来的研究能够给出更充分更有启发性的观点。

|               结构名称       | 结构形状 |
|:----------------------------:|:--------:|
| InputNode                    | 256*128  |
| Multi-Head Attention network | 128*50   |
| FeedForward                  | 50*1000  |
| Output                       | 1000*1   |

## 模型表现


## API 调用

## 历史版本

{% tabs first="Accuracy", second="Recall", third="F1-score" %}

{% content "first" %}
Content for first tab ...

{% content "second" %}
Content for second tab ...

{% content "third" %}
Content for third tab ...

{% endtabs %}