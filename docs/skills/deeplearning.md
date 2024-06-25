# Deep learning

[Python Tutorial](https://www.w3schools.com/python/default.asp)

[神经网络与深度学习_邱锡鹏著_2020年.pdf](https://www.yuque.com/attachments/yuque/0/2024/pdf/34417153/1709725036974-bb82fbd2-62ff-4d31-b38e-890c326c92c8.pdf)<br />[Pytorch常用API汇总(持续更新)_pytorch的api-CSDN博客](https://blog.csdn.net/qq_49134563/article/details/108200828)<br />[PyTorch | 广播机制（broadcast）_pytorch broadcast-CSDN博客](https://blog.csdn.net/m0_52650517/article/details/119913625)
<a name="Ap48w"></a>
## Deep learning
data<br />三要素：模型 model、学习准则 criteria、优化算法
<a name="tFbBb"></a>
### 模型
模型$f(x;θ)$<br />机器学习的目标是找到一个模型来近似真是映射函数$g(x)$或真是条件概率分布$p_r(y|x)$<br />非线性模型<br />KL 散度、交叉熵
<a name="I5ZUE"></a>
### 学习准则
期望风险<br />损失函数<br />平方、交叉熵、hinge<br />经验风险最小化 ERM<br />结构风险最小化 SRM：正则化防止过拟合
<a name="JNx6f"></a>
### 优化算法
（超）参数优化<br />（批量）梯度下降法 BGD：每次迭代时计算每个样本损失函数的梯度并求和<br />提前停止：防止过拟合<br />随机（增量）梯度下降法 SGD：抽 N 个样本，由它们计算出来的经验风险的梯度来近似期望风险的梯度<br />小批量梯度下降法：介于梯度下降法和随机梯度下降法之间

<a name="PNMXd"></a>
### 算法
前向传播：输入进去 网络做了什么计算
![](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709724929106-958fec79-3810-4abc-8ea5-7d799905dafe.png)
<a name="FEcw3"></a>
#### 常用的激活函数


1. **Sigmoid**，两端饱和函数
   1. **Logistic** <img src="https://cdn.nlark.com/yuque/0/2024/png/34417153/1709725299105-4c06743a-67ff-4933-8295-213c27a6ef32.png#averageHue=%23fcfbfa&clientId=u66705bcf-f251-4&from=paste&height=45&id=uf102fe18&originHeight=67&originWidth=222&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=7501&status=done&style=none&taskId=u6f8926d0-699d-4a35-898f-00eba4cd52d&title=&width=148" alt="Alt text">

   2. **Tanh** ![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709725314557-8451b1a3-64ae-4126-b6ee-c57d37eae75c.png#averageHue=%23dcd3ca&clientId=u66705bcf-f251-4&from=paste&height=48&id=u4360faec&originHeight=72&originWidth=292&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=16035&status=done&style=none&taskId=ud3b1fb52-4edc-4946-b705-f4af05fed80&title=&width=194.66666666666666)![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709725383719-55775481-905c-4583-a225-8823a6827840.png#averageHue=%23f8f7f5&clientId=u66705bcf-f251-4&from=paste&height=27&id=u6cacfb91&originHeight=40&originWidth=222&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=7148&status=done&style=none&taskId=ucd715632-e4ac-4f17-ba45-a382eb0df47&title=&width=148)
饱和定义对于函数 𝑓(𝑥)，若 𝑥 → −∞ 时，其导数 𝑓′(𝑥) → 0，则称其为左饱和．若 𝑥 → +∞ 时，其导数 𝑓′(𝑥) → 0，则称其为右饱和．当同时满足左、右饱和时，就称为两端饱和

1. Hard-Logistic & hard-Tanh 一阶泰勒展开的直线近似
2. **ReLU**(PReLU)

![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709725612997-13ad4348-a7c1-45ae-b72e-f13cbb5ae07e.png#averageHue=%23fbfaf9&clientId=u66705bcf-f251-4&from=paste&height=59&id=u8c2f6cff&originHeight=88&originWidth=237&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=10381&status=done&style=none&taskId=u6b09a76c-ec08-436b-a3cd-adb470da8b3&title=&width=158)![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815006287-233d495c-ffe3-4c14-a9e2-7c101d7239e0.png#averageHue=%23fbfbfa&clientId=u84e4090c-43d5-4&from=paste&height=92&id=u39688cc8&originHeight=138&originWidth=381&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=23005&status=done&style=none&taskId=uce4efad2-7d34-483a-9c66-bbbfad8d4a1&title=&width=254)<br />其中 𝛾𝑖 为 𝑥 ≤ 0 时函数的斜率．因此，PReLU 是非饱和函数．如果 𝛾𝑖 = 0，那么PReLU 就退化为 ReLU

4. **ELU**

![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815094072-4b37f2f5-6453-4da4-acf4-188bfc33f1b9.png#averageHue=%23fbfafa&clientId=u84e4090c-43d5-4&from=paste&height=91&id=u7148bb36&originHeight=136&originWidth=441&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=29726&status=done&style=none&taskId=u40b939fb-3b26-4e61-99bd-dcdcd3460a3&title=&width=294)

5. **Softplus**

![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815132024-7f02bb15-94eb-48c2-ad24-cc57bfe537ea.png#averageHue=%23ddd6ce&clientId=u84e4090c-43d5-4&from=paste&height=23&id=uf27f199f&originHeight=34&originWidth=306&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=11347&status=done&style=none&taskId=uddcab670-6e76-4666-8f38-b8807f17fd8&title=&width=204)<br />Softplus 函数其导数刚好是 Logistic 函数．Softplus 函数虽然也具有单侧抑制、宽兴奋边界的特性，却没有稀疏激活性

6. **Swish**

![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815228781-0b3008bd-cee3-48d9-a3e8-8a81f47337d4.png#averageHue=%23f9f8f7&clientId=u84e4090c-43d5-4&from=paste&height=133&id=u0ddc9319&originHeight=199&originWidth=769&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=102308&status=done&style=none&taskId=uc515cbfc-80f0-42d8-a624-3e4b4e22bff&title=&width=512.6666666666666)

7. **GELU**

![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815285967-80ed2bf3-8b53-4f0f-b19a-2f96562e3a04.png#averageHue=%23dfdad2&clientId=u84e4090c-43d5-4&from=paste&height=24&id=ud352bb2c&originHeight=36&originWidth=240&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=8528&status=done&style=none&taskId=udf1b892e-5ac4-4917-b35f-699b65c4c86&title=&width=160)![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815302136-66c55af4-61bc-48be-b58a-d92a63e77aa7.png#averageHue=%23ded6ce&clientId=u84e4090c-43d5-4&from=paste&height=79&id=u7282e022&originHeight=118&originWidth=777&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=80124&status=done&style=none&taskId=u2af67573-5093-4a9b-a65f-f9548d968a2&title=&width=518)<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/34417153/1709815329086-b72081ea-416c-4fda-adb4-73d1db78e8df.png#averageHue=%23fbfaf9&clientId=u84e4090c-43d5-4&from=paste&height=70&id=u4136e230&originHeight=105&originWidth=579&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30243&status=done&style=none&taskId=u86831f01-b63a-4e76-92a3-b7952b3ad74&title=&width=386)
<a name="njnWz"></a>
#### MLP（FNN）
多层感知器（MLP ）是现代前馈人工神经网络（ANN） 的名称，由具有非线性激活函数的**完全连接**的神经元组成，包含至少三层节点：输入层、一个或多个隐藏层和输出层。 一层中的每个节点或神经元以一定的权重连接到下一层中的每个节点，使网络完全连接。 MLP 使用称为**反向传播的监督学习**技术进行训练。 神经网络中的节点将**非线性激活函数**应用于从前一层接收的加权输入，然后将结果传递到下一层。 这种非线性使得 MLP 能够对输入和输出之间的复杂关系进行建模，而线性模型无法做到这一点。 <br />MLP 可用于从计算机视觉到语音识别等领域的各种任务，例如分类、回归和特征学习。 MLP 的关键特征包括其深度（层数）、宽度（每层中的节点数）、激活函数（例如 sigmoid、tanh 或 ReLU）以及用于训练的优化算法（通常是某种形式的梯度下降）。 MLP 被认为是深度学习的基础架构，尽管卷积神经网络 (CNN) 和循环神经网络 (RNN) 等更复杂的网络分别更常用于涉及图像和序列数据的任务。
<a name="t62Qq"></a>
#### CNN
滤波器 Filter，又叫卷积核 Kernal<br />卷积神经网络是多层感知器的变体<br />CNN 的层具有按3 个维度排列的神经元：宽度、高度和深度。[71]卷积层内的每个神经元仅与其之前层的一小部分区域相连，称为感受野。不同类型的层（局部连接和完全连接）堆叠在一起形成 CNN 架构。<br />局部连接：遵循感受野的概念，CNN 通过在相邻层的神经元之间强制执行**局部连接**模式来利用空间局部性。因此，该架构确保学习到的“过滤器”对空间局部输入模式产生最强的响应。堆叠许多这样的层会导致非线性滤波器变得越来越全局（即响应像素空间的更大区域），以便网络首先创建输入的小部分的表示，然后从它们组装更大区域的表示。<br />共享权重：在 CNN 中，每个过滤器都会在整个视野中复制。这些复制的单元共享相同的参数化（权重向量和偏差）并形成特征图。这意味着给定卷积层中的所有神经元在其特定响应场内响应相同的特征。以这种方式复制单元允许所得到的激活图在视野中输入特征的位置移动的情况下是等变的，即它们授予平移等变性——假设该层的步幅为一。[72]<br />池化：在 CNN 的池化层中，特征图被划分为矩形子区域，每个矩形中的特征被独立下采样为单个值，通常采用平均值或最大值。除了减小特征图的大小之外，池化操作还为其中包含的特征赋予一定程度的局部平移不变性，从而使 CNN 对于其位置的变化更加 ROBUST。


## Classification

**Example**
```python  title="MNIST" linenums="1"
import torch
from torch import nn
from torch import optim
from torch.utils.data import DataLoader
from torchvision.datasets import MNIST
from torchvision.transforms import ToTensor
from tqdm import tqdm  # visual bar
import matplotlib.pyplot as plt

class Mymodel(nn.Module):
    def __init__(self, in_channels, classnumber):
        super(Mymodel, self).__init__()
        self.mymodel = nn.Sequential(
            nn.Conv2d(
                in_channels=in_channels,
                out_channels=32,
                kernel_size=3,
                # stride=1,
                padding=1,
            ),
            nn.BatchNorm2d(32),  # 正则化
            nn.ReLU(),
            nn.MaxPool2d(2,2),  # 28/2=14
            nn.Conv2d(
                in_channels=32,
                out_channels=32,
                kernel_size=3,
                # stride=1,
                # padding=0,
            ),
            # 14-2=12
            nn.BatchNorm2d(32),  # 正则化
            nn.ReLU(),
            nn.MaxPool2d(2, 2),  # 12/2=6
            nn.Conv2d(
                in_channels=32,
                out_channels=32,
                kernel_size=3,
                # stride=1,
                # padding=0
            ),
            # 6-2=4
            nn.BatchNorm2d(32),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),  # 4/2=2
        )

        self.filter = nn.Sequential(
            nn.Linear(32*2*2, 64),
            nn.ReLU(),
            nn.Linear(64, classnumber)
        )
    def forward(self,inputs):
        inputs = self.mymodel(inputs)
        inputs = inputs.view(-1, 32*2*2)
        inputs = self.classifier(inputs)
        return inputs


if __name__ == '__main__':
    train_dataset = MNIST(root="D:\File\CODE\python\dataset")
    train_dataloader = DataLoader(dataset=train_dataset, batch_size=64, shuffle= True)

    test_dataset = MNIST(root= "D:\File\CODE\python\dataset", train=False, transform=ToTensor())
    test_dataloader = DataLoader(dataset=test_dataset, batch_size=10)

    device = "cuda"
    model = Mymodel(in_channels=1, classnumber=10).to(device)

    epochs = 100
    optimizer = optim.Adam(model.parameters()) # lr=1e-3 by default
    loss_fn = nn.CrossEntropyLoss()  # 交叉熵

    for i in range(epochs):
        model.train()
        train_data = tqdm(train_dataloader)

        mean_loss, acc = 0.0, 0.0  # 损失、精确度
        data_num = 0

        for x,y in train_data:  # x is input, y is label or target
            x = x.to(device)  # Move input and target to GPU if available
            y = y.to(device)

            predicts = model(x)  # 先预测
            # predicts: This is the output of the model for the current batch of inputs x.
            # [batch_size, n_classes], where n_classes is the number of classes in the classification problem.
            loss = loss_fn(predicts, y)  # 再算损失
            optimizer.zero_grad() # 优化器梯度清零
            loss.backward()  # 反向传播
            optimizer.step()  # 更新模型参数

            acc += torch.sum(torch.argmax(predicts,dim=1) == y).item()
            # torch.argmax(predicts, dim=1): This function finds the indices (i.e., the classes)
            # of the maximum values along dimension 1 (the class dimension) of predicts.
            # This effectively performs a prediction by selecting the class with the highest score for each input in the batch.
            # The output shape matches the batch size, containing the predicted class for each input.

            # torch.argmax(predicts, dim=1) == y: This compares the predicted classes to the true labels y.
            # If a prediction matches the true label, the comparison returns True; otherwise, it returns False.
            # this comparison effectively counts the correct predictions by returning a tensor of 1s and 0s.

            # torch.sum(...): This function sums up the values in the tensor of 1s (correct predictions) and 0s (incorrect predictions),
            # giving the total number of correct predictions in the batch.

            # item(): This method converts a PyTorch scalar tensor (a tensor with a single value) to a Python number.
            # It's used here to extract the number of correct predictions as a Python integer or float, which can then be accumulated in the acc variable.

            # acc += ...: This accumulates the number of correct predictions over all batches processed in the epoch.
            # By adding up the number of correct predictions after processing each batch, you keep a running total of how many samples have been correctly classified so far during the epoch.
            mean_loss /= loss.item() * x.size(0)
            data_num += x.size(0)
            train_data.set_description(f"Training..Epoach:{i+1}/{epochs},Loss:{loss.item(* x.size(0)):.4f}")

        mean_loss /=data_num
        acc /= data_num
        print(f"Training acc:{acc:.4f},Loss:{mean_loss:.4f}")

        model.eval()  # Set the model to evaluation mode评估模式
        test_data = tqdm(test_dataloader)  # Wrap dataloader with tqdm for a progress bar
        mean_loss, acc = 0.0, 0.0
        data_num = 0
        with torch.no_grad():  # Disable gradient calculation没有梯度计算和更新
            for x, y in test_data:
                x = x.to(device)
                y = y.to(device)
                predicts = model(x)
                loss = loss_fn(predicts, y)
                # 不需要优化和更新
                acc += torch.sum(torch.argmax(predicts, dim=1) == y).item()
                mean_loss += loss.item() * x.size(0)
                data_num += x.size(0)
                test_data.set_description(
                    f"Evaluation ... Epoch: {i + 1}/{epochs}, Loss: {loss.item() * x.size(0):.4f}")
            mean_loss /= data_num
            acc /= data_num
            print(f"\nTraining Acc: {acc:.4f}, Loss: {mean_loss:.4f}")

        torch.save(model.state_dict(), "./model.pth")

```