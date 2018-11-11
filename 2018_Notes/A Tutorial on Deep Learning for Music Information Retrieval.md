A Tutorial on Deep Learning for Music Information Retrieval

论文地址：https://arxiv.org/abs/1709.04396

作者希望能够通过这篇文章激发初学者的兴趣，因此对相关内容作了一个简单介绍，并且回顾了前面已有的相关研究。

由于深度学习领域日渐在MIR研究趋于流行，这一方面在ISMIR上的文章也越来越多，所以这篇文章也介绍了一些关于深度学习的方法和在MIR中的应用。怎么设计结构、如何训练、什么时候该使用深度学习是了解深度的基础。深度学习包括EBP(error backpropagation), CNN, LSTM, DNN等，DNN使训练速度明显提升，ReLU激活函数是在图像识别和声音识别上的一大创新。

几个基本的概念：node、layer、hidden layers、depth、width

深度学习相较于常规的只有一部分被学习的机器学习，可以体现更复杂的关系，所以也是end-to-end learning，更能体现输入和输出的关系。在深度神经网络的设计上包括选择类型、层数和损失函数，选择适当的激活函数也非常重要，一般以输出的范围与真实范围相同作为选择的依据，而深度的选择由数据量决定，如果数据不够，可以选择数据增强、transfer learning等方法。

在与音频相关的MIR问题中，subjectivity和decision time scale是两大主要因素。有的问题不能容易的分清背后的主观逻辑，可能需要多方知识。对于时间跨度，可分为与时间相关的(short decision time scale)和与时间无关的 (long decision time scale)（如节奏）

一般使用二维特征（频率、时间轴）来作研究，未处理过的音频信号可以通过STFT、mel-spectrograms、CQT等来得到可用于研究的频谱图。

DNN：在dense layer，一个节点可以代表大量信息，所以可用于表示某一方面，通过在频谱图顶层stacking dense layer，可以重塑频率特性。但无法对时间序列上的变化进行建模。一般用于hybrid structures，比如与隐马尔科夫模型相结合来做和弦识别，与recurrent layer相结合做singing voice transcription等

CNN：卷曲层通常和池化层一起使用，以减小特征映射的尺寸，最大值池化常用于MIR中以增加时间或频率的不变性，1D的卷曲层也直接常用于研究时间频率转换。CNN在MIR中的应用非常广泛，同时也包括music tagging、边界识别等。

RNN：在recurrent layer，上一时刻隐层的状态参与到了这个时刻的计算过程中 ，它具有记忆功能，也能更好地做预测，所以多用于时间变化的MIR问题中，如singing voice detection等。有多对多的recurrent layer和多对一的recurrent layer。

在时间不变的项目中，如music tagging algorithm，使用了convolutional layer 和 recurrent layer两种结构的结合。

在解决MIR问题中的一些有用的建议：Data preprocessing（如spectral whitening），Aggregation information（如pooling、strided convolutions），Depth of networks（在网络深度的问题上，要足够深才能估算输出和输入的关系），第一个输入层、中间层和输出层（一般是Dense layer，结点数为类别数）

同时作者也给出了对时间变化（如DNN、Conv2D等）和不变（Conv1d、CRNN）问题的一些典型模型。

