# 关于yolov8的使用

>本篇markdown文件主要讲解yolov8的使用，源代码请从GitHub上自行clone，环境配置请查看GitHub上的yolov8（ultralytics）对环境配置的要求，或者说，其实主要需要下载Anaconda，CUDA，CUDNN，pytorch等

## 1.VScode软件安装

[vscode下载](https://blog.csdn.net/weixin_43121885/article/details/131779104?fromshare=blogdetail&sharetype=blogdetail&sharerId=131779104&sharerefer=PC&sharesource=2302_80370776&sharefrom=from_link)
可以查阅这篇csdn文档，先下载Windows版本

## 2.Python环境配置

直接登录Python官网下载即可，这个也记得要是Windows的
[Python官方链接](https://www.python.org/)

## 3.Anaconda,CUDA,CUDNN,pytorch的安装

其实更希望大家自行查阅相关软件和环境的配置安装方法，但貌似也没什么必要，所以继续附上链接：
[Anaconda,CUDA,CUDNN,pytorch讲解和安装文档](https://blog.csdn.net/Little_Carter/article/details/135934842?fromshare=blogdetail&sharetype=blogdetail&sharerId=135934842&sharerefer=PC&sharesource=2302_80370776&sharefrom=from_link)

到此，使用yolo目标检测的前期配置基本完成（如有遗漏还请指正），另外，上述需要安装的内容有很多教程，大家也可以找自己看着顺眼的（推荐）

>接下来正式来到yolov8的使用环节，yolov8代码包的下载最好去GitHub找，
 或者我压缩给大家

## 1.yolov8文件包的解读

整个文件包名为ultralytics

其中，我们需要在ultralytics根目录新建一个datasets文件夹
在其中新建images和labels两个文件夹

images文件夹下再新建train，val，test文件夹，三个文件夹下放相同的png图片文件（利用jpg2png.py来实现jpg到png的转换）
labels文件夹下再新建train，val文件夹，两个文件夹下放相同的txt文件

## 2.关于视频抽帧和标注数据集

视频抽帧，我推荐使用我的frame.py程序来实现

标注数据集，我推荐使用网页端的makesense.ai来实现 （因为我不知道为啥用不了labelimg，然后这个makesense也没找到app），标注数据集的要求后续再讲

## 3.编写yaml配置文件和下载.pt模型

训练数据集之前需要在datasets目录下写一个.yaml文件，内容格式见color.yaml

另外还要先去官网上下载随便一个.pt模型，选哪个模型取决于你的数据集大小、你想要的训练速度和电脑配置
.pt模型也要放在datasets目录下

## 4.训练时的命令行指令

我使用的Anaconda prompt命令行，
调到d盘和yolo虚拟环境是必须的第一步
然后：
**训练**

```bash
yolo task=detect mode=train model=yolov8n.pt data=data/fall.yaml batch=16 epochs=50 close_mosaic=0 imgsz=640 workers=8 device=0
```

训练后验证
**验证**

```bash
yolo task=detect mode=val model=runs/detect/train3/weights/best.pt data=data/fall.yaml device=0 plots=True
```

验证后进行图片或视频的预测
**预测**

```bash
yolo task=detect mode=predict model=runs/detect/train3/weights/best.pt source=images/videos device=0
```

最终导出模型
**导出**

```bash
yolo task=detect mode=export model=runs/detect/train3/weights/best.pt format=onnx/ncnn
```

下面是yolo整体命令的格式
**整体**

```bash
yolo task=detect    mode=train    model=yolov8n.pt        args...
          classify       predict        yolov8n-cls.yaml  args...
          segment        val            yolov8n-seg.yaml  args...
                         export         yolov8n.pt        format=onnx  args...
```

连接电脑摄像头进行实时预测用下面这条指令：
**电脑摄像头**

```bash
yolo predict model=D:/ultralytics/yolov8s.pt source=0 show
```

其中，涉及路径的都建议要写全路径
如果想预测后保存预测结果，那么在预测的命令后添加一段命令：save_txt

![1729929656583](image/explain/1729929656583.png)
![1729929740330](image/explain/1729929740330.png)
![1729929838667](image/explain/1729929838667.png)
