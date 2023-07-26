- 雪花算法
- ULID
- UUID
- Leaf [GitHub - Meituan-Dianping/Leaf: Distributed ID Generate Service](https://github.com/Meituan-Dianping/Leaf)   美团分布式ID生成服务



## 方案

1. 独立的ID生成服务，下游服务从中拿取ID
2. 使用分布式ID生成算法，雪花算法等
3. 手动实现，将时间戳放在ID前面，后面加上随机算法等（应对需求为ID递增的场景）（实现：ULID）
4. 使用DB自增ID
5. 使用 redis 自增序列