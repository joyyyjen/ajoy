---
title: "Language Model"
date: 2019-03-03T19:44:13-06:00
---
1954 年的時候，IBM-Georgetown 展示了他們機器翻譯，就此，掀起了機器翻譯的熱潮。這股熱潮，最終被1966年的ALPAC Report 終結，直到研究人員開始使用統技方法取代基於規則方法。然後，早在1949年，就有學者提出多語義的解決辦法。瓦倫·韋弗在他1949年備忘錄提到：
> If one examines the words in a book, one at a time through an opaque mask with a hole in it one word wide, then it is obviously impossible to determine, one at a time, the meaning of words. 'Fast' may mean 'rapid'; or it may mean 'motionless'; and there is no way of telling which. "But, if one lengthens, the slit in the opaque mask, until one can see not only the central word in question but also say N words on either side, then if N is large enough one can unambiguously decide the meaning..."

- 讓我們做個小活動，猜猜下個字是什麼？
我今＿
我今天吃＿
我今天吃了一整＿
我今天吃了一整碗湯。
你看出了什麼？

我們可以用前文推測出下個字出現的是什麼。 原本我們理解一個句子，需要知道範圍，知道句法，知道字義，但其實這些都可以以簡單的統計技巧推測出。
<!--more-->
### N-Grams
N-grams are token sequences of length N. 
那麼 bigrams or 2-grams 就是 <我今>,<今天>,<天吃>,<吃了>, .... 
這代表，當們我知道某長度的字串出現在2-gram裡的次數時，我們可以計算他出現的機率，從而計算整行句子的可能性。 
例如：
<今天>出現的比率比<今夏>高，因此，我今＿，空格裡的字較有可能是「天」。

### Language Model 語言模型
預測一個字出現的機率是：
P(W_{n}|W_{1},W_{2}... W_{n-1})
我們稱這種統計式為語言模型
 
計算"The big dog"的機率是: P(The^big^dog) 
![img1](/lang-model.png)

- 1-grams(Unigrams): P(dog)
- Bigrams: P(dog|big)
- Trigrams: P(dog|the big)
- Quadrigrams: P(dog|the big fat)

假設我們不考慮前後文，一個字出現的機率是: 1/(numbers of token)

因此，語言模型給出的更加理想：![img2](/equation.png)

P(the big dog barks) = P(the)*P(big|the)*P(dog|the big)*P(barks| the big dog)

當然這樣的計算是有問題的，因為當我們說一句話，這句話完完全全重複的機率不高，尤其一個句子相當長的時候。我們不能完全依靠字串前出現的所有字，但我們可以簡化到 bigram, trigrams, 或者4-grams, 5 grams。只看該字的前2-5字。 
當然，這不是最完善。就像英文有長距語義關聯。例如："The computer which I had just put into the machine room on the 5th floor crashed."
我們先優先不考慮這些問題; 

從 N-grams probabilities我們可以得到一些語言的現象。

- **World knowledge** P(english|want) = 0.0011 P(Chinese|want) = 0.0065
-- want Chinese food 的機率比want English大  
- **語法** P(to|want) = 0.66 P(eat|to) = 0.28 P(food|to) = 0
- **Discourse** P(want|spend) = 0 P(i|\<s\>) = 0.25

### 評估N-Gram模型
#### 外在評估(Extrinsic Evaluation ):

- Evaluate the performance of the application with model A
- Put Model A into an application: a speech recognizer; MT system
   ・ Get performance for model A:
   ・ How many words were translated correctly?
   ・ How many misspelled words were corrected properly?
然而外在評估因為是real-world test，可能一個實驗就要跑上好幾天。因此有個替代方案 - 內在評估

#### 內在評估 (Intrinsic Evaluation): 又稱為Perplexity

- Evaluate the performance independent of any application.
- perplexity is a poor approximation unless the test data looks just like the training data

#### 評估基本步驟:
1. Train parameters of our model on a training set
2. Use a test test: use data we haven't seen
3. Use a evaluation metric to tell us how well our model is doin gon the test set. - one such metric is perplexity

### Smoothing

Back to Shakespeare: Recall that Shakespeare produced 300,000 bigram types out of v^2 = 844 million possible bigrams So, 99.96% of the possible bigrams were never seen. But it does not mean any sentence that contains one of those bigrams should have a probability of 0. 
Some of those zeros are really zeros:(ungrammatical). On the other hand, some of them are just rare event.
If the training corpus had been a little bigger they would have had a count.  Our estimates are sparse! We have no counts at all for the bast bulk of things we want to estimate!

Answer: estimate the likelihood of unseen N-grams
#### Laplace Smoothing - add one smoothing
intuition, just add one to all the counts
MLE estimate: P(wi) = ci/N
Laplace estimate: P(wi) = ci+1 / N+V 
Reconstructed count: 
- ci* = (ci+1)*N/N+V
- V is word type
- ci is count of word i
- N is number of token
### Better Smoothing
#### Good-Turing
Good Turing Kneser-Ney Written-Bell - to use the count of things we've seen once to help estimate the count of things we've never seen

假設你在釣魚。這裡有八種魚：carp, perch, whitefish, trout, salmon, eel, catfish, bass. 你已經釣過: 10 carp, 3 perch, 2 whitefist, 1 trout, 1 salmom, 1 eel = 18 fish 
有多少可能性，你釣到的下條魚是你沒釣過的魚? 3/18 
有多少可能性，你釣到的下條魚是一條trout? Maybe less then 1/18

Notation: Nx is the frequency-of-frequency-x
- N10 = 1 : number of fish species seen 10 times is 1 
- N1 = 3 number of fish species seen 1 is 3 
- To estimate total number of unseen species c0* = c1 po = N1/N = 3/18 c* = (c+1)*Nc+1/ NC

### Backoff vs.Interpolation
- Backoff: use trigram if you have it, otherwise bigram, otherwise unigram
- Interpolation: mix all three

### OOV-out of vocabulary = OOV words