# 项目介绍
## 帕金森病患者可穿戴设备研制

### 可穿戴设备介绍
手腕、左脚、右脚的传感器：加速度计+陀螺仪
![Device](https://github.com/leigaoyi/pd_classifier/blob/master/device.PNG)

### 加速度计数据步态识别实验


数据分析：

从视频中可以观察到，帕金森病人因身体健康需要，在座椅上穿戴好设备后，才开始采集设备。而
正常人采集的数据，视频中是行走中的数据。所以对数据清洗时，删除掉病人行走前的采集信号，只对
行走中的信号进行步态识别。

项目采集数据包括九位病人志愿者和九位健康志愿者的行走采集数据，和对应的收集拍摄短视频（已脱敏）。本实验到观察
手腕处的加速度计采集的信号，在行走测试中，最稳定。这可能是因为左脚、右脚行走中，两脚交替迈出，导致单只脚的传感器
信号不连续。而手腕处的传感器，能在病人和健康人行走中，持续的采集到手臂摆动信号。所以本实验选择手腕处传感器采集的信号，
作为步态识别的对象。

本实验每2s（600次长度）截取手腕的加速度计数据，整理出健康志愿者和病人志愿者的步态数据集。然后设计DeepConvLSTM模型，进行
步态辨识实验。数据文件存储在data中，分别是health.npy、pd.npy。模型文件在pa_model中，pa_v2和pa_v3是调试参数的文件，其中
最佳的实验结果保存在pa_v3中。

### 实验记录
RMSprop优化器

1)三层一维卷积，无优化器权重衰减，学习率 5e-4

损失函数

Cos   0.8598(val)   0.79(test)

logcosh  0.88(val)  0.8296(test)

KL diverge  0.85185  0.7704

2) 3 1Dconv,权重衰减1e-2，学习率5e-4
binary corss  0.8693  0.800

Possion  0.8519   0.8714(best)


