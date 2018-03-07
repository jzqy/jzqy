# 策划增加配置
```
1. 新增盘丝妖洞副本配置
	(1) 副本的类型为 19 
	(2) 盘丝妖洞副本的【逃跑怪】mapcopy_monster 中 avatar_type 应配置为 18
	(3) 按波数配置怪(程序缓存某一波的所有怪, 并按每种怪物个数, 随机生成怪物序列, 定时刷怪时, 直接读取序列)

2. factors 新增配置
	(1) cloak_map_copy_vertigo 配置【眩晕】花费, 按消耗格式配置
	(2) cloak_map_copy_refresh_monster_seconds 配置副本每只怪的刷新间隔
	(3) cloak_map_copy_wave_seconds 配置副本每波的间隔
	(4) cloak_map_copy_opt_buffer_id 配置眩晕操作给怪物增加的 buffer_id 
```

# 开发逻辑修改
```
1. 新增披风副本
	(1) define.lua - MAP_TYPE 新增 CLOAK_MAP_COPY = 19, -- 披风副本(单人副本)
	(2) cloak_map_copy 需要保存 monster_run_away_count -- 怪物逃跑数量, 用于结算星级
	(3) 新增【眩晕】副本操作 define.lua - MAPCOPY_OPER_TYPE 新增 CLOAK_MAP_COPY_VERTIGO
		a. 副本需要缓存 眩晕操作的最后使用时间
		b. 使用眩晕后, 给场景所有怪物加【眩晕】buffer
		c. 使用眩晕后, 不会刷新的怪物(直至眩晕结束)
	(4) 程序缓存某一波的所有怪, 并按每种怪物个数, 随机生成怪物序列, 定时刷怪时, 直接读取序列

2. cl_map_copy_info.lua 需要根据 DEFINE.MAP_TYPE.CLOAK_MAP_COPY 序列化以下字段
	(1) 怪物逃跑数量 - monster_run_away_count
	(2) 眩晕操作的最后使用时间 - vertigo_last_time

3. 新增【怪物】avatar_type = AVATAR_TYPE_RUN_AWAY_MONSTER = 18 (实际加载到场景为 AVATAR_TYPE_MONSTER), 
 (1) 此类型怪物出生后, 不会攻击玩家, 试图从出口逃跑消失
 (2) 创建怪物时，传入目的地坐标 & callback
 (3) 怪物至达指定地点后，消失， 并回调 callback->on_reach_dest_pos()

```
