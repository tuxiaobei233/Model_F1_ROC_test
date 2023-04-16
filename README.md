# 模型效果评估

本次实验采用Nvidia GTX 2080TI 11GB GPU来进行模型训练和推理，使用具有 32G 内存、500 GB固态硬盘，4TB机械硬盘，AMD Ryzen5 5600G 的计算机存储视频数据集并进行实验相关操作。实验的主要编程语言环境为Python 3.10.6，使用操作系统版本为 Ubuntu 22.04 LTS。

在模型性能对比实验中，除了使用本文提出的检测方法外，我们还选取了一些在视频、音频、文本检测中表现较好的成熟的检测方法作为评价基线，具体如下所示：

(1)视频分类模型

- C3D：C3D模型是一种使用3D卷积网络学习时空特征的模型，它可以对视频序列进行特征提取和分类。C3D模型的主要思想是将3D卷积和3D池化应用于视频帧，从而同时捕获空间和时间维度的信息。C3D模型的结构类似于VGG网络，但是将所有的2D卷积和2D池化替换为3D卷积和3D池化。C3D模型具有高效、简单、紧凑的特点，可以在多个视频理解任务上取得较好的效果。
- TSN：TSN模型是一种用于视频分类的网络模型，它基于2D-CNN，通过稀疏采样视频帧的方式来提取视频的全局信息和局部信息。TSN模型包含两个分支：空间分支和时间分支，空间分支用于提取每帧图像的静态特征，时间分支用于提取相邻帧之间的动态特征。两个分支的特征通过后期融合的方式来进行分类或检测。TSN模型是一种简单而有效的视频理解方法，可以适应不同长度和复杂度的视频。TSN模型是一种利用稀疏采样和双分支结构的视频CNN模型，可以同时学习空间和时间特征。
- Slowfast：Slowfast模型是一种用于视频理解的双模CNN模型，它由两个分支组成：Slow分支和Fast分支。Slow分支使用较少的帧数和较大的通道数来学习空间语义信息，Fast分支使用较多的帧数和较少的通道数来学习运动信息。两个分支通过侧向连接来融合特征，最后进行分类或检测。Slowfast模型受到了灵长类动物视网膜神经细胞种类的启发，可以有效地利用不同速度的视频信息，提高了视频识别的性能。Slowfast模型是一种利用双速率分治策略的视频CNN模型，可以同时学习空间和运动特征。
- VideoSwin：VideoSwin模型是一种基于Swin Transformer的视频分类模型，它利用了Swin Transformer的多尺度建模和高效局部注意力特性，可以在视频Transformer中引入局部性的归纳偏置，提高了速度-准确度的权衡。VideoSwin模型在动作识别和时序建模等视频理解任务上取得了最先进的性能，超过了其他的Transformer模型，例如ViViT和TimeSformer等。VideoSwin模型是一种利用局部注意力机制的视频Transformer模型，可以有效地处理视频序列数据。

(2)音频分类模型

- TDNN：即时延神经网络，是一种用于处理序列数据的神经网络，可以包含多帧的特征输入，通过一维卷积和空洞卷积来提取时序信息。TDNN模型最初用于语音识别问题，可以构建一个时间不变的声音模型，适应不同长度和方言的语音。
- ECAPA-TDNN：该模型是一种用于说话人识别的网络模型，它基于TDNN（Time Delay Neural Network），通过引入SE（Squeeze-Excitation）模块、多层特征融合和通道注意力统计池化等技巧来提高说话人特征的表达能力。ECAPA-TDNN模型在多个说话人验证任务上取得了优异的性能，超越了传统的x-vector和ResNet等模型。
- Res2Net：该模型是一种基于ResNet的卷积神经网络模型，它通过在残差块内部构造分层的类残差连接，来增强多尺度特征的表示能力和感受野范围。Res2Net模型将输入特征图分成多个子集，每个子集经过一个3x3卷积，并与前一个子集的输出相加，形成一个分层的连接结构。Res2Net模块可以提取不同尺度的时频特征，并增加每个网络层的感受野范围，从而提高音频分类的准确率和鲁棒性。Res2Net模型用于音频分类的一些应用场景包括说话人识别，语音情感识别，声纹识别等。
- ResNetSE：该模型是一种在ResNet模型的基础上引入了SE模块（Squeeze-and-Excitation module）的卷积神经网络模型，它通过对每个残差块的输出特征图进行通道间的自适应权重调整，来增强特征的表达能力和选择性。SE模块包括两个步骤：squeeze和excitation。squeeze步骤是对每个特征图进行全局平均池化，得到一个通道维度的向量，表示每个通道的全局信息。excitation步骤是对这个向量进行两层全连接操作，得到一个通道维度的权重向量，表示每个通道的重要性。然后将这个权重向量乘以原始的特征图，得到加权后的特征图。ResNetSE模型可以在不增加计算量和参数量太多的情况下，可以有效地捕获音频信号的通道间关系，增强音频特征的表达能力和选择性。
- PANNS_CNN14：该模型是一种用于音频模式识别的预训练音频神经网络，它在大规模的AudioSet数据集上进行了训练。它使用对数-梅尔谱图作为输入特征，并由14层卷积层和3层全连接层组成。

