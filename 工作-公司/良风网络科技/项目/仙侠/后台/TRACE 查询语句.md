
## OnlinePlayerCount: common_trace-server_info

在线玩家数量

```sql
T: SI | set session parallel_sql=true; SELECT MAX_BY("D",__time__)
```

## TodayActivePlayerCount: player_info

今日活跃玩家的数量

```sql
* | set session parallel_sql=true; SELECT COUNT(PlayerID) AS PlayerCount LIMIT 10000000
```

## TodayNewPlayerCount: player_info

今天新增玩家的数量（CreateTimestamp 为玩家账号创建的时间）

```sql
CreateTimestamp >= %d AND CreateTimestamp <= %d | set session parallel_sql=true; SELECT COUNT(PlayerID) AS PlayerCount LIMIT 10000000
```

## TodayActivePlayerShowADCount: advertise

今天活跃玩家观看广告次数

```sql
OpID = 0 | set session parallel_sql=true; SELECT COUNT(PlayerID) AS TotalViewAdCount LIMIT 100000;
```

今天活跃玩家观看广告次数（按照状态查）

```sql
OpID = 3 or OpID = 4 or OpID = 5 or OpID = 6 | set session parallel_sql=true; SELECT COUNT(PlayerID) AS TotalViewAdCount,OpID GROUP BY OpID  LIMIT 100000;
```

## TodayNewPlayerShowADCount: advertise

今天新玩家观看广告次数

```sql
OpID = 0 AND CreateTimestamp >= %d AND CreateTimestamp <= %d | set session parallel_sql=true; SELECT COUNT(PlayerID) AS TotalViewAdCount LIMIT 100000;
```

今天新玩家观看广告次数（按状态查）

```sql
(OpID = 3 or OpID = 4 or OpID = 5 or OpID = 6) AND CreateTimestamp >= %d AND CreateTimestamp <= %d | set session parallel_sql=true; SELECT COUNT(PlayerID) AS TotalViewAdCount,OpID GROUP BY OpID LIMIT 100000;
```

## TodayTriggerEventCount: common_trace-event 

今天触发事件总数

```sql
T: Ev | set session parallel_sql=true; SELECT COUNT(1) AS TotalEventCount LIMIT 100000
```

## TodaySignCount: common_trace-sign

今天登录总数

```sql
T: Sg | set session parallel_sql=true; SELECT COUNT(1) AS TotalSignCount LIMIT 100000
```