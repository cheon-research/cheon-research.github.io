---
key: GraphSAGE
title: "[NIPS'17] Inductive Representation Learning on Large Graphs 리뷰/설명"
author: "Sangjin Cheon"
tags: NIPS17 Representation-Learning Graph-Neural-Networks GraphSAGE
mathjax: true
---

<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_authors.png?raw=true">  
<br>
Paper: [https://arxiv.org/abs/1706.02216](https://arxiv.org/abs/1706.02216){: target="_blank"}  
Slide: [https://github.com/cheon-research/paper_reviw_archive/blob/master/200922_GraphSAGE_cheon.pdf](https://github.com/cheon-research/paper_reviw_archive/blob/master/200922_GraphSAGE_cheon.pdf){: target="_blank"}  
<br>
GraphSAGE가 발표되기 전, Graph Neural Networks(GNNs)의 대표적인 모델로 Graph Convolutional Network(GCN, ICLR'17)이 있었습니다.  
GCN은 transductive learning을 기반으로 graph의 adjacency matrix(인접행렬)을 이용해 node의 embedding을 생성하는 방법인데, 처음 제안된 이후 지금까지도 이를 기반으로한 논문이 많이 발표되고 있으며, 현재(2020.09.30 기준) 4,795회 citation 되었습니다.  
GCN을 포함한 이전의 node embedding 방법들의 단점을 보안하는 방법을 이 논문을 통해서 제안했습니다.  

<br>

>제가 이해한 내용을 바탕으로 작성되었습니다.  
>완벽하지 않으니 참고해서 봐주시고 의견이 있으시면 댓글로 남겨주세요!  
>cheon.research (at) gmail.com  

# Introductions
논문의 내용을 본격적으로 시작하기에 앞서, Inductive Learning과 Transductive Learning을 간단하게 설명드리겠습니다.  
Indcutive Learning과 Transductive Learning는 테스트에 이용될 데이터가 전체 학습과정에서의 이용 되었는지 여부로 구분할 수 있습니다.  

<br>
<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_ductive_learning.png?raw=true" width="50%" height="50%">  

>출처: https://academic.oup.com/bioinformatices/article/34/4/541/4222633  

위의 그림에서 볼 수 있는 것처럼, Inductive learning에서는 테스트에서 예측할 unknown sequences를 inductive classifier의 학습과정에서 쓰지 않아도 prediction이 가능하지만, Transductive learning에서는 transductive classifier의 학습과정에서도 unknown sequences가 있어야 테스트에서 prediction이 가능하다는 차이가 있습니다.  
<br>
Graph와 관련된 문제들을 푸는데 있어서, node의 low dimensional vector embedding은 상당히 유용합니다. Node embedding은 dimensionality reduction(차원 축소)을 통해 embedding을 만드려는 node의 neigborhood들의 high dimensional information을 정제하여(distill) dense vector embedding으로 만드는 것을 기반으로 하고있습니다. 
이전에는 single fixed graph 상에서의 node embedding을 중점적으로 연구해왔습니다. 하지만 실제로는 새로운(본적 없는, unseen) node나 (sub)graph에 대한 embedding을 빠르게 만드는 것이 필요합니다. 그렇기 때문에 위에서 설명한 transductive 모델이 아닌, features로 부터 graph 위의 node들의 embedding을 generalization(일반화)해서 생성할 수 있는 inductive approach가 필요합니다.  
지금까지의 연구들은 대부분 transductive 하고, 비교적 최근에 발표된 GCNs은 neural network를 이용하긴 하지만 fixed graph에서의 trasnductive setting에서 동작학하는 단점이 있습니다.  
본 논문에서는 GCNs을 inductive unsupervised learning으로 확장하고, trainable aggregation functions을 통해 GCN의 approach를 일반화하는 framework를 제안합니다.  


## Present Work

# GraphSAGE
<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_figure_1.png?raw=true" width="75%" height="75%">  

## Embedding Generation Algorithm 
<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_algorithm.png?raw=true" width="75%" height="75%">  

## Learning the Parameters of GraphSAGE
$$J_{g}\left(z_u\right) = -log\left(\sigma\left({z_u}^T z_v\right)\right) - Q\dot\mathbb{E}_{v_n\tilt P_{n}(v)}log\left(\sigma\left(-{z_u}^T z_{v_n}\right)\right)$$

## Aggregator Architectures
### Mean Aggregator

### LSTM Aggregator

### Pooling Aggregator
$${AGGREGATE_k}^{pool} = max\left(\left{\sigma\left(W_{pool}{h_{u_i}}^k + b\right), Au_i\in N\left(v\right)\right}\right)$$

## Experiments
### Performance
<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_performance.png?raw=true" width="75%" height="75%">  

### Runtime 
<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_runtime.png?raw=true" width="50%" height="50%">  

### Runtime repect to Negative Samples
<img src="https://github.com/cheon-research/cheon-research.github.io/blob/master/assets/post_img/GraphSAGE_negative_samples.png?raw=true" width="50%" height="50%">  

__working...__
