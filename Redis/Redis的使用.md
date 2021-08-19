## 一、Redis 键(Key) 构成

```c
typedef struct redisObject { 
	unsigned type:4;//类型 五种对象类型  REDIS_STRING(字符串)、REDIS_LIST (列表)、REDIS_HASH(哈希)、REDIS_SET(集合)、REDIS_ZSET(有序集合)。
	unsigned encoding:4; //编码 4表示位数
	void *ptr;//指向底层实现数据结构的指针,指向具体数据
	//... 
	int refcount;//引用计数 
	//... 
	unsigned lru:LRU_BITS; //LRU_BITS为24bit 记录最后一次被命令程序访问的时间 
        //高16位存储一个分钟数级别的时间戳&#xff0c;低8位存储访问计数&#xff08;lfu &#xff1a; 最近访问次数&#xff09;
	//... 
} robj;
```

1. 查看对象类型 `type key`

   ![image-20210819160437641](../img/redis_01.png)

2. 获取value具体编码 `object encoding key`

3. 查看key的结构信息 `debug object key`

