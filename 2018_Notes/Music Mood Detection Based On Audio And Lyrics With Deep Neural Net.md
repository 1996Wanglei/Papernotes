## Music Mood Detection Based On Audio And Lyrics With Deep Neural Net

论文地址：https://arxiv.org/abs/1809.07276

2018.10.31



作者基于2008的文章Multimodal Music Mood Classification using Audio and Lyrics上进一步研究audio，lyrics和valence/arousal之间的关系。作者复现了经典的方法：A svm on top of MFCC,spectral flux,rollof,centroid和A svm on top of basic,linguistic,stylistic features，与三种基于audio，lyrics，和融合两种模态的深度学习模型进行对比。
Dataset：

1. 来自MSD，其中的标签来自last FM，使用文献11的程序选择the tags that akin to a mood description。
2. 用文献30的数据集，讲14000个英语词汇映射到V/A空间。
3. Get the embedding values,normalize the database by centering and reducing valence and arousal
4. MSD does not provide audio signal and lyrics, we should synchronize audio and lyrics

实验的主要结论：

1. Lyrics and audio get similar performance on valence prediction; audio outperforms on arousal prediction
2. Deep learing approaches are much higher than CA based on audio, On the contrary, CA higher performing than deep learing based on lyrics(传统方法使用了基于心理学研究的情绪-词汇特征，而audio 的特征工程没有使用外部的资源)
3. 在late fusion中，arousal detection 任务，融合了lyrics和audio的深度学习模型没有得到提升
4. 在valence detection中，最优表现的模型出现在两个模型比较平均fusion 的情况下。
5. Something interesting：mid-level fusion 在valence检测上有显著得提升，似乎两个模态有某种初期的联系。但是从arousal detection上来看，似乎这种联系时无效的，因为我们已经能看到基于歌词信息的模型不能带来额外的信息。

