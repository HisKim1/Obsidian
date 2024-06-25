#### $M^r$
##### 제작 방법
$M^r \rightarrow M^{r+1}$ by splitting each triangular face into 4 small faces
regular icosahedron을 6회 나눠 (1 face $\rightarrow$ 4 faces)

$(V, E, F) : M^0 = (12, 30, 20) \rightarrow M^6 = (40962, 81920, 40960)$ [^Eular]

[^Euler]: Euler's Formula: V-E+F=2

##### Advantages
1. few message-passing steps으로 long-range interactions 가능
2. homo. spatial resolution over the globe
3. coarse-mesh nodes $\subset$ fine-mesh nodes 
   $\Rightarrow$ $\forall$ mesh edges $\mapsto$ finest-resolution mesh
   $\Rightarrow$ multi-scale set of meshes