---
layout: post
title: 对在NLP领域对比MLP、CNN和RNN的一点思考
category: 个人思考
tagline: 
tags: [NLP, MLP, CNN, RNN]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

深度学习这个领域仍在快速发展，各种细节处理策略也都在进化，更有很多细节还需要探索。个人认为，现在就对CNN、RNN和MLP三者应用于NLP问题的优缺点下结论有失稳妥。

以NLP里一个比较难的问题——机器翻译（MT, machine translation）为例，基于神经网络的机器翻译系统（NMT, Neural Machine Translation）正在逐步取代原先的基于短语的统计机器翻译系统（PBMT, Phrased-based Machine Translation）。2016年，Google公布了在Google Translate产品上用到的机器翻译技术（对应的核心翻译系统称呼为GNMT），并先后发表了2篇文章。（说明：在通用领域的机器翻译产品中，Google Translate确实做得很好，这里就先拿他家的paper作为代表）

+ [Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation](https://arxiv.org/abs/1609.08144)
+ [Google's Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation](https://arxiv.org/abs/1611.04558)

这两篇文章均是使用RNN（具体来说用的是LSTM RNN + attention）。确实在最近几年，对于很多NLP问题，比如机器翻译、自动问答、自动摘要等问题，业内主流的观点是认为RNN更合适些，因为它可以处理变长的输入文本（当然在CNN里可以使用dynamic pooling技术也能处理），而且能更好的处理远距离依赖（memory是RNN的一个重要特点）。但时间走到今年，Facebook先提出CNN做seq2seq问题，但发表后还不到一个月，Google就提出不用CNN和RNN，光有attention即可。这两个idea都比较大胆，突破了原先大部分人的认识，但他们确实在标准评测集上，不断刷新着state-of-the-art的翻译指标（BLEU）。

+ [Convolutional sequence to sequence learning](https://arxiv.org/abs/1705.03122)
+ [Attention Is All You Need](https://arxiv.org/abs/1706.03762)

语言的奥秘还没完全解开，机器翻译模型肯定还会进步，解决NLP各个问题的模型也会进步。这是我认为当前不好下结论的原因之一。

此外，务实一点的话，解决一个NLP问题的效果好坏肯定不只是与用CNN、RNN和MLP这种框架性的模型有关，还与诸多其他的因素有关。像《Attention Is All You Need》一文，在没有CNN、RNN的基础上把效果做得这么好，肯定与attention（scaled dot-product attention 和multi-head attention）、position embedding设计的精巧有关。另外，一个实用的线上NLP系统涉及到诸多语言细节的处理策略，比如初始时是从词粒度的embedding做起，还是从字粒度的embedding做起，还是从更细粒度的语言单元（比如Google用的word piece）的embedding做起，甚至是对它们做模型融合；定义好基础粒度后如何训练得到对应的embedding模型，如何设计网络层数和节点数，使用哪些normalization技术或者哪种dynamic max pooling技术或者gradient clip等等，很多细节策略都会影响到最终的效果。这段话像是堆砌词语，但总结来说就是要调的一手好参。

模型如此多，笔者在选模型时比较喜欢那种解释性比较好、效果和性能相对均衡的模型。对NLP问题，虽然使用MLP通常可以拿到一个比较好的结果，但因为网络结构的特殊性，难以可视化其每层的作用。这块笔者比较喜欢CNN以及attention，因为它们至少可以提供一定程度的模型可视化。当然这块的技术也在快速改进，也许过阵子我的观点就不对了。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
