# 简介
预测引擎接口包装处理

# 参数
- modelFileName:String 模型文件存放路径

# 返回
- `List<Integer>` 预测结果

## 方法详情
1. 获取各种文件路径
2. 结果文件存在->删掉
3. 获取配置文件信息[[sysConfigCp.properties]] - `cpEngineCmd` (执行命令行)
4. 执行命令 `$cpEngineCmd predict $paramFile` 同步等待执行完成
5. 结果文件存在
	1. 读取结果文件
	2. 结果文件包装成List 返回
