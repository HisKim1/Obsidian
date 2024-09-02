---
author: Eugenia Kalnay
datetime: 2024-08-19
---
# 6. Atmosepheric Predictability and Ensemble Forecasting

## 6.1 | Introduction to atmospheric predictability
어쩌다 Lorenz가 butterfly effect를 발견하게 되었는가에 대한 간략한 story-telling

## 6.2 | Brief review of fundamental concepts about chaotic systems
#### Lorenz's three-variable model
$$\displaystyle\begin{cases}
\dfrac{x}{t}=\sigma(y-x)\\
\dfrac{y}{t}=rx-y-xz\\
\dfrac{z}{t}=xy-bz
\end{cases}$$
- Characteristics
	[[Lorenz's three variable model is a dissipative system|dissipative system]]^[소멸하는] $\leftrightarrow$ Hamiltonian^[conserve total energy or some other similar property of the flow]
	nonlinear & autonomous system
	init cond ($\sigma, b, r$) sensitively dep $\rightarrow$ chaotic solution

#### Phase space
solution space
dimension = # of indep variables
dim of the attractor; init transient period 이후 방문한 subspace의 dim은 더 작다
#### Trajectory or Orbit
init cond가 주어졌을 때의 solution in Phase space
#### Transient
initial portion of the trajectory
#### Attractor
transient가 끝나고 trajectories가 계속 접근하는 set of points
각 components는 basins of attraction을 갖음
- stationary points^[equilibrium or steady state solutions of the dynamical squations]
- periodic orbits
- strange attractors^[can include periodic orbits]
#### Bifurcation point
flow가 abruptly change하는 지점

$$\displaystyle\begin{cases}
\text{stable sol.: bounded, }\forall t, \forall \text{sol. stay close to it}\\
\qquad \Rightarrow \text{periodic or at least almost periodic}\\
\\
\text{unstable sol.: very close two trajectories } \rightarrow \text{completely diverge}\\
\qquad \Rightarrow \text{not periodic or almost periodic}
\end{cases}$$
periodic motion bifurcation 
$\rightarrow$ periodic doubling 
$\rightarrow$ sequence of period doubling bifurcation 
$\rightarrow$ chaotic behavior
#### Lyapunov exponent 
Measures sensitivity to initial conditions in dynamical systems
$\rightarrow$ dynamical system of $n$-variables의 long-term stability
	$\exists \lambda_i >0$ : chaotic behavior
	$\forall i, \lambda_i \leq 0$ : stable system
$$$$$$\implies \quad \begin{aligned} &\sum \lambda_i = 0 &: \textrm{Hamiltonian (volume-conserving) system} \\ &\sum \lambda_i \neq 0 &: \textrm{dissipative system} \end{aligned}$$![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-22 17.10.53.excalidraw|700]]

## 6.3 | Tangent linear model, adjoint model, singular vecotrs, and Lyapunov vectors
이런 저런 방법으로 여러 모델들을 만들었다.
> He also pointed out that the predictability of the model is not constant with time: it depends on the stability of the evolving atmospheric flow.

### 6.3.1 | Tangent linear model and adjoint model

### 6.3.2 | Singular vectors 
#### step 1. Perturbation can be rewritten by linear combination of singular vectors.
$$\mathbf{y}(t_{1})=\mathbf{L}(t_{0},t_1)\mathbf{y}(t_0)$$
- $\mathbf{y}(t)$: perturbation at $t$
- $\mathbf{L}$: resolvent or propagator

Take Singular Value Decomposition on $\mathbf{L}$. Then
$$\mathbf{U^{T}LV=S}$$
where $\mathbf{S}$ is a diagonal matrix consists of singular values of $\mathbf{L}$, $\sigma_i$
and $\mathbf{UU^{T}=I}, \mathbf{VV^{T}=I}$.

- $\mathbf{v}_i$: right singular column vector $\to$ initial singular vector
- $\mathbf{u}_i$: left singular column vector $\to$ final / evolved singular vector

From $\mathbf{U^{T}LV=S}$,
$$\begin{cases} 
\mathbf{LV=US} \quad \Rightarrow \quad \mathbf{Lv}_{i}= \sigma_i\mathbf{u}_i\\
\mathbf{U^{T}L=SV^T} \quad \Rightarrow \quad \mathbf{L^{T}u}_{i}= \sigma_i\mathbf{v}_i
\end{cases}
$$

- initial singular vectors: $\mathbf{L}^T\mathbf{L}\mathbf{v}_i = \sigma_i^2 \mathbf{v}_i$
- final singular vectors: $\mathbf{L}\mathbf{L}^T\mathbf{u}_i = \sigma_i^2 \mathbf{u}_i$

perterbation = linear combination of singular vectors
$$\displaystyle\begin{align}
\mathbf{y}(t_0) &= \sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \mathbf{v}_i \\
\mathbf{y}(t_1) &= \sum_{i=1}^n \langle \mathbf{y}_1, \mathbf{u}_i \rangle \mathbf{u}_i
\end{align}$$

#### step 2. $\sigma_i$ are singular values representing growth factors.
$$\displaystyle\begin{align}
\Rightarrow \mathbf{y}(t_1) &= \mathbf{L}(t_0, t_1)\mathbf{y}(t_0) \\
&= \mathbf{L}(t_0, t_1)\sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \mathbf{v}_i \\
&= \sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \mathbf{L}\mathbf{v}_i\\
&= \sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \sigma_i\mathbf{u}_{i} \quad (\because \mathbf{Lv}_{i}= \sigma_i\mathbf{u}_i)\\
\end{align}$$
Take inner product of above equation with $\mathbf{u}_i$
$$\displaystyle\begin{align}
\langle \mathbf{y}(t_1), \mathbf{u}_j \rangle &= \left\langle \sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \sigma_i\mathbf{u}_{i}, \mathbf{u}_j \right\rangle \\
&=\sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \sigma_i \langle \mathbf{u}_{i}, \mathbf{u}_j \rangle \quad (\because  \text{linearity of inner product})\\
&= \sum_{i=1}^n \langle \mathbf{y}_0, \mathbf{v}_i \rangle \sigma_i \delta_{ij}\\
&=\langle \mathbf{y}(t_0), \mathbf{v}_j \rangle \sigma_j
\end{align}$$
since $\langle \mathbf{u}_i, \mathbf{u}_j \rangle = \delta_{ij}$; Kronecher delta 
$$\delta_{ij} = \begin{cases} 1 & \text{if } i = j \\ 0 & \text{if } i \neq j \end{cases}$$
$\Rightarrow i = j$인 항만 남음

Similarly, $\langle \mathbf{y}(t_0), \mathbf{v}_j \rangle = \sigma_j\langle \mathbf{y}(t_1), \mathbf{u}_j \rangle$

$$\therefore \begin{cases}
\langle \mathbf{y}(t_1), \mathbf{u}_j \rangle = \langle \mathbf{y}(t_0), \mathbf{v}_j \rangle \sigma_j\\
\\
\langle \mathbf{y}(t_0), \mathbf{v}_j \rangle = \sigma_j\langle \mathbf{y}(t_1), \mathbf{u}_j \rangle
\end{cases}$$

#### Step 3. Spherical perturbations grow into ellipses.
def. Euclidean norm$$||\mathbf{y}||^2 = \mathbf{y}^T\mathbf{y} = \langle \mathbf{y}, \mathbf{y} \rangle$$

Consider pertrubations $\mathbf{y}(t_0)$ of size 1. Then 
$$\sum_{i=1}^n \frac{\langle \mathbf{y}(t), \mathbf{u}_i \rangle}{\sigma_i} = \sum_{i=1}^n \langle \mathbf{y}(t_0), \mathbf{v}_i \rangle = ||\mathbf{y}(t_0)||^2 = 1$$
Initial sphere of radius 1 $\to$ hyperellipsoid of semiaxes $\sigma_i$

- $\mathbf{v}_1$: first initial singular vector = optimal vector
  $\to$ direction in phase spaced of the perturbation that will attain max. growth $\sigma_1$ in the interval ($t_0, t_1$)

![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-27 12.48.11.excalidraw|700]]
#### Step 4. How to find the initial vectors $\mathbf{y}(t_0)$ that maximize the norm of $\mathbf{y}(t_1)$ at the final time; Optimization problem
##### constraint maximization
$$\begin{align} 
\max_{\mathbf{y}(t_0)} &\quad J(\mathbf{y}(t_0)) \\
\text{subject to} &\quad |\mathbf{y}(t_0)|^2 = 1 
\end{align}
$$
where $J(\mathbf{y}(t_0)) \equiv \|\mathbf{y}(t_1)\|^2 = [\mathbf{Ly}(t_0)]^T\mathbf{Ly}(t_0) = \langle\mathbf{L}^T\mathbf{Ly}(t_0), \mathbf{y}(t_0)\rangle$ [[eq 6.3.27|why?]]
$J$: objective function

