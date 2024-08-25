# Definition
$$\psi(\sigma_1, \ldots, \sigma_k) = (\sum_{i=1}^k \sigma_i)^2 / \sum_{i=1}^k \sigma_i^2$$
- $\sigma_i$: singular values; correspond to $k$ bred vectors in a region of about $10^6$ m by $10^6$ m
$\Rightarrow$ effective local dimensionality를 define

# Example
bred vector 5개 중
	4개가 one direction으로 lie하고
	1개가 second direction으로 lie한다면
	$\psi(\sqrt{4}, 1, 0, 0, 0) = 1.8$
    - 이게 2보다 작은 이유는 one direction이 더 dominant하기 때문임
    - 이 calculation이 original data를 represent하는 거임

Patil et al., 2001