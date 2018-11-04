
![](http://p20tr36iw.bkt.clouddn.com/kg_learn.jpg)



# 社交网络之图论实战

## 0.前言

又到了新的一周，今天来学点新的知识，这节学的知识还是**非常重要**，那就是属于**社交网络**方向以及**知识图谱**以及我们研究生的一门课---**《图论》**！

本节将从**我的学习方式**到**英文文档如何看**以及**如何处理问题**，以及**如何去研究社交网络及图论**等角度来分析！

下面一起来学习新知识吧，记得打开你的python哦，哈哈，就是一篇**python实战篇**！

## 1.准备工作

本节以`python-igraph`来学习社交网络与图论相关知识！

【**两个网站**】

那么我们一起来安装一下，这里引入两个网站。

第一：**(whl)包安装网站**:

> https://www.lfd.uci.edu/~gohlke/pythonlibs/

第一：**igraph API官网**:

> http://igraph.org/python/doc/tutorial/tutorial.html#structural-properties-of-graphs

【**安装包**】

在第一个网站搜索**Python-igraph**，然后找到相应的版本下载即可。

最后`pip install  xxx.whl`即可完成安装！

## 2.学习方法

【**学习方法**】

之前有人在交流群或者私下问我学习的方式，那么我现在告诉各位我的学习方法之一就是阅读官网API，我看了一下这个官网API，很详细，虽然是英文的，但是对于英文我们总不能躲避，而是**顺其意，码其码**！

在阅读中，我们可以学到一些API术语，以及相关操作的表达，这些在平时开发中学不到，但是却对于平时开发的异常处理十分重要！比如写了一个bug，报了个错，有些API中会把这些作为警告表示出来，你看到了，也就学会了，**在出现这些问题的时候，直接查问题即可，而不是盲目的不知所措，虽然说搜素很重要，但比搜索更重要的是你的思路，也就是先导**！

【**正确阅读**】

这里贴出一张图，我们看到这个API，会发现上面是描述，下面是代码。

![](http://p20tr36iw.bkt.clouddn.com/igraph.png)

我的学习方式是**对比法**，就是将上述英文与代码对比来实战！先看一下代码如果能看懂，则直接简化上述的文字，略读即可！如果碰到十分重要的代码，则从文字中提取信息对比代码来看！实在不行，谷歌或者其他的翻译手段进行翻译！

【**什么值得读**】

有些API非常建议读，比如这个，但是并不是所有的API具有可读性，像那种排版很差，解释性不强的，直接略过即可！

API分类明确，详细阐述的，可读！

## 3.社交网络实战

> 导包

```
from igraph import *
```

> 版本

```
igraph.__version__
```

'0.7.1'

> 创建图

```
# 创建图
g=Graph()
g
```

输出：

```
<igraph.Graph at 0x21d1237a138>
```

另一种打印

```
print(g)
```

输出：

```
IGRAPH U--- 0 0 --
```

>  添加三个节点

```
# 添加三个节点
g.add_vertices(3)
```

> 打印

```
print(g)
```

输出：

```
IGRAPH U--- 3 0 --
```

> 添加两条边

```
#添加两条边
g.add_edges([(1,2),(0,1)])
```

> 添加三个节点

```
# 生成3个节点，2条边
print(g)
```

输出：

```
IGRAPH U--- 3 2 --
+ edges:
1--2 0--1
```

> 再添加三个节点

```
# 再添加三个节点
g.add_vertices(3)
print(g)
```

输出：

```
IGRAPH U--- 6 2 --
+ edges:
1--2 0--1
```

>  添加更多关系

```
# 添加更多关系
g.add_edges([(2,3),(3,4),(4,5),(5,3)])
```

> 6个节点，6条边的无向图

```
# 6个节点，6条边的无向图
print(g)
```

输出：

```
IGRAPH U--- 6 6 --
+ edges:
1--2 0--1 2--3 3--4 4--5 3--5
```

> 获取边id

```
g.get_eid(1,2)
```

输出：

```
0
```

同理获取边id

```
g.get_eid(0,1)
```

输出：

```
1
```

> 获取边列表

```
g.get_edgelist()
```

输出：

```
[(1, 2), (0, 1), (2, 3), (3, 4), (4, 5), (3, 5)]
```

> 获取图的顶点与边

```
summary(g)
```

输出：

```
IGRAPH U--- 6 6 -- 
```

> 树生成边与顶点

```
# 生成127个顶点，126条边，2代表每个顶点两个孩子
g2=Graph.Tree(127,2)
print(g2)
```

输出：

```
IGRAPH U--- 127 126 --
+ edges:
0--1 0--2 1--3 1--4 2--5 2--6 3--7 3--8 4--9 4--10 5--11 5--12 6--13 6--14
7--15 7--16 8--17 8--18 9--19 9--20 10--21 10--22 11--23 11--24 12--25 12--26
...
...
...
```

> 随机生成图

```
#随机生成图
g = Graph.GRG(100, 0.2)
print(g)
```

输出：

```
IGRAPH U--- 100 597 --
+ attr: x (v), y (v)
+ edges:
  0 --   3   5   6   9  11
  1 --   3   8  10  16
  2 --   5   6  13
  ...
  ...
```

> 检查两图是否同构

```
#检查两图是否同构
#g.isomorphic(g2)
```

> 生成一个完整无向图

```
g = Graph([(0,1), (0,2), (2,3), (3,4), (4,2), (2,5), (5,0), (6,3), (5,6)])
print(g)
```

输出：

```
IGRAPH U--- 7 9 --
+ edges:
0 -- 1 2 5     2 -- 0 3 4 5   4 -- 2 3       6 -- 3 5
1 -- 0         3 -- 2 4 6     5 -- 0 2 6
```

> 查看顶点

```
g.vs
```

输出：

```
<igraph.VertexSeq at 0x21d123a08b8>
```

> 顶点属性定义

```
g.vs["name"] = ["Alice", "Bob", "Claire", "Dennis", "Esther", "Frank", "George"]
print(g)
```

输出：

```
IGRAPH UN-- 7 9 --
+ attr: name (v)
+ edges (vertex names):
 Alice -- Bob, Claire, Frank             Esther -- Claire, Dennis
   Bob -- Alice                           Frank -- Alice, Claire, George
Claire -- Alice, Dennis, Esther, Frank   George -- Dennis, Frank
Dennis -- Claire, Esther, George
```

另一属性定义：

```
g.vs["age"] = [25, 31, 18, 47, 22, 23, 50]
print(g)
```

输出：

```
IGRAPH UN-- 7 9 --
+ attr: age (v), name (v)
+ edges (vertex names):
 Alice -- Bob, Claire, Frank             Esther -- Claire, Dennis
   Bob -- Alice                           Frank -- Alice, Claire, George
Claire -- Alice, Dennis, Esther, Frank   George -- Dennis, Frank
Dennis -- Claire, Esther, George
```

另一属性定义

```
g.vs["gender"] = ["f", "m", "f", "m", "f", "m", "m"]
print(g)
```

输出：

```
IGRAPH UN-- 7 9 --
+ attr: age (v), gender (v), name (v)
+ edges (vertex names):
 Alice -- Bob, Claire, Frank             Esther -- Claire, Dennis
   Bob -- Alice                           Frank -- Alice, Claire, George
Claire -- Alice, Dennis, Esther, Frank   George -- Dennis, Frank
Dennis -- Claire, Esther, George
```

> 边属性定义

```
g.es["is_formal"] = [False, False, True, True, True, False, True, False, False]
print(g)
```

输出：

```
IGRAPH UN-- 7 9 --
+ attr: age (v), gender (v), name (v), is_formal (e)
+ edges (vertex names):
 Alice -- Bob, Claire, Frank             Esther -- Claire, Dennis
   Bob -- Alice                           Frank -- Alice, Claire, George
Claire -- Alice, Dennis, Esther, Frank   George -- Dennis, Frank
Dennis -- Claire, Esther, George
```

> 边属性获取

```
g.es[0]
```

输出：

```
igraph.Edge(<igraph.Graph object at 0x0000021D1237A408>, 0, {'is_formal': False})
```

属性获取

```
g.es[0].attributes()
```

输出：

```
{'is_formal': False}
```

属性深入获取

```
g.es[0]["is_formal"]
```

输出：

```
False
```

修改属性值

```
g.es[0]["is_formal"]=True
g.es[0].attributes()
```

输出：

```
{'is_formal': True}
```

> 顶点属性获取

```
g.vs[0]
输出：igraph.Vertex(<igraph.Graph object at 0x0000021D1237A408>, 0, {'name': 'Alice', 'age': 25, 'gender': 'f'})
g.vs[0].attributes()
输出：{'age': 25, 'gender': 'f', 'name': 'Alice'}
g.vs[0]['age']=0
g.vs[0].attributes()
输出：{'age': 0, 'gender': 'f', 'name': 'Alice'}
g.vs[0]['age']=25
g.vs[0].attributes()
输出：{'age': 25, 'gender': 'f', 'name': 'Alice'}
```

> 添加新顶点属性

```
g.vs[3]["foo"]="bar"
g.vs["foo"]
```

输出：

```
[None, None, None, 'bar', None, None, None]
```

> 删除顶点属性

```
del g.vs["foo"]
```

> 验证是否存在

```
g.vs["foo"]
```

输出：

```
---------------------------------------------------------------------------

KeyError                                  Traceback (most recent call last)

<ipython-input-151-a2e2f8e7cb08> in <module>()
----> 1 g.vs["foo"]
KeyError: 'Attribute does not exist'

```

> 顶点度

```
g.degree()
```

输出：

```
[3, 1, 4, 3, 2, 3, 2]

```

> 入度与出度

```
# mode instead type
g.degree(mode="in")
输出：[3, 1, 4, 3, 2, 3, 2]
g.degree(mode="out")
输出：[3, 1, 4, 3, 2, 3, 2]


```

> 获取度

```
g.degree([2,3,4])
```

输出：

```
[4, 3, 2]
```

> 边缘中介

```
# 边缘中介
g.edge_betweenness()
```

输出：

```
[6.0, 6.0, 4.0, 2.0, 4.0, 3.0, 4.0, 3.0, 4.0]

```

> 获取最大边缘中介边

```
[g.es[idx].tuple for idx, eb in enumerate(ebs) if eb == max_eb]
```

输出：

```
[(0, 1), (0, 2)]
```

> 顶点度

```
g.vs.degree()
```

输出：

```
[3, 1, 4, 3, 2, 3, 2]
```

> 查询

```
#查询
g.vs.select(_degree = g.maxdegree())["name"]
输出：['Claire']

```

> 布局绘图

下面两个等价

```
layout = g.layout_kamada_kawai()
layout = g.layout("kamada_kawai")
```

> 完整绘图

```
layout = g.layout("kk")
plot(g, layout = layout)
```

输出：

![](http://p20tr36iw.bkt.clouddn.com/output_70_0.svg)

> 绘图配置

```
g.vs["label"] = g.vs["name"]
color_dict = {"m": "green", "f": "pink"}
g.vs["color"] = [color_dict[gender] for gender in g.vs["gender"]]
plot(g, layout = layout, bbox = (300, 300), margin = 30)
```

输出：

![](http://p20tr36iw.bkt.clouddn.com/output_71_0.svg)

> 自定义绘图

```
visual_style = {}
visual_style["vertex_size"] = 20
visual_style["vertex_color"] = [color_dict[gender] for gender in g.vs["gender"]]
visual_style["vertex_label"] = g.vs["name"]
visual_style["edge_width"] = [1 + 2 * int(is_formal) for is_formal in g.es["is_formal"]]
visual_style["layout"] = layout
visual_style["bbox"] = (300, 300)
visual_style["margin"] = 20
plot(g, **visual_style)
```

输出：

![](http://p20tr36iw.bkt.clouddn.com/output_72_0.svg)

> 绘图存储

```
plot(g, "social_network.png", **visual_style)
```

输出：

![](http://p20tr36iw.bkt.clouddn.com/output_73_0.svg)

![](http://p20tr36iw.bkt.clouddn.com/res_out.png)

## 4.问题处理

在`plot`时报错！

解决办法：

首先安装`cairo`，在我上面写到的whl中查找这个包，然后安装，安装后按照下面图片找到包的位置，在官网给出的地址处下载下面第三点的相关dll文件，并放置包位置即可！(下面给出地址)

![](http://p20tr36iw.bkt.clouddn.com/problem.png)

> http://igraph.org/python/doc/tutorial/install.html#installing-igraph

## 5.作者的话

欢迎各位关注公众号：guangcity



