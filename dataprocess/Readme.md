# 数据的处理
主要工作就是做了一些数据的处理，
2yolo和2coco文件进行了坐标转换，分别将给出的标注转换成yolov5和coco格式
# 数据增广
DaraArguementation进行了数据增广，方法是CutPaste
先从原图中裁剪出标注区域，作为一个样本库，
再从原图中随机取图，和样本，将样本随机放入图片

# 生成的一些图片
![](./0313.jpg)
![](./media_images_Mosaics_0_2.jpg)
以及标注