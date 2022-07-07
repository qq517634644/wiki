# 现金预测管理表

|          名称           |      实体字段    | 表字段 |            备注        |
|-------------------------|-----------------|-------|-----------------------|
|ID                       |id               |       ||
|ATM 号码                 |atmid            |       |link=m_atm_inf.id|
|状态                     |cpSts            |       |0=权重中，1=执行中，6=完成，7=失败， 9=取消|
|交易数据开始日期          |startTime        |       |“系统管理数据的开始时间（cp_trans_atm和cp_trans_atm_day的开始日期）”|
|时间合并结束日期          |mergedTime       |       |cp_trans_atm结束日期后的第二天|
|合并结束日期              |mergedDay        |       |cp_trans_atm_day结束日期后的第二天|
|预测数据开始日期          |predictStartTime |       |cp_trans_atm_prd和cp_trans_atm_day_prd的开始日期|
|时间预测结束日期          |predictedTime    |       |cp_trans_atm_prd结束日期|
|预测结束日期              |predictedDay     |       |cp_trans_atm_day_prd结束日期|
|现有模型的数据开始时间     |modelTimeS       |       |训练的数据范围（基本上 = 开始时间）|
|时间单位模型的数据结束时间 |modelTimeE       |       |训练数据范围|
|每日模型的数据结束时间     |modelDayE        |       |训练数据范围|
|导出数据的时间            |exportedTime     |       |从银行系统输出管理|























































