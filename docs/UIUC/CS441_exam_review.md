## Exam 2 Review (Lectures 2–20)

Format: 25 multiple choice / multi-select questions, conceptual only (no coding). MC = 3 pts, multi-select = 5 pts with partial credit (no multiple attempts). L2–20 都考，前后半程比重差不多。点开 "Answer" 前先自己做。**MS** = select all that apply.

**建议顺序**：先过一遍 [算法与缩写总表](#glossary) 和 [易混点对比](#cross-lecture)，再做 [Mock exam](#mock-exam) 找弱点，最后回到对应 lecture 的题补漏。题目是按课件和笔记自拟的，不是真题；课程官方练习题（不显示答案）在 [All Questions form](https://tinyurl.com/AML441-AllQs)，其中 L2–L20 和 "Exam 2: Extra Questions" 都相关。

### One-page cheat sheet

| Topic                    | Must know                                                    |
| ------------------------ | ------------------------------------------------------------ |
| **Trees (L12)**          | Greedy split by **information gain** $IG=H(Y)-H(Y\mid X)$; $H=-\sum p\log_2p$ (max 1 bit for a binary variable at $p=0.5$); $H\ge0$, $H(Y\mid X)\le H(Y)$, $H(Y\mid Y)=0$. Regression tree: minimize squared error, leaf = **mean**. Axis-aligned splits; stop early (min leaf size / max depth) to generalize; Gini is an alternative criterion. One tree is weak, a forest is strong |
| **Ensembles (L13)**      | Expected error = variance + noise + bias². **Random forest**: deep trees (low bias/high variance), random data + features, **average** → ↓**variance**. **Boosting/AdaBoost**: small trees (high bias/low variance), sequential, re-weight mistakes, weighted vote / sum of logits → ↓**bias**, can overfit. Weak learner = better than 50% |
| **SGD (L14)**            | Step opposite the gradient; lr too big → overshoot, too small → slow. Convex (linear reg., logistic, SVM) = no local-minima issue; MLPs are not. Mini-batch: cost $O(B)$, gradient noise $O(1/\sqrt B)$. Pegasos: only in-margin examples push; always shrink $(1-\eta\lambda)$. New random order each epoch |
| **MLP / backprop (L15)** | Perceptron = linear. Layers need **non-linear activations** (stacked linear = one linear). Sigmoid (max slope 0.25 → vanishing gradient), ReLU (slope 1 for $x>0$). Backprop = chain rule, **sum over paths**, reuse shared terms (dynamic programming). MLP: lower bias, higher variance, non-convex, more data/compute |
| **CNN / ResNet (L16)**   | Conv = shared learned filter → feature map, translation invariance; pooling grows receptive field. AlexNet 2012 = ReLU + ImageNet + GPU (+ dropout). Deep nets got *worse training error* → optimization problem. **ResNet** $F(x)+x$ skip. **BatchNorm** normalize per batch, learn $\gamma,\beta$. Adam = momentum + RMSProp |
| **Training / CV (L17)**  | Loop: forward → loss → `zero_grad` → `backward` → `step`. Augmentation ↓**variance**. Little data → **linear probe**; moderate → **fine-tune** (low lr!); huge → fine-tune or scratch. R-CNN → Fast (share features, RoI pool) → Faster (RPN) → Mask (RoIAlign + masks + keypoints). U-Net = encoder–decoder + skips |
| **Words / attention (L18)** | Tokenization: character / subword (BPE: merge the most frequent pair, recount) / word (`<unk>`). Skip-gram: center → context; CBOW: context → center. **Attention = average of values, weighted by key–query similarity.** Self-attention ≈ soft clustering; cross-attention ≈ instance-based regression. Block = multi-head attention + MLP, residual + LayerNorm. Order-invariant → positional encoding |
| **BERT / ViT (L19)**     | BERT: encoder-only, bidirectional, pre-trained on **MLM + NSP**, unlabeled text, fine-tune with a linear layer. ViT: patches → linear projection + position + [CLS] → same Transformer encoder. CNN: better with less data (locality bias); Transformer: scales better, any modality |
| **CLIP / GPT (L20)**     | **Foundation model** = huge data + broad task. **Zero-shot** = no examples for this task. CLIP: image + text encoders, **contrastive** matching (32K × 32K, cross-entropy both ways), 400M pairs; zero-shot via label → caption. GPT: **predict the next token**. GPT-1 fine-tuned; GPT-2 zero-shot; GPT-3 (175B) few-shot in context, no weight updates. ChatGPT = SFT → RLHF. Scaling laws: loss is a power law in N, D, C. CoT helps reasoning and only works at scale |
| **Foundations (L2–11)**  | KNN: larger K → smoother, ↓variance ↑bias. Train/val/test roles. PCA keeps max variance (linear); MDS distances; IsoMap graph distances; t-SNE/UMAP neighbors. L1 sparse, L2 small + closed form. LR: every point has loss; SVM: support vectors, "confident enough". NB: independent **given y**. EM: E = latent probabilities, M = weighted parameters, local optimum; K-means = hard EM. MoG semi-parametric; KDE/histogram non-parametric. Median, RANSAC, IRLS are robust; least squares isn't |

**Frequent traps**

-   Bagging / RF reduce **variance**; boosting reduces **bias** (small ↔ large trees are swapped in wrong answers)
-   Training error rising with depth = **optimization**, not overfitting
-   Data augmentation reduces variance; it does **not** add expressiveness
-   Fine-tuning lr is **lower** than from-scratch lr; linear probe freezes the encoder
-   Perceptron/linear models can't fit XOR / circle-shaped boundaries; MLPs can but aren't convex
-   Larger batch = more stable gradient, but it costs proportionally more per step
-   Attention averages **values**, weighted by **key–query** similarity (not "queries weighted by key–value")
-   BERT = fill in masked tokens + next *sentence*; GPT = next *token*; CLIP = match image to text
-   Telling *log* (wood) from *log* (math) needs context (attention); word and subword tokenizers both give it the same token
-   GPT-3 few-shot = examples in the prompt, **no gradient updates**; fine-tuning changes the weights
-   Fine-tuning CLIP's encoder makes it lose its general image–text matching; zero-shot, linear probe and K-NN on its features don't

### 易混点对比（跨 lecture） {#cross-lecture}

考题常把不同 lecture 的概念放进同一题。这几张表按**考法**整理，不按 lecture。

#### 1. 这个方法到底在解决什么问题？

先看症状，再选方法：**train error 高 → bias 或 noise**；**test error 远高于 train error → variance**；**更深的网络 train error 反而更高 → optimization**。

| 问题             | 有效的方法                                                   | 常见错误选项                                  |
| ---------------- | ------------------------------------------------------------ | --------------------------------------------- |
| **↓ Variance**   | Larger K; more training data; stronger regularization; simpler model; bagging / RF; data augmentation; averaging networks; linear probe (little data) | Boosting; more layers                         |
| **↓ Bias**       | Smaller K; weaker regularization; more complex model (perceptron → MLP); boosting; fine-tune instead of linear probe; decrease weight | More data; bagging                            |
| **Optimization** | ReLU instead of sigmoid; skip connections; BatchNorm; momentum / Adam; learning-rate tuning | Dropout, augmentation (those target variance) |
| **Noise**        | None: irreducible for the given features                     | "A bigger model fixes it"                     |

#### 2. 所有方法对比总表 {#all-methods}

L2–20 的所有方法放在同一张表里，列都一样，可以直接横向比（例如 "BERT 和 CLIP 都不用人工标签"、"t-SNE 和 K-means 都依赖初始化"）。按方法类型分组，括号里是 lecture。

!!! info "三种 SVM 的关系"
    **Kernelized SVM** = 把 dual 里的点积 $x_i^Tx_j$ 换成核函数 $k(x_i,x_j)$。**Linear SVM** 就是用 linear kernel 的特例；**RBF SVM** 是用 Gaussian (RBF) kernel 的 kernelized SVM，polynomial kernel 也是一种。三者都是**凸**的，区别在于：边界是否线性、参数个数（primal 每个特征一个 vs. dual 每个训练样本一个 $\alpha$）和速度。Pegasos 是用 SGD 解 linear SVM 的 primal。

| 方法 | 任务 | 监督方式 | 函数形式 | 怎么学（目标） | 求解 | 最优解 | 依赖初始化 / 随机性 | 需要 feature scaling | 关键超参 | 考点 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ***有监督 · 经典模型*** | | | | | | | | | | |
| **KNN** (L2–3) | 分类 / 回归 | 有监督 | 非线性，按距离划分 | 不学，存训练集 | 无训练 | — | 否 | **要** | K、距离度量 | 1-NN 训练误差 0；加新样本最容易；预测慢；K↑ → ↓var ↑bias |
| **Linear regression** (L6) | 回归 | 有监督 | 线性 | 平方误差 + L1/L2 | 无正则或 L2：闭式；L1：迭代 | 凸，全局 | 否 | 有正则时要 | λ | 能外推、系数可解释；对 outlier 敏感 |
| **Logistic regression** (L7) | 分类 | 有监督 | 线性 | $-\log P(y\mid x)$ + 正则 | 迭代（GD） | 凸，全局 | 否 | 有正则时要 | λ | 每个点都有 loss；概率估计好；分类网络的最后一层 |
| **Perceptron** (L14) | 分类 | 有监督 | 线性 + 阈值 | MSE / logistic loss | SGD | 凸 | 基本否 | 要 | lr | 只能拟合线性可分数据（XOR 不行） |
| **Linear SVM** (L7, L14) | 分类 | 有监督 | 线性 | hinge loss + $\lVert w\rVert^2$（最大 margin） | QP，或 Pegasos（SGD） | 凸，全局 | 否 | 要 | C 或 λ | 只依赖 support vectors；"够自信就行" |
| **Kernelized SVM**（RBF / polynomial）(L7) | 分类 | 有监督 | **非线性** | dual：每个训练样本一个 $\alpha$，用 $k(x_i,x_j)$ 代替点积 | QP | **凸，全局** | 否 | **要** | C、核函数、RBF 的 σ | σ 越小越像最近邻，越能贴合训练集；训练和预测慢；已基本被深度网络取代 |
| **Naïve Bayes** (L8) | 分类 | 有监督 | 通常线性 | MLE / MAP 计数 | 闭式 | 全局 | 否 | 否 | 平滑 α | 假设给定 y 时特征独立；数据少也行；置信度不准 |
| **Decision tree** (L12) | 分类 / 回归 | 有监督 | axis-aligned，分段常数 | 每步最大 IG / 最小平方误差 | **贪心**递归 | 不保证 | 否（但数据稍变树就变 → 高 var） | **否** | 深度、最小叶子 | 不限深度时训练误差可为 0；可解释 |
| ***有监督 · 集成*** | | | | | | | | | | |
| **Bagging** (L13) | 分类 / 回归 | 有监督 | 同基模型 | bootstrap 抽样后各自训练，投票 | 独立，可并行 | — | 有随机抽样 | 同基模型 | 模型个数 | ↓**variance** |
| **Random forest** (L13) | 分类 / 回归 | 有监督 | 分段常数 | **深**树 + 随机样本 + 随机特征，**平均** | 独立，可并行 | — | 有随机性，但结果稳定 | 否 | 树数、每次选的特征数 | ↓**variance**；很难训坏；高维数据表现好 |
| **Boosted trees / AdaBoost** (L13) | 分类 / 回归 | 有监督 | 分段常数 | **小**树，**按顺序**加权错误样本，logit 求和 | 顺序 | — | 否 | 否 | 树数、树深 | ↓**bias**；可能过拟合；Caruana 对比中最好 |
| ***无监督 · 聚类、密度、隐变量*** | | | | | | | | | | |
| **K-means** (L4) | 聚类 | 无监督 | 硬分配到最近中心 | 最小化到中心的平方距离 | 迭代，两步交替 | **局部** | **是** | **要** | K | = hard EM |
| **EM**（通用算法）(L9) | 隐变量 + 参数 | 无监督 / 缺失数据 | 取决于模型 | 最大化似然（下界） | 迭代：E 求隐变量概率，M 加权重估参数 | **局部** | **是** | — | 模型形式 | 不是模型，是求解方法；用于 MoG、bad annotators、topic models |
| **MoG / GMM** (L10) | 密度 / 软聚类 | 无监督 | 半参数：高斯加权和 | 最大似然 | 用 EM 迭代 | **局部** | **是** | — | 成分数 | 软分配（K-means 是硬分配）；可检测 outlier |
| **KDE / histogram** (L10) | 密度 | 无监督 | 非参数 | 不学，存数据 / 计数 | 无训练 | — | 否 | KDE 要 | 带宽 h / bin 数 | 低维好、高维差；用验证集 log-likelihood 选超参 |
| ***无监督 · 降维、检索*** | | | | | | | | | | |
| **PCA** (L5) | 降维 | 无监督 | **线性**投影 | 最大方差 = 最小重建 MSE | 闭式（特征分解 / SVD） | 全局 | 否 | **要** | 维数 | 不用标签，可能丢判别信息；重建误差可找 outlier |
| **MDS / IsoMap** (L5) | 降维 | 无监督 | 非线性嵌入 | 保留两两距离（IsoMap 用图最短路径距离） | 经典 MDS：闭式 | 经典 MDS：全局 | 否 | 要 | 维数；IsoMap 的邻居数 | IsoMap 能展开全局流形；MDS 受远点影响大 |
| **t-SNE** (L5) | 可视化降维 | 无监督 | 非线性嵌入 | 最小化 KL（邻居概率分布） | 梯度下降 | **局部** | **是** | 要 | σ（邻域大小） | 簇分得最开，但破坏全局形状；慢；通常先 PCA |
| **UMAP** (L5) | 降维 | 无监督 | 非线性嵌入 | 保留 kNN 局部结构 | 迭代优化 | 局部 | 是 | 要 | 邻居数、目标维数 | 比 t-SNE 快很多 |
| **LSH** (L4) | 近似检索 | 无监督 | 随机投影 → bit → bucket | 不学 | 无训练 | — | 随机投影 | 要 | bit 数 | 用精确度换速度 |
| ***鲁棒拟合*** | | | | | | | | | | |
| **RANSAC** (L11) | 鲁棒拟合 | — | 任意模型 | 最大化 inlier 比例 | 随机抽最少点拟合并打分，重复 | — | 随机 | — | 阈值、迭代次数 | outlier 直接排除；outlier 越多越慢 |
| **IRLS** (L11) | 鲁棒拟合 | — | 任意模型 | 鲁棒 loss | 迭代重加权最小二乘 | 局部 | 从最小二乘解开始 | — | loss 形状 | 保留所有点，只降低权重 |
| ***神经网络与 foundation models*** | | | | | | | | | | |
| **Word2Vec** (L18) | 词向量 | 自监督（上下文） | 浅层线性 | CBOW / skip-gram 预测上下文 | SGD | 非凸 | 是 | — | 向量维数 | 向量算术：Paris − France + Italy = Rome |
| **MLP** (L15) | 分类 / 回归 | 有监督 | 非线性 | 任意 loss | SGD + backprop | **非凸** | **是** | 要（输入归一化） | lr、宽度、深度 | 比 perceptron ↓bias ↑var；sigmoid 会梯度消失 |
| **CNN / ResNet** (L16–17) | 图像 | 有监督（如 ImageNet） | 卷积 + pooling + FC | 交叉熵 | SGD / Adam | 非凸 | 是 | 要（像素归一化） | lr、深度、augmentation | 局部性偏置，数据少时更好；skip connection 解决优化问题；常作预训练 backbone |
| **Transformer** (L18) | 任意 token 序列 | 视任务 | attention + MLP，residual + LayerNorm | 视任务 | SGD / Adam | 非凸 | 是 | — | 层数、维数、头数 | 与顺序无关，所以要 PE；数据越多越占优 |
| **BERT** (L19) | 语言表示 | **自监督** | encoder-only，双向 | **MLM + NSP**（BooksCorpus + Wikipedia） | SGD / Adam | 非凸 | 是 | — | — | 加线性层**微调** |
| **GPT-1 / 2 / 3** (L18, L20) | 语言生成 | **自监督** | decoder-only，causal（masked） | **预测下一个 token**（GPT-2：WebText；GPT-3：300B tokens） | SGD / Adam | 非凸 | 是 | — | — | GPT-1 微调；GPT-2 zero-shot；GPT-3（175B）few-shot in context，不更新权重；ChatGPT = SFT + RLHF |
| **ViT** (L19) | 图像分类 | 有监督（JFT / ImageNet-21k） | encoder-only，16×16 patch | 分类 | SGD / Adam | 非凸 | 是 | — | patch 大小 | 预训练数据越大越好；[CLS] + 线性头 |
| **CLIP** (L20) | 图文表示 | **自然语言监督**（无类别标签） | 图像 encoder + 文本 Transformer | **对比匹配** 4 亿图文对 | SGD / Adam | 非凸 | 是 | — | batch 大小（32K） | zero-shot、linear probe、K-NN；微调会丢掉通用性 |

#### 3. 按性质反查 {#by-property}

跨课程的题通常问"下列哪些具有某性质"。先在这里查，再回总表看原因。

| 题目问法 | 符合 | 常被误选 |
| --- | --- | --- |
| 线性决策边界 / linear classifier | Perceptron、Logistic regression、Linear SVM、Naïve Bayes（通常） | Kernelized / RBF SVM、1-NN、Decision tree、MLP |
| 凸 / 只有一个局部最优 / 能得全局最优 | Linear & logistic regression、Linear SVM、**Kernelized SVM**、Naïve Bayes、PCA、经典 MDS | Decision tree（贪心）、K-means、EM / MoG、t-SNE、所有神经网络 |
| 不同初始化 → 参数明显不同 | K-means、EM / MoG、t-SNE、UMAP、MLP、CNN、Transformer（BERT / GPT / ViT / CLIP） | Logistic regression、SVM（凸） |
| 一定能把训练误差降到 0（没有冲突样本时） | 1-NN、不限深度的决策树 | 线性模型、Naïve Bayes（RBF SVM 只在 σ 很小时接近） |
| 有闭式解 | Linear regression（无正则或 L2）、Naïve Bayes、PCA、经典 MDS | L1 regression、Logistic regression、SVM、K-means、EM |
| 不用训练 / 最容易加新样本 | KNN、KDE、LSH | — |
| 不需要 feature scaling | Decision tree、Random forest、Boosted trees、Naïve Bayes | KNN、K-means、PCA、SVM |
| 只依赖少数训练样本 | Linear / kernelized SVM（support vectors） | Logistic regression（每个点都有 loss） |
| 能外推 | Linear regression | KNN、树、RF（输出的是训练目标的平均） |
| 无监督 | K-means、EM / MoG、KDE、PCA、MDS / IsoMap、t-SNE、UMAP、LSH | — |
| 预训练不需要人工标签 | Word2Vec、BERT、GPT、CLIP（用自然语言） | ImageNet CNN、ViT（用类别标签） |
| 能 zero-shot | CLIP、GPT-2 / GPT-3 | BERT、ImageNet CNN（要微调） |
| 用 SGD / backprop 训练 | MLP、CNN、Transformer 系列、Word2Vec；Pegasos 解 linear SVM | Naïve Bayes、PCA、决策树 |
| 主要 ↓variance / ↓bias | 见第 1 节 | — |

#### 4. 同一个词，不同的意思

| 词                | 不同 lecture 里的含义                                                                                                   |
| ----------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Weights**       | Sample weights (AdaBoost: raise for mistakes); latent probabilities (EM $w_a$); inlier weights (IRLS: lower for outliers); attention weights (computed from data, sum to 1); network parameters (learned) |
| **Encoder / decoder** | Pre-trained backbone + final linear layer (L17); U-Net downsample + upsample (L17); translation Transformer with cross-attention (L18). BERT and ViT are encoder-only with a simple head; GPT is decoder-only with masked attention |
| **Skip connection** | ResNet: add input to the block output, helps gradients. U-Net: mirrored encoder → decoder, passes spatial detail. Transformer: residual around attention and MLP |
| **Normalization** | BatchNorm: over the mini-batch (CNNs). LayerNorm: within each token (Transformers). Both are for stable training, not for expressiveness |
| **Position**      | CNN: index in the feature map. Transformer: added positional embedding. Fourier features (L15): input encoding so the dot product reflects closeness |
| **Projection**    | PCA: from data covariance, unsupervised. LSH: random. ViT patch embedding and Q/K/V: learned by backprop |
| **Embedding**     | PCA / t-SNE / UMAP: low-D coordinates of data points. Word2Vec and token embeddings: a learned vector per token. CLIP: shared space for images and text |
| **Random**        | Bagging / RF: data (and features). SGD: batches. RANSAC: minimal samples to fit. LSH: projections. Boosting differs: trees are trained **sequentially** on re-weighted samples |
| **Soft vs. hard** | K-means = hard, EM/MoG = soft. Self-attention behaves like soft clustering; cross-attention like distance-weighted KNN regression |
| **Few / zero**    | Zero-shot: no examples for this task. Few-shot (GPT-3): a few examples in the prompt. Linear probe: trains a new linear layer. Fine-tune: updates the whole network |

#### 5. 网络组件对比：FC / MLP vs. convolution / CNN vs. attention / Transformer

| 性质 | Linear / FC（MLP） | Convolution（CNN） | Self-attention（Transformer） |
| --- | --- | --- | --- |
| 输出依赖输入顺序 | 是（每个位置有自己的权重） | 是（窗口里的相对位置） | **否**，除非加了位置编码 |
| 不同位置用同一组权重 | 否 | **是**（权重共享） | 投影 $W_q,W_k,W_v$ 共享，但混合权重由数据算出 |
| 假设邻域结构 | 否 | **是**（局部窗口） | 否：每个 token 看所有 token |
| 计算主要是线性运算 | 是 | 是 | 是 |
| 输入长度可变 | 否 | 是 | 是 |
| 内置的先验 | 无 | 局部性 + 平移不变 → 数据少时 variance 低 | 几乎没有 → 数据越多越占优 |
| 经典 ML 里的类比 | 叠起来的线性模型（perceptron、logistic regression） | 线性滤波（L16） | cross-attention ≈ 距离加权的 **KNN regression**（L3）；self-attention ≈ **soft clustering**（K-means / EM，L4 / L9–10） |
| 典型模型 | MLP；各种网络的最后一层 | LeNet、AlexNet、ResNet、U-Net、Mask R-CNN | BERT、GPT、ViT、CLIP 的文本（和 ViT 图像）encoder |

!!! tip "EM、K-means、KNN 和 attention 为什么像"
    它们都在做**按相似度加权平均**：

    -   MoG 的 M-step：$\hat\mu_m=\frac{\sum_n\alpha_{nm}x_n}{\sum_n\alpha_{nm}}$，权重 $\alpha_{nm}$ 是隐变量的后验概率
    -   Attention：$out(q)=\frac{\sum_i s(k_i,q)\,v_i}{\sum_i s(k_i,q)}$，权重来自 key–query 相似度
    -   KNN regression：只对最近的 K 个取平均（权重为 0 或 1）；K-means 也是硬分配

    区别：EM / K-means 是**反复迭代到收敛**的拟合算法；attention 是网络里的**一层**，相似度用**学到的** Q/K 投影计算，靠 backprop 训练。软的对应 EM 和 attention，硬的对应 K-means 和 1-NN。

### 算法与缩写总表（L2–20） {#glossary}

按 lecture 顺序列出所有算法、模型和缩写，方便查名字；要跨课程比较性质，看 [所有方法对比总表](#all-methods) 和 [按性质反查](#by-property)。"考点"一栏只写最常考的一句；细节回 [CS441 笔记](CS441.md)。没有缩写的算法（K-means、Pegasos 等）也放在这里。

#### 缩写撞车：同一个缩写，不同的意思

| 缩写       | 意思 1                                              | 意思 2                                                  |
| ---------- | -------------------------------------------------- | ------------------------------------------------------ |
| **LR / lr** | Logistic Regression（L7）                           | learning rate（L14 起，写作 `lr`）                       |
| **NN**     | Nearest Neighbor（L2、L7 recap）                      | Neural Network（L15 起）                                 |
| **MAP / mAP** | Maximum A Posteriori 最大后验（L8）                 | mean Average Precision，检测指标（L17）                   |
| **CV**     | Cross-Validation（L6）                               | Computer Vision（L17）                                   |
| **Bias**   | bias–variance 里的偏差（L3）                          | 模型里的常数项 $b$（L6）                                   |
| **Kernel** | SVM 核函数（L7）                                     | KDE 核（L10）；卷积核 `kernel_size`（L16）                  |
| **Encoder** | 预训练 backbone（L17）                              | Transformer encoder（L18–19）；CLIP 两个 encoder（L20）     |

#### L2–3 · KNN 与泛化

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **KNN**     | K-Nearest Neighbors               | K 近邻         | 分类取多数标签，回归取均值。K 越大越平滑：↓variance ↑bias；1-NN 训练误差为 0 |
| **i.i.d.**  | independent and identically distributed | 独立同分布 | 默认 train/test 来自同一分布                                         |
| **L1 / L2** | Manhattan / Euclidean distance    | 曼哈顿/欧氏距离 | 加上 dot product、cosine similarity，是 KNN 常用的相似度               |
| **RMSE**    | Root Mean Squared Error           | 均方根误差      | 有单位                                                               |
| **MAE**     | Mean Absolute Error               | 平均绝对误差    | 有单位，对 outlier 没 RMSE 敏感                                      |
| **R²**      | coefficient of determination      | 决定系数        | 无单位，解释的方差比例；接近 1 = 线性可预测                            |
| Generalization error | test error − training error | 泛化误差      | 课程定义；数据越多，这个差距越小                                      |

#### L4 · 检索与聚类

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **FAISS**   | Facebook AI Similarity Search     | —             | 高度优化的检索库，暴力搜索也很快                                       |
| **LSH**     | Locality Sensitive Hashing        | 局部敏感哈希    | 随机投影 → bit → bucket，近似搜索；hash key 越长越准，但查询更慢（课上说法） |
| K-means     | —                                 | K 均值         | 交替"分给最近中心 / 中心取均值"；依赖初始化，K 要自己选；= hard EM         |
| Hierarchical K-means | —                        | 层次 K 均值     | 查找 $O(\log K\cdot D)$，比 $O(K\cdot D)$ 快                          |
| Agglomerative clustering | —                    | 凝聚聚类       | 自底向上合并，找数据结构                                              |
| Purity      | —                                 | 纯度           | 每簇最多标签的数量之和 ÷ N；需要标签                                   |

#### L5 · 降维

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **PCA**     | Principal Component Analysis      | 主成分分析      | **线性**投影，保留最大方差（= 最小重建 MSE）；协方差矩阵的特征向量；不用标签，可能丢掉判别信息 |
| **SVD**     | Singular Value Decomposition      | 奇异值分解      | $A=U\Sigma V^T$，可以用来算 PCA                                      |
| Eigenfaces  | —                                 | 特征脸         | PCA 用在人脸上；成分越多重建越好                                       |
| **MDS**     | MultiDimensional Scaling          | 多维缩放       | 保留**两两距离**；欧氏距离有闭式解；受远点影响大                         |
| Non-metric MDS | —                              | 非度量 MDS     | 只保留距离的**排序**，更慢                                            |
| **IsoMap**  | Isometric Mapping                 | 等距映射       | MDS + **图最短路径**（geodesic）距离；能展开 S-curve                    |
| **t-SNE**   | t-distributed Stochastic Neighbor Embedding | t 分布随机邻域嵌入 | 保留**邻居概率分布**，最小化 KL；簇分得最开，但破坏全局形状，慢       |
| **UMAP**    | Uniform Manifold Approximation and Projection | 均匀流形近似投影 | 保留局部结构，比 t-SNE 快很多                                    |
| **KL**      | Kullback–Leibler divergence       | KL 散度        | t-SNE 的目标函数                                                     |

#### L6 · 线性回归

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| Least squares | ordinary least squares          | 最小二乘       | 闭式解 $w=(X^TX)^{-1}X^Ty$（伪逆）；对 outlier 敏感                   |
| **L1 = Lasso** | —                              | L1 正则        | 权重**稀疏**（正好为 0），自动特征选择；**无**闭式解                    |
| **L2 = Ridge** | —                              | L2 正则        | 权重小但不为 0，适合相关特征；**有**闭式解                             |
| Elastic net | —                                 | 弹性网络       | L1 + L2                                                              |
| Grid / line / randomized search | —           | 超参搜索       | 3 个以上超参时 randomized 往往最好                                     |
| **CV / LOOCV** | Cross-Validation / Leave-One-Out CV | 交叉验证 / 留一法 | 训练数据少时用；LOOCV 是 N 折                                      |

#### L7 · 线性分类器

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **LR**      | (Linear) Logistic Regression      | 逻辑回归       | 用线性函数建模 **log-odds（logit）**；每个点都有非零 loss；凸；"最大化置信度" |
| Sigmoid / softmax | —                           | —             | 二分类 / 多分类时把分数变成概率                                       |
| **SVM**     | Support Vector Machine            | 支持向量机      | 最大化 margin；只依赖 **support vectors**；"足够自信就行"；凸           |
| Hinge loss  | —                                 | 合页损失       | margin ≥ 1 时为 0，否则线性增长                                       |
| Soft margin / $C$ | —                           | 软间隔        | $C$ 控制允许多少违反 margin                                          |
| Primal / dual | —                               | 原问题/对偶    | primal 每个**特征**一个参数；dual 每个**样本**一个 $\alpha$（大多为 0）  |
| Representer theorem | —                         | 表示定理       | L2 正则的最优 $w$ 是训练样本的加权和；L1 不适用                        |
| **RBF** kernel | Radial Basis Function          | 径向基（高斯）核 | 非线性 SVM；$\sigma$ 越小越像最近邻                                 |
| **HOG**     | Histogram of Oriented Gradients   | 方向梯度直方图   | Dalal–Triggs 2005：HOG + linear SVM 行人检测                          |

#### L8 · 朴素贝叶斯

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **NB**      | Naïve Bayes                       | 朴素贝叶斯      | 假设特征**在给定 y 时**条件独立；训练/预测都快；数据少时不易过拟合；置信度不准 |
| **MLE**     | Maximum Likelihood Estimation     | 最大似然估计    | 只用数据：count / total                                               |
| **MAP**     | Maximum A Posteriori              | 最大后验估计    | 数据 + 先验；Laplace smoothing $\frac{count+\alpha}{N+\alpha k}$；α=0 即 MLE |
| Bernoulli / categorical / Gaussian NB | —     | —             | 二值 / 多值离散 / 连续特征                                             |

#### L9–10 · EM 与概率密度估计

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **EM**      | Expectation-Maximization          | 期望最大化      | **E**：给定参数算隐变量概率；**M**：按这些概率加权重估参数；每步提高似然下界（Jensen），收敛到**局部**最优 |
| Hard EM     | —                                 | 硬 EM         | E-step 只取最可能的值；**K-means 就是 hard EM**                         |
| Latent variable | —                             | 隐变量        | 没观测到但模型需要的变量（好/坏标注者、前景/背景、topic）                  |
| **PDF**     | Probability Density Function      | 概率密度函数    | 积分为 1，但**值可以大于 1**                                          |
| **MoG / GMM** | Mixture of Gaussians / Gaussian Mixture Model | 高斯混合模型 | **半参数**；用 EM 拟合；成分够多能拟合几乎任何分布              |
| **KDE**     | Kernel Density Estimation         | 核密度估计      | **非参数**；bandwidth 太小 → 尖刺，太大 → 过平滑；最通用                 |
| Histogram   | equal width / equal count         | 直方图         | 非参数；偏态数据（工资）用 equal count                                  |
| **CLT**     | Central Limit Theorem             | 中心极限定理    | 很多随机变量之和近似 Gaussian，所以常用 Gaussian 做噪声模型               |

#### L11 · 离群点与鲁棒估计

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| Moving average / median | —                     | 滑动平均/中位数 | 均值抗随机噪声但**不抗 outlier**；中位数抗 outlier                      |
| **RANSAC**  | RANdom SAmple Consensus           | 随机抽样一致    | 随机取最少点拟合，按 inlier 比例打分；outlier **直接排除**；outlier 越多、参数越多越慢 |
| **IRLS**    | Iteratively Reweighted Least Squares | 迭代重加权最小二乘 | 保留所有点，每轮按拟合程度**重新加权**                             |
| M-estimation | robust least squares             | M 估计         | 换成对大残差增长更慢的 loss                                           |
| Outlier detection | —                           | 离群点检测      | 低概率（MoG）、低密度（KNN 距离）、难压缩（PCA 重建误差）、低维可视化     |

#### L12–13 · 树与集成

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **DT**      | Decision Tree                     | 决策树         | **贪心**分裂，不保证全局最优；axis-aligned；不需要 feature scaling；可解释 |
| **H / IG**  | entropy / Information Gain        | 熵 / 信息增益   | $IG=H(Y)-H(Y\mid X)$，选 IG 最大的分裂                                |
| Gini        | Gini index $1-\sum p_i^2$         | 基尼指数       | 熵的替代，不用 log，稍快                                               |
| Regression tree | —                             | 回归树         | 最小化平方误差，叶子输出**均值**                                       |
| Bootstrap   | —                                 | 自助法         | **有放回**抽样，估计统计量及其方差                                     |
| **Bagging** | Bootstrap AGGregatING             | 装袋法         | bootstrap 训练多个模型再投票 → ↓**variance**                           |
| **RF**      | Random Forest (Breiman 2001)      | 随机森林       | **深**树 + 随机样本 + 随机特征，**平均** → ↓**variance**；很难训坏      |
| Boosting    | —                                 | 提升法         | **按顺序**训练，修正前面的错误 → ↓**bias**                             |
| **AdaBoost** | Adaptive Boosting                | 自适应提升      | 错分样本**加权**；weak learner 误差 < 50%；最终加权投票；可能过拟合      |
| Real AdaBoost | —                               | —             | 每个 learner 输出半个 logit，最后求和取符号                             |
| **BST-DT**  | Boosted Decision Trees            | 提升决策树      | **小**树（深度 2–4）+ 叶子 logit 求和；Caruana 对比中最好               |
| Cascade     | —                                 | 级联           | 前面的模型处理简单样本，难的才交给后面                                  |
| Mean-shift  | —                                 | 均值漂移       | Kinect 中从每像素部位预测找关节（找众数）                               |

#### L14–15 · 优化与 MLP

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **GD**      | Gradient Descent                  | 梯度下降       | 沿负梯度走；每步 $O(N)$，路径稳定                                      |
| **SGD**     | Stochastic Gradient Descent       | 随机梯度下降    | 用一个/一小批样本估梯度；每步 $O(B)$，噪声 $O(1/\sqrt B)$；噪声可帮助逃离局部极小 |
| Epoch       | —                                 | 轮次           | 完整过一遍训练集；每轮重新随机打乱最好                                  |
| **Pegasos** | Primal Estimated sub-GrAdient SOlver for SVM | —     | SVM 的 SGD：总是收缩 $(1-\eta\lambda)$，只有 margin 内的样本推动 $w$     |
| Perceptron  | —                                 | 感知机         | 线性 + 阈值；只能拟合**线性可分**数据                                  |
| **MLP**     | Multi-Layer Perceptron            | 多层感知机      | 线性层 + **非线性激活**；↓bias ↑variance；非凸                          |
| **FC**      | Fully Connected layer             | 全连接层        | $x_{k+1}=Wx_k$                                                       |
| **ReLU**    | Rectified Linear Unit             | 修正线性单元    | $\max(0,x)$；正区间导数 1，缓解梯度消失；稀疏                           |
| Sigmoid     | —                                 | —             | 导数 ≤ 0.25 → 深层**梯度消失**；适合输出概率                            |
| Backprop    | backpropagation                   | 反向传播       | 链式法则，**路径求和**，复用公共项（动态规划）                           |
| **MSE**     | Mean Squared Error                | 均方误差       | 回归 loss                                                            |
| **NeRF**    | Neural Radiance Fields            | 神经辐射场      | 坐标 MLP；配合 **Fourier features** 输入编码，图像更清晰                |

#### L16–17 · CNN 与视觉

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| **CNN**     | Convolutional Neural Network      | 卷积神经网络    | 共享卷积核 → 平移不变，参数少；pooling 扩大感受野                        |
| LeNet-5     | (LeCun 1998)                      | —             | average pooling + sigmoid/tanh，MNIST                                |
| AlexNet     | (2012)                            | —             | ReLU + max pooling + dropout + ImageNet + GPU                         |
| **ILSVRC**  | ImageNet Large Scale Visual Recognition Challenge | — | 1.2M 训练图，1000 类                                         |
| VGG / GoogLeNet | —                             | —             | 更深的网络；GoogLeNet 用 bottleneck + auxiliary classifiers            |
| **ResNet**  | Residual Network (He 2016)        | 残差网络        | skip connection $F(x)+x$；解决**优化**问题；bottleneck 1×1→3×3→1×1 省算力 |
| **BN / BatchNorm** | Batch Normalization        | 批归一化       | 按 mini-batch 归一化，再学 $\gamma,\beta$；训练更稳更快                 |
| Dropout     | —                                 | 随机失活       | 正则化 → ↓variance                                                    |
| Momentum    | —                                 | 动量           | 梯度的滑动平均；更快，滚过浅的局部极小                                   |
| **AdaGrad** | Adaptive Gradient                 | —             | 每个权重按累计梯度大小归一化；后期会变很慢                              |
| **RMSProp** | Root Mean Square Propagation      | —             | AdaGrad + 滑动平均衰减                                                |
| **Adam**    | Adaptive Moment Estimation        | —             | Momentum + RMSProp；好调参                                            |
| **AdamW**   | Adam with decoupled Weight decay  | —             | 正确地做 weight decay；最常用之一                                      |
| Data augmentation | —                           | 数据增强       | 不改标签的变换 → ↓**variance**，不增加表达力                            |
| Linear probe | feature extraction               | 线性探测       | 冻结 encoder，只训线性层；数据**很少**时用                              |
| Fine-tune   | —                                 | 微调           | 全部训练，lr 比从头训练**低 ≥10×**；数据**中等**时用                     |
| **R-CNN**   | Regions with CNN features         | —             | Selective Search 约 2K 候选框，每个都过一遍 CNN → 很慢                  |
| Fast R-CNN  | —                                 | —             | 整图只算一次特征 + **RoI pooling** → 约 100× 快                         |
| Faster R-CNN | —                                | —             | 加 **RPN** 生成候选框 → 再约 10× 快                                    |
| **RPN**     | Region Proposal Network           | 区域建议网络    | 共用卷积特征，每个 anchor 输出 objectness + 框修正                      |
| **RoI**     | Region of Interest                | 感兴趣区域      | RoI pooling → **RoIAlign**（双线性插值，对齐更准）                      |
| Mask R-CNN  | —                                 | —             | Faster R-CNN + RoIAlign + 实例 mask + keypoints                       |
| **NMS**     | Non-Max Suppression               | 非极大值抑制    | 检测后处理，去掉重叠框                                                 |
| **AP / mAP** | (mean) Average Precision         | 平均精度       | 检测指标（不是 L8 的 MAP）                                             |
| **DPM**     | Deformable Part Model             | 可变形部件模型   | CNN 之前的检测方法（HOG 之后）                                         |
| U-Net       | —                                 | —             | encoder–decoder + 镜像 skip；分割和图像生成                             |

#### L18–19 · 文本、注意力、Transformer

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| Token       | —                                 | 词元           | 整数 token 只是 ID；向量 token 才有相似度                               |
| **BPE**     | Byte Pair Encoding                | 字节对编码      | 从字符开始，反复合并**最频繁的相邻对**，每次重新计数                      |
| WordPiece / SentencePiece | —                   | —             | 子词分词；BERT 用 WordPiece，Unified-IO 用 SentencePiece                |
| `<unk>`     | unknown token                     | 未知词         | 只有 word tokenizer 需要                                              |
| Word2Vec    | (Mikolov 2013)                    | —             | 从上下文学词向量；Paris − France + Italy = Rome                        |
| **CBOW**    | Continuous Bag of Words           | 连续词袋        | 周围词 → 中心词；训练更快                                              |
| Skip-gram   | —                                 | 跳字模型       | 中心词 → 每个周围词；语义准确率更高                                     |
| **Q / K / V** | Query / Key / Value             | 查询/键/值     | 输出 = **values** 按 key–query 相似度加权平均；都是输入乘可学的线性投影  |
| Self- / cross-attention | —                     | 自/交叉注意力   | self ≈ soft clustering；cross（Q 和 K/V 来自不同集合）≈ 实例回归        |
| Multi-head attention | —                        | 多头注意力      | $h$ 个头各有投影，每头输出 $D/h$，拼接后再过线性层                       |
| Scaled dot-product | —                          | 缩放点积       | 除以 $\sqrt{d_k}$ 防止点积过大                                         |
| **PE**      | Positional Encoding               | 位置编码       | 注意力与顺序无关，所以要加；sinusoidal 或可学                            |
| **LayerNorm** | Layer Normalization             | 层归一化       | Transformer block 里的归一化（每个 token 内部）                         |
| **FFN / MLP** | Feed-Forward Network            | 前馈层         | block 里对每个 token 单独的 2 层 MLP；attention = 处理，MLP = 记忆       |
| Masked attention | —                            | 掩码注意力     | 只看**前面**的 token；GPT 和翻译 decoder 用                             |
| **EOS**     | End Of Sequence                   | 序列结束符      | decoder 输出它时停止                                                  |
| **BLEU**    | BiLingual Evaluation Understudy   | —             | 翻译质量指标，越高越好                                                 |
| Label smoothing | —                             | 标签平滑       | 原始 Transformer 用的正则化之一                                        |
| **BERT**    | Bidirectional Encoder Representations from Transformers | — | **encoder-only**，双向；预训练 = **MLM + NSP**；加线性层微调   |
| **MLM**     | Masked Language Modeling          | 掩码语言模型    | 选 15% token：80% `[MASK]`，10% 随机，10% 不变；只算选中的 loss          |
| **NSP**     | Next Sentence Prediction          | 下一句预测      | 50% 的 B 换成随机句，用 [CLS] 判断                                     |
| **[CLS] / [SEP]** | classification / separator token | —         | [CLS] 汇总整句（ViT 汇总整图）；[SEP] 分隔句子                          |
| **GLUE / SQuAD** | General Language Understanding Evaluation / Stanford Question Answering Dataset | — | BERT 刷榜的 benchmark |
| **ViT**     | Vision Transformer                | 视觉 Transformer | 16×16 patch → 线性投影 + PE + [CLS] → 同样的 encoder；数据越多越占优    |
| **JFT**     | Google 内部超大图像数据集           | —             | ViT 预训练数据越大越好（JFT > ImageNet-21k）                            |
| **LLM**     | Large Language Model              | 大语言模型      | BERT 是最早的之一                                                     |
| Unified-IO  | —                                 | —             | 一个 encoder–decoder 处理文本+图像的各种任务；所有东西变成离散 token       |
| **VQ-VAE**  | Vector-Quantized Variational AutoEncoder | —      | Unified-IO 用它把输出图像变成离散 code                                  |
| **VQA**     | Visual Question Answering         | 视觉问答       | 视觉-语言任务之一                                                     |

#### L20 · Foundation models

| 缩写 / 名称 | 全称                              | 中文          | 考点                                                                 |
| ----------- | --------------------------------- | ------------- | -------------------------------------------------------------------- |
| Foundation model | —                            | 基础模型       | 超大数据 + 算力 + 宽泛任务，通用或再适配                                |
| Zero / one / few-shot | —                       | 零/单/少样本    | prompt 里有 0 / 1 / 几个例子；**都不更新权重**                           |
| In-context learning | —                         | 上下文学习      | GPT-3 在推理时靠 prompt 里的例子"学"                                    |
| **CLIP**    | Contrastive Language–Image Pre-training | 对比语言-图像预训练 | 图像 + 文本 encoder，对比匹配 4 亿图文对；zero-shot 分类；微调会丢通用性 |
| **GPT**     | Generative Pre-trained Transformer | 生成式预训练    | **decoder-only**，预测下一个 token；GPT-1 微调，GPT-2 zero-shot，GPT-3 few-shot |
| WebText     | —                                 | —             | GPT-2 数据：Reddit ≥3 karma 的链接，800 万文档；去掉了 Wikipedia         |
| **PPL**     | Perplexity                        | 困惑度         | $2^{\text{entropy}}$，越低越好                                        |
| **SOTA**    | State Of The Art                  | 当前最优       | —                                                                    |
| **SFT**     | Supervised Fine-Tuning            | 监督微调       | ChatGPT 第一步：在人写的示范上微调                                      |
| **RLHF**    | Reinforcement Learning from Human Feedback | 基于人类反馈的强化学习 | 人对多个输出排序 → 训 **reward model** → 用 RL 调模型        |
| **RL**      | Reinforcement Learning            | 强化学习       | —                                                                    |
| **PPO**     | Proximal Policy Optimization      | 近端策略优化    | RLHF 里用的 RL 算法                                                    |
| Scaling laws | (Kaplan 2020)                    | 缩放定律       | test loss 对参数 N、数据 D、算力 C 是**幂律**；与结构形状关系弱；大模型更 sample-efficient |
| **CoT**     | Chain-of-Thought                  | 思维链         | prompt 里给推理示例；**只有大模型**才有效（emergent）                    |
| **GRPO**    | Group Relative Policy Optimization | —            | DeepSeek-R1 用的 RL；只奖励正确答案 + 格式，不学 reward model            |
| DeepSeek-R1 / R1-Zero | —                       | —             | R1-Zero = 纯 RL，长思考自己涌现；R1 = SFT 热身 + RL + SFT + RLHF         |
| Distillation | —                                | 蒸馏           | 用大模型输出 SFT 小模型                                                |
| Best-of-N   | —                                 | —             | 并行跑 N 次挑最好的；增加 **test-time compute**                         |
| Benchmarks  | MMLU / GPQA / AIME / SWE-bench / GSM8K / SuperGLUE | — | 知识 / 博士级科学 / 竞赛数学 / 修 GitHub issue / 数学应用题 / 语言理解；只需认得 |

### Practice questions

#### Lecture 12 — Trees

**Q1 (MC).** A node has 4 positive / 4 negative samples. A split yields children with (3+, 1−) and (1+, 3−). Information gain ≈ ?  
A. 0 B. 0.19 C. 0.5 D. 0.81

??? success "Answer"
    **B.** $H(\text{parent})=1$. Each child: $H(\tfrac34,\tfrac14)\approx0.811$; weighted average 0.811; $IG=1-0.811\approx0.19$.

**Q2 (MC).** Which binary distribution has the highest entropy?  
A. (0.9, 0.1) B. (0.7, 0.3) C. (0.5, 0.5) D. (1.0, 0)

??? success "Answer"
    **C** (1 bit). Others: 0.47, 0.88, 0 bits. Uncertainty is maximal when outcomes are equally likely.

**Q3 (MS).** Which statements about entropy are true?  
A. $H(Y\mid X)\le H(Y)$ B. If $X,Y$ are independent, $H(Y\mid X)=H(Y)$ C. $H(Y\mid Y)=1$ D. $H(X,Y)=H(X\mid Y)+H(Y)$ E. Entropy can be negative

??? success "Answer"
    **A, B, D.** C is wrong ($H(Y\mid Y)=0$, $Y$ tells everything about $Y$). E is wrong ($H\ge0$).

**Q4 (MC).** A regression tree chooses splits to minimize ______ and predicts ______ at a leaf.  
A. entropy; majority label B. sum of squared error; mean of $y$ in the leaf C. Gini; median D. margin; mean

??? success "Answer"
    **B.** It minimizes the conditional variance of $y$ within the leaves.

**Q5 (MS).** Compared with 1-NN, a decision tree…  
A. is typically axis-aligned B. can stop early to improve generalization C. is guaranteed to find the globally optimal tree D. produces piecewise-constant decision regions E. is most powerful as one single tree

??? success "Answer"
    **A, B, D.** Tree growth is *greedy* (C false); the real power comes from ensembles of trees (E false).

#### Lecture 13 — Ensembles

**Q6 (MC).** Why does a random forest beat one decision tree?  
A. Average many large trees: low bias, averaging reduces variance B. Average many small trees: low variance, averaging reduces bias C. Train large trees sequentially to fix mistakes D. Train small trees sequentially to fix mistakes

??? success "Answer"
    **A.** (B/C/D mix up bias/variance or describe boosting.)

**Q7 (MC).** Why do boosted decision trees beat one decision tree?  
(same options as Q6)

??? success "Answer"
    **D.** Small trees (high bias, low variance) trained sequentially on re-weighted mistakes → bias goes down.

**Q8 (MS).** Which methods primarily reduce **variance**?  
A. Bagging B. Random forest C. AdaBoost D. Data augmentation E. Averaging several independently trained networks

??? success "Answer"
    **A, B, D, E.** AdaBoost mainly reduces bias.

**Q9 (MS).** True statements about AdaBoost:  
A. Misclassified samples get larger weights B. Weak learners are trained independently in parallel C. Final prediction is a weighted vote / sum of weak learner outputs D. A weak learner must have < 50% training error under the current weights E. Too many/too large trees can overfit

??? success "Answer"
    **A, C, D, E.** Training is *sequential* (B false).

**Q10 (MS).** In a random forest, each tree uses…  
A. a random subset of the training samples B. a random subset of features C. a deep tree D. predictions that are added up in logit space and trained sequentially E. predictions that are averaged

??? success "Answer"
    **A, B, C, E.** D describes boosting.

**Q11 (MC).** Samples $(w,x,y)$: (0.1,0,0),(0.1,0,0),(0.2,1,0),(0.1,0,0),(0.2,1,0),(0.2,0,1),(0.1,1,1). Weighted $P(x=0\mid y=0)$?  
A. 3/5 B. 3/7 C. 0.3 D. 1/2

??? success "Answer"
    **B.** (0.1+0.1+0.1)/(0.1+0.1+0.2+0.1+0.2)=0.3/0.7. Unweighted would be 3/5.

**Q12 (MC).** In the Kinect pose system, the random forest predicts…  
A. the 3D joint directly B. a body-part label (probability) for each depth pixel C. the person's identity D. a depth image

??? success "Answer"
    **B.** Features = depth differences at two offsets; joints are then found by mean-shift on the part predictions. Lots of (synthetic) training data matters.

**Q13 (MC).** Which term of expected error can *not* be reduced by any model choice?  
A. Bias² B. Variance C. Noise D. All can be reduced

??? success "Answer"
    **C.** Noise = irreducible error from the data/problem.

#### Lecture 14 — SGD

**Q14 (MC).** Going from batch size 100 to 10,000: gradient computation time and gradient standard error change by…  
A. 100× more time, 10× less noise B. 10× more time, 100× less noise C. 100× more time, 100× less noise D. same time, 10× less noise

??? success "Answer"
    **A.** Time $O(B)$; standard error $O(1/\sqrt B)$.

**Q15 (MS).** Compared with full-batch gradient descent, mini-batch SGD…  
A. is cheaper per step B. has noisier gradients C. noise may help escape local minima D. always reaches the global minimum E. is easy to parallelize on a GPU

??? success "Answer"
    **A, B, C, E.**

**Q16 (MS).** Which objectives are convex (no local-minimum problem)?  
A. Linear regression B. Logistic regression C. Linear SVM D. MLP with ReLU E. Deep ResNet

??? success "Answer"
    **A, B, C.** Multi-layer networks are non-convex.

**Q17 (MC).** In Pegasos, if $y_i\langle w,x_i\rangle\ge1$ for the sampled example, the update is…  
A. no change B. $w\leftarrow(1-\eta\lambda)w$ C. $w\leftarrow w+\eta y_ix_i$ D. $w\leftarrow0$

??? success "Answer"
    **B.** Only the regularization shrink; the example is outside the margin so it adds no hinge gradient.

**Q18 (MC).** Which sampling procedure was best for SGD in the Pegasos experiments?  
A. Always same order B. Sample with replacement each step C. A new random permutation each epoch D. Sort by label

??? success "Answer"
    **C.**

**Q19 (MC).** A learning rate that is far too large will most likely…  
A. converge faster with no downside B. overshoot / oscillate / diverge C. get stuck at a saddle only D. not matter

??? success "Answer"
    **B.**

**Q20 (MC).** A perceptron can reach zero training error only if…  
A. the data are linearly separable B. there are fewer than 100 features C. a hinge loss is used D. ReLU is used

??? success "Answer"
    **A.** It is a thresholded *linear* model — it fails on XOR / ring-shaped classes.

#### Lecture 15 — MLPs and backprop

**Q21 (MC).** Stacking 5 fully-connected layers with **linear** activations is equivalent to…  
A. a 5-layer non-linear net B. one linear layer C. a decision tree D. a CNN

??? success "Answer"
    **B.** Product of matrices = one matrix → need non-linear activations.

**Q22 (MC).** MLP 784 → 256 (ReLU) → 10, no biases. Number of parameters?  
A. 784·256 B. 256·10 C. 784·256 + 256·10 D. 784·10

??? success "Answer"
    **C.** = 200,704 + 2,560 = 203,264.

**Q23 (MS).** Which statements about activations are true?  
A. Sigmoid's derivative is ≤ 0.25 B. Sigmoid causes vanishing gradients in deep nets C. ReLU's derivative is 1 for positive inputs D. ReLU gives dense (non-sparse) activations E. Sigmoid is common on a probability output

??? success "Answer"
    **A, B, C, E.** ReLU gives *sparse* activations (negatives → 0).

**Q24 (MC).** In backprop, the gradient of the loss w.r.t. a weight is…  
A. computed independently for every weight from scratch B. the sum over paths to the loss of products of local gradients, reusing shared terms C. only the last layer's gradient D. the average of weights

??? success "Answer"
    **B.** Dynamic programming from output to input (e.g. $\partial E/\partial w_8$ sums two paths).

**Q25 (MC).** In the 2-2-2-1 example, $\partial E/\partial w_2$ (the weight from $h_1$ to $g_1$; $out=w_3g_1+w_0g_2$) is…  
A. $2(out-y)\,w_3\,h_1$ B. $2(out-y)\,w_0\,h_1$ C. $2(out-y)\,(w_3w_7+w_0w_9)\,x_2$ D. $2(out-y)\,h_1$

??? success "Answer"
    **A.** Single path: $out\leftarrow g_1\leftarrow w_2$.

**Q26 (MS).** Compared with a perceptron, an MLP…  
A. has lower bias B. has higher variance C. needs more data for a good fit D. has a convex objective E. can model non-linear functions

??? success "Answer"
    **A, B, C, E.** Optimization is non-convex.

**Q27 (MC).** Why use a Fourier (sin/cos) encoding of pixel position?  
A. It reduces parameters to zero B. $\gamma(x_i)^T\gamma(x_j)$ is a good similarity (peaks when $x_j=x_i$), making the target more linearly predictive C. It makes the loss convex D. It removes the need for ReLU

??? success "Answer"
    **B.** Principle: input representation matters.

#### Lecture 16 — CNNs and ResNet

**Q28 (MC).** A 56-layer plain network had *higher training error* than a 20-layer one. This shows…  
A. overfitting B. an optimization difficulty C. too little data D. label noise

??? success "Answer"
    **B.** Overfitting would give *low* training error and high test error.

**Q29 (MS).** Benefits of ResNet skip connections:  
A. Gradients flow directly to early layers B. Each block only needs to add information (learn a residual) C. They remove the need for non-linearities D. They make very deep nets (100+ layers) trainable E. They reduce the number of layers

??? success "Answer"
    **A, B, D.**

**Q30 (MS).** True for convolutional layers:  
A. The same filter weights are applied at every position B. They encode local patterns in a translation-invariant way C. Pooling increases the effective receptive field of later filters D. Every output unit connects to every input pixel E. They are used only for images

??? success "Answer"
    **A, B, C.** D describes a fully connected layer; 1D/3D CNNs exist (E false).

**Q31 (MC).** The 2012 AlexNet breakthrough came from…  
A. ReLU + large labeled dataset (ImageNet) + GPUs B. new SVM kernels C. bigger decision forests D. unsupervised clustering

??? success "Answer"
    **A.** (Also dropout and max pooling.)

**Q32 (MC).** Batch Normalization…  
A. normalizes each mini-batch's features then applies learned scale/shift ($\gamma,\beta$) B. normalizes the labels C. adds noise to weights D. replaces the loss function

??? success "Answer"
    **A.** Stabilizes and speeds up training.

**Q33 (MC).** The ResNet bottleneck (1×1 → 3×3 → 1×1) is used mainly to…  
A. increase the number of parameters B. cut computation (≈70K vs ≈600K ops) while keeping 256-channel width C. replace the skip connection D. do pooling

??? success "Answer"
    **B.**

**Q34 (MC).** Adam combines…  
A. momentum and RMSProp-style per-weight scaling B. AdaGrad and dropout C. momentum and batch norm D. SGD and weight decay only

??? success "Answer"
    **A.** (AdamW additionally fixes the weight-decay update.)

**Q35 (MC).** Momentum $m_t=\beta m_{t-1}+g(w_t)$ helps because…  
A. it keeps a running average of past gradients, speeding convergence and rolling through shallow minima B. it shrinks the batch size C. it zeroes the gradient D. it normalizes per weight by gradient size

??? success "Answer"
    **A.** D describes AdaGrad/RMSProp.

#### Lecture 17 — Training and computer vision

**Q36 (MC).** If you forget `optimizer.zero_grad()` in the training loop, then…  
A. nothing changes B. gradients accumulate across batches C. weights are not updated D. the loss is zero

??? success "Answer"
    **B.** Correct order: forward → loss → zero_grad → backward → step.

**Q37 (MC).** Data augmentation (flip, crop, color jitter) mainly…  
A. reduces variance B. reduces bias C. increases model capacity D. speeds up inference

??? success "Answer"
    **A.** Same label, more varied inputs → less memorizing of quirks. It doesn't make the model more expressive.

**Q38 (MC).** You have an ImageNet-pretrained ResNet and only 16 labeled examples per class for a new task. Best choice?  
A. Train from scratch B. Linear probe C. Fine-tune all layers with a high lr D. Decision tree on raw pixels

??? success "Answer"
    **B.** Very little data → keep the encoder frozen to avoid overfitting. Moderate data → fine-tune; very large → fine-tune or scratch.

**Q39 (MS).** Good fine-tuning practice:  
A. Use a learning rate ≥10× lower than from-scratch training B. Freeze early layers first, then unfreeze (warm start) C. Use a smaller lr for earlier layers D. Use a larger lr than scratch training E. Replace the final layer to match the new classes

??? success "Answer"
    **A, B, C, E.** Learning rate is the most critical fine-tuning parameter.

**Q40 (MC).** Advantage of the "freeze encoder" linear probe over "pre-compute features"?  
A. Faster B. Can apply data augmentation (and needs no stored features) C. More accurate always D. Updates the encoder

??? success "Answer"
    **B.** It is slower, though.

**Q41 (MC).** What made Fast R-CNN ~100× faster than R-CNN?  
A. Computing CNN features once per image and RoI-pooling per proposal B. Using SVMs C. Fewer classes D. A smaller image

??? success "Answer"
    **A.** R-CNN ran the CNN on ~2K warped crops.

**Q42 (MC).** Faster R-CNN's key addition is…  
A. Selective Search B. A Region Proposal Network sharing the conv features (anchors with objectness + box refinement) C. Masks D. U-Net

??? success "Answer"
    **B.**

**Q43 (MS).** Mask R-CNN adds to Faster R-CNN:  
A. RoIAlign (bilinear interpolation) B. A per-object mask (28×28 per category) C. Keypoint heatmaps D. A transformer encoder E. Random-forest classifier

??? success "Answer"
    **A, B, C.**

**Q44 (MC).** U-Net's skip connections between mirrored encoder/decoder layers are for…  
A. passing fine spatial detail to the decoder for pixel-level output B. adding more classes C. batch normalization D. dropout

??? success "Answer"
    **A.** Used for segmentation and image generation.

**Q45 (MS).** In a trained CNN (Zeiler & Fergus), …  
A. Layer 1 detects edges/colors B. Middle layers detect textures and parts C. Late layers respond to object-specific patterns (e.g. dog faces) D. All layers detect whole objects E. Early layers are class-specific

??? success "Answer"
    **A, B, C.**

#### Lecture 18 — Tokens, embeddings, attention

**Q46 (MS).** Which tokenizations can represent any character string without an unknown token?  
A. Character B. Subword (BPE) C. Word

??? success "Answer"
    **A, B.** A word tokenizer has to map unseen words (*1298*, *Area-52*) to `<unk>`.

**Q47 (MC).** Running BPE on `abababcab`, which pair is merged first, and what is the result if it becomes `X`?  
A. `ab`; `XXXcX` B. `ba`; `aXXbcab` C. `ab`; `XbXbcX` D. `ca`; `abababXb`

??? success "Answer"
    **A.** Counts: `ab` 4, `ba` 2, `bc` 1, `ca` 1. Replace every `ab`, then recount before the next merge.

**Q48 (MS).** Which statements are true?  
A. Subword tokens are formed from statistical analysis of a text corpus  
B. Subword tokenizers separate the meanings of *log* (wood) and *log* (math), while word tokenizers don't  
C. Integer token IDs that are numerically close have similar meanings  
D. Subword tokenization gives slightly longer sequences than word tokenization  
E. Learned token vectors make distance and dot product meaningful

??? success "Answer"
    **A, D, E.** B: both give one token to every *log*; context handles the meaning. C: integer IDs are just names.

**Q49 (MC).** In Word2Vec, "the center word predicts each surrounding word" describes…  
A. CBOW B. Skip-gram C. BPE D. Self-attention

??? success "Answer"
    **B.** CBOW is the reverse: surrounding words predict the center word.

**Q50 (MC).** The output of attention for a query is…  
A. an average of the queries, weighted by key–value similarity  
B. an average of the values, weighted by key–query similarity  
C. an average of the keys, weighted by value–query similarity  
D. the value of the single nearest key

??? success "Answer"
    **B.** D would be 1-NN regression; attention is a soft version of it.

**Q51 (MC).** Let $s(k,q)=\frac1{(k-q)^2+1}$ and $\langle k,v\rangle=\langle1,2\rangle,\langle3,4\rangle,\langle7,10\rangle$. The attention output for $q=2$ is about…  
A. 3.00 B. 3.26 C. 5.33 D. 7.00

??? success "Answer"
    **B.** Similarities $\frac12,\frac12,\frac1{26}$, so $\frac{1+2+10/26}{1+1/26}\approx3.26$. C is the unweighted mean; A ignores the far key.

**Q52 (MS).** Which statements about self- and cross-attention are true?  
A. In self-attention, Q, K and V all come from the same tokens  
B. In a translation decoder's cross-attention, Q comes from the decoder, while K and V come from the encoder  
C. Q, K and V are obtained by multiplying tokens by learned linear projections  
D. Cross-attention behaves like instance-based regression  
E. Without positional encoding, shuffling the tokens changes each token's output

??? success "Answer"
    **A, B, C, D.** E is false: attention is order-invariant, which is why position must be added.

**Q53 (MS).** Which are true of Transformer blocks?  
A. A block has multi-head attention followed by a 2-layer MLP applied to each token  
B. Each sub-layer uses a residual connection and LayerNorm  
C. With input dimension 512 and 8 heads, each head outputs 64 dimensions before concatenation  
D. Attention is the only source of non-linearity  
E. Every Transformer block must use masked attention

??? success "Answer"
    **A, B, C.** D: the MLP has ReLU. E: only causal decoders (GPT, translation decoders) mask; BERT and ViT don't.

**Q54 (MC).** Scaled dot-product attention divides by $\sqrt{d_k}$ so that…  
A. the keys become orthogonal B. dot products don't get too large C. the output has fewer dimensions D. position is encoded

??? success "Answer"
    **B.**

**Q55 (MS).** Which hold for **both** a convolution layer and a self-attention layer without positional encoding?  
A. Most of the compute is in linear operations  
B. A position's output depends on other features  
C. Output depends on the order of the inputs  
D. They assume a neighborhood structure

??? success "Answer"
    **A, B.** C and D are true only for convolution.

#### Lecture 19 — BERT, ViT, CNN vs. Transformer

**Q56 (MS).** BERT is pre-trained to…  
A. Predict the next word B. Fill in masked or replaced tokens C. Predict whether one sentence follows another D. Translate English to French

??? success "Answer"
    **B, C.** A is GPT; D is the original encoder–decoder Transformer.

**Q57 (MS).** In BERT's masked language modeling…  
A. about 15% of tokens are selected for prediction  
B. selected tokens become `[MASK]` 80% of the time, a random token 10%, and stay unchanged 10%  
C. the loss is evaluated on all tokens  
D. human-labeled data is required  
E. the random and unchanged cases mean it cannot rely on seeing `[MASK]`

??? success "Answer"
    **A, B, E.** C: only selected tokens count. D: it needs no labels.

**Q58 (MS).** What do ViT and BERT have in common?  
A. Tokenized input B. Positional encoding added to tokens C. Sentence (segment) embedding D. Encoder is a stack of Transformer blocks E. Simple linear/MLP output head F. [CLS] token for categorical prediction

??? success "Answer"
    **A, B, D, E, F.** The sentence embedding is BERT only.

**Q59 (MC).** A ViT receives a 224×224 image with 16×16 patches and a [CLS] token. How many tokens enter the encoder?  
A. 196 B. 197 C. 224 D. 768

??? success "Answer"
    **B.** $14\times14=196$ patches + 1. (768 is the length of a flattened RGB patch: $16\times16\times3$.)

**Q60 (MS).** Which describe a self-attention layer?  
A. Each position is updated based on other features  
B. A position is updated only from nearby positions  
C. Unless the features encode position, processing is independent of position  
D. Each vector becomes a weighted average of linear projections of all features, with the same projections for every vector  
E. Each vector becomes a linear projection of nearby vectors, with the same projection at each position

??? success "Answer"
    **A, C, D.** A is true of convolution too. B and E describe convolution.

**Q61 (MS).** Comparing CNNs and Transformers in vision:  
A. CNNs tend to do better with less data  
B. Transformers scale more efficiently with large data and compute  
C. With enough data, they perform similarly on pure vision tasks  
D. ViT's learned position embeddings end up most similar for nearby patches  
E. All ViT heads attend only locally in early layers

??? success "Answer"
    **A, B, C, D.** E: some heads already attend far in early layers.

**Q62 (MC).** Generating a translation with an encoder–decoder Transformer runs…  
A. encoder once, decoder once per generated token  
B. encoder once per generated token, decoder once  
C. both once per generated token  
D. both once

??? success "Answer"
    **A.** Encoder keys and values are reused at every decoding step.

**Q63 (MC).** Why can a CNN's locality assumption help with little data?  
A. It acts like a prior, reducing variance  
B. It removes all bias  
C. It makes the objective convex  
D. It eliminates the need for labels

??? success "Answer"
    **A.** The same assumption limits it when data is huge, since a Transformer can learn better patterns itself.

#### Lecture 20 — CLIP and GPT

**Q64 (MC).** "Zero-shot" means…  
A. applying a model to a new task with no training examples for that task  
B. training a model from scratch in one epoch  
C. freezing the encoder and training a linear layer  
D. giving a few examples in the prompt

??? success "Answer"
    **A.** C is linear probe; D is few-shot.

**Q65 (MC).** What is CLIP trained to do?  
A. Generate the words of a caption  
B. Make correct image–text pairs much more similar than incorrect pairs  
C. Fill in the missing words of a caption  
D. Generate an image from a caption

??? success "Answer"
    **B.** C is BERT's idea. D is what later models do with CLIP as a component.

**Q66 (MS).** CLIP training…  
A. encodes images and text with separate encoders  
B. computes similarity for all image–text pairings in a batch  
C. uses cross-entropy to match each image to its text and each text to its image  
D. needs human-assigned class labels  
E. uses a decoder that reconstructs the caption

??? success "Answer"
    **A, B, C.** It uses scraped natural language, and it is contrastive rather than generative.

**Q67 (MC).** With batch size 4, CLIP's similarity matrix has how many correct and incorrect pairs?  
A. 4 and 4 B. 4 and 12 C. 16 and 0 D. 8 and 8

??? success "Answer"
    **B.** $4\times4=16$ pairs, with the diagonal correct.

**Q68 (MC).** Why use a contrastive objective rather than predict the exact caption?  
A. The exact target text is unpredictable, while matching is learnable  
B. Contrastive learning needs no batch  
C. It makes the objective convex  
D. It removes the need for a text encoder

??? success "Answer"
    **A.** Many captions could describe one image.

**Q69 (MC).** To use CLIP as a zero-shot classifier, you…  
A. train a linear layer on labeled images  
B. convert labels to captions, encode them and the image, and pick the best-matching caption  
C. fine-tune the text encoder on the labels  
D. cluster the images with K-means and name the clusters

??? success "Answer"
    **B.** Every training batch already resembles a new 32K-way classification task.

**Q70 (MS).** Which adapt CLIP to a new task **without** losing its general image–text matching?  
A. Zero-shot with encoded text labels  
B. Train a linear classifier on the image encoding  
C. K-NN on stored image features  
D. Fine-tune the image encoder for the target task

??? success "Answer"
    **A, B, C.** Fine-tuning changes the encoder, so it loses its generality.

**Q71 (MC).** Which result was reported for CLIP?  
A. Zero-shot is about as good as a strong baseline with 16 examples per class; linear probe needs about 4 examples to match zero-shot  
B. Zero-shot is always better than linear probe  
C. Linear probe needs thousands of examples per class to match zero-shot  
D. Zero-shot is near chance

??? success "Answer"
    **A.**

**Q72 (MC).** What is the training task of GPT-3?  
A. Fill in the blank B. Sentence classification C. Predict the next token D. A suite of benchmark tasks

??? success "Answer"
    **C.**

**Q73 (MS).** Which apply to both GPT-3 and BERT?  
A. Transformer architecture  
B. Pre-training by next-token prediction  
C. Adapted to target tasks by fine-tuning  
D. Pre-trained on large text data without task labels  
E. Bidirectional attention

??? success "Answer"
    **A, D.** B and causal attention are GPT. C and E are BERT.

**Q74 (MS).** Which statements about the GPT line are true?  
A. GPT-1 was fine-tuned for each task  
B. GPT-2 was trained on WebText and not fine-tuned, yet reached state of the art on many tasks zero-shot  
C. GPT-2 far beat state of the art on summarization and translation  
D. In GPT-3, few-shot performance rises even faster with scale than zero-shot  
E. Few-shot GPT-3 beats specialized per-task models on every task

??? success "Answer"
    **A, B, D.** C: those were GPT-2's weak spots. E: its average is about that of fine-tuned BERT-Large, and specialized models are still best.

**Q75 (MC).** When GPT-3 does "in-context learning", its weights…  
A. don't change: the examples are in the prompt  
B. change only in the last layer  
C. are fully fine-tuned  
D. are reset

??? success "Answer"
    **A.** That is why GPT-3 can be "trained" at inference time.

**Q76 (MC).** What took GPT-3 toward ChatGPT?  
A. Human feedback on outputs creates a quality scorer that the model is tuned against (RLHF)  
B. Replacing the Transformer with a CNN  
C. Removing the next-token objective  
D. Adding a bag-of-words classifier

??? success "Answer"
    **A.**

#### Foundations — Lectures 2–11

**Q77 (MS).** Which are direct evidence of **high variance**?  
A. Test error is high, but training error is much lower  
B. Test error is high, and training error is almost as high  
C. The model has few parameters  
D. Different training sets give very different predictions for the same test sample

??? success "Answer"
    **A, D.** B points to bias or noise. C is a cause you might suspect, not evidence about the error.

**Q78 (MS).** As K increases in KNN…  
A. the decision function gets smoother B. variance decreases C. bias increases D. training error tends to increase E. test error must decrease

??? success "Answer"
    **A, B, C, D.** Test error can move either way, depending on where you are on the bias–variance curve.

**Q79 (MS).** Which reflect correct evaluation practice?  
A. Pick hyperparameters on the validation set  
B. Use cross-validation when training data is limited  
C. Set the regularization weight from the same training error used to fit the weights  
D. Report final performance on a held-out test set  
E. Comparing training and test error is useless

??? success "Answer"
    **A, B, D.** C always favors less regularization. E: the gap diagnoses variance.

**Q80 (MC).** The top principal components are…  
A. orthogonal directions of maximum variance  
B. the features that best predict the labels  
C. random projections  
D. directions that preserve each point's nearest neighbors

??? success "Answer"
    **A.** Eigenvectors of the covariance matrix, with the largest eigenvalues. PCA uses no labels (B); C is LSH; D is closer to t-SNE/UMAP.

**Q81 (MS).** Match the method to what it preserves:  
A. MDS: pairwise distances  
B. IsoMap: graph-based (geodesic) distances  
C. t-SNE: a probability distribution over each point's neighbors  
D. PCA: discriminative information  
E. PCA: variance, under a linear projection

??? success "Answer"
    **A, B, C, E.** PCA may lose discriminative information.

**Q82 (MS).** Regularization:  
A. L1 tends to set some weights exactly to zero  
B. L2 linear regression has a closed-form solution  
C. Larger $\lambda$ tends to raise bias and lower variance  
D. L2 tends to give many exactly-zero weights  
E. L1 linear regression has a simple closed-form solution

??? success "Answer"
    **A, B, C.**

**Q83 (MS).** Linear SVM vs. logistic regression:  
A. Both give a linear decision boundary  
B. Logistic regression adds a non-zero penalty on every training point  
C. Hinge loss is zero once a point is correct with margin at least 1  
D. Removing a non-support vector doesn't change the SVM boundary  
E. SVM maximizes confidence, while logistic regression stops at "confident enough"

??? success "Answer"
    **A, B, C, D.** E is swapped.

**Q84 (MC).** Naïve Bayes assumes the features are…  
A. independent of each other B. conditionally independent given the label C. Gaussian D. linearly separable

??? success "Answer"
    **B.**

**Q85 (MC).** $x_1=1$ appears in 3 of 5 samples with $y=1$. With Laplace smoothing ($\alpha=1$) on binary $x_1$, $P(x_1=1\mid y=1)$ is…  
A. 3/5 B. 4/6 C. 4/7 D. 3/7

??? success "Answer"
    **C.** $(3+1)/(5+1\cdot2)$. A is the MLE. Compare Q11, where 3/7 is a *weighted* estimate.

**Q86 (MS).** The EM algorithm:  
A. E-step: estimate the latent variables' probabilities given current parameters  
B. M-step: re-estimate parameters, weighted by those probabilities  
C. Each iteration maximizes a lower bound on the data likelihood  
D. Is guaranteed to find the global maximum  
E. K-means is a "hard" version of it

??? success "Answer"
    **A, B, C, E.** It reaches a local maximum, so random restarts can help.

**Q87 (MS).** Density estimation:  
A. A PDF value can exceed 1  
B. Mixture of Gaussians is semi-parametric  
C. Too small a KDE bandwidth gives a spiky estimate  
D. Non-parametric methods work best on high-dimensional data  
E. Choose bins, bandwidth or number of components by validation log-likelihood

??? success "Answer"
    **A, B, C, E.** D is reversed: those methods work best on low-dimensional data.

**Q88 (MS).** Robust estimation:  
A. The median is robust to outliers, while the mean isn't  
B. RANSAC scores a model by its fraction of inliers  
C. IRLS keeps all points but re-weights them each iteration  
D. Least squares is robust to outliers  
E. RANSAC's cost grows quickly with the outlier fraction and number of parameters

??? success "Answer"
    **A, B, C, E.**

**Q89 (MS).** K-means:  
A. Alternates assigning points to the nearest center and recomputing means  
B. Its result depends on initialization  
C. Weights all feature dimensions equally  
D. Automatically finds the best K  
E. Is an example of hard EM

??? success "Answer"
    **A, B, C, E.**

### Mock exam (混合 25 题) {#mock-exam}

全部跨 lecture，9 道 MC + 16 道 MS，共 107 分（比例和实际考试不一定相同）。做完再统一看答案，答案里标了涉及的 lecture。错题对应回 [易混点对比](#cross-lecture)。

**M1 (MS).** For which of these will different initializations likely give substantially different parameters?  
A. K-means B. Mixture of Gaussians fit with EM C. Logistic regression D. MLP E. RBF SVM F. ViT

??? success "Answer"
    **A, B, D, F.** L4/L10/L15/L19. Logistic regression and SVMs are convex.

**M2 (MC).** Your model has 1% training error and 28% test error on a small image dataset. What should you try first?  
A. Add many more layers B. Remove regularization C. Add data augmentation D. Switch to a boosted ensemble of many large trees

??? success "Answer"
    **C.** L3/L17. The large gap means high variance. A and B raise variance; large boosted trees also overfit (L13).

**M3 (MS).** Which objectives have a single local optimum?  
A. Logistic regression B. Linear regression C. Kernelized SVM D. EM for MoG E. K-means

??? success "Answer"
    **A, B, C.** L6/L7/L14 vs. L4/L9.

**M4 (MS).** Which of these primarily reduce **variance**?  
A. Increasing K in KNN  
B. Adding training data  
C. Increasing the L2 weight  
D. Adding more boosting rounds  
E. Using a linear probe rather than fine-tuning when data is very limited

??? success "Answer"
    **A, B, C, E.** L3/L13/L17. Boosting targets bias.

**M5 (MC).** A deep plain CNN has *higher training error* than a shallower one. Which is the best fix?  
A. Add dropout B. Add skip connections C. Collect more data D. Increase weight decay

??? success "Answer"
    **B.** L16. This is optimization, not overfitting. The other options address variance.

**M6 (MS).** Which reduce **bias**?  
A. Decreasing K in KNN  
B. Replacing a perceptron with an MLP  
C. Fine-tuning instead of a linear probe, given enough data  
D. Decreasing regularization weight  
E. Bagging

??? success "Answer"
    **A, B, C, D.** L3/L15/L17. Bagging targets variance.

**M7 (MC).** Which is easiest to adapt to new training examples without re-optimizing?  
A. 1-NN B. Linear SVM C. Decision tree D. Linear logistic regression

??? success "Answer"
    **A.** L2. Just store the new example.

**M8 (MS).** Assuming no identical inputs have different labels, which can always reach zero training error?  
A. 1-NN B. Unrestricted decision tree C. Linear logistic regression D. Linear SVM E. Naïve Bayes

??? success "Answer"
    **A, B.** L2/L12. The others have limited model forms (L7/L8).

**M9 (MS).** Which statements about "weights" are true?  
A. AdaBoost raises the weights of misclassified samples  
B. EM's M-step weights data by latent-variable probabilities  
C. Attention mixing weights are computed from the input and sum to 1  
D. IRLS gives poorly fit points lower weight  
E. Random forests re-weight samples for each next tree

??? success "Answer"
    **A, B, C, D.** L9/L11/L13/L18. E describes boosting.

**M10 (MC).** With labels $y=x_1\oplus x_2$ (XOR) on all four binary inputs, which is true?  
A. A perceptron can reach zero training error  
B. Each feature alone has zero information gain, but a depth-2 tree can fit the data  
C. A greedy tree picks a split with information gain 1 bit first  
D. An MLP with one hidden layer and linear activations can fit it

??? success "Answer"
    **B.** L12/L14/L15. Each child of a first split is still 50/50. D is still linear, since stacked linear layers equal one layer.

**M11 (MS).** Which improve the flow of gradients from the loss to early layers?  
A. Using ReLU instead of sigmoid  
B. Adding skip connections  
C. Using fewer layers  
D. Adding data augmentation  
E. Using a larger batch

??? success "Answer"
    **A, B, C.** L15/L16. Augmentation targets variance (L17); batch size changes gradient noise (L14).

**M12 (MC).** Cross-attention over stored $\langle$key, value$\rangle$ pairs is most like…  
A. Distance-weighted KNN regression B. K-means C. PCA D. AdaBoost

??? success "Answer"
    **A.** L3/L18. Match the query against keys, then average their values.

**M13 (MS).** Skip connections:  
A. ResNet adds the input to the block's output  
B. U-Net connects mirrored encoder and decoder layers  
C. Transformer blocks use residual connections  
D. U-Net skips pass fine spatial detail to the decoder  
E. Their main purpose is to reduce the parameter count

??? success "Answer"
    **A, B, C, D.** L16/L17/L18.

**M14 (MC).** Which of these foundation models is pre-trained with human-assigned class labels?  
A. ImageNet ResNet B. BERT C. GPT-3 D. CLIP

??? success "Answer"
    **A.** L17/L19/L20. CLIP uses scraped natural language, not annotated labels.

**M15 (MS).** Linear projections in different methods:  
A. PCA directions come from the data's covariance  
B. LSH can use random projections  
C. ViT's patch embedding is learned by backprop  
D. Q, K and V projections are learned by backprop  
E. PCA guarantees that class-discriminative information is kept

??? success "Answer"
    **A, B, C, D.** L4/L5/L18/L19.

**M16 (MC).** You must classify images into new categories. You have class names but **no** labeled examples. What should you do?  
A. Train from scratch B. Fine-tune an ImageNet model C. Use CLIP zero-shot D. Fit Naïve Bayes

??? success "Answer"
    **C.** L20. Options A, B and D all need labeled data.

**M17 (MS).** Position information:  
A. A Transformer adds positional encoding because attention is order-invariant  
B. A CNN encodes position through the index in the feature map  
C. Fourier features of pixel position help an MLP map position to color  
D. ViT can't work at all without position embeddings  
E. The dot product of two sinusoidal encodings reflects positional similarity

??? success "Answer"
    **A, B, C, E.** L15/L18/L19. ViT still works surprisingly well without them.

**M18 (MS).** How are pre-trained models usually applied?  
A. An ImageNet ResNet: replace the last layer, then linear-probe or fine-tune  
B. BERT: add a linear layer and fine-tune  
C. GPT-2: fine-tune on every target task to get its results  
D. CLIP: encode text labels for zero-shot classification  
E. GPT-3: put examples in the prompt, with no gradient updates

??? success "Answer"
    **A, B, D, E.** L17/L19/L20. GPT-2's results were zero-shot.

**M19 (MC).** Self-attention applied repeatedly to scalars 1, 9, 8, 2 pulls them toward about 2 and 8. This behaves most like…  
A. Soft clustering B. Linear regression C. Boosting D. Dropout

??? success "Answer"
    **A.** L4/L18/L19. Compare the soft assignment in EM (L9).

**M20 (MS).** More training data for a **fixed** model:  
A. Test error tends to move closer to training error  
B. Variance decreases  
C. Fitting the training data becomes harder  
D. Bias is eliminated  
E. Training error tends to decrease

??? success "Answer"
    **A, B, C.** L3. D and E are the usual wrong intuitions: training error tends to rise toward its limit.

**M21 (MS).** Optimizers:  
A. Momentum keeps a running average of past gradients  
B. RMSProp normalizes each weight's update by a moving average of its gradient magnitude  
C. Adam combines momentum and RMSProp  
D. A larger batch reduces gradient noise, but with diminishing returns  
E. These optimizers guarantee a global optimum for MLPs

??? success "Answer"
    **A, B, C, D.** L14/L16. Noise scales as $1/\sqrt B$; MLPs stay non-convex.

**M22 (MC).** Which of these can extrapolate beyond the range of the training targets?  
A. KNN regression B. Regression tree C. Linear regression D. Random forest regression

??? success "Answer"
    **C.** L6/L12/L13. The others output averages of training targets.

**M23 (MS).** Which correctly pair a model with its training objective?  
A. Regression tree: minimize squared error within leaves  
B. Classification tree: maximize information gain at each split  
C. Linear SVM: hinge loss plus weight penalty  
D. CLIP: cross-entropy on image–text matching  
E. GPT: cross-entropy on masked tokens, using bidirectional attention

??? success "Answer"
    **A, B, C, D.** L7/L12/L20. E mixes in BERT's approach.

**M24 (MS).** Which require or strongly benefit from feature scaling?  
A. KNN with L2 distance  
B. K-means  
C. Decision tree  
D. Random forest  
E. PCA, when features have very different units

??? success "Answer"
    **A, B, E.** L2/L4/L5/L12. Trees compare one feature at a time against a threshold, so scale doesn't matter.

**M25 (MS).** Which are good model-selection practice?  
A. Choose KNN's K using a validation set  
B. Compare density models on held-out log-likelihood  
C. Tune fine-tuning learning rate on validation performance  
D. Pick among models by test error, then report that error as unbiased  
E. Pick $\lambda$ by training error

??? success "Answer"
    **A, B, C.** L3/L10/L17. D leaks the test set; E always favors less regularization.

### Exam tips

-   For multi-select, partial credit exists, but wrong picks likely cost points → select the ones you can justify
-   Judge each multi-select option as its own true/false question; don't guess from how many "feel right"
-   Many wrong options are the **bias ↔ variance swap** or **linear ↔ non-linear / convex ↔ non-convex** swap — check those first
-   Swaps of **value ↔ query**, **BERT ↔ GPT**, **zero-shot ↔ few-shot ↔ fine-tune** and **sequential ↔ independent** are just as common
-   First ask what a question really tests: bias, variance, optimization, or compute. The lecture it seems to come from often doesn't matter
-   Not required: code, but know the *roles* of `zero_grad`, `backward`, `step`, `requires_grad=False`