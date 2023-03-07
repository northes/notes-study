每小时统计一次（传入截止时间）：
OnlinePlayerCount: ommon_trace-server_info
[]
*|set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID), __time__ ... LIMIT 100000000

```
T: PI | SELECT count(1) as pv , date_trunc('hour',__time__) as hour group by hour order by hour limit 1000000
```

TodayActivePlayerCount: player_info

今日活跃玩家的数量

```

```

TodayNewPlayerCount: player_info

今天新增玩家的数量

```
T: PI | SELECT count(1) as pv , date_trunc('hour',__time__) as hour group by hour order by hour limit 1000000
```

TodayActivePlayerShowADCount: advertise
TodayNewPlayerShowADCount: advertise

TodayTriggerEventCount: common_trace-event 

TodaySignCount: common_trace-sign