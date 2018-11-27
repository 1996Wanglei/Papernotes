### MUSICAL TEXTURE AND EXPRESSIVITY FEATURES FOR MUSIC EMOTION RECOGNITION

2018 ismir

论文地址：http://ismir2018.ircam.fr/doc/pdfs/250_Paper.pdf


BY 朱鸿宁_(:з」∠)_
### Motivation：

- 在整个MER领域的研究中，依然有很多Limitation：一是缺乏公共的高质量的数据集；二是与情感相关的声学特征的数量不足
- 很多的音频特征最初都是被用于解决其他的问题（比如语音识别），而缺乏情感相关性
- 所以作者认为需要设计更新颖的音频特征来捕获音乐中的情感，于是作者在这篇文章中解决的问题：高层的特征，即expressivity和music texture features，能否提高在歌曲中的情感内容的检测
- 同时，由于没有数据集能满足作者目前的需求，作者也创建了一个数据集来验证其工作，数据集的分类依据来源于Russell's emotion model



### Methods：

- 建立数据集

  使用心理学模型Russell's circumplex model，从ALLMusic API（Rovi Data）上获取音乐片段（30s）及元数据（歌手、心情、种类等），包括289种心情，与Warriner's list做交集，最后得到200种基于AV的ALLMusic tags。之后要求受试者根据Russell's quadrants进行标记。最后去除了受试者与ALLMusic提供的不相符的标记。

  得到每一个象限一共有225个片段，一共有900个片段。

- 特征的确定

  很多的音频特征都处于low-level，仅仅从频谱图或声波中提取信息。但是人类能感知处于high-level的音乐概念，比如和声、旋律、甚至间隔。所以作者需要提取出high-level的特征

  - estimating MIDI notes

    使用的是现成的算法来完成，没有创新。

  - musical texture features

    提出特征来捕获与一首歌的音乐层面相关的信息。

    - Musical Layers statistics：

    使用六项来统计：mean, standart deviation, skewness, kurtosis, maximum, minimum values

    - Musical Layers Distribution

    - Ratio of Musical Layers Transitions

  - expressivity features

    - Articulation Features 演奏法

      连奏 legato 和 断奏 staccato 对歌曲片段中音符之间的所有过度进行分类

      定义了几种特征：Staccato Ratio (SR), Legato Ratio (LR) and Other Transitions Ratio (OTR). 

      Staccato Notes Duration Ratio (SNDR), Legato Notes Duration Ratio (LNDR) and Other Transition Notes Duration Ratio (OTNDR) statistics. 

    - Glissando Features 滑奏

      从一个音符滑奏到另一个音符。通常被使用为装饰音,与音乐中的某种情感有关

      通过分析两个音之间的过渡来评估。

      - Glissando Presence(GP) 

      - Glissando Extent (GE) statistics 

      - Glissando Duration (GD) and Glissando Slope (GS) statistics

      - Glissando Coverage (GC)

      - Glissando Direction (GDIR)

      - Glissando to Non-Glissando Ratio (GNGR)

    - Vibrato and Tremolo Features 颤音 

      Vibrato包括音高的变化的比例和数量、持续性。

      - Vibrato Presence (VP)

      - Vibrato Rate (VR) statistics

      - Vibrato Extent (VE) and Vibrato Duration (VD) statistics

      - Vibrato Notes Base Frequency (VNBF) statistics

      - Vibrato Coverage (VC)

      - High-Frequency Vibrato Coverage (HFVC)

      - Vibrato to Non-Vibrato Ratio (VNVR)

        但是由于在tremolo范围内的研究较为缺乏，所以作者决定使用vibrato range

- 情感分类

基于大量特征，使用ReliefF feature selection algorithms来排名更适合做情感分类的特征。

使用Support Vector Machines (SVM)来做分类，因为它在以往的MER研究中表现较好



### Results

分类的结果，主要是评估目前的音频特征以及作者提出的新型特性与MER的相关性。其中baseline最好为67.5%左右（100个特征内），而加入novel features之后，novel+baseline的最好F1-Score为76.0%，100个特征中有29个是novel，8个texture，21个expressive，剩下71个还是baseline（50个tone color相关 音色）

同时：有更高的arousal的情感更容易区分（Q1、Q2），而Q3、Q4的歌曲一般具有相同的音乐特征。在novel features的加入后，对Q3的提升最大。



## Musical Texture And Expressivity Features For Music Emotion Recognition

By 王磊

这篇是对朱鸿宁的论文笔记做一些补充。

**Key points**

作者分析当前情感研究中使用的特征，发现大多数特征是底层特征，大多tone color相关的特征。非常缺乏和musical form，music texture和expressive techniques有关的特征，基于此，作者提出一组新的算法，捕捉和musical texture，expressive techniques有联系的信息。为了验证算法，作者构建了一个包含900个30秒的音乐片段的数据集，以Russell emotion quadrants的形式，[此数据集开放下载](http://mir.dei.uc.pt/downloads.html)。

作者用自己提出的novel features和一些经典的特征一起，获得了7.9%F1-Score的提升。

**dataset**

1.作者通过AllMusic API 获得30秒长的audio clips，和歌曲的metadata(包括artist，title，mood，genre)，每首歌带有几个情感标签，总共有289类，将这289类标签和Warriner list取交集，获得每个标签的AV 值，一共有200个tags可以获得匹配的AV值，由于每首歌可能有多个标签，作者只选择了超过总标签数50%的那个标签。

2.由于AllMusic这些标签的获得过程没有完全记录，除了有些标签是由专家标注的，还有一些疑惑就是这些标签标注的过程中，标注者只单独考虑了audio还是lyrics，还是两者一并考虑。同样作者也观察到一些无效的clips，因此作者又对数据集进行了验证，随机分配给验证者一些clips，根据自己perceived的情感来进行标注

3.作者最后移除掉验证者和AllMusic两者标注不符合的clips，最后重新平衡了每个象限clip的数目，每个象限有225个，公共900个。

**Methods**

作者将Marsyas，MIR Toolbox，PsySound3提取的1702个特征，使用Relief 特征选取算法计算出每个特征对于这个问题的权重值，移除了每对相关值超过0.9中权值低的那个，将1702个特征降到898个，将这898个特征用来训练baseline models。

.....

**my opinion**

这篇文章的创新点在于提出一组Musical texture features和Expressivity features，可惜我现在怎么也不懂。