##### Unconstrained maximization by Lagrange multiplier
Define a norm using other weight matrix $\mathbf{W}$ applied to $\mathbf{y}$.
$$\|\mathbf{y}(t_0)\|^2 = (\mathbf{Wy}(t_0))^T \mathbf{Wy}(t_0) = \mathbf{y}(t_0)^T \mathbf{W}^T \mathbf{Wy}(t_0) = 1$$
Then the size of the perturbation at the final time , $J(\mathbf{y}(t_0))$, is, by a projection operator at the end of the interval $\mathbf{P}$,
$$J(\mathbf{y}(t_0)) = [\mathbf{PLy}(t_0)]^T \mathbf{PLy}(t_0) = \mathbf{y}(t_0)^T\mathbf{L}^T\mathbf{P}^T \mathbf{PLy}(t_0)$$

##### gradient to minimize
Convert strong constraint maximization to unconstrained one with Lagrange multipliers.
$$\begin{align} 
\max_{\mathbf{y}(t_0)} &\quad K(\mathbf{y}(t_0))\\
&=J(\mathbf{y}(t_0))+\lambda[1-\mathbf{y}(t_0)^T \mathbf{W}^T \mathbf{Wy}(t_0)]\\
&=\mathbf{y}(t_0)^T\mathbf{L}^T\mathbf{P}^T \mathbf{PLy}(t_0)+\lambda[1-\mathbf{y}(t_0)^T \mathbf{W}^T \mathbf{Wy}(t_0)]
\end{align}$$
Compute gradient of $K$ w.r.t. the control variable $\mathbf{y}(t_0)$ and make it equal to zero.
$$\nabla_{\mathbf{y}(t_0)} K = \mathbf{L}^T\mathbf{P}^T\mathbf{PLy}(t_0) - \lambda\mathbf{W}^T\mathbf{Wy}(t_0) = 0$$
It is convenient, given the constraint, to change variables:
$$
\mathbf{Wy}(t_0) = \hat{\mathbf{y}}(t_0) \quad \text{or} \quad \mathbf{y}(t_0) = \mathbf{W}^{-1}\hat{\mathbf{y}}(t_0)
$$$$\begin{align}
\|\mathbf{y}(t_0)\|^2 &= (\mathbf{Wy}(t_0))^T \mathbf{Wy}(t_0) \\
&= \hat{\mathbf{y}}^T(t_0)\hat{\mathbf{y}}(t_0)\\
&= 1\\
\end{align}$$
Then, the gradient condition becomes
$$\begin{align}
\mathbf{L}^T\mathbf{P}^T\mathbf{PLy}(t_0) &= \lambda\mathbf{W}^T\mathbf{Wy}(t_0)\\
\mathbf{L}^T\mathbf{P}^T\mathbf{PLW}^{-1}\hat{\mathbf{y}}(t_0) &= \lambda\mathbf{W}^T\hat{\mathbf{y}}(t_0)\\
(\mathbf{W}^{-1})^T\mathbf{L}^T\mathbf{P}^T\mathbf{PLW}^{-1}\hat{\mathbf{y}}(t_0) &= \lambda\hat{\mathbf{y}}(t_0)
\end{align}
$$
subject to the constraint
$$\hat{\mathbf{y}}^T(t_0)\hat{\mathbf{y}}(t_0) = 1$$
##### Result
$\hat{\mathbf{y}}(t_0)$: eigenvectors of the matrix $(\mathbf{W}^{-1})^T\mathbf{L}^T\mathbf{P}^T\mathbf{PLW}^{-1}$ 
$\lambda_i$: Lagrange multipliers / eigenvalues of $\hat{\mathbf{y}}(t_0)$ / $\lambda_i = \sigma_i^2$
weight matrix of initial norm, $W$,과 a projection operator, $\mathbf{P}$,를 general & arbitrary하게 골라도 된다.

