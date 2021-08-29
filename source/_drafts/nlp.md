---
title: Natural Language Process (NLP) 簡介
date: 2021-08-04 17:25:57
categories: 深度學習
tags: [deep learning, NLP]
---

最近因為工作需求，接觸了一些NLP的技術，趁著記憶還新鮮的時候，整理一下讀過的東西。以下內容多半是出於我自己的理解，並參考一些別人的文章，如果有發現任何錯誤，歡迎來信告知。


&nbsp;

### Natural Language Processing (NLP)

自然語言處理（NLP）是一門結合語言學、電腦科學以及人工智慧的技術，目的是讓機器能夠辨認、理解並運用書面或口說形式的人類語言。NLP的任務包含自然語言理解（Natural Language Understanding, NLU）及自然語言生成（Natural Language Generation）。自然語言理解關心的是如何將自然語言轉換成機器可以理解的形式，也就是將自然語言轉換成010010；相反地，NLG關心的是如何讓機器可以自行產生自然語言。

早期（1990年以前）NLP的技術多半是基於規則法（rule-based），建立字詞之間的關係，並定義語法，或以此來設計聊天系統。Rule-based法不易於擴展，窮舉所有例子。也無法舉一反三。

1990s-2010s時盛行基於統計的機器學習方法，有別於rule-based method，這種方法需要annotated data來建模。想法上是用人工定義的特徵去建立模型，然後透過annotated data來訓練模型的參數。這種方法大大改善rule-based method的表現。不過，這種方法受限於label資料的多寡及好壞，需要大量人工標註的資料。此外，面對不同的NLP任務，模型的表現會有顯著的差異，如果要在特定task上表現得好，需要該任務的label資料，顯示機器學習訓練出來的模型不能泛用。最後，在處理更高階、抽象的文義時，人工標註的方式會出現瓶頸，使得機器只能學習一些看過的概念。

2010s後深度學習崛起，類神經網路在NLP取得巨大的成功，幾乎取代所有NLP原有的語言模型。其中，類神經網路在word representation(將文字轉成vector)上表現得相當突出，取代原有機率(probabilistic models)及人工定義特徵的word vector (通常為discrete, sparse vector)，成功將字詞映射到embedding space，用continuous/distributed representation來表示字詞，稱為word embedding。word embedding滿足特徵工程的需求，解決機器學習法無法表現高階、抽象意涵的自然語言。此外，深度學習並不需要專家人工標註資料，大大解決訓練資料有限的問題。

> **Word Embedding**

嚴格來說，word embedding算是模型訓練的副產物。2003年，Bengio等人提出神經語言模型(neural network language model)，成功利用類神經網路預測下一個詞的機率分布，同時得到word embedding副產物。

現今要得到word embedding有好幾種方法，例如CBOW、skip-gram、GloVe、等等，但大方向上訓練的方法都一樣，首先蒐集一大堆字詞、句子的語料庫(corpus)，然後依照不同的方法抽出字詞，將字詞輸入embedding matrix矩陣，轉成word embedding，然後經過output layer輸出後，透過unsupervised learning的方式去訓練模型。當模型訓練完成，就得到embedding matrix，可以將文字轉換成word embedding。

詳細訓練方法如下：

將corpus中的字詞都表示成one-hot encode，抽取一段文字，例如每次抽4個字，如a glass of juice，將a、glass、of的one-hot encode輸入模型，各自轉成word embedding，經過concat後，輸出softmax，長度跟input的one-hot encode一樣，預期model會吐出juice這個字，所以餵給model的是juice的one-hot encode。如此，就能算出loss，經過back propagation去訓練模型。完成後，就能得到word matrix(模型的hidden layer)，能夠將文字轉成word embedding。

word embedding的突破種點在於：過去機器學習在面對不同NLP任務，例如自動文摘、翻譯、情緒分析等，需要依據該task設計模型框架，並且所需的label資料也不同，更慘的是，模型學完之後，還不一定能泛用到其他領域。如今，深度學習透過大量無label資料做unsupervised learning，學到共用的word embedding，針對不同task，只需要設計對應的output layer就好，例如情緒分析就是classification layer。

> **Sequence to Sequence Model / Language Model**

- RNN
最基礎、可以處理sequence data的model。缺點會有vanishing gradients的問題，也就是loss無法back propagate回去t=1的輸入。白話講就是無法記住太久遠以前的文字，會忘記東西。

- Long Short Term Memory (LSTM)
LSTM解決了RNN的vanishing gradients，它透過forget gate

- GRU
GRU和LSTM一樣，都是為了解決RNN的vanishing gradients而誕生，架構差不多，只不過少了...


- Bidirectional LSTM



> **Attention**


> **Transformer**

> **ViT**

&nbsp;

### 參考資料

