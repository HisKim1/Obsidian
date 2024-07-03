: Deep Message-passing GNN on Mesh subgraph $\mathcal{G}_M(\mathcal{V}^M, \mathcal{E}^M)$ 
$\mathcal{E}^{M^i} \subset \mathcal{E}^{M} \quad \forall i\Rightarrow$ long dist. communication 가능

[[multi-mesh]] GNN
1. edge update$$\mathbf{e}^{M'}_{\nu_s^M \rightarrow \nu_r^M} = \text{MLP}^{\text{Mesh}}_{\mathcal{E}_M} \left( [ \mathbf{e}^{M}_{\nu_s^M \rightarrow \nu_r^M}, \mathbf{v}^M_s, \mathbf{v}^M_r ] \right)$$
2. vertex update$$\mathbf{v}^{M'}_i = \text{MLP}^{\text{Mesh}}_{\mathcal{V}_M} \left( \left[ \mathbf{v}^M_i, \sum_{\mathbf{e}^{M'}_{\nu_s^M \rightarrow \nu_r^M} : \nu_r^M = \nu^M_i} \mathbf{e}^{M'}_{\nu_s^M \rightarrow \nu_r^M} \right] \right)$$
3. reassign$$\begin{align} \mathbf{v}^M_i &\leftarrow \mathbf{v}^M_i + \mathbf{v}^{M'}_i \\ \mathbf{e}^{M}_{\nu_s^M \rightarrow \nu_r^M} &\leftarrow \mathbf{e}^{M}_{\nu_s^M \rightarrow \nu_r^M} + \mathbf{e}^{M'}_{\nu_s^M \rightarrow \nu_r^M} \end{align}$$
4. 를 16번 iterate w/ MLP의 각 layer에서 unshared weights