# stata-ddml-
stata上跑ddml环境配置教程（内含解决mac常出现的crossfit 报错unrecognized command 问题的方法）

1、安装Python和R/Rstudio
均推荐官网下载 我用的是R version 4.5.1  Python 3.14.0

2、安装Python的依赖包
在终端（windows系统为CMD）或命令行中运行以下命令，安装Python的依赖包：
pip install scikit-learn  // 安装 scikit-learn 库，支持多种机器学习算法

3、安装R的依赖包
在R控制台中运行以下命令，安装R的依赖包：
install.packages("causalweight")  //用于因果中介效应分析
install.packages("haven")         // 支持读取 Stata 数据文件
install.packages("officer")       //用于生成格式化输出文档
install.packages("grf")           // 用于广义随机森林算法

4、安装Stata命令包
在Stata命令窗口中运行以下命令，安装必要的Stata命令包：
ssc install ddml, replace          // 安装DDML核心包
ssc install pystacked, replace     // ddml常用的机器学习方法执行器，支持多种算法
ssc install rforest, replace       // 另一个机器学习包，有时ddml会调用或可作为备选
ssc install lassopack, replace     // Lasso相关包，用于高维变量选择
search st0738.pkg                  // 可能与特定版本的lassopack或相关功能有关
ssc install rsource, replace       // Stata调用R的接口
ssc install parallel, replace      // 加速运行

5、设置Python路径
在Stata中设置Python路径，确保Stata能够正确调用Python环境：
python clear  // 清除Stata中已有的Python设置信息
python search  // Stata搜索可用的Python环境
set python_exec  "*" // "*"替换为你的Python可执行文件实际路径（选择上述环境之一）
set python_userpath 
python query  // 查询当前Stata配置的Python环境
python which sklearn  // 检查Stata是否能通过配置的Python找到sklearn库

6.mac crossfit 报错unrecognized command时可以尝试通过安装anaconda解决
（也有其他解决方式 比如安装windows虚拟机但是非常麻烦不建议）
1）下载Anaconda
 推荐使用清华镜像：访问清华镜像站的Anaconda下载页面 https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/
2） 检查Anaconda是否安装成功
在终端中输入以下命令，检查是否能找到 conda：
conda info 或者 conda --version
//如果显示 command not found: conda，说明 conda 命令未被正确识别，可以尝试以下方法
方法1：在终端（windows系统为CMD）运行以下命令，将Anaconda的路径添加到环境变量中：
source ~/.bash_profile
方法2：在终端（windows系统为CMD）手动设置环境变量，将Anaconda的路径添加到 PATH 中：
export PATH="/Users/your-username/anaconda3/bin:$PATH"
将 /Users/your-username/anaconda3/bin 替换为你的Anaconda安装路径
3）在stata中配置Python路径
python search //检查Stata是否能够识别到Anaconda的Python路径
如果Stata识别到的路径是 /Users/your-username/anaconda3/bin/python，则说明路径正确。
如果路径不正确，可以手动设置Python路径
set python_exec /Users/your-username/anaconda3/bin/python 

