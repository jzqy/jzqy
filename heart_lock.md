同心锁界面
```
    （1）数据库
	tb_player_detail 增加 heart_lock_level, heart_lock_exp

    （2）策划新增配置
	1.新增表 heart_lock 
	level | exp | attr | lover_attr
	心锁等级 | 升级经验 | 基础属性 | 仙侣加成属性

	2.factors 新增字段 heart_lock_activate_cost = {cost, exp}
	3.factors 新增字段 heart_lock_reinforcing_cost = {cost, exp}

    （3）逻辑
	1.DEFINE新增
		PLAYER_HEART_LOCK_OPT = {
			ACTIVATE = 1, -- 激活
			REINFORCING = 2， -- 强化
		}

	2.新增 gw_player_heart_lock_opt协议
		request = {opt_type}
	
	3.新增 gwi_player_heart_lock_update -- 通知伴侣更新进度, 方便客户端显示红点

	4.新增 UPDATE_DEFINE 
		HEART_LOCK_EXP
		HEART_LOCK_LEVEL

		LOVER_HEART_LOCK_LEVEL
	
	5. gbm_player_update 增加更新同心锁处理, 更新 globalmgr - player_info

```
