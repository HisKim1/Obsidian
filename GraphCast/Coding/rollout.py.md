chunked_prediction_generator가 각 예측을 생성해주면 chunked_prediction가 그걸 이어붙여서 긴 시간 범위 예측을 만든다

나머지 2개 함수는 generator에서 쓰려고 만든 겨

```python
predictions = rollout.chunked_prediction(
	# preditorFn
    run_forward_jitted,
	# random key
    rng=jax.random.PRNGKey(0),
    
    inputs=eval_inputs,
	# equispaced in time 
	# -> 그래서 그냥 truth에 nan 곱해서 형태만 남긴 듯
    targets_template=eval_targets * np.nan,
	
    forcings=eval_forcings
)
```

#Question 
```ad-question
predictorFn은 뭔가. 
-> 실행을 하는 protocol
```