(3)文本分类模型

- AttentiveConvNet：该模型是一种在卷积神经网络中引入注意力机制的模型，它可以动态地调整卷积操作的视野，使得每个单词或短语的特征表示不仅包含局部上下文信息，还包含全局或跨文本的信息。AttentiveConvNet模型可以应用于自然语言理解的任务，如文本分类、文本蕴含、答案选择等。AttentiveConvNet模型有两个版本：light版本和advanced版本。light版本是基于标准的卷积层和池化层，通过在每个卷积窗口内计算注意力权重来加权求和得到特征表示。advanced版本是在light版本的基础上增加了残差连接和多头注意力机制，以提高特征的多样性和表达能力。
- DPCNN：该模型是一种利用深度金字塔结构和注意力机制进行文本特征提取和分类的模型。它可以通过堆叠卷积层和池化层来提取文本的长距离依赖关系和抽象特征。使用region embedding层将word embedding转换为能够覆盖多个词的特征表示。使用等长卷积层来增强每个词或短语的特征表示，使其包含更广的上下文信息。1/2池化层来降低文本的长度，扩大卷积操作的有效覆盖范围，捕获更多的全局信息。使用固定数量的特征图来减少计算复杂度，保持语义空间的一致性。使用残差连接来支持训练深层网络，解决梯度消失和网络退化的问题。
- DRNN：该模型是一种深层循环神经网络，它可以通过增加隐藏层的层数来增强模型的表达能力和学习长距离依赖的能力12。DRNN模型的主要特点有：每个时刻上的循环体重复多次，形成一个深层的循环结构。每一层循环体中参数是共享的，但不同层之间的参数可以不同。循环体可以是任何类型的递归神经单元，如RNN，LSTM，GRU等。
- FastText：该模型是一种Facebook AI Research在2016年开源的文本分类和词向量训练的工具，它的特点是模型简洁，训练速度快，文本分类准确率也令人满意12。使用所有的单词和相应的n-gram特征作为输入，可以捕捉到词序信息。简单的平均词向量作为文本的表示，可以减少计算复杂度。使用层次softmax作为输出层，可以加速训练过程，适用于大规模的类别数。用预训练的词向量作为输入层，可以提高文本分类的效果。
- TextCNN：该模型是一种用于文本分类的卷积神经网络，它的基本思想是利用不同大小的卷积核来提取句子中的局部特征，然后通过最大池化层和全连接层得到最终的分类结果。可以有效地提取句子中的局部特征，捕捉词序和语义信息。可以使用预训练的词向量，增强模型的泛化能力。
- TextRNN：该模型是一种用于文本分类的循环神经网络（RNN），它的基本思想是利用RNN将句子中的每个词的词向量编码成一个固定长度的向量，然后将该向量输入到一个全连接层得到分类结果。可以有效地处理序列结构，考虑到句子的上下文信息。
- TextRCNN：该模型是一种结合了循环神经网络（RNN）和卷积神经网络（CNN）的文本分类模型，它的基本思想是利用双向RNN来获取句子的上下文信息，然后将词向量和上下文向量拼接起来，通过一个卷积层和一个最大池化层提取特征，最后通过一个全连接层得到分类结果。可以有效地利用双向RNN捕捉句子中的上下文信息，考虑词序和语义信息。可以通过最大池化层自动判断哪些特征在文本分类过程中更重要，减少噪声和冗余信息。可以使用预训练的词向量，增强模型的泛化能力。
- Transformer：该模型是一种基于注意力机制的深度学习模型，它主要用于自然语言处理领域，如机器翻译、文本摘要等。Transformer模型的核心思想是“注意力即是一切”，它摒弃了传统的循环神经网络（RNN）或卷积神经网络（CNN）结构，而是完全使用自注意力机制来捕捉序列中的依赖关系。Transformer模型由编码器（Encoder）和解码器（Decoder）两部分组成，每部分都包含6个子层。编码器负责将输入序列（如源语言句子）编码成一个高维的向量表示，解码器负责根据编码器的输出和已生成的目标序列（如目标语言句子）来生成下一个词。

我们采用了准确率、精确率、召回度、F1值还有ROC 曲线及 AUC 面积，对每一个神经网络模型进行效果评估。这些评价指标已经广泛应用于研究界，成为了现在评价模型性能的重要依据。

