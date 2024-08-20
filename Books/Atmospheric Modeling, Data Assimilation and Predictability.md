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

![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-20 15.54.43.excalidraw]]

###### 6.4.1 | Stochastic-dynamic forecasting
