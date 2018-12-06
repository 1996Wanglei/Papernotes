## Representation Learning Using Artist Labels For Audio Classification Tasks

论文地址：https://www.music-ir.org/mirex//abstracts/2017/PLNPH1.pdf

源码地址：https://github.com/jiyoungpark527/MIREX_2017_music_classification

by 王磊

**key point**

作者使用一个在MSD上训练的DCNN做为特征提取器，网络的输入是audio mel-spectrogram,在网络的输出层使用了很多的神经元，每个神经元代表一个艺术家的标签。最后的隐层输出就是特定的特征向量。

**method**

输出层有5000个艺术家，每个艺术家使用20首歌来训练。

输入的频谱使用128大小的音框。

计算mel-spectrogram的参数：

> To compute a spectrogram, 1024 samples
> are used as FFT and hanning window sizes, and 512
> samples are used for hop size. We performed magnitude
> compression with a nonlinear curve as log(1 + 10|A|)

使用的网络结构：

预测层使用categorical cross entropy loss作为激活函数

每一次卷积层后都用了batch normalization,relu激活函数，最后一层使用0.5 的dropout，优化函数使用SGD.

作者通过大量的实验决定选用３秒的audio作为输入，但是MSD的audio是三十秒长，所以十个三秒长的输出特征向量平均成一个。然后再使用linear discriminative analysis将256维的特征向量降为100维。这个特征将作为分类器的输入。

**总结**

基于艺术家的标签，通过卷积神经网络来寻找艺术家标签和音频之间的联系。确实每个艺术家的音乐作品都蕴含了这个艺术家的音乐特征，将这个音乐特征找出来用作音乐分类任务是合理的。她们的方法是近五年mirex情感分类任务准确率最高的方法，将近70%!