### 6.3.3 | Lyapunov vectors

### 6.3.4 | Simple examples of singular vectors and eignenvectors

## 6.4 | Ensemble forecasting: early studies
instability로 인한 error growth는 ineveitably lead to a total loss of skill in the weather forecasts after a finite forecast length.
> Lorenz estimated this limit of weather predictability as about two weeks.

![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-20 15.54.43.excalidraw|700]]

### 6.4.1 | Stochastic-dynamic forecasting

### 6.4.2 | Monte Carlo forecasting
**Symbols)**
$\mathbf{u}_0$ : true state of the atmosphere
$\hat{\mathbf{u}}$ : unbiased estimate of $\mathbf{u}_0 \rightarrow \langle\hat{u}\rangle = 0$ 

**Background)** 
climatological forecast error covariance
$$\begin{align*}
\langle (0-\mathbf{u}_0)(0-\mathbf{u}_0)^T\rangle &= \langle\mathbf{u}_0\mathbf{u}_0^T\rangle\\ &=\mathbf{U}\end{align*}$$
> Since forecasts lose their skill at longer lead times, and individual forecasts eventually are further away from the verification thatn the climatology, <font color="#00e676">optimal estimation of the verification is equivalent to tempering</font> (i.e., hedging the forecast towards climatology).

