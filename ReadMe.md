# object_detection_hog_svm

使用HOG和SVM进行目标检测，主要代码来源于[object-detector](https://github.com/bikz05/object-detector)，可直接参考该仓库，本仓库仅仅为了自己的理解对文中代码进行阅读，后期加入定制的目标检测方法以及数据集。

---
## 基本思路

### 训练过程
准备一个数据集，包含pos（存在检测物体）和neg（不存在检测物体），这个数据集中的图像大小相同，比如（40, 100）高度x宽度，那么使用HOG检测子对数据集检测HOG特征，pos标记为正例样本，neg标记为负例样本，输入到SVM分类起进行训练，得到分类模型。

### 测试过程
输入一张图像，使用图像金字塔对图像进行下采样，每一个octave的图像进行滑窗操作，滑窗大小与训练数据集中的图像大小相同，比如（40, 100）高度x宽度，每一次滑窗后的图像提取HOG特征子，输入训练好的SVM分类器中进行预测，如果检测结果为正例样本，即pos存在检测物体，那么记录该检测结果，detection（x,y,pred_prob,w,h），这个检测结果包含较多的重叠区域，使用非极大值抑制对重叠区域进行剔除，最后的结果即为检测物体结果，包括检测结果的bounding box和检测结果置性度（pred_prob）。

---
## 数据集

UIUC Image Database for Car Detection

---
## 参考资料

[UIUC Image Database for Car Detection](https://www.youtube.com/watch?v=SPXocFBjr70) Car汽车数据集。

[Object Detection using HOG-Linear SVM in Python](https://www.youtube.com/watch?v=SPXocFBjr70) HOG SVM汽车检测视频演示。

[Histogram of Oriented Gradients and Object Detection](https://www.pyimagesearch.com/2014/11/10/histogram-oriented-gradients-object-detection/)

[Image Pyramids with Python and OpenCV](https://www.pyimagesearch.com/2015/03/16/image-pyramids-with-python-and-opencv/)

[Sliding Windows for Object Detection with Python and OpenCV](https://www.pyimagesearch.com/2015/03/23/sliding-windows-for-object-detection-with-python-and-opencv/)

[Non-Maximum Suppression for Object Detection in Python](https://www.pyimagesearch.com/2014/11/17/non-maximum-suppression-object-detection-python/)

[YOLO_v3_tutorial_from_scratch](https://github.com/ayooshkathuria/YOLO_v3_tutorial_from_scratch) YOLO实现原理。
