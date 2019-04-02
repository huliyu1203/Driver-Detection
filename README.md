# Driver-Detection
同乘司机和副驾驶检测方案

项目描述：在拍摄的道路照片（10亿张）中，如何在不同图片中找出同一辆车的驾驶员和副驾驶？（达到追踪汽车，并检查是否为相同的驾驶员和副驾驶的目标）

项目方案：
步骤一（车辆匹配）：在不同的照片中找出同一辆车，即在已知一辆需要寻找的车辆后，需要在其他照片中搜索是否存在该车辆。
车辆是一个多特征事物，如车牌，车标，车型，车身颜色等特征，可以用卷积神经网络提取特征。
针对车辆匹配问题，设计算法对已知车辆和其他图片中的车辆给出相似度评分，设定阈值，如某张图片的一辆车和已知车辆相似度大于一定阈值，可初步判定是同一辆车。


步骤二（司机及副驾驶检测和超分辨率处理）：
（1）司机及副驾驶检测：
在初步确定某辆车之后，需检测出车辆中的驾驶员和副驾驶。
针对司机和副驾驶检测问题，训练深度学习模型，在拍摄图片中只检测出汽车中驾驶员和副驾驶，那么需要排除行人的干扰。
在训练时只需训练识别驾驶员和副驾驶即可，不需要对行人进行标注。
（2）超分辨率处理：
使用预先训练好的超分辨率深度学习模型将步骤二（1）中检测出的驾驶员和副驾驶进行超分辨率处理，
使得到的驾驶员和副驾驶图片更加清晰。


步骤三（最终确定是否为同一辆车，是否为同乘乘客）：
根据步骤二中的司机和副驾驶检测及超分辨率方法，将步骤一中检测出的不同图片中的“同一辆车”中的驾驶员和副驾驶检测出来，
进一步对司机和副驾驶进行比对，如果“同一辆车”的司机和副驾驶相似度均较低，那么忽略步骤一中匹配的某一图片中的“同一辆车”。
如果驾驶员和副驾驶相似度较高，则可以对步骤一中检测出的结果进行进一步确认，即确定步骤一检测出的车辆是同一辆车，同时可以判断是否为同乘乘客。
