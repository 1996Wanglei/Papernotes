### MUSICAL TEXTURE AND EXPRESSIVITY FEATURES FOR MUSIC EMOTION RECOGNITION

2018 ismir

论文地址：http://ismir2018.ircam.fr/doc/pdfs/250_Paper.pdf

####Motivation：

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



####Results

分类的结果，主要是评估目前的音频特征以及作者提出的新型特性与MER的相关性。其中baseline最好为67.5%左右（100个特征内），而加入novel features之后，novel+baseline的最好F1-Score为76.0%，100个特征中有29个是novel，8个texture，21个expressive，剩下71个还是baseline（50个tone color相关 音色）

同时：有更高的arousal的情感更容易区分（Q1、Q2），而Q3、Q4的歌曲一般具有相同的音乐特征。在novel features的加入后，对Q3的提升最大。