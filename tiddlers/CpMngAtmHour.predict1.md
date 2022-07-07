# 简介
- 现金预测模型1 
- 适用于存取款机（非循环机）预测
- 标识 CP_MODE_1
# 参数
- service:StdJdbcServiceI 提供基本的JDBC查询
- cpMngEntity:[[CpMngEntity - cp_mng_atm]]
- start:Date
- end:Date
- cashValNum:int
# 返回
- boolean 是否预测成功
# 方法详情
1. 获取配置文件信息[[sysConfigCp.properties]] - [[algorithmHour - BAGGING]] 算法
2. 获取参数信息 [[CpParamTypeEntity - cp_param_type]] -> CpMngParams
3. 获取配置文件信息[[sysConfigCp.properties]] - cpModelPath 模型存放路径
4. 初始化需要预测的存取款容器 List
5. 根据币种数量循环（存取款分开）
	1. 获取模型文件的路径 -> sFileModelCwd
	2. 准备attr数据 CpMngAtmHour.makeAttrBuf4Predict
	3. 生成文件目录准备写入数据流
	4. 数据流为空，返回false
	5. 写入数据
	6. 开始预测 (sFileModelCwd) -> [[CpEngIF.predict]] -> (预测结果 predWithdraw)
		- 存取款极其类似，不再赘述
	7. 存取款的预测结果 
		- 有一个为空 返回false
		- 数量不一致 或者不是24的倍数 返回false
	8. 将预测结果存入容器
	9. 事务处理
		1. 将预测结果写入数据库 [[CpTransAtmPrdEntity - cp_trans_atm_prd]]
		2. 更新管理表 [[CpMngEntity - cp_mng_atm]] (predictstarttime?null = start, predictedtime = end)
	10. 返回 true