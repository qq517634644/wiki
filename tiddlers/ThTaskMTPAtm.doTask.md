# 参数

# 返回
- `boolean` 任务执行情况

# 方法详情
1. 任务排他（时效内幂等）
2. 开始任务并更新任务状态 `cpMngAtmHour.startTask()`
3. 开始训练模型 `(service, cpMngEntity)` -> [[CpMngAtmHour.trainModel]]
    1. 训练数据的时间范围
    2. 已训练的数据时间范围
    3. `delete from cp_trans_atm_prd where atmid=? and transtime>=?`
        - 删除模型训练数据时间以后的预测数据
				- [[CpTransAtmPrdEntity - cp_trans_atm_prd]]
    4. `update cp_mng_atm set predictedTime=? where atmid=?`
        - 更新预测时间
				- [[CpMngAtmEntity - cp_mng_atm]]
    5. `int cashValNum = CpMngTPUtil.getCashValNum(service, atmid)`
        - 按atmid取得对应的币种数
        - `select cashValNum from a_atm_status where id=:atmid`
    6. 机型为：存取款机（非循环机）时，或者指定预测模型为1时
        - 只能是存取款分开预测（CP_MODE_1）
    7. 其他模型2的预测
4. 训练模型成功？
    1. `processWork(iStepWork)` 更新任务进度
    2. `(service, cpMngEntity)` ->[[CpMngAtmHour.predict]] 预测模型
    3. 预测模型成功
        - `processWork(iStepWork)` 更新任务进度
4. 如果支持每日预测
    - ##TODO 支持   训练 预测 更新任务进度
5. 训练预测成功 评估模型
    - `(service, cpMngEntity)` -> [[CpMngTPUtilAtm.predictAccuracy]]
    > 分析每个 ATM 的每小时模型的预测精度 评估模型
    TODO
    
6. 更新任务进度
7. 更新表 `cp_mng_atm`

