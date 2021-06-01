# dfgx
东方国信杯比赛的记录
结果成绩并不好初赛 8 / 217 但是因为是自己参与的一个经历，所以想记下来
# baseline
因为是缺陷检测的问题，所以用目标检测的baseline应该是合理的，然后参考了一下其他比赛中前几名的方案，大部分方案是EffcienteDet/yolo/faster Rcnn
并且只要不是禁用yolo那么yolo总是会比较好，恰好手边有两个机器,所以就使用了yolov5 和 EffcienteDet两个baseline想要做一个对比。

最后得出EffcienteDet确实没有yolo那么强，训练也要慢一些，于是最后确定还是用了yolov5
# 数据标注
比赛没有给出数据标注，所以找了一下数据标注的方法，最后选用了coco-annotation工具作为数据标注的工具。可以导出coco格式的标注。
标注到一半官方给出了训练集的标注，于是就使用了官方的标注。
# 标注转换
coco跟yolov5跟官方给出的标注的格式都不相同，因此还需要互相转换。
在dataprocess文件夹中记录了标注转换的操作。
# 数据增广
给出的数据集训练集300张，测试集97张，样本数量还是比较少的。于是进行了一下数据增广。参考CutPaste的方法，对数据进行了增广，增加到了1000张训练图像，并且有标注，
虽然1000张图片也并不是很大的一个数据集，但是增广总比没有强
# 训练
分别用了最小的模型s和最大的模型x来进行yolo的训练，可能是数据集小的原因，x的效果是要比s好，但是也确实要慢很多。不过比赛嘛，还是要效果好的，不管推理速度。所以还是选择了x来进行finetune
## 调参
应该算是调参吧，数据集一张图片有很大 大概`4800 * 5000`的分辨率，大小有5M一张图，最开始使用640的大小来进行训练测试，得到的效果不太满意。解决方法应该是**crop和resize**时间原因没有进行切割，只用了resize将训练和测试图片的大小都设为了1280，其实如果能够再大一点效果应该也会更好，为什么没设置呢…… 
anchor的大小也应该修改，但是发现yolov5直接用了k均值聚类最后给出了一个最佳的阈值大小和anchor的大小，就直接用了。yolo yyds。
# 小结
其实并没有做什么创新，但是这样的过程应该会比较贴近工程吧？因此记录一下。
