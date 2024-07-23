---
site: https://www.nature.com/articles/ngeo2424
summary: stratosphere가 troposphere에 영향을 미치는 mechanism mainly w/ jet stream
keyword:
  - Stratosphere-Troposphere Coupling
  - Eddy Feedbacks
  - Brewer-Dobson Circulation
  - SSW
status:
  - WorkingOn
tags:
  - paper
datetime: 2015-05-18
where published:
  - Nature Geoscience
title: Stratospheric influence on tropospheric jet streams, storm tracks and surface weather
---
```ad-abstract
A powerful influence on the weather that we experience on the ground can be exerted by the stratosphere. This highly stratified layer of Earth's atmosphere is found 10 to 50 kilometres above the surface and therefore above the weather systems that develop in the troposphere, the lowest layer of the atmosphere. The troposphere is dynamically coupled to fluctuations in the speed of the circumpolar westerly jet that forms in the winter stratosphere: ==a strengthening circumpolar jet causes a poleward shift in the storm tracks and tropospheric jet stream, whereas a weakening jet causes a shift towards the equator. Following a weakening of the stratospheric jet, impacts on the surface weather include a higher likelihood of extremely low temperature over northern Europe and the eastern USA.== Eddy feedbacks in the troposphere amplify the surface impacts, but the mechanisms underlying these dynamics are not fully understood. The same dynamical relationships act at very different timescales, ranging from daily variations to longer-term climate trends, suggesting a single unifying mechanism across timescales. Ultimately, an improved understanding of the dynamical links between the stratosphere and troposphere is expected to lead to improved confidence in both long-range weather forecasts and climate change projections.
```

# Box 1  | Stratospheric downward influence
$$\bar{u}_t = \underbrace{\bar{v}^*(f-(a\cos\phi)^{-1}(\bar{u}\cos\phi)_\phi)}_{(i)} - \underbrace{\bar{w}^*\bar{u}_z}_{(ii)} + \underbrace{(\rho_0a\cos\phi)^{-1}\nabla \cdot \mathbf{F}}_{(iii)} + \underbrace{\bar{X}}_{(iv)}$$
(i) $\bar{v}^*(f-(a\cos\phi)^{-1}(\bar{u}\cos\phi)_\phi)$
- 잔류 평균 순환의 남북 성분을 나타냅니다.
- 위도에 따른 각운동량 수송을 설명합니다.

(ii) $-\bar{w}^*\bar{u}_z$
- 잔류 평균 순환의 연직 성분을 나타냅니다.
- 고도에 따른 운동량 수송을 설명합니다.

(iii) $(\rho_0a\cos\phi)^{-1}\nabla \cdot \mathbf{F}$
- Eliassen-Palm (EP) 플럭스의 발산을 나타냅니다.
- 파동에 의한 각운동량 전달을 quantify합니다.

(iv) $\bar{X}$
- 규모 중력파 등 모델에서 직접 해상되지 않는 다른 강제력들을 포함합니다.

- $\bar{u}$: 평균 동서 바람
- $\bar{v}^*, \bar{w}^*$: 잔류 평균 자오면 순환의 남북, 연직 성분
- $a$: 지구 반경
- $\phi$: 위도
- $z$: 고도
- $f$: 코리올리 매개변수
- $\rho_0$: 평균 대기 밀도
- $\mathbf{F}$: Eliassen-Palm 플럭스

아주 term 하나하나가 뭔지 모르겠다!
![[Pasted image 20240709144318.png]]

### 1 ~ 3
wave driving (momentum) $\downarrow \quad \rightarrow \quad \bar{ U_t }\uparrow$ w/ abnormal ==residual mean meridual circulation==

$\Rightarrow \quad$ polar cap의 mass $\downarrow \quad (\because$ fast mass redistribution$)$
$\Rightarrow \quad$ polar cap의 pressure $\downarrow$
$\Rightarrow \quad$ adiabatic cooling & air rising
$\Rightarrow \quad$ tropopause elevation $\uparrow$
$\Rightarrow \quad$ SLP $\downarrow$

compansate action으로 mid-, low latitude에서
air descent / warming / tropopause elevation $\downarrow$ / SLP $\uparrow$


### 4: tropospheric eddy feedbacks
### 5: poleward shift of tropospheric jet
은 ==eddy feedback이 뭔지 몰라서== 이해할 수 없음.

마지막 문단을 이해할 수 있길...

---
# Tropospheric response to stratosphere-troposphere Coupling

jet stream meridional vacillation(흔들림)인 N/SAM[^N/SAM] & NAO[^NAO]가 stratopheric Variability의 영향을 받는다
stratosphere의 variability = circumpolar jet의 strength variation, !latitude

stratospheric wind가 약해지면 tropospheric jet stream이 equatorward로, 강해지면 poleward로 
*(남북반구 동일)*

$\therefore$ strato.-tropo. coupling 
    = strato. circumpolar jet $\Leftrightarrow$  tropo. jet stream $\Leftrightarrow$ meridional P $\boldsymbol{\nabla}$ near the surface, $\forall$ timescales

Note that coupling $\perp\!\!\!\perp$ strato. jet speed change를 야기한 mechanism
	1) Monthly: nagative NAM
	2) Seasonal: late winter NAO
	3) Decadal: solar output & aerosols by volcano eruptions
	4) Centennial: GHG increase

남반구도 매한가지

$\therefore$ Strato. changes can actually affect the behaviour of the troposphere and surface climate

strato. wind anomalies가 tropo. jet stream의 lat.을 바꾸고, surface effect하여 zonal mean tropospheric response에 영향

N/SAM persistence $\uparrow$ & strato.-tropo. coupling이 tropo. eddies가 momentum을 저장해둔 장소에 영향을 줌

downward influence of strato. perturbation on tropo.는 tropo.의 response를 realizing에 중요
$\because$ strato. influence가 tropo.의 eddy & weather system의 생성과 전파에 영향

upward propagating planetary-scale wave가 스스로 circumpolar jet를 변화했을 가능성 있다
1) refracted more equatorward해서 
2) reflected back downward해서 

###### 결론
- tropo. response is qualitatively similar accross all timescales
- observed response can be realized w/ the additional contribution from tropospheric eddy momentum feedbacks
---
# Surface Weater Impacts

---
[^N/SAM]: [[Northern and Southern Annular Mode]]
[^NAO]: North Atlantic Oscilliation