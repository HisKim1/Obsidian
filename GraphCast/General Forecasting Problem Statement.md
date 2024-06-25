p.23~24

$$\mathbf{Z}^{d+\Delta d:d+T\Delta d} = \left( \Phi(\mathbf{Z}^d), \Phi(\mathbf{Z}^{d+\Delta d}), \ldots, \Phi(\mathbf{Z}^{d+(T-1)\Delta d}) \right)$$
$T$ : Forecast horizon. forecast할 total step 수
$d$ : Validity time. 특정 weather state의 일시
$d_0$ : Forecast initialization time. forecast initial input
$\tau$ : Forecast lead time. forecast동안 elapsed time; $\tau = t\Delta d$
**$\mathbf{Z}^d$** : time $d$일 때의 true state of global weather
$\Phi(\mathbf{Z}^d)$ : $\mathbf{Z}^d$에서 $\Delta d$ 만큼 지난 next state를 generate하는 discrete-time dynamics function 
$\Rightarrow \Phi(\mathbf{Z}^d) = \mathbf{Z}^{d+\Delta d}$ 

 이론상 $T$ autoregressive iterations 돌리면 예측 가능하다.


---

*Assume that*  $\mathbf{Z}^d$ observe 불가능 but partial인 $\mathbf{X}^d$는 가능

$\Rightarrow$ $\Phi(\mathbf{Z}^d, \cdots )$ 대신에 $\phi(\mathbf{X}^d, \cdots)$로 $T\Delta d$ 이후를 잘 구해보자
$$\hat{\mathbf{X}}^{d+\Delta d} = \phi(\mathbf{X}^d, \mathbf{X}^{d-\Delta d}, \ldots)$$$$\begin{aligned} \hat{\mathbf{X}}^{d+\Delta d:d+T\Delta d} = & \left( \phi(\mathbf{X}^d, \mathbf{X}^{d-\Delta d}, \ldots), \right. \\ & \phi(\hat{\mathbf{X}}^{d+\Delta d}, \mathbf{X}^d, \ldots), \\ & \ldots, \\ & \left. \phi(\hat{\mathbf{X}}^{d+(T-1)\Delta d}, \hat{\mathbf{X}}^{d+(T-2)\Delta d}, \ldots) \right). \end{aligned}$$
그러면 Loss function은
$$\mathcal{L}\left( \hat{\mathbf{X}}^{d+\Delta d : d+T\Delta d}, \mathbf{X}^{d+\Delta d : d+T\Delta d} \right)$$
(GC에서는 $\Delta d = 6h, T=40$)