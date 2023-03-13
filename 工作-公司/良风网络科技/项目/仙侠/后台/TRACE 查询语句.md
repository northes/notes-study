
## OnlinePlayerCount: common_trace-server_info

在线玩家数量

```sql
T: SI | set session parallel_sql=true; SELECT MAX_BY("D",__time__)
```

## TodayActivePlayerCount: player_info

今日活跃玩家的数量

```sql
* | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS PlayerCount LIMIT 10000000
```

## TodayNewPlayerCount: player_info

今天新增玩家的数量（CreateTimestamp 为玩家账号创建的时间）

```sql
CreateTimestamp >= %d AND CreateTimestamp <= %d | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS PlayerCount LIMIT 10000000
```

## TodayActivePlayerShowADCount: advertise

今天活跃玩家观看广告次数（按照状态查）

```sql
OpID = 0 OR OpID = 3 OR OpID = 4 OR OpID = 5 OR OpID = 6 | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS TotalViewAdCount,OpID GROUP BY OpID  ORDER BY OpID LIMIT 100000;
```

## TodayNewPlayerShowADCount: advertise

今天新玩家观看广告次数（按状态查）

```sql
(OpID = 0 OR OpID = 3 OR OpID = 4 OR OpID = 5 OR OpID = 6) AND playercreatetimestamp >= %d AND playercreatetimestamp <= %d | set session parallel_sql=true; SELECT COUNT(DISTINCT PlayerID) AS TotalViewAdCount,OpID GROUP BY OpID LIMIT 100000;
```

## TodayTriggerEventCount: common_trace-event 

今天触发事件总数

```sql
T: Ev | set session parallel_sql=true; SELECT COUNT(1) AS TotalEventCount LIMIT 100000
```

## TodaySignCount: common_trace-sign

今天签到总数

```sql
T: Sg | set session parallel_sql=true; SELECT COUNT(1) AS TotalSignCount LIMIT 100000
```

## PlayerDungeonLevel: player_info

统计某天创建的玩家的通关进度

> CreateTimestamp 为玩家创建时间

```sql
CreateTimestamp >= %d AND CreateTimestamp <= %d  | select count(DISTINCT PlayerID) as PlayerCount ,DungeonMainLevel group by DungeonMainLevel order by DungeonMainLevel
```

新版：

```sql
CreateTimestamp >= %d AND CreateTimestamp <= %d  | set session parallel_sql=true; SELECT PlayerID,max(DungeonMainLevel) AS MaxLevel GROUP BY PlayerID ORDER BY MaxLevel LIMIT 1000000
```

拿到数据后用 go 统计总数