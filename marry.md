```
婚礼: wedding
结婚: marry
宾客: guests
预约: reservation
伴侣: lover
亲密度: affinity
```

### 策划配置
1. 新增【结婚】配置表 marry
```
	type, 表示结婚类型
	name, 表示结婚类型名称(永结同心/金玉良缘/神仙眷侣)
	cost, 表示消耗
	reward, 表示获得的奖励
	wedding_type, 表示婚礼档次(配置 wedding 表的type, 0表示没有婚礼)
```

2. 新增【婚宴】配置表 wedding
```
	type, 表示婚礼档次
	time, 表示婚礼时长(单位: 秒)
	free_guests_count, 表示免费宴请人数
	buy_guests_count, 表示最多可增加的宴会宾客人数
	buy_guests_cost, 表示每增加一宴会宾客人数的消耗
	guests_reward, 宴会宾客奖励
```

3. 新增【婚宴预约时间】配置表 wedding_reservation
```
	id, 唯一id，不可修改
	day_begin_time: 相对于每天 00:00:00 开始的秒数
	day_end_time:   相对于每天 00:00:00 结束的秒数
```

4. server_language_cn 增加
```
(1) 宴会宾客奖励邮件标题 lang_type=MARRY, lang_id=GUESTS_REWARD_MAIL_TITLE
(2) 宴会宾客奖励邮件内容 lang_type=MARRY, lang_id=GUESTS_REWARD_MAIL_CONTENT
(3) 提亲成功邮件标题     lang_type=MARRY, lang_id=MARRY_SUCCESS_MAIL_CONTENT
(4) 提亲成功邮件内容     lang_type=MARRY, lang_id=MARRY_SUCCESS_MAIL_CONTENT
(5) 提亲被拒邮件标题     lang_type=MARRY, lang_id=MARRY_FAILED_MAIL_CONTENT
(6) 提亲被拒邮件内容     lang_type=MARRY, lang_id=MARRY_FAILED_MAIL_CONTENT
(7) 婚礼预约成功邮件标题 lang_type=MARRY, lang_id=WEDDING_RESERVATION_MAIL_TITLE
(7) 婚礼预约成功邮件内容 lang_type=MARRY, lang_id=WEDDING_RESERVATION_MAIL_CONTENT
```

5. 配置表 function 新增
(1) MARRY 表示结婚系统
