## Exam 2 Review (Lectures 12–17)

Format: 25 multiple choice / multi-select questions, conceptual only (no coding). MC = 3 pts, multi-select = 5 pts with partial credit. 点开 "Answer" 前先自己做。**MS** = select all that apply.

### One-page cheat sheet

| Topic                    | Must know                                                    |
| ------------------------ | ------------------------------------------------------------ |
| **Trees (L12)**          | Greedy split by **information gain** $IG=H(Y)-H(Y\mid X)$; $H=-\sum p\log_2p$ (max 1 bit for a binary variable at $p=0.5$); $H\ge0$, $H(Y\mid X)\le H(Y)$, $H(Y\mid Y)=0$. Regression tree: minimize squared error, leaf = **mean**. Axis-aligned splits; stop early (min leaf size / max depth) to generalize; Gini is an alternative criterion. One tree is weak, a forest is strong |
| **Ensembles (L13)**      | Expected error = variance + noise + bias². **Random forest**: deep trees (low bias/high variance), random data + features, **average** → ↓**variance**. **Boosting/AdaBoost**: small trees (high bias/low variance), sequential, re-weight mistakes, weighted vote / sum of logits → ↓**bias**, can overfit. Weak learner = better than 50% |
| **SGD (L14)**            | Step opposite the gradient; lr too big → overshoot, too small → slow. Convex (linear reg., logistic, SVM) = no local-minima issue; MLPs are not. Mini-batch: cost $O(B)$, gradient noise $O(1/\sqrt B)$. Pegasos: only in-margin examples push; always shrink $(1-\eta\lambda)$. New random order each epoch |
| **MLP / backprop (L15)** | Perceptron = linear. Layers need **non-linear activations** (stacked linear = one linear). Sigmoid (max slope 0.25 → vanishing gradient), ReLU (slope 1 for $x>0$). Backprop = chain rule, **sum over paths**, reuse shared terms (dynamic programming). MLP: lower bias, higher variance, non-convex, more data/compute |
| **CNN / ResNet (L16)**   | Conv = shared learned filter → feature map, translation invariance; pooling grows receptive field. AlexNet 2012 = ReLU + ImageNet + GPU (+ dropout). Deep nets got *worse training error* → optimization problem. **ResNet** $F(x)+x$ skip. **BatchNorm** normalize per batch, learn $\gamma,\beta$. Adam = momentum + RMSProp |
| **Training / CV (L17)**  | Loop: forward → loss → `zero_grad` → `backward` → `step`. Augmentation ↓**variance**. Little data → **linear probe**; moderate → **fine-tune** (low lr!); huge → fine-tune or scratch. R-CNN → Fast (share features, RoI pool) → Faster (RPN) → Mask (RoIAlign + masks + keypoints). U-Net = encoder–decoder + skips |

**Frequent traps**

-   Bagging / RF reduce **variance**; boosting reduces **bias** (small ↔ large trees are swapped in wrong answers)
-   Training error rising with depth = **optimization**, not overfitting
-   Data augmentation reduces variance; it does **not** add expressiveness
-   Fine-tuning lr is **lower** than from-scratch lr; linear probe freezes the encoder
-   Perceptron/linear models can't fit XOR / circle-shaped boundaries; MLPs can but aren't convex
-   Larger batch = more stable gradient, but it costs proportionally more per step

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

### Exam tips

-   For multi-select, partial credit exists, but wrong picks likely cost points → select the ones you can justify
-   Many wrong options are the **bias ↔ variance swap** or **linear ↔ non-linear / convex ↔ non-convex** swap — check those first
-   Not required: code, but know the *roles* of `zero_grad`, `backward`, `step`, `requires_grad=False`