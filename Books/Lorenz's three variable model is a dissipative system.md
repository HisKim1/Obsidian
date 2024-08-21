---
{}
---

# proof
### Divergence of the flow
$$\dfrac{\partial \dot{x}}{\partial x} + \dfrac{\partial \dot{y}}{\partial y} + \dfrac{\partial \dot{z}}{\partial z} = -(\sigma + b + 1)$$

divergence와 volume change rate의 관계: $$\frac{1}{V}\frac{dV}{dt} = \nabla \cdot \vec{v} = \dfrac{\partial \dot{x}}{\partial x} + \dfrac{\partial \dot{y}}{\partial y} + \dfrac{\partial \dot{z}}{\partial z}$$ $$\frac{1}{V}\frac{dV}{dt} = -(\sigma + b + 1)$$
$$\ln|V| = -(\sigma + b + 1)t + C$$
$$V = e^{-(\sigma + b + 1)t + C} = Ae^{-(\sigma + b + 1)t}$$where $A = e^C$
$$\therefore V(t) = V_0e^{-(\sigma + b + 1)t}\\
\Rightarrow \exists \text{ bounded globally attracting set of zero volume}$$
