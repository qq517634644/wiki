# 参数
- `service`:`StdJdbcServiceI`
- `cpMngEntity`:  [[CpMngAtmEntity - cp_mng_atm]]

# 返回
- `boolean`     是否预测完成

# 方法详情
1. 获取已经训练模型`cpMngEntity`的`modelE`和`modelS`
2. 任一时间为空 则返回`false`(没有模型)

3. 获取配置文件信息[[sysConfigCp.properties]]-maxDay2Predict
4. 判断`predictedTime`
	- 为空：`predictstarttime` = `calendar` = `modelE`
	- 否则：`calendar` = `predictedTime` + 1D
5. `start` = `calendar`; `end` = `reqPredicttimee`
6. 判断end
	- 为空： `end` = `calendar` + (`maxDay2Predict`-1)D
7. 判断`end<=start`
	- 返回`true`(已经预测过了)

8. 获取币种 `cashValNum`
9. 判断 存取款机(非循环机) 或者指定预测模型为1时
	- [[CpMngAtmHour.predict1]] - (`service`,`cpMngEntity`,`start`,`end`,`cashValNum`)
	- 否则：[[CpMngAtmHour.predict2]] - (`service`,`cpMngEntity`,`start`,`end`,`cashValNum`)
	
