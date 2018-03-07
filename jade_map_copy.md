东海宝阁（灵玉副本）
# 策划配置
```
1. 新增东海宝阁副本配置
	(1) 副本的类型为 20
	(2) 按波数配置
		a. 进入战斗阶段立即刷出的怪配置为 第一波
		b. 采集完所有宝箱才刷出的怪配置为 第二波

2. collection 表新增 avatar_type 字段, 并增加采集宝箱的配置
	(1) 新增加宝箱的 avatar_type 为 19
	(2) 原来已有的记录 avatar_type 配置为 10

3. 宝箱奖励配置需要(区分开两种)
	(1) factors 表新增配置 jade_map_copy_treasure_reward, 配置格式, { [collect_item_id] = {reward}, .... }
	注: collect_item_id 为采集宝箱对应配置的 collect_item_id, reward 按奖励格式配置
```

# 开发逻辑修改
```
1. 新增灵玉副本
	(1) define.lua - MAP_TYPE 新增 JADE_MAP_COPY = 20, -- 灵玉副本(单人副本)
	(2) BOSS需要采完所有宝箱才刷出

2. cl_map_copy_info.lua 需要根据 DEFINE.MAP_TYPE.JADE_MAP_COPY 序列化以下字段
	(1) 采集宝箱数量 - monster_treasure_count
	(2) 击杀小怪数量 - monster_killed_count
	(3) 击杀BOSS数量 - boss_killed_count

3. 新增采集宝箱类型 avatar_type = AVATAR_TYPE_MONSTER_TREASURE = 19
	(1) 参考 rob_treasure 的实现, 提供 collect_start, collect_stop 接口, 增加周围有怪不能采集的限制
	(2) ce_rob_treasure_collect_oper 改为 ce_treasure_collect_oper(天灵夺宝和采集宝箱 cellapp 共用同一个逻辑)
	(3) 采集协议在 gateway 新增协议 gw_monster_treasure_collect_oper(需要先判断玩家背包是否已满)
	(4) 创建宝箱时, 传入 callback
	(5) 宝箱被采集完时, 回调 callback->on_collect_stop(self) (用于处理boss出生的逻辑 & 副本信息采集箱子个数的显示)
```
