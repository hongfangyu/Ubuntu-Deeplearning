####这里是安装NVIDIA的cuda文件夹(默认已经禁用nouveau)

1.下载好需要的cuda版本
https://developer.nvidia.com/cuda-toolkit-archive

2. 禁用X-Window服务
Ctrl-Alt+F1输入用户名和密码以后，再执行上：
sudo service lightdm stop

3.开始安装
进入驱动所在的文件夹下
sudo ./cuda_8.0.61_375.26_linux.run --no-opengl-libs
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

