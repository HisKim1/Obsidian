#### $v_i^M \in \mathcal{V}^M$

| Refinement, $M$ | Num Nodes, $V$ | Num Faces, $F$ | Num Edges, $E$ | Num Multilevel Edges, $E_{\text{multilevel}}$ |
| --------------- | -------------- | -------------- | -------------- | --------------------------------------------- |
| 0               | 12             | 20             | 60             | 60                                            |
| 1               | 42             | 80             | 240            | 300                                           |
| 2               | 162            | 320            | 960            | 1,260                                         |
| 3               | 642            | 1,280          | 3,840          | 5,100                                         |
| 4               | 2,562          | 5,120          | 15,360         | 20,460                                        |
| 5               | 10,242         | 20,480         | 61,440         | 81,900                                        |
| 6               | 40,962         | 81,920         | 245,760        | 327,660                                       |
Mesh edge는 bidirectional $\Rightarrow$ edge는 uni-로 count해서 doubled

$$V^{M+1} = V^M + \frac{1}{2}E^M$$
$$E^{M+1}_{\text{multilevel}} = E^{M}_{\text{multilevel}} + E^{M + 1}$$