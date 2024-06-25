이전 두 state로 그 다음 state를 만든다![^why?]

[^why?]: [1개보다 2개가 performance가 좋았고, 3개 하면 mem. footprint만큼의 효용을 얻지 못함; p.25 3.1]
$$\hat{\mathbf{X}}^{t+1} = \text{GraphCast}(\mathbf{X}^t, \mathbf{X}^{t-1})$$
$$\begin{aligned} \Rightarrow \hat{\mathbf{X}}^{t+1:t+T} = & \left( \text{GraphCast}(\mathbf{X}^t, \mathbf{X}^{t-1}), \right. \\
& \text{GraphCast}(\hat{\mathbf{X}}^{t+1}, \mathbf{X}^t), \\ 
& \ldots, \\ 
& \left. 
\text{GraphCast}(\hat{\mathbf{X}}^{t+T-1}, \hat{\mathbf{X}}^{t+T-2}) \right). \end{aligned}$$
---
![[GraphCast's Graph]]

---
![[Encoder]]
![[Processor]]
![[Decoder]]
