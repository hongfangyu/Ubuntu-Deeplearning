####这是安装NVIDIA驱动的文件夹
注意：如果是刚刚安装Ubuntu系统，应该在刚刚安装完系统的第一次重启之后，刚进入Ubuntu系统选择界面时，按字母e，
找到并编辑"quiet spalsh"更改为"nomodeset",之后按F10进入系统，这会使用CPU来刷新屏幕，比较卡，没关系。

1.准备适合显卡的NVIDIA驱动
https://www.nvidia.com/Download/index.aspx

2.禁止Ubuntu默认的nouveau第三方NVIDIA驱动(以后也不用更改回来)
sudo gedit /etc/modprobe.d/blacklist.conf
在最后面另起一行加上：
blacklist nouveau
options nouveau modeset=0
执行：
sudo update-initramfs -u
lsmod | grep nouveau
若上一句有输出，则重启系统重新执行上一句,否则直接进行下一步：
reboot
lsmod | grep nouveau

3. 禁用X-Window服务
Ctrl-Alt+F1输入用户名和密码以后，再执行上：
sudo service lightdm stop
进入驱动所在的文件夹下
给驱动run文件赋予执行权限：
sudo chmod +x NVIDIA-Linux-x86_64-384.59.run
最好先卸载以前可能存在的驱动：
sudo sh ./NVIDIA-Linux-x86_64-384.59.run --uninstall
安装驱动
sudo sh ./NVIDIA-Linux-x86_64-384.59.run –no-opengl-files
以下参数可选：
–no-opengl-files：表示只安装驱动文件，不安装OpenGL文件。这个参数不可省略，否则会导致登陆界面死循环，英语一般称为”login loop”或者”stuck in login”。
–no-x-check：表示安装驱动时不检查X服务，非必需。
–no-nouveau-check：表示安装驱动时不检查nouveau，非必需。
-Z, --disable-nouveau：禁用nouveau。此参数非必需，因为之前已经手动禁用了nouveau。
-A：查看更多高级选项。

4.测试驱动
#若列出GPU的信息列表，表示驱动安装成功
nvidia-smi

5.恢复图形界面
sudo service lightdm start

