1. **class** TaskConfig
2. **class** ModelConfig
   [[Properties]]  
3. **class** Graphcast
   3 key GNN
	1) grid2mesh_gnn: [[Encoder]]
	2) mesh_gnn: [[Processor]]
	3) mseh2grid_gnn: [[Decoder]]
	   
	\_init\_(name)\_graph로 GNN 초기화 in maybe_init
	-> \_run\_(name)\_gnn으로 실행 in \_\_call\_\_
	
	\_\_call\_\_
	: GNN 초기화 -> 3 GNNs 순차적 run -> 마지막 output을 \_grid\_node\_outputs\_to\_prediction으로 return
	
	\_grid\_node\_outputs\_to\_prediction
	: grid node output을 xarray.Dataset으로 변환
	
4. 