####这里是安装NVIDIA的cuda文件夹(默认已经禁用nouveau)

1.下载好需要的cuda版本
https://developer.nvidia.com/cuda-toolkit-archive

2. 禁用X-Window服务
Ctrl-Alt+F1输入用户名和密码以后，再执行上：
sudo service lightdm stop

3.开始安装
进入驱动所在的文件夹下
sudo sh ./cuda_8.0.61_375.26_linux.run --no-opengl-libs
可选参数：
--no-opengl-libs：表示只安装驱动文件，不安装OpenGL文件。必需参数，原因同上。注意：不是-no-opengl-files。
--uninstall (deprecated)：用于卸载CUDA Driver（已废弃）。
--toolkit：表示只安装CUDA Toolkit，不安装Driver和Samples。
--help：查看更多高级选项。

以下为安装过程中选择：
q#退出阅读用户协议
accept #同意安装
n #不安装Driver，因为已安装最新驱动
y #安装CUDA Toolkit
<Enter> #安装到默认目录
y #创建安装目录的软链接
n #不复制Samples，因为在安装目录下有/samples

若有补丁，#最后安装补丁CUDA官方补丁
sudo sh ./cuda_8.0.61.2_linux.run

回到图形界面：
sudo service lightdm start

4.注册cuda路径
sudo gedit ~/.bashrc
在最后一行加入：
export PATH=/usr/local/cuda-7.5/bin/:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda7.5/lib64/：$LD_LIBRARY_PATH
使环境变量立即生效：
source ~/.bashrc
或者注销用户(logout)并重进
可查看环境变量：
env

5.查案cuda版本
cat /usr/local/cuda/version.txt
或者
nvcc -V

为了安装全面的cuda(一些额外的功能，加快神经网络前向传递速度，主要按照tensorflow的安装要求)
1.查看cuda-command-line-tool
sudo apt-cache search cuda-command-line-tool
如果有输出，如：
cuda-command-line-tools-8-0 - CUDA command-line tools
cuda-command-line-tools-9-0 - CUDA command-line tools
cuda-command-line-tools-9-1 - CUDA command-line tools
则选择需要的进行安装，如：
sudo apt install cuda-command-line-tools-9-0
有输出则直接进行第3步，否则进行第2步

2.否则，进行以下操作：
进入以下网站下载以下必要的deb，按照顺序安装文件
https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/

sudo dpkg -i cuda-license-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-misc-headers-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-core-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-driver-dev-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-cudart-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-cudart-dev-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-command-line-tools-9-0_9.0.176-1_amd64.deb

查看cuda-command-line-tool
sudo apt-cache search cuda-command-line-tool
如果有输出，如：
cuda-command-line-tools-8-0 - CUDA command-line tools
cuda-command-line-tools-9-0 - CUDA command-line tools
cuda-command-line-tools-9-1 - CUDA command-line tools
则选择需要的进行安装，如：
sudo apt install cuda-command-line-tools-9-0

3.进入以下网站下载以下必要的deb，按照顺序安装文件
https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/

sudo dpkg -i cuda-cublas-9-0_9.0.176-1_amd64.deb
sudo dpkg -i cuda-cublas-9-0_9.0.176.1-1_amd64.deb
sudo dpkg -i cuda-cublas-9-0_9.0.176.2-1_amd64.deb
