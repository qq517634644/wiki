```
# 预测功能的配置文件 （cpbase/cp)

# ---------------------------------------------
# 预测执行的命令行
cpEngineCmd = java -Xbootclasspath/a:d://aims//cpEng//weka.jar -jar d://aims//cpEng//cpEng.jar
# 予測エンジン用の臨時データフォルダー
cpEngTmpPath = d://aims//cpEngTmp
# 予測モデル保存するベースパス
cpModelPath = d://aims//cpEngModel
# 日単位予測サポートするか
cpDaySupport = true
# 営業店単位予測サポートするか
cpSiteSupport = false
# 営業店単位予測結果によって補正するか
cpSiteFix = false
# 预测模式: 1=模式1(存取款分别预测), 2=模式2(直接预测需求量)
predictMode = 2
# 时间单位 算法
algorithmHour=BAGGING
# 天单位 算法:SMO_REG/BAGGING
algorithmDay=BAGGING
# 天单位算法中以历史交易记录作为参数的条数 (SMO_REG算法采用30天输入),小时单位暂不支持
hisRecCnt4AlgoParamDay = 0
# 算法最少数据天数要求
minTransRecDay = 60
# 超前预测多少天
maxDay2Predict = 10
# 最多币种数
maxCashNum = 5

# 予測精度分析ポートするか
predictAccuracy = false

# ルート生成アルゴリズム(半天：RoutePlanCwex, 半天分组：RoutePlanCwex2, 全天分组：RoutePlanCwap)
routePlanAlgo = cn.hitachi.rt.algo.RoutePlanCwex

# 提取的JNL文件导入成功之后，备份到此目录下（如果设成null或空，则删除服务器本地的文件）
backupDir4JNL= D://aims//EJNLBak

# 予測用マージしたデータのＩＯ処理のフォルダー
cpDataPath=D://aims//metaCSVData

# ---------------------------------------------
# データの最大保有期間(単位: ヶ月) (36ヶ月=3年)
dataKeepMonths=36
# データ削除のタイマーの間隔(単位: 秒)(86400秒=24*60*60=24時間)
timer4DelOldData=1800
# データ削除の延期起動時間(単位: 秒)(30秒)
timeDelay4DelOldData=30
# データ削除の起動時間(hh:mm:ss),空なら、起動しない
startTime4DelOldData=00:00:00
# データ削除の起動終了時間(hh:mm:ss),この時間越えると、チェックしない；空なら、制限しない
endTime4DelOldData=08:00:00

# ---------------------------------------------
# 自動予測 (タイマー制御はＸＭＬに設定）
# 自動予測の起動時間(hh:mm:ss),空なら、起動しない
startTime4Predict=02:00:00
# 自動予測の起動終了時間(hh:mm:ss),この時間越えると、チェックしない；空なら、制限しない
endTime4Predict=08:00:00

# ---------------------------------------------
# 交換データインポート
# 交換データインポートのタイマーの間隔(単位: 秒)(30分), ０なら、起動しない
timer4ImpCsvData = 1800
# 交換データインポートの延期起動時間(単位: 秒)(30秒)
timeDelay4ImpCsvData = 30


# ---------------------------------------------
# 默认计划的各阶段截止时间
# 时间格式：n,hh:mm:ss
#     其中n表示偏移的天数
# +++++++  上午
# 默认上午计划的现金准备截止时间
defCashInTimeAm  = -1,18:00:00
# 默认上午计划的CIT移交的截止时间
defToCITTimeAm   = 0,08:30:00
# 默认上午计划的加钞截止时间
defAtmFillTimeAm = 0,11:30:00
# 默认上午计划的从CIT回收的截止时间
defFromCITTimeAm = 0,12:30:00
# 默认上午计划的回收现金清分截止时间
defCashOutTimeAm = 0,15:30:00
// +++++++  下午
# 默认下午计划的现金准备截止时间
defCashInTimePm  = 0,12:30:00
# 默认下午计划的CIT移交的截止时间
defToCITTimePm   = 0,13:30:00
# 默认下午计划的加钞截止时间
defAtmFillTimePm = 0,16:30:00
# 默认下午计划的从CIT回收的截止时间
defFromCITTimePm = 0,17:30:00
# 默认下午计划的回收现金清分截止时间
defCashOutTimePm = 1,10:30:00

# ---------------------------------------------
# 交易记录分析控制
# 平均均衡坚持天数的超级限界值（例：平均均衡坚持天数超过此数算超级均衡型）
transAnaBalanceDaysEx = 30
# 平均均衡坚持天数的限界值（例：平均均衡坚持天数超过此数算均衡型）
transAnaBalanceDays = 15
# 平均存取款数额判断的限界值（例：平均日消耗量超过此数算取款型）
transAnaVol2Fix = 10000
# 平均存取款数额判断的超级限界值（例：平均日消耗量超过此数算超级取款型）
transAnaVol2FixEx = 200000
```