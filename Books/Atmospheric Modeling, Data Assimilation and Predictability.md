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
2. breeding & singular vector
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

##### Implications for Complex Systems (e.g., Atmosphere)

- Breeding may be more appropriate than Lyapunov vectors
- Lyapunov vectors in full atmospheric models → associated with Brownian motion (fastest but irrelevant instabilities)

##### Potential Applications
- Seasonal and interannual forecasting (coupled ocean-atmosphere systems):
    - Could capture slower-growing, high-energy ENSO instabilities
    - Eliminates irrelevant weather perturbation details through nonlinear saturation

### 6.5.2 | singular vectors