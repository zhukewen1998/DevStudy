### 常见的id生成策略：

   1、数据库自增长字段

​        优点：简单、性能良好，对分页及排序非常方便

​        缺点：完全自增易造成数据泄露，迁移麻烦，单库的时候易造成单点，多库维护较麻烦

   2、UUID

​        优点：简单、性能有保证，全球唯一

​        缺点：无序无法实现趋势递增，字符串存储查询效率较低，不可读

   3、redis自增

​        借助redis单线程通过incr、incrby实现唯一自增id

​        优点：速度比数据库自增快，对分页及排序友好

​        缺点：引入redis增加一定维护成本

   4、mongodb的objectid（目前图虫社区在用）

​        实现方式与snowflake类似，非常轻量级，不同机器能采用全局唯一id生成。

​        优点：分布式全局唯一id

​        缺点：需要维护mongodb成本

   5、snowflake

snowflake是Twitter开源的分布式ID生成算法，结果是一个long型的ID。其核心思想是：使用41bit作为毫秒数，10bit作为机器的ID（5个bit是数据中心，5个bit的机器ID），12bit作为毫秒内的流水号（意味着每个节点在每毫秒可以产生 4096 个 ID），最后还有一个符号位，永远是0。

​        优点：分布式全局唯一id，灵活方便，不依赖具体储存工具、趋势递增

​        缺点：实现成本更高、时钟有可能出现不同步