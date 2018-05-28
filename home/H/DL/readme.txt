####这里是安装深度学习框架及相关软件的文件夹
第一部分 安装tensorflow
1.安装tensorflow GPU版本（参照官网）
启动和关闭tensorflow的python虚拟环境：
source /home/gaoyuxin/H/DL/tensorflow/bin/activate
deactivate

2.安装models
2.1 下载models和安装依赖库
下载models
git clone https://github.com/tensorflow/models.git
或者直接到
https://github.com/tensorflow/models
下载压缩包，然后再解压，更改文件名为models（比较快）

依赖库
pip install Cython
pip install pillow
pip install lxml
pip install jupyter
pip install matplotlib

2.2 COCO API installation
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
make
cp -r pycocotools ../../models/research/

2.3 Protobuf Compilation
cd ../../models/research/
sudo apt install protobuf-compiler
新建文件夹protoc,cd protoc,从
https://github.com/google/protobuf/releases
下载3.3版本以上的，如protoc-3.5.1-linux-x86_64.zip，解压，执行：
sudo cp bin/protoc /usr/bin/
cd ..
protoc object_detection/protos/*.proto --python_out=.

2.4 Add Libraries to PYTHONPATH
sudo gedit ~/.bashrc
加入以下：
#models
export PYTHONPATH=$PYTHONPATH:/home/gaoyuxin/H/DL/models/research:/home/gaoyuxin/H/DL/models/research/slim
执行：
source ~/.bashrc
source /home/gaoyuxin/H/DL/tensorflow/bin/activate
通过env或者
python
import sys
sys.path
查看Python路径有没有上述路径

2.5 测试安装models是否在成功
python object_detection/builders/model_builder_test.py
