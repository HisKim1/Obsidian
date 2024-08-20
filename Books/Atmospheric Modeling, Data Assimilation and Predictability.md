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

- Phase space
	solution space
	dimension = # of indep variables
	dim of the attractor; init transient period 이후 방문한 subspace의 dim은 더 작다

- Trajectory or Orbit
	init cond가 주어졌을 때의 solution in Phase space

- Transient
	initial portion of the trajectory

- Attractor
	transient가 끝나고 trajectories가 계속 접근하는 set of points
	각 components는 basins of attraction을 갖음
	- stationary points^[equilibrium or steady state solutions of the dynamical squations]
	- periodic orbits
	- strange attractors^[can include periodic orbits]

- Bifurcation point
	flow가 abruptly change하는 지점





### 6.3 | Tangent linear model, adjoint model, singular vecotrs, and Lyapunov vectors