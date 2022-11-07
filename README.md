# python_Cplex
<a name="xtOo0"></a>
# CPLEX库是干什么的？
npy问我这个库是干嘛用的？<br />这个连接回答你的问题：<br />[https://www.ibm.com/cn-zh/analytics/cplex-cp-optimizer](https://www.ibm.com/cn-zh/analytics/cplex-cp-optimizer) <br />CP optimizer 是一个强大的优化器，可以处理编辑约束问题，主要可以解决 调度问题和约束条件下最优问题。<br />这里连接一个CPLEX 优化器的中文文档？IBM公司提供的<br />[https://www.ibm.com/docs/zh/icos/12.8.0.0?topic=guide-discovering-cplex-optimization-studio](https://www.ibm.com/docs/zh/icos/12.8.0.0?topic=guide-discovering-cplex-optimization-studio)<br />CPLEX Optimization Studio的优化引擎主要为CPLEX Optimizer 和 CP Optimizer。数学规划优化引擎称为 CPLEX Optimizer，它实施单纯形法、障碍法和混合整数规划。 约束规划引擎称为 CPLEX CP Optimizer。约束规划和数学规划经常互补。
<a name="XhlbF"></a>
# python3.8 安装cplex库
因为这个库的普通的库不一样，直接pip没用，需要提前安装以个cplex 到本地。

1. **安装**：

[https://ibm.ent.box.com/s/p1g0mrjnb0rs6am5evuvndy8f7vsug3t/file/936983566126](https://ibm.ent.box.com/s/p1g0mrjnb0rs6am5evuvndy8f7vsug3t/file/936983566126)<br />下载 CPLEX的 可执行程序，执行exe安装程序：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/26588248/1667825141144-f224a3ec-e98b-42d7-b384-c36656be147d.png#averageHue=%23fcf9f9&clientId=uc0c41eed-6960-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=493&id=udcef5998&margin=%5Bobject%20Object%5D&name=image.png&originHeight=444&originWidth=2260&originalType=binary&ratio=1&rotation=0&showTitle=false&size=58909&status=done&style=none&taskId=u642a9557-f4cf-4615-9857-a408b982445&title=&width=2511.11117763284)<br />执行后，计科安装CPLEX程序。一直next也是可以的<br />这里下载的是CPLEX22.10的window的包，可以支持python3.7-3.10，很强大！<br />安装完之后，在我的目录下可以看到：XX/cplex/python下有3.7-3.10的版本<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/26588248/1667825292277-8813f756-44c9-4469-a3ba-36f304d9b822.png#averageHue=%23fcfcfb&clientId=uc0c41eed-6960-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=537&id=udf3d69bf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=483&originWidth=1035&originalType=binary&ratio=1&rotation=0&showTitle=false&size=30178&status=done&style=none&taskId=ue64e21c1-b928-4c18-8bd7-f0a44a03c06&title=&width=1150.000030464597)

2. **打开cmd**，输入 pip install cplex 安装cplex。（cmd需要管理员权限）

我是在pycharm执行的cplex，我一般用pycharm'编辑python项目<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/26588248/1667825379034-18d8ca07-310e-4ce2-8030-69408b65009a.png#averageHue=%23312f2c&clientId=uc0c41eed-6960-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=532&id=ua4792f80&margin=%5Bobject%20Object%5D&name=image.png&originHeight=479&originWidth=1061&originalType=binary&ratio=1&rotation=0&showTitle=false&size=85965&status=done&style=none&taskId=ubabd52ce-490b-4266-9f18-9cd4882886c&title=&width=1178.88892011878)

3.进入到已经安装的cplex/python/3.8目录，**执行setup.py文件**<br />这里，我的python是3.8的所以才这么执行。<br />执行 python setup.py install 。会把cplex 自动安装到yourpythonpath/site-package（python 外部库路径下）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/26588248/1667825920096-24ef56f8-e5f6-414a-88da-056192ce3b20.png#averageHue=%23222121&clientId=uc0c41eed-6960-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=556&id=u78552487&margin=%5Bobject%20Object%5D&name=image.png&originHeight=500&originWidth=941&originalType=binary&ratio=1&rotation=0&showTitle=false&size=41094&status=done&style=none&taskId=u9c1af305-4ab8-47f7-bf7c-7ed932a19d1&title=&width=1045.5555832533196)<br />4.接下来输入pip install decplex 安装就可以在python中使用cplex 工具了<br />测试:
```shell
from docplex.mp.model import Model  #导出库，只用这一个就够了
model = Model() #创建模型
var_list = [i for i in range(0, 7)] #创建列表
X = model.binary_var_list(var_list, lb=0, name='X') #创建变量列表
#设定目标函数
model.maximize(11* X[0] + 9 * X[1] + 29 * X[2]+9* X[3]+21*X[4]+31*X[5]+22*X[6])
#添加约束条件
model.add_constraint(X[0]+X[1]+X[2] <= 2)
model.add_constraint(X[3] + X[4] >=1)
model.add_constraint(X[5] + X[6] >=1)
model.add_constraint(10* X[0] + 8* X[1] + 20 * X[2]+5* X[3]+13*X[4]+22*X[5]+10*X[6] <=60)
sol = model.solve() #求解模型
print(sol)  #打印结果
```
输出为：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/26588248/1667826061159-a7514b09-4e4d-492b-98e6-e73aef769bfe.png#averageHue=%232c2c2c&clientId=uc0c41eed-6960-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=326&id=u702bf3e5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=293&originWidth=819&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18865&status=done&style=none&taskId=u76a208bb-fe56-4100-96da-0122646e67f&title=&width=910.0000241067681)

参考文档：<br />测试代码参考文档：[https://zhuanlan.zhihu.com/p/479835520](https://zhuanlan.zhihu.com/p/479835520)<br />安装流程参考文档：[http://www.chenxm.cc/article/1280.html](http://www.chenxm.cc/article/1280.html)<br />cplex 的中文文档：[https://www.ibm.com/docs/zh/icos/12.9.0?topic=cplex-setting-up-python-api](https://www.ibm.com/docs/zh/icos/12.9.0?topic=cplex-setting-up-python-api)<br />这个中文文档还有一些 cplex的使用说明<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/26588248/1667826165373-791bdb9a-7375-4807-9f7d-1936ad475a99.png#averageHue=%23e6e4e3&clientId=uc0c41eed-6960-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=1086&id=uac42c563&margin=%5Bobject%20Object%5D&name=image.png&originHeight=977&originWidth=1639&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194120&status=done&style=none&taskId=u513790dd-7a63-433f-9cba-e2f54781c64&title=&width=1821.1111593540816)