$\Rightarrow$ forecast error covariance를 최대한 $\mathbf{U}$에 가깝게 만들어보자

##### Case 1) single forecast error covariance
$$\begin{align}
\langle (\hat{\mathbf{u}}-\mathbf{u}_0)(\hat{\mathbf{u}}-\mathbf{u}_0)^T \rangle &= \langle (\hat{\mathbf{u}}\hat{\mathbf{u}}^T + \mathbf{u}_0\mathbf{u}_0^T - \hat{\mathbf{u}}\mathbf{u}_0^T - \mathbf{u}_0\hat{\mathbf{u}}^T) \rangle \\
&= \langle \hat{\mathbf{u}}\hat{\mathbf{u}}^T \rangle + \langle \mathbf{u}_0\mathbf{u}_0^T \rangle - \langle \hat{\mathbf{u}}\mathbf{u}_0^T \rangle - \langle \mathbf{u}_0\hat{\mathbf{u}}^T \rangle \\
&\xrightarrow{t \to \infty} \langle \hat{\mathbf{u}}\hat{\mathbf{u}}^T \rangle + \langle \mathbf{u}_0\mathbf{u}_0^T \rangle - 0 - 0 \quad (\because\text{decorrelation between }\hat{\mathbf{u}} \text{ \& }\mathbf{u}_0)\\
&= \mathbf{U} + \mathbf{U}\quad (\because\text{unbiased model }\rightarrow \mathbb{E}[\hat{\mathbf{u}}\hat{\mathbf{u}}^T ]\simeq \mathbb{E}[\mathbf{u}_0\mathbf{u}_0^T])\\
&= 2\mathbf{U}
\end{align}$$
##### Case 2) regression forecast
$$\begin{gathered}
\hat{u}_0 = \hat{u}A \\
\textrm{s.t.} \quad \min \varepsilon^T\varepsilon = \min (\langle (u_0-\hat{u}A)^T(u_0-\hat{u}A) \rangle)
\end{gathered}$$
where $A$: const. reg. coeff. matrix 
Let $y = XA \Rightarrow \varepsilon = y - XA$.
$$ \varepsilon^T\varepsilon = (y-XA)^T(y-XA) $$ $$\begin{align}
\frac{\partial \varepsilon^T\varepsilon}{\partial A} &= \frac{\partial}{\partial A} (y-XA)^T(y-XA)\\
&= -2X^T(y-XA)\\ &= 0 \\ 
\Rightarrow 2X^Ty &= 2X^TXA \end{align}$$ $$ \therefore A = (X^TX)^{-1}X^Ty = X^\dagger y $$$$\Rightarrow A = \langle \hat{u}^T\hat{u} \rangle^{-1} \langle \hat{u}^Tu_0 \rangle \quad (\because u_0 \sim y, \hat{u} \sim X)$$but matrix size $\uparrow$ $\Rightarrow$ computational cost $\uparrow$

