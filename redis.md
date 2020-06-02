SET     设置一个键值对
GET     获取一个键值对
DEL     删除一个键值对
INCR    将一个键对应的值加一
SETNX   当键不存在时，创建键值对
EXPIRE  设置一个键值对的有效期
TTL     查询一个键值对的剩余有效期，默认值为-1

存储列表
RPUSH
LPUSH
LLEN
LRANGE  获得当前子列表，两个参数分别表示起始和终止，第二个参数设置为-1表示到末尾,下标从0开始
LPOP
RPOP


存储集合
SADD
SREM
SISMEMBER
SMEMBERS
SUNION

有序集合
ZADD
ZRANGE等
