每小时统计一次（传入截止时间）：
OnlinePlayerCount: ommon_trace-server_info
[]
*|set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID), __time__ ... LIMIT 100000000

TodayActivePlayerCount: player_info


TodayNewPlayerCount: player_info

今天新增玩家的数量

```
* | T: PI 
```

TodayActivePlayerShowADCount: advertise
TodayNewPlayerShowADCount: advertise

TodayTriggerEventCount: common_trace-event 

TodaySignCount: common_trace-sign