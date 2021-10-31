

[查询文档](https://www.tabnine.com/code/javascript/functions/sequelize/Model/bulkCreate)

[官方文档](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-findOne)

[Sequelize 中文API文档](https://itbilu.com/nodejs/npm/V1PExztfb.html)



# 创建

## 单个创建或更新 - upsert

```js
	const batchRes = biz_waybill_batch.upsert({
		    batchId: batch ? batch.batchId : uuidv4().replace(/-/g, ''),
    		//  upsert - 判断主键，如果存在就更新，不存在就创建
		});
```



## 批量创建 - bulkCreate

```javascript
const res = await biz_waybill.bulkCreate(Array)
```



## 批量创建或更新 - updateOnDuplicate

```sql
const waybillRes = await biz_waybill.bulkCreate(list, {
            updateOnDuplicate: ['id', 'waybillId', 'stationList', 'vin', 'placeId', 'status', 'currStationIdx']
		});
```



# 条件

## 筛选当天数据

```sql
//获取前一天
SELECT * FROM 表名 WHERE create_time = DATE_SUB(CURDATE(),INTERVAL 1 DAY) 

//获取前两天、、、、依次类推
SELECT * FROM 表名 WHERE create_time = DATE_SUB(CURDATE(),INTERVAL 2 DAY) 

//获取当天
// 方法1：SELECT * FROM 表名 WHERE create_time = DATE_SUB(CURDATE(),INTERVAL 0 DAY) 
// 方法2：where update_time > date(now())
/** date(now())是MYSQL获取当天时间的写法，别的数据库不一定适用 **/
```