##### Case 3) ensemble forecast error covariance
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

### 6.4.3 | lagged average forecasting
$t = -\tau, -2\tau, \cdots, -(N-1)\tau$ 로 init time을 잡아서 ensemble 생성
$\rightarrow$ automatically generated forecast error를 perturbation으로 사용
$\quad$ !randomly chosen error, but contains "errors of the day"
	$\rightarrow$ apparent predicting forecast skills (? 이게 뭐노)
$\rightarrow$ forecast에 weight w.r.t. age
![[Pasted image 20240822165733.png]]
lagged avg forecasting이 Monte Carlo보다 조금 더 낫더라.

**adventages)**
- simple to perform
- no need to generate perturbations
- errors of the day (Lyapunov vectors) $\subset$ perturbations
**disadventages)**
- large하게 쓰면 excessively old forecasts도 사용해야 함
- weight 조절 제대로 못하면 result가 older forecasts한테 tainted 수 있음

scaled lagged average forecasting
:= 같은 init time에서 error에 $\displaystyle\pm\frac{1}{j}$ 곱해
**adventages)**
- 다른 init time에 perturbation scale이 거의 비슷
- ??? $\rightarrow$ Laypunov exponent에 sign 부여해서 better
- regional scale에서 easy implement $\because$ boundary condition을 generate

## 6.5 | Operational ensemble forecasting Methods

#### Elements
1) *control* forecast, $\mathbf{C}$
	analysis에서 시작
	= best estimate of the true initial state of the atmosphere에서 시작
1) two *perturbed* ensemble forecasts, $\mathbf{P}^+, \mathbf{P}^-$
	*control* $\pm$ perturbation
3) *ensemble average*, $\mathbf{A}$
4) *true evolution* of the atmosphere, $\mathbf{T}$
![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-22 16.59.37.excalidraw|700]]

(a) $\mathbf{T}$랑 멀면 slow error growth, 가까우면 fast $\rightarrow$ $\mathbf{A}$랑 $\mathbf{T}$랑 가까워
(b) $\mathbf{T}$랑 model 결과랑 서로 다른 방향으로 나아감 $\rightarrow \exists$ ststematic error,  $\exists$ deficiency in the forecasting system

#### Goals of ensemble forecasting
1. improve the forecast by ensemble averaging
	uncertain한 members를 filter out해서 $\mathbf{A}$을 $\mathbf{T}$에 가깝게
	perturbation이 nonlinear하게 증가해야 filtering 가능
	
2. provide an indication of the reliability of the forecast
	ensemble spread $\leftrightarrow$ forecast error 
	forecast agreement $\leftrightarrow$ forecast skill
	예측의 근거를 만들어 준다
3. provide a quantitative basis for probabilistic forecasting
   확률 제공해 줌

#### Perturbations
어떻게 generate해서 amplitude를 어느 정도로 잡을 것인가
1. Monte Carlo forecasting
	value: random
	amplitude: realistic, estimated analysis uncertainty랑 compatible하게
	> random initial perturbations do not grow as fast as the real analysis errors, even if they are in quasi-geostrophic balance.
2. breeding & singular vector 등 
	underlying atm flow를 반영한 perturbation grow error를 사용

### 6.5.1 | breeding
evolving underlying dynamics를 알고 있는 perturbation을 주면 error grow faster
$\rightarrow$ breeding := nonlinear integration 2개 돌려 나온 차이로부터 approx. linear perturbation을 obtain하는 방법
![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-25 16.26.01.excalidraw|700]]
1) introduce a random initial perturbation (a.k.a. random seed) w/ a given init size. 1번만
2) control (!perturbed) & perturbed init cond + the same nonlinear model로 integration (적분)
3) fixed time interval마다 $$
\text{bred vector} = (\text{perturbed forecast}) - (\text{control forecast})$$$$\text{new analysis | model state} \leftarrow \dfrac{\text{bred vector}}{2} + \text{analysis | model state}$$
4) transient 3~4일 지나면 fast growth rate 가진 bred vectors가 breeding cycle에 생긴다 

