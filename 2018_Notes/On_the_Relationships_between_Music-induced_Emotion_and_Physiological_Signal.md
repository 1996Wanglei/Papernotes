## On the Relationships between Music-induced Emotion and Physiological Signal

论文地址：http://ismir2018.ircam.fr/doc/pdfs/115_Paper.pdf

2018.10.24



作者基于一个mir系统(歌曲来源Jamendo数据集)，受测者要求在这个系统里面寻找并且听歌，当每首歌曲的dwell time超过30秒要回答两个问题，进行arousal值评价和情绪评价，同时使用可穿戴设备记录受测者的生理特征。实验完成后将每首歌的起止时间和生理特征校准。在提取特征之前，作者将数据进行了normalize处理，得到raw database和normalized database(作者考虑到不同的人生理特征不同)，将情绪评价和arousal评价分为positive，negative，neutral三类。生理特征提取的是一些在前人研究里证明有用的特征，其中包括skin conductance response(SCR)和heart rate variability(HRV),作者使用单因素方差分析和t-test检验来寻找在两个数据集上最具有区分度的生理特征。之后作者使用KNN,决策树，朴素贝叶斯，SVM在平衡的数据集上进行分类，因为两种不同类别的数据集(positive，negative)数量不相同，作者在所有用户数据集，单个用户数据集，拥有相同性格特征的用户数据集，具有相同音乐偏好的用户数据集上进行了分类，得出的结论表明分类性能在单个用户数据集上最好，但是也出现了矛盾的数据组，作者认为是所使用的生理特征不同的人差异性很大，同样在电子音乐，摇滚，流行偏好的类别里分类性能也很好，在agreeable性格上也性能比较好，但是作者又发现受测者的数量和性能表现负相关（正好这几个类别人数很少)。