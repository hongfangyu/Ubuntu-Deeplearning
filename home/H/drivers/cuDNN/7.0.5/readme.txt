####这里是cuDNN的安装文件夹

1.进入以下站点下载合适的cudnn
https://developer.nvidia.com/rdp/cudnn-archive

2.解压文件到此目录，并在次文件夹下执行
sudo cp cuda/include/cudnn*.h /usr/local/cuda/include 
sudo cp -P cuda/lib/libcudnn* /usr/local/cuda/lib64 
sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*

this:
sudo cp cuda/include/cudnn*.h /usr/local/cuda-9.0/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64
sudo chmod a+r /usr/local/cuda-9.0/include/cudnn*.h /usr/local/cuda-9.0/lib64/libcudnn*

Read more at: http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#ixzz52pJLKn3G 
Follow us: @GPUComputing on Twitter | NVIDIA on Facebook

3.扩展功能（安装最佳tensorflow的需要，其实对其他软件也都好）
进入NVIDIA TensorRT 3.0文件夹，从
https://developer.nvidia.com/rdp/cudnn-archive
下载cuDNN v7.0.5 Runtime Library for Ubuntu16.04 (Deb)和cuDNN v7.0.5 Developer Library for Ubuntu16.04 (Deb)
也就是libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb和libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb文件
执行：
wget https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64/nvinfer-runtime-trt-repo-ubuntu1404-3.0.4-ga-cuda9.0_1.0-1_amd64.deb
sudo apt-key add /var/nvinfer-runtime-trt-repo-3.0.4-ga-cuda9.0/7fa2af80.pub
sudo dpkg -i nvinfer-runtime-trt-repo-ubuntu1404-3.0.4-ga-cuda9.0_1.0-1_amd64.deb
sudo apt-get update
sudo dpkg -i  libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
sudo dpkg -i  libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb
sudo apt-get install -y --allow-downgrades libnvinfer-dev libcudnn7-dev=7.0.5.15-1+cuda9.0 libcudnn7=7.0.5.15-1+cuda9.0

锁定cuDNN版本，执行：
sudo apt-mark hold libcudnn7 libcudnn7-dev

另外，释放操作为：
sudo apt-mark unhold libcudnn7 libcudnn7-dev