breeding ~ analysis cycle
![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-25 16.58.49.excalidraw|700]]

competing bred vectors: $\exists$ 2개 이상의 same shape, different signs vectors originated from different random seeds

empirically, finite amplitude bred vectors $\not\to$ single leading bred vector

사례)
![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-25 17.16.44.excalidraw|700]]

collapse of the perturbations into fewer dimensions
$\simeq$ [[local bred vector dimension]]이 smaller subspace로 align
$\Rightarrow$ underlying atm flow의 regional dominant instability를 표현하는 dominant Lyapunov vectors가 locally grow한다

#### @Toth and Kalnay, 1993
>suggested that the use of nonlinear perturbations in breeding filter out Lyapunov vectors related to fast-growing but energetically irrelevant instabilities. like convection.

case 1) baroclinic modes
initial amplitude $\leq$ estimated analysis error
	(i.e., 1-15m for 500 hPa geopotential height)
Bred vectors가 strong baroclinic areas에서 developed faster 
$\to$ horizontal scale $\simeq$ short baroclinic waves
& hemispherical growth rate = ~1.5/day $\simeq$ estimated analysis errors

case 2) convective modes
smaller initial amplitude $<<$ estimated analysis error
	(≤10cm)
bred vector $\mapsto$ convective instabilities
growth rate > 5/day; faster than baroclinic instabilities
$\rightarrow$ analysis error range보다 작은 amplitude에서 saturated됨

![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-25 19.07.26.excalidraw|700]]

#### @Lorenz, 1996
- Low-order models
    - large amplitude, slow-growing modes
    - small amplitudes, fast-growing modes
- Results
    - finite amplitudes → Lyapunov vectors of slow-growing modes
    - very small amplitudes → Lyapunov vectors of fast system

##### Implications for complex systems (e.g., Atmosphere)
- Breeding may be more appropriate than Lyapunov vectors
- Lyapunov vectors in full atmospheric models → associated with Brownian motion (fastest but irrelevant instabilities)

##### Potential applications
- Seasonal and interannual forecasting (coupled ocean-atmosphere systems):
    - Could capture slower-growing, high-energy ENSO instabilities
    - Eliminates irrelevant weather perturbation details through nonlinear saturation

##### Targeted observations
> If the ensemble indicates a region of large uncertainty in the short-term forecasts, it should be possible to find the area that originated this region of uncertainty in time to launch new observations for the next analysis cycle, and thus decrease significantly the forecast error.

- observations 필요한 지역을 찾는 방법
	- adjoint sensitivity approach
	- singular vectors
	- quasiinverse of the tangent linear model
	- ensemble-based singular value decomposition

### 6.5.2 | singular vectors
1. singular vector를 16개 선택해야 함
	앞 4개는 고정
	그 다음부터는 energy의 50%가 기선택된 vectors의 영역 밖에 있는 애들로
2. orthogonal rotation in phase space & final rescaling
	to generate perturbations that have the same globally averaged energy as the singular vectors but smaller local maxima and more uniform spatial distribution.
1. create 33 initial conditions
	$$\begin{align}
33 &= 16 \times 2 + 1\\
&= \text{16 singular vectors} \times \text{added or substracted} + \text{control}
\end{align}$$

1997에 ensemble 수를 50개로 늘렸는데,
> This increase in resolution had a major positive effect on the quality of the ECMWFensemble forecasting system.

### 6.5.3 | Ensembles based on multiple data assimilation
init cond 만들기 위한 data assimilation system ensemble
observation + random errors & physical parameterization에 diffrent param.

cost: breeding = 0 < singular vectors $\simeq$ ensemble
performance: singular vectors || breeding < ensemble

### 6.5.4 | Multisystem ensemble approach
ideally, 
init perturbation 
= statistical uncertainty in the init cond 
= leading eigenvectors of the analysis error covariance
$\hookleftarrow$  model imperfections / uncertainty abt model deficiencies

여러 센터의 operational global forecasts' ensemble mean이 more skillful하다 
shorter-range, regional model ensemble도 마찬가지
거기에 systematic error correction by regression by regression하면 더 좋아지더라; a.k.a superensemble

