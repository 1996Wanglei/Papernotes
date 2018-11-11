## Music Emotion Recognition_ A State Of The Art Review

论文地址：http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.231.7740&rep=rep1&type=pdf

本文综述了音乐情感自动识别的研究现状（2010年）。

* 情绪心理学研究
  * （在用模型表示情感前，先确定所处理情感的来源）音乐情感分为“表达说”和“唤起说”，“表达说”认为音乐情感是作曲家或演奏者的情感表达，“唤起说”认为音乐情感是听者的情感体验。本文从“表达说”的角度进行。
  * 不同文化背景的人对于音乐情感的感知有`universal psychophysical and emotional cues`
  * 情感表示模型
    * 离散类别模型----分类问题
    * 环形结构模型valence-arousal-----回归问题
    <img src="http://notes-pictures.nos-eastchina1.126.net/20181108065208-717449.jpg" style="zoom:80%">
* 人工标注：调查研究、商业app搜集、有目的的游戏
* contextual text information：歌词、web文档、social tags
* 基于内容的音频分析`content-based  audio analysis`（取代人工标注）
  * 声学特征`Acoustic Features`
    * 用于情绪识别的常用声学特征
      <img src="http://notes-pictures.nos-eastchina1.126.net/20181108064536-883005.jpg"  style="zoom:50%">
    * 多特征融合效果，优于单特征
  * `Audio-based systems`
    * 分类
    * 回归
  * 情绪随时间的变化`Emotion Recognition Over Time`
* 多个特征域混合

  * 音频+歌词
  * 音频+标签
  * 音频+图象



主要结论

１）与其他的音乐概念识别任务相比，情感识别还处于初级阶段。
２）人情感固有的模糊性，使情感主观且难以量化。
３）音乐情感识别都依赖一个情感模型，但情感模型仍然是心理学研究的一个活跃课题。
４）音乐情感并不是完全包含在音频中．单靠音频数据本身，不能完全识别音乐情感。
５）基于音频的音乐情感识别是音乐信息检索研究者的一项长期目标。


