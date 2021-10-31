



# 增加

## 增加column

```sql
# 在table_name中新增routing_name字段
alter table table_name
	add column routing_name varchar(125) not null default '' comment '路由名称' after routing_id,
	add column routing_name varchar(125) not null default '' comment '路由名称' after routing_id;
```





# 更改

## 更改column类型

```sql
# routing_id的类型由INT扩展为VARCHAR类型

alter table biz_send_routing modify routing_id varchar(125);


```



字段值

```mysql
UPDATE biz_station SET name = '1号1' WHERE name = '1号'
```





# 查询



## 查询总数

```sql
select count(*) from sim_ads  ;
```



## 查询指定数量

```sql
select * from vresv_record_history limit 50
```



## 查询多个Id

```sql
select * from biz_waybill where order_id in (21458027891,21456389327,21460894591);

```





# 删除



## 以Select结果作为删除条件

```sql
# 把select结果写在()里面即可
DELETE FROM biz_waybill WHERE order_id in (SELECT order_id FROM (SELECT COUNT(*) as num, order_id, status, min(id) as id FROM biz_waybill GROUP BY order_id,status) e WHERE e.num>1);
```

