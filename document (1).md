# arcgis遥感影像海岸线数据集制作

## 画陆地轮廓

1.打开目录

2.创建shapefile文件，命名"land"

![](https://github.com/QJR-wj/images/blob/1662800bc2e02ad3c6d80dcff5768bf184595d29/1.png))

3.编辑要素，创建要素，画陆地轮廓

## 建立陆地面要素

1.打开ArcToolBox——数据管理工具——要素——要素转面

![](https://github.com/QJR-wj/images/blob/6713eaddab801317fad10b7410057c97de99d13f/2.png)

## 建立海洋面要素

1.画一个比原始影像图尺寸大的AOI（只做一个，全部图都用它）

2.打开ArcToolBox——分析工具——叠加分析——擦除

3.用AOI擦除polygon面，得到sea面要素

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/3.png)

## 陆地和海洋合成一个面要素

1.地理处理——合并——命名为merge

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/4.png)

## 制作栅格

1.打开merge面的打开数据表，创建字段class

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/5.png)

2.点击对应的区域，再右键点击class，打开字段计算器，将陆地输入4，海洋输入5

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/6.png)

3.打开ArcToolBox——转换工具——转为栅格——面转栅格——改参数和环境参数（注意这里的输出文件命名后缀带上.tif，负责它生成不出tif主文件，只会得到一个文件夹）

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/7.png)

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/8.png)

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/9.png)

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/10.png)

4.搜索——栅格计算器——输入
```javascript
Con(Raster("mask.tif") == 4, 1, 0)
```
（这里文件输出也需要后缀带上.tif）

## 裁剪mask

1.打开ArcToolBox——Spatial Analyst工具——提取分析——按掩膜提取

![](https://github.com/QJR-wj/images/blob/c2a9e6c3394fb6a2493119c39960a4425ead616f/11.png)
