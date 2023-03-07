
## OnlinePlayerCount: ommon_trace-server_info
每小时统计一次（传入截止时间）：

> \*|set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID), __time__ ... LIMIT 100000000

```
T: Si
```



## TodayActivePlayerCount: player_info

今日活跃玩家的数量

```sql
* | select count(DISTINCT PlayerID) as player, date_trunc('day', LastActiveDayUpdateTimestamp) as day group by day order by day desc limit 1
```

每日活跃玩家的数量

```sql
* | select count(DISTINCT PlayerID) as player, date_trunc('day', LastActiveDayUpdateTimestamp) as day group by day order by day desc limit 1000000
```

## TodayNewPlayerCount: player_info

今天新增玩家的数量

```sql
* | select count(DISTINCT PlayerID) as player, date_trunc('day', CreateTimestamp) as day group by day order by day desc limit 1
```

每日新增玩家数量

```sql
* | select count(DISTINCT PlayerID) as player, date_trunc('day', CreateTimestamp) as day group by day order by day desc limit 1000000
```

## TodayActivePlayerShowADCount: advertise

今天活跃玩家观看广告次数

```sql

```

## TodayNewPlayerShowADCount: advertise

今天新玩家观看广告次数

```sql

```

## TodayTriggerEventCount: common_trace-event 

今天触发事件总数

```sql
T: Ev | select count(1) as count, date_trunc('day',__time__) as day group by day order by day desc limit 1
```

## TodaySignCount: common_trace-sign

今天登录总数

```sql
T: Sg | select count(1) as count, date_trunc('day',__time__) as day group by day order by day desc limit 1
```