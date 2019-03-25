# PingCAPinterview

the interview for PingCAP

##### 时间

###### 开始时间：北京时间 2019年3月22日，下午17:00       结束时间：北京时间 2019年3月24日，下午2:00

##### 作业要求

在GitHub上实现，截止时间前提交项目链接。

##### 题目：data_collection

###### description

A system contains multiple data sources, every data source would generate data endless.

data source would send two messages to itself streaming in order for every data

- prepare message(type == prepare), contains prepare token
- commit message(type == message), contains prepare andcommit token

###### requirement

- sort data by commit token ascending, and output them in the fastest way you can implement(this system has a real time requirement)
- add flow control for your code (data are endless, I think we need to control memory and cpu usage) 
- describe your alghorithm and implemention in README.md
- add test case (any fashion) to prove your alghorithm correctness

I have complete code relate data source, you just need to complete sort and output code in collect(), and you can add some auxiliary structures, variables and functions, but don't modify any definitions.

###### Notice: welcome any problems and feedbacks

##### 分析题目：

​        数据无限，排序要高效，要控制内存和CPU使用量。

##### 实现思路:

​         1.用一台电脑接收客户端产生的数据，哈希分流处理，对数据进行大致分类，然后用多个电脑接收分类后的数据，如，以500（根据实际数据可以修改，这里用来举例）为界限，那么数据范围在0到499就放在第一台电脑上，数据范围在500到999就放在第二台电脑上，以此类推，如果存在负数，依然是这样哈希处理，所以电脑的编号从负数...-1,0,1...正数。

​         2.在每个电脑上建立下标为0~499的vector，初始化为0，然后使用桶排序，将每台电脑接收到的数据根据%500后的key装进桶中。

​         3.依据哈希分流，每台电脑再次接收数据时，只要将新接收到的数据装进key值对应的桶中即可。

​         4.输出的时候要将各电数据同时输出，按照电脑的编号从小到大，根据桶从小到大顺序依次反馈。

##### 说明：

​        之前问出题人员输出的时候输出 commit message(type == message), contains prepare andcommit token中的commit token还是要输出 commit message(type == message), contains prepare andcommit token中的ontains prepare and commit token，得到的回复是都可以，这不是最重要的。因为我用到的是桶排序，如果要再输出contains prepare，只是增加每只桶内排序时比较的复杂度，不影响算法总体的复杂度。

© 2019 GitHub, Inc.
