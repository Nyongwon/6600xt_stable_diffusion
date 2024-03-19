说明：读者你好，我是一个正在学习 专业与计算机专业相关但联系不是特别紧密的大三本科地理学生，需要并想要学习深度学习，来学习处理卫星影像。但当我知道AMD的显卡无法进行该学习时，我只得寻找办法。我尝试过安装Ubuntu，但不了了之。因为我的能力很薄弱，且没有人指导我学习，以至于我面对GitHub上的一个教程时手足无措，我只得放弃学习。无意间看到AMD显卡的深度学习有关AI绘图，便尝试搭建一个AI绘图的环境，在慢慢学习中进步，以学习更多有关深度学习的知识。如果你看到这篇文章，不知道我在该库贡献了什么，这很正常，因为这是我的第一篇GitHub文章，我无法熟练使用github来上传我的分享。如果由于此我无法提供很有效的帮助，只能对您说一句‘抱歉’。
如果您有其他问题，欢迎我们来讨论，我会尽我的绵薄之力帮助您。以下便是我安装Stable difussion 的步骤，耗时数个小时。
一.前提
1.电脑配置：
CPU:I5 10400f
GPU:RX6600XT
RAM:16G DDR4 2600
2.操作系统：
WINDOWS 11
3.所需软件：
python 3.9：https://www.python.org/ftp/python/3.9.7/python-3.9.7-amd64.exe
git：https://github.com/git-for-windows/git/releases/download/v2.42.0.windows.1/Git-2.42.0-64-bit.exe
notepad++：https://sourl.cn/DwKKM5
二.步骤
1.安装python3.9，注意安装左下角界面勾选”add python3.9 to path
2.安装git，一直点击NEXT，直到”choosing the default editor used by git“界面，选择nottpad++，之后一直点击NEXT直到安装完成；如果选择notepad++后无法点击NEXT，尝试重新安装git，或者notepad++需要添加进path。
添加path方法：windows界面搜索‘查看高级系统设置’，在高级界面点击右下角环境变量，选中系统变量下的path点击编辑
，点击右侧浏览选中notepad++安装路径。如果此处存在问题，请搜索自行解决。
3.下载stable diffusion；运行cmd，输入‘python’并回车，查看是否存在python3.9版本，如果提示没有找到，请查找添加路径方法，方法同2。
3.1更新pip，在cmd输入‘pip install --upgrade pip’，提示成功更新即可，如果失败，请更换pip下载源
（pip下载源更新方法：cmd界面输入‘pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple’ -------此处为清华pip源，如果无法更新，请自行搜索）
3.2在C区外创建文件夹，用于保存Stable difussion（SD）文件，创建后在该文件夹目录上方导航栏全选并输入cmd，或使用cd命令cd 到该文件夹。
3.3输入命令：
  git clone https://github.com/lshqqytiger/stable-diffusion-webui-directml && cd stable-diffusion-webui-directml && git submodule init && git submodule update ---------回车后等待下载完成。
4.配置webuyi user.bat，右键以notepad++打开，在‘set COMMANDLINE_ARGS=’右侧输入‘--medvram --backend directml --no-half --no-half-vae --precision full --opt-sub-quad-attention --opt-split-attention-v1 --disable-nan-check --no-gradio-queue --sub-quad-q-chunk-size 256 --sub-quad-kv-chunk-size 256 --sub-quad-chunk-threshold 70 --theme dark --autolaunch_’，保存后运行webuyi user.bat。
4.1首次启动webui user.bat的错误修复（你需要有看懂部分英文的能力，否则无法知道错误信息是什么）：
A.#pip更新
[notice] A new release of pip available: 22.2.1 -> 23.0.1
[notice] To update, run: F:\SDAI\stable-diffusion-webui\venv\Scripts\python.exe -m pip install --upgrade pip
解决：查看方法3.1，在cmd输入‘run：’后面的命令（由于路径不同，你需要运行你的报错信息下run后的命令）并执行。
B.#gfpgan安装失败 （典型问题）
RuntimeError: Couldn't install gfpgan
解决方法1：cd至目录venv--Scripts，并执行pip 安装程序（pip install gfpan）（提示错误，则需要换源）
解决方法2：在modules\launch_utils.py右键并使用ctrl +f搜索找到
if not is_installed("gfpgan"):
run_pip(f"install {gfpgan_package}", "gfpgan")
将该两行注释掉，注释方法为在行前面加‘#’
C：SSL问题（997）
解决办法：更换源或复制报错代码自行搜索
D：其他问题，包括无法克隆，几乎都是网络问题，需要自行根据自己的运行报错结果来处理，如果你什么都不知道，复制在浏览器搜索你的报错信息即可。
E：对于报错问题B，安装失败的肯定不止一个插件，如CLIP，需要你自己下载至目录venv--Scripts，并执行安装命令。具体问题具体分析，对于安装问题请自行网页搜索。
5.当你解决问题后，再次启动webui user.bat，会有很多东西需要更新以及下载，请耐心等待。之后再次打开webui user.bat，如果卡在”Launching Web UI with arguments: --medvram --backend directml --no-half --no-half-vae --precision full --opt-sub-quad-attention --opt-split-attention-v1 --disable-nan-check --no-gradio-queue --sub-quad-q-chunk-size 256 --sub-quad-kv-chunk-size 256 --sub-quad-chunk-threshold 70 --theme dark --autolaunch“，请不要关闭，继续等待，此时正在加载webUI，等待后将会自动打开一个网页，这就是你的本地AI绘图环境。
5.1AI绘图界面左上角的checkpoint是模型
你可以在网站上（_https://www.liblibai.com/#/index/model_）
免费下载你感兴趣的绘图类型，注意下载checkpiont；下载完成后将该模型复制粘贴至SD目录下的models--Stable-diffusion中，之后再次重启webui user.bat，将会启动该模型。如果你想要更多模型，请下载后放置在该目录。
5.2AI绘图界面需要你输入提示词，你可以根据你的模型下载网站上生成的示例图的数据进行仿照，点击右侧生成按钮等待。你可以时刻注意你的任务管理器中的GPU占用，比率越高表示使用率越高。
5.3绘图错误：
A.memory问题，显存不够，需要降低绘图质量，如更改迭代、图幅大小
B.黑色图片，换个模型，或者换个提示词多次尝试
C.其他问题，根据错误搜索
三.总结
以上步骤为我遇到的问题，不是特别全面，但大多数问题都是通过复制错误信息并搜索后解决的，如果你有耐心，并有一定的英语基础我相信，你能比我更快的搭建AI绘图环境。
谢谢你看到这里，对于文章不规范之处，请见谅
