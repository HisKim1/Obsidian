---
author: Eugenia Kalnay
datetime: 2024-08-19
---
# 6. Atmosepheric Predictability and Ensemble Forecasting

### 6.1 | Introduction to atmospheric predictability
어쩌다 Lorenz가 butterfly effect를 발견하게 되었는가에 대한 간략한 story-telling

### 6.2 | Brief review of fundamental concepts about chaotic systems
##### Lorenz's three-variable model
$$\displaystyle\begin{cases}
\dfrac{x}{t}=\sigma(y-x)\\
\dfrac{y}{t}=rx-y-xz\\
\dfrac{z}{t}=xy-bz
\end{cases}$$
- Characteristics
	[[Lorenz's three variable model is a dissipative system|dissipative system]]^[소멸하는] $\leftrightarrow$ Hamiltonian^[conserve total energy or some other similar property of the flow]
	nonlinear & autonomous system
	init cond ($\sigma, b, r$) sensitively dep $\rightarrow$ chaotic solution

##### Phase space
solution space
dimension = # of indep variables
dim of the attractor; init transient period 이후 방문한 subspace의 dim은 더 작다
##### Trajectory or Orbit
init cond가 주어졌을 때의 solution in Phase space
##### Transient
initial portion of the trajectory
##### Attractor
transient가 끝나고 trajectories가 계속 접근하는 set of points
각 components는 basins of attraction을 갖음
- stationary points^[equilibrium or steady state solutions of the dynamical squations]
- periodic orbits
- strange attractors^[can include periodic orbits]
##### Bifurcation point
flow가 abruptly change하는 지점

$$\displaystyle\begin{cases}
\text{stable sol.: bounded, }\forall t, \forall \text{sol. stay close to it}\\
\qquad \Rightarrow \text{periodic or at least almost periodic}\\
\\
\text{unstable sol.: very close two trajectories } \rightarrow \text{completely diverge}\\
\qquad \Rightarrow \text{not periodic or almost periodic}
\end{cases}$$
periodic motion bifurcation $\rightarrow$ periodic doubling $\rightarrow$ sequence of period doubling bifurcation $\rightarrow$ chaotic behavior


##### Lyapunov exponent 
Measures sensitivity to initial conditions in dynamical systems
$\rightarrow$ dynamical system of $n$-variables의 long-term stability
	$\exists \lambda_i >0$ : chaotic behavior
	$\forall i, \lambda_i \leq 0$ : stable system
$$\displaystyle\Rightarrow \quad \begin{cases}
\sum \lambda_i = 0 \text{: Hamiltonian (volume-conserving) system}\\
\sum \lambda_i \neq 0\text{: dissipative system}\end{cases}$$

### 6.3 | Tangent linear model, adjoint model, singular vecotrs, and Lyapunov vectors
이런 저런 방법으로 여러 모델들을 만들었다.
> He also pointed out that the predictability of the model is not constant with time: it depends on the stability of the evolving atmospheric flow.

### 6.4 | Ensemble forecasting: early studies
instability로 인한 error growth는 ineveitably lead to a total loss of skill in the weather forecasts after a finite forecast length.
> Lorenz estimated this limit of weather predictability as about two weeks.

![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-20 15.54.43.excalidraw|700]]

###### 6.4.1 | Stochastic-dynamic forecasting

###### 6.4.2 | Monte Carlo forecasting
**Symbols)**
$\mathbf{u}_0$ : true state of the atmosphere
$\hat{\mathbf{u}}$ : unbiased estimate of $\mathbf{u}_0 \rightarrow \langle\hat{u}\rangle = 0$ 

**Background)** 
climatological forecast error covariance
$$\begin{align*}
\langle (0-\mathbf{u}_0)(0-\mathbf{u}_0)^T\rangle &= \langle\mathbf{u}_0\mathbf{u}_0^T\rangle\\ &=\mathbf{U}\end{align*}$$
> Since forecasts lose their skill at longer lead times, and individual forecasts eventually are further away from the verification thatn the climatology, <font color="#00e676">optimal estimation of the verification is equivalent to tempering</font> (i.e., hedging the forecast towards climatology).

$\Rightarrow$ forecast error covariance를 최대한 $\mathbf{U}$에 가깝게 만들어보자

