1. 关系模型和文档模型的区别在哪里
-  关系模型需要把一个数据对象，拆分成零部件，然后存储在各个对应的表中，需要的时候再拼起来。
- mongoDB的文档模式,由于我们存储单位是一个文档，可以支持数组和嵌套的文档。

2. 如何考虑mongoDB 文档模式设计的基本策略
- 一般先考虑内嵌，按照你的对象模型设计数据模型。如果模型对象不多，关系也不是很复杂，可能一种对象对应一个集合就可以
适合一对-，一对多。局限性：文档最大16M，大数组性能欠佳
- 有些时候引用难以避免，比如:一个明星博客可能有几十万或者几百万的回复，这个时候如果把comments放到一个数组中。可能会超出16M的限制。
适合多对多，两个对象都是主要对象。局限性：多次查询，写入，无跨表事务性。

3. mongoDB模式设计原则
- 为应用程序服务，而不是未来存储优化
- 为实现最佳性能优化而设计

5. 例子
- 购物车
  特点:单个购物车的数据项不会太大，一般来说不会超过100项目。(双十一淘宝购物车最多存放99件商品)
  > 设计考量:
   * 一个cart数据项不会太大，一般项数是少于100
   * 数据自动过期  
- 社交网络
  特点:关键场景就是维护朋友关系以及朋友圈或微博墙等。
  > 设计考量
   * 如何维护朋友关系 - 关注,被关注 
    如果是一个明星,则关注的人可能是千万级,1)会造成16M的硬件限制，2) 数组太大会严重影响性能
   * 朋友圈或者微博墙的设计 - 名人效应
