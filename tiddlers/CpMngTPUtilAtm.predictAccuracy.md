# 简介
分析每个 ATM 的每小时模型的预测精度

# 参数
- service:`StdJdbcServiceI`
- cpMngEntity:[[CpMngAtmEntity - cp_mng_atm]]

# 返回
- `boolean` 预测精度分析

# 方法详情
1. 获取配置文件信息[[sysConfigCp.properties]] - `predictAccuracy` 是否允许精度预测 不允许则返回`true`
2. 获取已经训练模型`cpMngEntity`的`modelE`，`modelS`，`predictedTime`，`mergedDay`
3. 任一为空，表示没有新数据，则令`bNoDataHour` = `true`
4. `mergedDay` <= `modelE`，表示没有新数据，则令`bNoDataDay` = `true`
5. 获取配置文件信息[[sysConfigCp.properties]] - `cpDaySupport` 是否支持每日预测
6. 判断？ 返回 `false`
	- 并且
		- 当没有小时数据`bNoDataHour`==`true` 
		- 或者 
			- 没有日数据`bNoDataDay`==`true`
			- 不支持每日训练
7. 判断 ？ `cpDaySupport` = `false`
	- 支持每日训练且没有日数据
8. 创建模型预测准确率分析容器 [[CpAlgoAccuracyEntity - cp_algo_accuracy]] `acc`
9. 查询模型预测准确率 [[CpAlgoAccuracyEntity - cp_algo_accuracy]] 
	1. 更新容器的id
	2. 设置偏差（默认2万）
	3. 设置偏差率（默认20%）
10. 获取配置文件信息[[sysConfigCp.properties]] - `predictMode` 预测模式: 1=模式1(存取款分别预测), 2=模式2(直接预测需求量)
11. 连表查询预测数据`mapList`
	```sql
	select 
		DATE_FORMAT(t.transtime, '%Y-%m-%d') as transDay,
		sum(t.withdraw-t.deposit) as needT,
		t.enable as enableT,
		sum(p.demand) as needP,
		sum(pd.demand) as needPD
	from
		cp_trans_atm t,
		cp_trans_atm_prd p
	left join cp_trans_atm_day_prd pd 
	on
		pd.atmid = p.atmid
		and pd.transtime = p.transtime
	where 
		t.atmid = p.atmid
		and t.atmid = '10000001'
		and t.transtime = p.transtime
		and t.transtime> '2020-12-31 16:00:00.0'
		and t.enable = '1'
	group by
		transDay
	order by
		transDay
	```
12. 判断查询出具为空 返回`false`
13. 循环`mapList`
	1. 记录中获取`needP` `needPD` `needT`
	2. 业务处理
14. 循环都被跳过 说明没有交易记录 返回`false`
15. 容器`acc`更新字段
16. 更新数据库 `acc` -> [[CpAlgoAccuracyEntity - cp_algo_accuracy]]