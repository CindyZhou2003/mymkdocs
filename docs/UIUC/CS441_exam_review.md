## Exam 2 Review (Lectures 2–20)

Format: 25 multiple choice / multi-select questions, conceptual only (no coding). MC = 3 pts, multi-select = 5 pts with partial credit (no multiple attempts). 重点是 L12–20，L2–11 考基本原理。点开 "Answer" 前先自己做。**MS** = select all that apply.

**建议顺序**：先看 [易混点对比](#cross-lecture)，再做 [Mock exam](#mock-exam) 找弱点，最后回到对应 lecture 的题补漏。题目是按课件和笔记自拟的，不是真题；课程官方练习题（不显示答案）在 [All Questions form](https://tinyurl.com/AML441-AllQs)，其中 L12–L20 和 "Exam 2: Extra Questions" 最相关。

!!! note "L20 的来源"
    FA26 的 L20 在 11/3 才上，这里的 CLIP/GPT 内容来自 [FA25 课件](https://courses.grainger.illinois.edu/CS441/fa2025/lectures/Lecture%2020%20-%20Foundation%20Models%20-%20CLIP%20and%20GPT.pdf)。上完课后对照一下今年的 slides，数字以今年为准。

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
| **CLIP / GPT (L20)**     | **Foundation model** = huge data + broad task. **Zero-shot** = no examples for this task. CLIP: image + text encoders, **contrastive** matching (32K × 32K, cross-entropy both ways), 400M pairs; zero-shot via label → caption. GPT: **predict the next token**. GPT-1 fine-tuned; GPT-2 zero-shot; GPT-3 (175B) few-shot in context, no weight updates |
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

| 问题              | 有效的方法                                                                                                   | 常见错误选项                  |
| ----------------- | -------------------------------------------------------------------------------------------------------- | ----------------------------- |
| **↓ Variance**    | Larger K; more training data; stronger regularization; simpler model; bagging / RF; data augmentation; averaging networks; linear probe (little data) | Boosting; more layers         |
| **↓ Bias**        | Smaller K; weaker regularization; more complex model (perceptron → MLP); boosting; fine-tune instead of linear probe | More data; bagging            |
| **Optimization**  | ReLU instead of sigmoid; skip connections; BatchNorm; momentum / Adam; learning-rate tuning                 | Dropout, augmentation (those target variance) |
| **Noise**         | None: irreducible for the given features                                                                 | "A bigger model fixes it"     |

#### 2. 模型性质总表

| Model                 | Boundary / function          | Optimum                     | Init matters? | Training                      |
| --------------------- | ---------------------------- | --------------------------- | ------------- | ----------------------------- |
| 1-NN / KNN            | Non-linear, instance-based   | No optimization             | No            | Store data; new examples are trivial to add |
| Linear regression     | Linear                       | Convex, global              | No            | Closed form (with or without L2) |
| Logistic regression   | Linear                       | Convex, global              | No            | Iterative                     |
| Linear / RBF SVM      | Linear / non-linear          | Convex, global              | No            | QP or Pegasos                 |
| Naïve Bayes           | Usually linear               | Global (counts / MLE)       | No            | Closed form                   |
| Decision tree         | Axis-aligned partitions      | **Greedy, not guaranteed**  | No            | Recursive splits              |
| K-means               | Clusters                     | **Local**                   | **Yes**       | Iterative (hard EM)           |
| MoG with EM           | Density                      | **Local**                   | **Yes**       | Iterative (soft EM)           |
| MLP / CNN / Transformer | Non-linear                 | **Non-convex, local**       | **Yes**       | SGD + backprop                |

#### 3. 同一个词，不同的意思

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

#### 4. Foundation models 总表

| Model        | Architecture                               | Pre-training data              | Objective                | Human labels? | How it is applied                              |
| ------------ | ------------------------------------------ | ------------------------------ | ------------------------ | ------------- | ---------------------------------------------- |
| ImageNet CNN | CNN / ResNet                               | ImageNet                       | Classification           | **Yes**       | Linear probe or fine-tune                      |
| ViT          | Encoder-only on image patches              | ImageNet-21k / JFT             | Classification           | **Yes**       | Head on [CLS]                                  |
| BERT         | Encoder-only, bidirectional                | BooksCorpus + Wikipedia        | MLM + NSP                | No            | Fine-tune with a linear layer                  |
| GPT-1        | Decoder-only, causal, 117M                 | BooksCorpus                    | Next token               | No            | Fine-tune per task                             |
| GPT-2        | Same, larger                               | WebText (8M documents)         | Next token               | No            | Zero-shot; task stated in the text             |
| GPT-3        | Same, 175B                                 | Even more text                 | Next token               | No            | Zero-shot and few-shot, in context             |
| CLIP         | Image encoder + text Transformer           | 400M scraped image–text pairs  | Contrastive matching     | No (natural language) | Zero-shot, linear probe, K-NN; fine-tune loses generality |

#### 5. Linear vs. convolution vs. attention

| 性质                             | Linear | Convolution | Attention                       |
| -------------------------------- | ------ | ----------- | ------------------------------- |
| Output depends on input order    | Yes    | Yes         | **No**, unless position is encoded |
| Same weights at different positions | No  | **Yes**     | No: mixing weights come from data |
| Assumes a neighborhood structure | No     | **Yes**     | No: every token sees every token |
| Compute is mostly linear operations | Yes | Yes         | Yes                             |

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