# [中文](README.md) [English](English.md)

<a href="https://www.r-project.org/" target="_blank">
    <img width="24" height="24"  src="./img/Rlogo.png"/>
</a>
<a href="https://posit.co/download/rstudio-desktop/" target="_blank">
    <img width="24" height="24"  src="./img/RStudio.png"/>
</a>
<a href="https://qgis.org/en/site/" target="_blank">
    <img width="24" height="24"  src="./img/QGIS.png"/>
</a>

<div align="center">
    <img width="125" height="125" src="./img/CoastlineFD.png" alt="legado"/>
<br>
CoastlineFD
<br>
<a href="https://mirrors.tuna.tsinghua.edu.cn/CRAN/web/packages/CoastlineFD/index.html" target="_blank">CRAN</a> / <a href="https://github.com/redworld123/CoastlineFD" target="_blank">GitHub</a>
<br>
使用量规法和网格法计算海岸线的分形维数
</div>

[![](https://img.shields.io/badge/-Contents:-696969.svg)](#contents)
[![](https://img.shields.io/badge/-Download-F5F5G5.svg)](#Download-下载方法-)
[![](https://img.shields.io/badge/-Function-F5F5F5.svg)](#Function-主要功能-)
[![](https://img.shields.io/badge/-Example-F565F5.svg)](#Example-操作范例-)
[![](https://img.shields.io/badge/-Interface-F5F5F5.svg)](#Interface-运行界面-)
[![](https://img.shields.io/badge/-Other-A5F5F5.svg)](#Other-其他-)

> 新用户？  
>
> 建议频繁使用`help(package=‘CoastlineFD’)`  

# Download-下载方法 [![](https://img.shields.io/badge/-Downlaod-F5F5G5.svg)](#Downlaod-下载方法-)

```
# CRAN
install.package('CoastlineFD')

# GitHub
library('devtools')
install_github("redworld123/CoastlineFD")
```

# Function-主要功能 [![](https://img.shields.io/badge/-Function-F5F5F5.svg)](#Function-主要功能-)

- 网格法计算分形维数
- 量规法计算分形维数
- 网格法和量规法共同计算分形维数
- 绘制计算结果时序图
- 导出计算结果为`.xlsx`

# Example-操作范例 [![](https://img.shields.io/badge/-Example-F565F5.svg)](#Example-操作范例-)

### 量规法

> 海岸线矢量数据需要进行拓扑检查，确保每期岸线均为一条完整直线，不存在断点和自相交  
> 海岸线矢量数据必须进行实密化处理，建议使用`QGIS`以`1m`间隔增密岸线矢量文件点号串  

<div align="center">
    <img src="./img/QGIS1.png"/>
</div>

> 使用`DividersFD()`函数单独计算量规法分形维数  

```
DinputPath = './DividersFD'                     # 其中放置多期岸线矢量文件
outputPath = './FD.xlsx'                        # 结果导出的位置
year = c(1985:2023)                             # 多期岸线的起止年份
r = c(                                          # 量规的尺度
    30, 60, 75, 90, 150, 200, 300, 400,
    500, 600, 700, 800, 900, 1000, 1050,
    1100, 1150, 1200, 1300, 1400, 1500,
    1650, 1800, 2500, 3000, 3500, 4500,
    6000, 7500, 9000
)
pearsonValue = 0.98                             # 皮尔森系数
writeF = TRUE                                   # 是否将结果导出到.xlsx文件
showF = TRUE                                    # 是否绘制结果图

DividersFD(
    DinputPath,
    outputPath,
    year,
    r,
    pearsonValue,
    FALSE,
    TRUE
)
```

### 网格法

> 建议使用`QGIS`紧贴研究区域生成采样网格，不同范围的网格会导致网格法分形维数计算结果的不同  
> 海岸线矢量数据需要进行拓扑检查，确保每期岸线均为一条完整直线，不存在断点和自相交  
> 无需实密化处理，该处理会极大增加网格法的计算时间  
> 使用`BoxesFD()`函数单独计算网格法分形维数  

```
BinputPath = './BoxesFD'                        # 其中放置多期岸线矢量文件
Fishnet = './Fishnet'                           # 其中放置多个尺度的网格
outputPath = './FD.xlsx'                        # 结果导出的位置
year = c(1985:2023)                             # 多期岸线的起止年份
r = c(                                          # 网格的尺度
    30, 60, 75, 90, 150, 200, 300, 400,
    500, 600, 700, 800, 900, 1000, 1050,
    1100, 1150, 1200, 1300, 1400, 1500,
    1650, 1800, 2500, 3000, 3500, 4500,
    6000, 7500, 9000
)
pearsonValue = 0.98                             # 皮尔森系数
writeF = TRUE                                   # 是否将结果导出到.xlsx文件
showF = TRUE                                    # 是否绘制结果图

BoxesFD(
    BinputPath,
    Fishnet,
    outputPath,
    year,
    r,
    pearsonValue,
    FALSE,
    TRUE
)
```

### 网格法和量规法

> 注意上述所有提示，使用`FD()`函数同时计算两者  

```
DinputPath = './DividersFD'                     # 其中放置已实密化多期岸线矢量文件
BinputPath = './BoxesFD'                        # 其中放置未实密化多期岸线矢量文件
Fishnet = './Fishnet'                           # 其中放置多个尺度的网格
outputPath = './FD.xlsx'                        # 结果导出的位置
year = c(1985:2023)                             # 多期岸线的起止年份
r = c(                                          # 量规和网格的尺度
    30, 60, 75, 90, 150, 200, 300, 400,
    500, 600, 700, 800, 900, 1000, 1050,
    1100, 1150, 1200, 1300, 1400, 1500,
    1650, 1800, 2500, 3000, 3500, 4500,
    6000, 7500, 9000
)
pearsonValue = 0.98                             # 皮尔森系数
writeF = TRUE                                   # 是否将结果导出到.xlsx文件
showF = TRUE                                    # 是否绘制结果图

FD(
    DinputPath,
    BinputPath,
    Fishnet,
    outputPath,
    year,
    r,
    pearsonValue,
    FALSE,
    TRUE
)
```

> 运行结果图  

<div align="center">
    <img src="./img/Rplot.png"/>
</div>

# Interface-运行界面 [![](https://img.shields.io/badge/-Interface-F5F5F5.svg)](#Interface-运行界面-)

> 耐心等待进度条结束即可  

<div align="center">
    <img src="./img/res.png"/>
</div>

# Other-其他 [![](https://img.shields.io/badge/-Other-A5F5F5.svg)](#Other-其他-)

> 参考文献  

- 海岸线分形维数计算方法及其比较研究
- 山东省围填海演进过程及其对自然岸线资源的影响
- 基于自动化量规法的中国大陆海岸线分形特征研究

> 样本数据

- `R`包帮助文档中数据携带量有限，无法进行分形维数的完整计算，可在`example`文件夹中获取完样本数据  

***
