---
title: Forecasting Global Weather with Graph Neural Networks
site: https://arxiv.org/abs/2202.07575
summary: GNN으로 기후 예측 가능하다고 처음 말한
keyword:
  - MPNN
status:
  - Done
aliases:
tags:
  - paper
datetime: 2024-06-22T13:58:00
when_published: 2022-02-15
where_published:
  - arXiv
---
## **Dataset**
1) ERA5
2) NOAA's GFS
3) additional dataset
	1) land-sea mask
	2) orography (산악학)
	3) TOA solar radiation $\rightarrow$ *왜 얘를 추가했을까?*  
```ad-faq
#Question 
왜 TOA solar radiation을 forcing term으로 사용?

#Answer
forcing:= variables that can be fed to the model, but do not need to be predicted

1) can be computed analytically 
   (e.g. the toa radiation of the sun is mostly a function of geometry)
2) are considered to be controlled for the experiment 
   (e.g., impose a scenario of C02 emission into the atmosphere)
3) can include information "from the future", that is, formation at target times specified in the `targets_template`.

-> TOA는 수식으로 구할 수 있으니 autoregressive할 때 future도 구해서 넣을 수 있다.
수식으로 구한 값이랑 비교 prediction이 너무 이상한 값으로 튀지 않도록 'forcing'해서 신뢰, 정확성 향상
제어 시나리오 실험도 할 수 있다.
(e.g. CO2 농도 변화 시나리오)

from predator_base.py
```
	   
		
## **Encoder**
1) lat/lon grid $\rightarrow$ icosahedron(이십면체) grid
2) bipartite graph 사용
3) physical data를 abstract latent feature로 mapping
4) 78 atm. var. $\in$ vertex 
	$\Rightarrow$ *78 channels* 
5) lat/lon node positions $\in$ edge
	
*using MPNN? 어떻게 넣었단 말?*

## **Processor**
1) 256-channel latent feature data를 MPNN 9 round 돌려

## **Decoder**
1) icosahedron grid $\rightarrow$ lat/lon grid
2) processor output + lat/lon original input을 받아서
   $\Rightarrow$ 6h change output 만들어
   $\Rightarrow$ initial state에 더해서 6h 뒤 예측 생산

*6h이 장기, 단기에 적당했다 $\rightarrow$ 바꾸면 좋을 듯?*

## **Overfitting**
training error = validation error = true error
$\Rightarrow$ $\not \exists$ overfitting

## **Training**
1) Adam 사용
2) 이유는 모르지만 $2^\circ \Rightarrow 1^\circ \Rightarrow 1^\circ$ data로 학습하는 게 $1^\circ$로만 3번 하는 것보다 잘 되더라
3) ~10d 예측 위해 $2^\circ$ (4 step loss) $\Rightarrow 1^\circ$ (8 step loss) $\Rightarrow 1^\circ$ (12 step loss) 사용
4) loss normalization 사용 $$x_{norm}= \frac{x-\bar{x}}{\sigma}$$
## **Conclusion** : 앞으로 뭘 해볼 수 있을까
1) spatial resolution 향상 $\rightarrow$ [[@Lam. et al., 2023]]
2) adaptive mesh refinement  $\rightarrow$ [[@Lam. et al., 2023]]
3) generate large ensembles  $\rightarrow$ 딥마인드가 한 거 같은데?
4) data-driven data assimilation model $\rightarrow$ 가 뭘 말하는지 모르겟음
5) end-to-end, data-driven forecast system $\rightarrow$ 22p