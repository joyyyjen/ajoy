---
title: "Nn Implement"
date: 2019-06-05T20:22:36+08:00
draft: true
---

## nn.Module:
以 torch 實作 neural network 時，最常用的套件為 nn，而在 nn 中，建構 neural network 最基本的單位為 nn.Module

```python

import torch.nn as nn

class RNN(nn.Module): 
    def __init__(self, input_size, hidden_size, output_size):
        super(RNN, self).__init__()

        self.hidden_size = hidden_size

        self.i2h = nn.Linear(input_size + hidden_size, hidden_size)
        self.i2o = nn.Linear(input_size + hidden_size, output_size)
        self.softmax = nn.LogSoftmax(dim=1)

    def forward(self, input, hidden):
        combined = torch.cat((input, hidden), 1)
        hidden = self.i2h(combined)
        output = self.i2o(combined)
        output = self.softmax(output)
        return output, hidden

    def initHidden(self):
        return torch.zeros(1, self.hidden_size)

n_hidden = 128
rnn = RNN(n_letters, n_hidden, n_categories)

```

### nn.Linear()

- nn.Linear(2,3)

 nn.Linear 是用來進行 y=Wx+b 這類的線性運算所用的模組。
 它繼承了 nn.Module 。 
 而 2 和 3 分別代表了 x 和 y 的維度。 當它被建構出來時， weight 和 bias 的值會以隨機值來初始化。

建構 Linear 所需的參數有 inputSize , outputSize 和 bias 。 bias 不一定要給，如果沒有給，則預設值會讓它是隨機的。

reference: https://ckmarkoh.github.io/blog/2016/12/19/torch-nn-tutorial-1-nn-module/


### hidden_size / hidden dimension

#### 為什麼hidden_size = 128?? 

There are really two decisions that must be made regarding the hidden layers: how many hidden layers to actually have in the neural network and how many neurons will be in each of these layers.

- Hidden Layers 層數
NNs with more hidden layers are extremely hard to train 


- The Number of Neurons in the Hidden Layers

Using too few neurons in the hidden layers will result in something called underfitting
reference: https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw

Using too many neurons in the hidden layers can result in several problems. First, too many neurons in the hidden layers may result in overfitting. Overfitting occurs when the neural network has so much information processing capacity that the limited amount of information contained in the training set is not enough to train all of the neurons in the hidden layers. A second problem can occur even when the training data is sufficient. An inordinately large number of neurons in the hidden layers can increase the time it takes to train the network.

There are many rule-of-thumb methods for determining the correct number of neurons to use in the hidden layers, such as the following:

The number of hidden neurons should be between the size of the input layer and the size of the output layer.
The number of hidden neurons should be 2/3 the size of the input layer, plus the size of the output layer.
The number of hidden neurons should be less than twice the size of the input layer.


### 神經網路的核心元件
- Layer (層)：深度學習的基石 + followed by softmax
- 模型：由層所組成的神經網路
- 損失函數 criterion, loss function
- 優化器, optimizer 