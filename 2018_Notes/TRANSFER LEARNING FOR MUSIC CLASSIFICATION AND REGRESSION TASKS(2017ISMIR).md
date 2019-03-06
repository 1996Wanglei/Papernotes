TRANSFER LEARNING FOR MUSIC CLASSIFICATION AND REGRESSION TASKS(2017ISMIR)

论文地址：

**1.论文摘要**

作者将一个使用music tag训练的五层VGG网络迁移到六个相关音乐分类和回归任务上。每个任务，作者将网络的一二三四五层网络排列组合起来，关注那些层次的特征和此任务相关性更强。同样作者使用了MFCC特征做为bseline特征，以及一些取得了state-of-the-art结果的方法进行对比。

迁移学习的概念最初是在计算机视觉上得到应用，图片分类任务中的神经网络能够区分一些基本的物体形状。在nlp中，在大数据集上训练出来的词向量可以用到情感分析等任务上。在mir上有人用tag和play-count data训练多层感知机，将训练好的权重迁移到流派分类和音乐自动标注上，此外还有一些别的工作。

**2.model**

作者选用了music tagging作为source task。理由有两个，其一是大量的可以用来训练的数据，第二是标签覆盖到了音乐的各个层面，比如说genre，mood，era和instrumentations等。**神经网络的输入是二维的梅尔频谱**

神经网络模型是一个五层的VGG，3*3的卷积核

![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/VGG%20net.png)

**3.论文亮点**

3.1 Representation Transfer

> Relying solely on the last hidden，layer may not maximally extract the knowledge from a pretrained network。

作者认为，**受卷积神经网络结构的限制，一些像tempo，pitch，harmony，envelop这样的low-level信息会在底层被网络学到，但是由于subsampling的存在，这些在更深的层也许不会被保留的**。所以作者模仿了一篇music tagging的文章里，使用multi-layer的特征表示。为每个子任务将所有的层的特征组合起来，寻找在每个子任务中最具有效率的特征。

作者还注意到**有研究表明随机初始化权重的神经网络也能够作为一个很好的特征提取器**，所以他又增设一组对照实验，使用的是随机初始化权重的神经网络作为特征提取器。通过对这组实验的性能评价能够明确迁移过来的知识，卷积神经网络的贡献，非线性高维变换的贡献。

**4.experiment**

4.1 source task

用了244244首Million Song Dataset 里面的preview clips，[50个从 last.fm取得的标签](https://github.com/keunwoochoi/MSD_split_for_tagging)，包括了genre，eras，instrumentations，moods。**这里值得一提的是我原来以为作者是用整首歌来训练，实际上他们只用了从7digital获得的每首歌曲的preview来训练，30秒**。

4.2 target task

![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/%E5%9B%9B%E7%BB%84%E7%89%B9%E5%BE%81.png)

- 任务一：舞厅舞蹈分类
- 任务二：流派分类
- 任务三：语音和音乐分类
- 任务四：情感预测
- 任务五：歌声和非歌声检测
- 任务6：非音乐任务，音频事件检测，包括有空调声，汽车喇叭声，狗叫声等。

**5.experiments reauslt**

作者对比了1.具有最好表现的卷积特征2.将1,2,3,4,5层特征和MFCC特征concatenate的特征3.MFCC特征4.state-of-the-art结果。

![](/home/wanglei/Pictures/四组特征.png)

有如下结论，具有最好表现的卷积特征在6个任务比baseline特征MFCC要好很多，且比联合5层卷积特征和MFCC的特征都要好，除了第6个任务。和state-of-the-art方法对比，则是有一段差距。随后作者深入分析了6个任务的实验结果，得到一些更深的结论。

**在子任务上**，作者使用了四组对照实验，分别是随机组合的特征，随机初始化权重的特征，联合特征，baseline特征（MFCC），SoTA特征。

**5.1 令我非常惊讶的是随机初始化权重的特征表现**

虽然这个特征在任何任务上的表现都没有超过具有最佳表现的卷积特征，但是它的变现和MFCC特征相当，在某些任务上甚至超过。作者认为卷积特征之所以这么强大有一部分原因来源是卷积神经网络结构自己，第二就是如果没有合适的source task，直接使用随机初始化权重的卷积特征是有用的。

**5.2 task1 Ballroom Genre Classification**

结论：变现排名前7的特征都包含了第二层特征，6/7的特征包含了第一层，变现最低的7个特征都没有包含第一层特征，甚至只使用第一层特征都能取得73.8%的准确率。ballroom genre labels和底层特征rhythmic，tempo有关，source task中没有tempo的标签，高层特征中tempo这个都是恒定不变的。

**5.3 task2 Gtzan Music Genre Classification**

结论：排名前7的特征都包含超过3层，排名后7 的特征都只有一层或者两层。联合所有层的特征对于这个任务是一个很好的方法。有趣的结论是，由于训练的tag中包含了7个流派分类，理论上来说高层的特征应该变现更好才对，然而实验结果表明，底层的特征更能够提升流派分类的表现。

**5.4 task3 tzan Speech/music Classification**

结论：这个任务被轻松解决了，所有特征的分类准确率为100%，表明语音和音乐本质上是两种截然不同的东西

**5.5 task4  Music Emotion Prediction**

结论：对arousal的预测，前7的特征都包含了第五层，非常依赖于高层特征，第一层也同样重要，前五都包含了第一层特征。对于valence的预测，第三层的特征尤其重要。

**5.6 task5 Vocal/non-vocal Classification**

结论： 第4层特征最终要，所有包含了第4层特征的14组特征比没有包含第4层的14组特征都表现得更好。

**5.7 task 6  Acoustic Event Detection**

结论：source task中没有包含任何有关于这个任务的标签，不期待第五层的特征具有很好的表现。在这个任务当中也没有观察到对某一层特征的依赖。但是卷积特征仍然比传统的音频特征取得更好的变现，表明卷积特征具有多样性。

6.我的感想

这篇论文的实验做得太完整了，实验结论也非常的完整，论文的结构也非常的完整，这是这篇文章获得2017ISMIR最佳论文的原因。

同时这篇文章也是基于作者之前音乐自动标注的工作做的。因为要给244244首歌打上标签再训练需要这一步工作，那篇文章的引用短短时间有110多。

