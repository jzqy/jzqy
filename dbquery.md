打开 `Navicat Premium` 工具, 打开对应游戏服数据库，点击 `查询` -> `新建查询`    

|查询内容|SQL|  
|------|---|
|玩家 vip 等级和过期时间|select id, vip_level, FROM_UNIXTIME(vip_time) as vip_time_out from tb_player where id = xxx;|
