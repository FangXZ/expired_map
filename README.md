# ExpiredMap
golang写的带有超时性质的map，可以给key设置存活时间，超期就会自动删除。
时间精度：秒级

# key过期策略：
  采用主动删除+被动删除的策略。
  - 每隔一秒删一次过期的key。
  - 用户访问该key时，判断是否过期，过期则删除。

# 适用场景：
  - 服务local cache，服务local cache会比使用redis缓存更为快速，有过期机制不会使内存持续增长。
  - 数据定期刷新，如每隔x分钟刷新一次榜单的逻辑，可以设置key过期时间为x分钟，每次Get判断有缓存，则用这些数据；如果没有缓存，则去db加载，set到缓存并设置过期时间。