init analysis에 perturbation을 더하지 않고 best init cond + best models 해서 뽑아냄 
$\Rightarrow$ poor person's approach
비용 효율적

## 6.6 | Growth rate of errors and the limit of predictability in mid-latitudes and in the tropics
$$\displaystyle \frac{d\varepsilon}{dt} = a\varepsilon(1 - \varepsilon)$$
$\varepsilon$: rms avg forecast error; $\epsilon \to 1$
$a$: growth rate
$\varepsilon_0$: init error
$$\begin{align}
\frac{d\varepsilon}{\varepsilon(1 - \varepsilon)} &= adt \\
\int \frac{d\varepsilon}{\varepsilon(1 - \varepsilon)} &= \int adt \\
\int (\frac{1}{\varepsilon} + \frac{1}{1-\varepsilon}) d\varepsilon &= at + C\\ 
\ln\lvert\frac{\varepsilon}{1-\varepsilon}\rvert &= at + C \\
\frac{\varepsilon}{1-\varepsilon} &= Ke^{at}, \quad K = e^C
\end{align}$$
$$\begin{align} 
\varepsilon &= Ke^{at}(1-\varepsilon) \\ 
\varepsilon(1 + Ke^{at}) &= Ke^{at} \\ 
\varepsilon &= \frac{Ke^{at}}{1 + Ke^{at}} 
\end{align}$$
initial condition:  $\varepsilon(0) = \varepsilon_0$
$$\displaystyle  \begin{align}
\varepsilon_0 &= \frac{K}{1 + K} \\
K &= \frac{\varepsilon_0}{1-\varepsilon_0} \end{align} $$
$$\displaystyle \begin{align} 
\therefore \varepsilon(t) &= \frac{\frac{\varepsilon_0}{1-\varepsilon_0}e^{at}}{1 + \frac{\varepsilon_0}{1-\varepsilon_0}e^{at}} \\ 
&= \frac{\varepsilon_0e^{at}}{1 + \varepsilon_0(e^{at} - 1)} 
\end{align} $$
init error, $\varepsilon$ = 0.1, 0.01, $a$ = 0.35/day일 때 $\varepsilon$ doubling time은 about 2 days

> The upper limit for the best initial error achievable from data assimilation can be reasonably estimated to be no less than 1%. This is because, as pointed out by Lorenz, even if the observing system was essentially perfect at synoptic scales, errors in much smaller, unresolved scales would grow very fast and trough nonlinear interactions quickly introduce finite errors in the initial synoptic scales of the model.

2주면 small error가 saturated되어서 mid-latitude 예측 lost
![[Atmospheric Modeling, Data Assimilation and Predictability 2024-08-30 16.02.58.excalidraw|700]]

하지만 atmospheric instabilities of the day에 따라 skillful period가 달라지더라
그래서 ensemble 돌려서 variability를 줘야 하는거야

instabilities time scale $\propto$ spatial scale
$\Rightarrow$ small-scale instability grow faster than larger scale
$\Rightarrow$ mesoscale phenomena, mesoscale convective systems, tornadoes는 예측하기 어렵다. 하지만 larger scale에서 forced or organized된 activity라면 예측성 향상 가능
\+ unforced convective activity여도 하루 이틀 정도는 예측 가능하다

> The dynamics of mid-latitudes is dominated by synoptic-scale baroclinic instabilities, and the limit of deterministic weather predictability is a reflection of their baroclinic instability rates of growth.

반면 tropics는 barotropic & convective instability가 더 dominant
convective precip이 mid-lat에서는 synoptic wave에 영향 없지만 tropic에서는 easterly에 영향 많이 줘.

> Moreover, global atmospheric models are less accurate in the tropics, because their ability to parameterize realistically the subgrid scale processes such as convection, which are dominant in tropics, is not as good as the numerical representation of the resolved baroclinic dynamics, which is dominant in the extratropics.

random error growth rate in an imperfect model
: operational forecast error + logistic equation
$$\frac{dv}{dt} = (bv+s)(1-v)$$
$v$: systematic random error variancez
$b$: growth rate for small error variance $\because$ instability
$s$: external random error variance $\because$ model deficiency


## 6.7 | The role of the oceans and land in monthly, seasonal, and interannual predictability


## 6.8 | Decadal variability and climate change