对于二分类问题，可将样例根据其真实类别与学习器（分类器） 预测的类别的组合划分为真正例（True Positive）、假正例（False  Positive），真负例（True Negative）、假负例（False Negative）四种 情况，令TP，FP，TN，FN分别表示其对应的样例数， 显然 TP+FP+TN+FN=样例总数。

- True Positive（真正例，TP），被模型预测为正的正样本 
- True Negative（真负例，TN），被模型预测为负的负样本 
- False Positive（假正例，FP），被模型预测为正的负样本
- False Negative（假负例，FN），被模型预测为负的正样本

准确率（Accuracy） 是分类问题中最为原始的评价指标，准确率的定义是预测 正确的结果占总样本的百分比，其公式如下：
$$
Accuracy=\frac{TP+TN}{TP+TN+FP+FN}
$$
精确率（Precision）它是针对预测结果而言的，它的含义是在所有被预测为正的样本 中实际为正的样本的概率，意思就是在预测为正样本的结果中，我们 有多少把握可以预测正确，其公式如下：
$$
Precision=\frac{TP}{TP+FP}
$$
召回率（Recall）它是针对原样本而言的，它的含义是在实际为正的样本中被预测 为正样本的概率，其公式如下：
$$
Recall=\frac{TP}{TP+FN}
$$
综合评价指标 F1 得分，Precision和Recall指标有时是此消彼长的，即精准率高了，召回率 就下降，在一些场景下要兼顾精准率和召回率，最常见的方法就是 F1-Measure，又称F1-Score， 是Precision和Recall的调和平均，当F1-Score较高时，模型的性能越好。
$$
F1-Score=2\times \frac{Precision\times Recall}{Precision+Recall}
$$
而对于本项目的三分类问题而言，我们要依次选取三个标签的每一个作为正样本，然后把其他两个标签作为负样本，计算当前的 TP、TN、FP、FN，依据之前的公式分别计算准确率、精确率、召回率、综合评价指标 F1 得分，再对所有的样本取平均值，这样就得到了最终的确率，精确率，召回率，F1值。具体而言，对于三分类的混淆矩阵 $F_{i,j}$ ，$F_{i,j}$ 即实际标签为 $i$ 的样本被预测为 $j$ 的样本数量，$N$ 为样本总数。
$$
Accuracy=\frac{F_{0,0}+F_{1,1}+F_{2,2}}{N}\\
Precision=(\frac{F_{0,0}}{F_{0,0}+F_{1,0}+F_{2,0}}+\frac{F_{1,1}}{F_{0,1}+F_{1,1}+F_{2,1}}+\frac{F_{2,2}}{F_{0,2}+F_{1,2}+F_{2,2}})\times \frac{1}{3}\\
Recall=(\frac{F_{0,0}}{F_{0,0}+F_{0,1}+F_{0,2}}+\frac{F_{1,1}}{F_{1,0}+F_{1,1}+F_{1,2}}+\frac{F_{2,2}}{F_{2,0}+F_{2,1}+F_{2,2}})\times \frac{1}{3}\\
F1-Score=2\times \frac{Precision\times Recall}{Precision+Recall}
$$

ROC（Receiver Operating Characteristic）曲线，又称接受者操作 特征曲线。该曲线最早应用于雷达信号检测领域，用于区分信号与噪 声。曲线的横坐标为FPR（假正例率），纵坐标为TPR(真正例率)，对 角线对应于“随机猜测”模型，而（0,1）则对应于将所有正例排在所 有反例之前的“理想模型”。FPR和TPR的定义如下：

假正例率（ False Positive Rate ， FPR ）， 又 称 特 异 度 （specificity）：
$$
FPR=\frac{FP}{FP+TN}
$$
真正例率（True Positive Rate，TPR），又称灵敏度（sensitivity），
$$
TPR=\frac{TP}{TP+FN}
$$
若一个模型A的ROC曲线被另一个模型B的ROC曲 线完全包住，则称B的性能优于A。若A和B的曲线发生了交叉，则谁 的曲线下的面积大，谁的性能更优。AUC(Area Under Curve)又称为曲 线下面积，是处于ROC曲线下方的那部分面积的大小。

对于ROC曲线下方面积越大表明模型性能越好，于是AUC就是 由此产生的评价指标。通常，AUC的值介于0.5到1.0之间，较大的AUC 代表了较好的性能。如果模型是完美的，那么它的AUC=1，证明所有 正例排在了负例的前面，如果模型是个简单的二类随机猜测模型，那 么它的AUC=0.5，如果一个模型好于另一个，则它的曲线下方面积相 对较大，对应的AUC值也会较大。

对于 ROC 曲线和 AOC 面积，我们规定谣言视频为正样本，而非谣言与辟谣类视频为正样本，也就是重点关心谣言视频的检测性能。