# 简介
- 现金预测模型2 
- 适用于除存取款机（非循环机）之外的机器预测
- 标识 `CP_MODE_2`
# 参数
{{CpMngAtmHour-Params_of_Method-predict1,predict2}}
# 返回
- boolean 是否预测成功
# 方法详情
1. 获取配置文件信息[[sysConfigCp.properties]] - [[algorithmHour - BAGGING]] 算法
2. 获取参数信息 [[CpParamTypeEntity - cp_param_type]] -> CpMngParams
3. 获取配置文件信息[[sysConfigCp.properties]] - `cpModelPath` 模型存放路径
4. 初始化需要预测的存取款容器 `List` - `predDemandList`
5. 根据币种数量循环（存取款分开）
	1. 获取模型文件的路径 -> `sFileModelDemand`
	2. 准备attr数据 (`cpMngParams`, `atmid`, `start`, `end`) -> `CpMngAtmHour.makeAttrBuf4Predict`
	3. 生成文件目录准备写入数据流 `CpEngIF`
	4. 数据流为空，返回`false`
	5. 写入数据
	6. 开始预测 (`sFileModelCwd`)-> [[CpEngIF.predict]] -> (预测结果 `predWithdraw`)
	7. 存取款的预测结果 
		- 有一个为空 返回`false`
		- 数量不一致 或者不是24的倍数 返回`false`
	8. 将预测结果存入容器
	9. 事务处理
		1. 将预测结果写入数据库 [[CpTransAtmPrdEntity - cp_trans_atm_prd]]
		2. 更新管理表 [[CpMngAtmEntity - cp_mng_atm]] (`predictstarttime`?`null` = `start`, `predictedtime` = `end`)
	10. 返回 `true`