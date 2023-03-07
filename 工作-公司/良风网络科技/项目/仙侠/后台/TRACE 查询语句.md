
## OnlinePlayerCount: common_trace-server_info
每小时统计一次（传入截止时间）：

> \*|set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID), __time__ ... LIMIT 100000000

```sql
T: SI | SELECT MAX_BY("D",__time__)
```


## TodayActivePlayerCount: player_info

今日活跃玩家的数量

```sql
* | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS player, date_trunc('day', LastActiveDayUpdateTimestamp) AS day GROUP BY day ORDER BY day DESC LIMIT 1
```

每日活跃玩家的数量

```sql
* | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS player, date_trunc('day', LastActiveDayUpdateTimestamp) AS day GROUP BY day ORDER BY day DESC LIMIT 1000000
```

## TodayNewPlayerCount: player_info

今天新增玩家的数量

```sql
* | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS player, date_trunc('day', CreateTimestamp) AS day GROUP BY day ORDER BY day DESC LIMIT 1
```

每日新增玩家数量

```sql
* | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS player, date_trunc('day', CreateTimestamp) AS day GROUP BY day ORDER BY day DESC LIMIT 1000000
```

## TodayActivePlayerShowADCount: advertise

今天活跃玩家观看广告次数

```sql
* | set session parallel_sql=true; SELECT SUM(daytotal) AS daytotal ,date_trunc('day',__time__) AS day GROUP BY day ORDER BY day DESC LIMIT 1000000
```

今天活跃玩家观看广告次数（按照状态分）

```sql

```

## TodayNewPlayerShowADCount: advertise

今天新玩家观看广告次数

```sql
* | set session parallel_sql=true; SELECT SUM(daytotal) AS daytotal ,date_trunc('day', playercreatetimestamp) AS day GROUP BY day ORDER BY day DESC LIMIT 1000000
```

## TodayTriggerEventCount: common_trace-event 

今天触发事件总数

```sql
T: Ev | set session parallel_sql=true; SELECT COUNT(1) AS count, date_trunc('day',__time__) AS day GROUP BY day ORDER BY day DESC LIMIT 1
```

## TodaySignCount: common_trace-sign

今天登录总数

```sql
T: Sg | set session parallel_sql=true; SELECT COUNT(1) AS count, date_trunc('day',__time__) AS day GROUP BY day ORDER BY day DESC LIMIT 1
```