**Case 1)** 
single forecast error covariance
$$\begin{align}
\langle (\hat{\mathbf{u}}-\mathbf{u}_0)(\hat{\mathbf{u}}-\mathbf{u}_0)^T \rangle &= \langle (\hat{\mathbf{u}}\hat{\mathbf{u}}^T + \mathbf{u}_0\mathbf{u}_0^T - \hat{\mathbf{u}}\mathbf{u}_0^T - \mathbf{u}_0\hat{\mathbf{u}}^T) \rangle \\
&= \langle \hat{\mathbf{u}}\hat{\mathbf{u}}^T \rangle + \langle \mathbf{u}_0\mathbf{u}_0^T \rangle - \langle \hat{\mathbf{u}}\mathbf{u}_0^T \rangle - \langle \mathbf{u}_0\hat{\mathbf{u}}^T \rangle \\
&\xrightarrow{t \to \infty} \langle \hat{\mathbf{u}}\hat{\mathbf{u}}^T \rangle + \langle \mathbf{u}_0\mathbf{u}_0^T \rangle - 0 - 0 \quad (\because\text{decorrelation between }\hat{\mathbf{u}} \text{ \& }\mathbf{u}_0)\\
&= \mathbf{U} + \mathbf{U}\quad (\because\text{unbiased model }\rightarrow \mathbb{E}[\hat{\mathbf{u}}\hat{\mathbf{u}}^T ]\simeq \mathbb{E}[\mathbf{u}_0\mathbf{u}_0^T])\\
&= 2\mathbf{U}
\end{align}$$
**Case 2)** 
regression forecast
$$ \begin{align}
\hat{u}_0 &= \hat{u}A \\
\text{s.t.} \quad \min \varepsilon^T\varepsilon &= \min \langle (u_0-\hat{u}A)^T(u_0-\hat{u}A) \rangle \end{align}$$ where $A$: const. reg. coeff. matrix 
Let $y = XA \Rightarrow \varepsilon = y - XA$.
$$ \varepsilon^T\varepsilon = (y-XA)^T(y-XA) $$ $$\begin{align}
\frac{\partial \varepsilon^T\varepsilon}{\partial A} &= \frac{\partial}{\partial A} (y-XA)^T(y-XA)\\
&= -2X^T(y-XA)\\ &= 0 \\ 
\Rightarrow 2X^Ty &= 2X^TXA \end{align}$$ $$ \therefore A = (X^TX)^{-1}X^Ty = X^\dagger y $$$$\Rightarrow A = \langle \hat{u}^T\hat{u} \rangle^{-1} \langle \hat{u}^Tu_0 \rangle \quad (\because u_0 \sim y, \hat{u} \sim X)$$but matrix size $\uparrow$ $\Rightarrow$ computational cost $\uparrow$

**Case 3)** 
ensemble forecast error covariance
$\mathbf{r_i}$: perturbation
$\hat{\mathbf{u}}$: init best estimate
$\displaystyle\overline{u} := \frac{1}{m} \sum u_i$: avg of ensemble $m$ forecasts
$m$: # of ensemble

initial error cov: $P_0 = \langle rr^T \rangle$ (in practice !measurable $\rightarrow$ approx.)
$$\displaylines{\begin{align}
\langle (\overline{u} - u_0)(\overline{u} - u_0)^T \rangle &= \langle \overline{u}\overline{u}^T + u_0u_0^T - \overline{u}u_0^T - u_0\overline{u}^T \rangle \\
&= \langle \overline{u}\overline{u}^T \rangle + \langle u_0u_0^T \rangle - \langle \overline{u}u_0^T \rangle - \langle u_0\overline{u}^T \rangle \\
&\xrightarrow{t \to \infty} \frac{m}{m^2}U + U + 0 + 0 \quad(\because \text{same reason with Case 1})\\ 
&= (1+\frac{1}{m})U
\end{align}}$$
$$\begin{align} 
\because \langle \overline{u}\overline{u}^T \rangle &= \langle\frac{1}{m} \sum u_i \frac{1}{m} \sum u_j \rangle \\
&= \frac{1}{m^2} \langle \sum u_i \sum u_j \rangle \\
&= \frac{1}{m^2} \times m U \\
&= \frac{1}{m} U
\end{align}$$
$\Rightarrow$ ensemble 개수가 적어도 tempering 잘 됨 / stochastic보다 practical, computable /
$\quad$ ensemble mean은 8개만 있어도 되지만 forecast error는 많이 필요하다
$\Rightarrow$ init perturbation을 어케 줄건지, # of ensemble이 중요

###### 6.4.3 | lagged average forecasting
$t = -\tau, -2\tau, \cdots -(N-1)\tau$ 