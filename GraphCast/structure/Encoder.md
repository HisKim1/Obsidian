1. Embedder
   [[GraphCast's Graph]]의 features, $\mathcal{V}^G, \mathcal{V}^M, \mathcal{E}^M, \mathcal{E}^{G2M}, \mathcal{E}^{M2G}$를 5 Multi-layer Perceptrons, MLP로 fixed sized latent space로 embed 
   
```ad-question
   #question
   5 MLP가 5 hidden layer라는건지, 아니면 그냥 feature 5개를 각 MLP에 넣은 건지. 그렇다면 각 MLP는 어떻게 생겼는지 확인
```
   
   $$\begin{align*} \mathbf{v}^{G}_i &= \text{MLP}_{\text{embedder}}^{\mathcal{V}_G} (\mathbf{v}^{G, \text{features}}_i) \\ \mathbf{v}^{M}_i &= \text{MLP}_{\text{embedder}}^{\mathcal{V}_M} (\mathbf{v}^{M, \text{features}}_i) \\ \mathbf{e}^{M}_{\nu_s^M \rightarrow \nu_r^M} &= \text{MLP}_{\text{embedder}}^{\mathcal{E}_M} (\mathbf{e}^{M, \text{features}}_{\nu_s^M \rightarrow \nu_r^M}) \\ \mathbf{e}^{G2M}_{\nu_s^G \rightarrow \nu_r^M} &= \text{MLP}_{\text{embedder}}^{\mathcal{E}_{\text{G2M}}} (\mathbf{e}^{G2M, \text{features}}_{\nu_s^G \rightarrow \nu_r^M}) \\ \mathbf{e}^{M2G}_{\nu_s^M \rightarrow \nu_r^G} &= \text{MLP}_{\text{embedder}}^{\mathcal{E}_{\text{M2G}}} (\mathbf{e}^{M2G, \text{features}}_{\nu_s^M \rightarrow \nu_r^G}) \end{align*}$$
2. Grid2Mesh GNN
   bipartite subgraph $\mathcal{G}_{G2M}(\mathcal{V}^G, \mathcal{V}^M, \mathcal{E}^{G2M})$에서 Message-passing GNN 1 step행ge update$$\mathbf{e}^{\text{G2M}'}_{\nu_s^G \rightarrow \nu_r^M} = \text{MLP}^{\text{Grid2Mesh}}_{\mathcal{E}_{\text{G2M}}} \left( [ \mathbf{e}^{\text{G2M}}_{\nu_s^G \rightarrow \nu_r^M}, \mathbf{v}^G_s, \mathbf{v}^M_r ] \right)$$
   2) mesh vertex update$$\mathbf{v}^{M'}_i = \text{MLP}^{\text{Grid2Mesh}}_{\mathcal{V}_M} \left( \left[ \mathbf{v}^M_i, \sum_{\mathbf{e}^{\text{G2M}'}_{\nu_s^G \rightarrow \nu_r^M} : \nu_r^M = \nu^M_i} \mathbf{e}^{\text{G2M}'}_{\nu_s^G \rightarrow \nu_r^M} \right] \right)$$
   3) grid vertex update (no change)$$\mathbf{v}^{G'}_i = \text{MLP}^{\text{Grid2Mesh}}_{\mathcal{V}_G} \left( \mathbf{v}^G_i \right)$$
   4) reassign variables $$\begin{align} \mathbf{v}^G_i &\leftarrow \mathbf{v}^G_i + \mathbf{v}^{G'}_i, \notag \\ \mathbf{v}^M_i &\leftarrow \mathbf{v}^M_i + \mathbf{v}^{M'}_i, \notag \\ \mathbf{e}^{\text{G2M}}_{\nu_s^G \rightarrow \nu_r^M} &\leftarrow \mathbf{e}^{\text{G2M}}_{\nu_s^G \rightarrow \nu_r^M} + \mathbf{e}^{\text{G2M}'}_{\nu_s^G \rightarrow \nu_r^M}. \end{align}$$
   