[[Encoder]]와 동일, but opposite direction

bipartite subgraph $\mathcal{G}_{M2G}(\mathcal{V}^M, \mathcal{V}^G, \mathcal{E}^{M2G})$에서 Message-passing GNN 1 step 실행
1. Mesh2Grid GNN
	1) edge update $$\mathbf{e}^{\text{M2G}'}_{\nu_s^M \rightarrow \nu_r^G} = \text{MLP}^{\text{Mesh2Grid}}_{\mathcal{E}_{\text{M2G}}} \left( [ \mathbf{e}^{\text{M2G}}_{\nu_s^M \rightarrow \nu_r^G}, \mathbf{v}^M_s, \mathbf{v}^G_r ] \right)$$
	2) grid vertex update (mesh vertex는 no change)$$\mathbf{v}^{G'}_i = \text{MLP}^{\text{Mesh2Grid}}_{\mathcal{V}_G} \left( \left[ \mathbf{v}^G_i, \sum_{\mathbf{e}^{\text{M2G}'}_{\nu_s^M \rightarrow \nu_r^G} : \nu_r^G = \nu^G_i} \mathbf{e}^{\text{M2G}'}_{\nu_s^M \rightarrow \nu_r^G} \right] \right)$$
	3) reassign$$\mathbf{v}^G_i \leftarrow \mathbf{v}^G_i + \mathbf{v}^{G'}_i$$
	4) output function
	   : 서로 다른 MLP로 생성된 $\forall i$th grid node의 prediction $\hat{y}_i$;
	   prediction variables of each grid 227개 포함 $$\hat{y}_i^G = \text{MLP}^{\text{output}}_{\mathcal{V}_G} (\mathbf{v}^{G}_i) $$
	5) 예측 $\hat{\mathbf{X}}^{t+1}$ = 현재 $\mathbf{X}^t$ + change $\hat{Y}^t$
$$\begin{align*}\hat{\mathbf{X}}^{t+1} &= \text{GraphCast}(\mathbf{X}^t, \mathbf{X}^{t-1}) \\&= \mathbf{X}^t + \hat{Y}^t \end{align*}$$

 