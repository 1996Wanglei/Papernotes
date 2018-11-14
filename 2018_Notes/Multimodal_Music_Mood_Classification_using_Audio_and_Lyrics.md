## Multimodal Music Mood Classification using Audio and Lyrics 

论文地址：http://www.grivolla.net/articles/icmla2008.pdf

By 王磊，好难读啊，好烦啊。

**1.Motivation**

前人没有将歌词和声学信息结合起来用作音乐情感分类，Mahedero等人将歌词用作音乐主题分类，Neumayer等人表明歌词个声学信息在音乐体裁分类中有互补的作用。也有人发现歌词可以用作艺术家相似性检测上。**这篇文章是第一个将歌词和声学信息结合起来用作情感分类的文章。**

**2.Database**

使用categorical classification，分为四个类别，happy，sad，angry，relaxed，理由是覆盖了Russell模型。每一类又作为一个二分类问题，比如说happy or not happy。

情感标签来源于Last.fm,只选用英文歌曲，用Wordnet对上述的四个情感类别建立同义词集合，选择每首歌被标记得最多的标签。之后是validation，验证者要听一首歌三十秒来手动验证这个标签的正确性，可能存在的问题是验证者不能听到整首歌词，可能会倾向于根据音频来判断。对于歌词表达的情感和整首歌表达的情感不一致的时候会产生负面的结果。作者说大多数情况下还是歌词和音频表达的情感是符合的。这个database包含1000首歌曲。

**3.Classification**

- **audio-based** 

  timbral (for instance MFCC, spectral centroid), rhythmic(for example tempo, onset rate), tonal (like Harmonic Pitch Class Profiles) and temporal descriptors,使用的分类器是SVM，Logistic Regression，Random Forest

  ![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/reauslt_1.jpg)

- **Lyrics-based classification**

  三种方法：similarity between lyrics，feature vectors based on Latent Semantic Analusis dimensional reduction，select the most discriminative terms looking at the difierences between language models

  前两种方法对待文本是无监督的方法，向量的表示和情感类别是相互独立的。第三种方法是用四类情感类别来选择一个恰当的歌词表征。

  **第一个实验Classification based on similarity using Lucene** 

  基于一个假设：相似的歌曲它们的体裁，情感也是相似的。一个词袋模型对应一首歌曲，模型的元素是tf-idf权重，歌曲之间的相似性可以用词袋模型来表示。分类器使用的KNN算法，相似的向量就划分到一起。

  ![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/reauslt_2.jpg)

  实验的结果不是很好，因为随机分类的baseline是50%。同样也很难直接融合audio的和lyrics的相似性计算方法，audio这边有不同的分类算法，而lyrics方面则不是。歌词词向量的维度很高，而且是稀疏向量。

  **实验2Classification using Latent Semantic Analysis (LSA)** 

  > 浅层语义分析（LSA）是一种自然语言处理中用到的方法，其通过“矢量语义空间”来提取文档与词中的“概念”，进而分析文档与词之间的关系。LSA的基本假设是，如果两个词多次出现在同一文档中，则这两个词在语义上具有相似性。LSA使用大量的文本上构建一个矩阵，这个矩阵的一行代表一个词，一列代表一个文档，矩阵元素代表该词在该文档中出现的次数，然后再此矩阵上使用奇异值分解（SVD）来保留列信息的情况下减少矩阵行数，之后每两个词语的相似性则可以通过其行向量的cos值（或者归一化之后使用向量点乘）来进行标示，此值越接近于1则说明两个词语越相似，越接近于0则说明越不相似

  作者在第一个实验中发现词-文档矩阵的维度太高，使用LSA的方法将这个矩阵降维到一个低维的空间，更多的分类器可以使用这个特征，作者发现不同的类别，具有最好性能的矩阵维度也不同。

  ![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/reauslt_3.jpg)

  > If our mood categories, as seems to be the case, do not relate to clusters of songs that would be considered similar according to the metrics used in document retrieval,this severely limits the potential of any approaches that are based on document distances with tf.idf weighting 

  作者发现他们的情感类别似乎和被认为相似的歌曲聚类没有对应起来，这会严重限制任何基于tf-idf权重的文献相似性方法的性能。LSA方法也没有解决这个问题，因为在投影空间中的数据点也直接反映出基于tf-idf权重的距离。

  **实验3Classification using Language Model Differences (LMD)** 

  定义document frequency :the proportion of documents containing a given term ,选出不同语言模型中出现频率最高的词汇，这些词汇属于四种分类类别。选用公式3的计算方法，选出n个具有最高mixed值得词汇组成向量。使用SVM,Logstic,RandForest分类器分类。

  ![1542202355257](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/reauslt_4.jpg)

    ![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/reauslt_5.jpg)

 实验结果表明这种方法的分类性能比前面基于距离的方法有较大的提升，其中SVM的分类准确率达到了80%，这个结果也接近基于audio特征的分类结果。

- **Combining Audio and Lyrics information** 

  使用了两种融合方法，一种是先用两个模态单独进行分类，将结果进行融合，另外一种是使用特征融合，将歌词特征个audio特征在一个向量空间里融合。

  其中第二种融合的实验结果，在happy和sad分类上有5%的准确率增加，在angry和relaxed上只有轻微的提升，主要是基于audio的分类准确率已经达到了98%，同样在relaxed类别上的分类准确率也是由于基于audio的准确率已经很高的原因。

  此外，融合特征的分类方法可以减伤标准差，分类的系统会更加鲁棒。

  ![](https://github.com/1996Wanglei/Papernotes/blob/master/2018_ImageSet/reauslt_6.jpg)

