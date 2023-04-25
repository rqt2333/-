### 1.distinct去重

对包含重复数据的列进行去重

```sql
select distinct(university)
from user_profile
```



### 2.limit

用于限制查询结果返回的行数。

```sql
select * from table order by id limit i,n;
```

i 是偏移量，SQL的结果集从0开始计算。

n是条数，意思是从偏移量索引下标开始取n条数据。

如：

```sql
select * from table 10,10
```

表示从下标10开始（包括10），取10个数据。

在开发中，我们经常需要用到分页，前端通常会传过来两个参数：**页码（pageNumber），每页显示的条数（pageSize）**，根据需求，sql分页语句应该如下：

```sql
select * from table order by id limit (pageNumber-1)*pageSzie,pageSize;
```

对于数据量不大的情况下，这种方式的查询速度相对可以，但是如果数据量大的话，比如说需要查询从第10000行到后面的10条数据，这样的情况下，偏移量很大，SQL会扫描`i+n` 条记录，无疑是非常影响性能的。

为此，我们有了下面的方法：

* **建立主键索引或唯一索引** 

  ```sql
  select * from table where id > (pageNumber-1)*pageSize order by id limit pageSize;
  ```

  比如说id是主键，从1开始，我们要查询1000-1050之间的数据，实际上是查询id 从 1001 开始到id为1050之间的数据，这样的话SQL会走索引，从而提高效率。



### 3.as关键字

as关键字的作用是为列名或者表重新命名。

```sql
select device_id as user_infos_example
from user_profile limit 0,2
```



### 4.where关键字

where用于过滤一些条件。



### 5. between  ...  and    ...

表示包含。要注意：**在mysql中，  between   and   语句是闭区间**。 但是在别的数据库就不一定了。

```sql
select device_id,gender,age
from user_profile
where age between 20 and 23 
```



### 6.！=  

表示不等于。

```sql
select device_id ,gender,age ,university
from user_profile
where university != '复旦大学'
```



### 7. is  null   ,is  not null

过滤空值的操作。在MySQL中，有以下的方法来过滤空值：

```sql
where 列名 is not null
where 列名 ！= ''
where 列名 ！= 'null'
where 列名  <> ''
where 类名  <> 'null'
```



### 8. or 跟 and

and 要求都满足，or 要求只要有一个满足就行了。

```sql
select device_id ,gender, age,university,gpa
from user_profile
where gender = 'male' and gpa > 3.5


select device_id,gender,age,university,gpa
from user_profile
where university = '北京大学' or gpa >3.7
```



### 9. in 跟 not in

in：选出符合集合中的元素的数据

not：跟上面相反

```sql
select device_id,gender,age,university,gpa
from user_profile
where university in('北京大学','复旦大学','山东大学')

```



### 10.like 模糊查询

模糊查询。

```sql
select device_id,age,university
from user_profile
where university like '%北京%'
```

注意差别：

* %在最前面，比如说`%北京` ，表示以“北京”结尾的字符串。
* %在最后面，比如说`北京%` ，表示以“北京”开头的字符串。
* %前面和后面都有，比如说`%北京%`  ，表示匹配中间存在“北京”的字符串。当然%也可以表示匹配0个。



### 11.max 和 min 函数

max(列名)：返回一组中的最大值

min(列名)：返回一组中的最小值

```sql
select max(gpa) 
from user_profile
where university = '复旦大学'
```



### 12.count()和avg()函数

count(列名)：返回符合条件的行数。默认情况下计算全部，包括重复值，如果不想重复，可以使用`distinct` 指定。

avg()：返回平均数。

```sql
select count(gender) as male_num,avg(gpa) as avg_gpa
from user_profile
where gender = 'male'
```



### 13. group by分组

用于分组。后面可以接多个字段，按照字段顺序来排序，比如`group by a1,a2` 则表明先按照a1分组，然后按照a2 分。

```sql
select
    gender,
    university,
    count(*) as user_num,
    avg(active_days_within_30) as avg_active_day,
    avg(question_cnt) as avg_question_cnt
from
    user_profile
group by
    gender,
    university
```



注意：**`where` 字句只能用在 group by 前面，group by后面如果要筛选条件的话用`having`** 。

同时还要注意：**如果使用 group by，那么 select 后面跟的字段要跟 group by后面的字段一样。不然会报错。**如果select 后面有聚合函数的话，那么不会报错。



### 14.round函数

用于把数值字段舍入为指定的小数位数。

```sql
select
    university,
    round(avg(question_cnt), 4) as avg_question_cnt    /* 小数点后保留4位数字  */
from
    user_profile
group by
    university
order by
    avg_question_cnt ASC

```



### 15.order by排序

对指定的字段进行排序，可以跟多个字段，按照顺序来排序。

* ASC：升序，默认的排序规则
* DESC：降序



### 16.union all 跟union 

* **union  all** ：将两个结果集进行并集操作，**结果不去重**。

  ```sql
  select
      device_id,
      gender,
      age,
      gpa
  from
      user_profile
  where
      university = '山东大学'
  union all
  select
      device_id,
      gender,
      age,
      gpa
  from
      user_profile
  where
      gender = 'male'
  
  ```

* **union**  :将两个结果集进行并集操作，**结果去重**。

需要注意：**使用union all 或者 union 的时候，需要两边的结果集的列数是一样的，否则报错。** 

从执行效率上来讲，union all比 union 效率要快，因为没有去重操作。



### 17.if函数

IF(条件表达式,值1,值2)。如果条件表达式为true，返回值1，否则返回值2。

```sql
select if(age>=25,"25岁及以上","25岁以下") as age_cut,
count(device_id) as number
from user_profile
group by age_cut
```

| age_cut    | number |
| ---------- | :----: |
| 25岁以下   |   4    |
| 25岁及以上 |   3    |



### 18. case when 函数

```sql
select
    (
        case
            when age >= 25 then '25岁及以上'
            else '25岁以下'
        end
    ) as age_cut,
    count(device_id)
from
    user_profile
group by
    age_cut

```



### 19.year(),month(),day()函数

根据日期获取对应的年，月，日。

```sql
select
    day (date) as day,
    count(*) as question_cnt
from
    question_practice_detail
where
    year (date) = '2021'
    and month (date) = '08'
group by
    day

```





### 20.substring_index()函数

substring(字符串，分隔符，计数) 。

```sql
substring_index(www.wikbit.com,'.',1)    /* 结果是www */
substring_index(www.wikbit.com,'.',2)    /* 结果是www.wikbit */

substring_index(www.wikbit.com,'.',-1)    /* 结果是com */
substring_index(www.wikbit.com,'.',-2)    /* 结果是wikbit.com */
```

如果计数是正数，那么代表从左往右数，第N个分隔符左边的所有内容。

如果计数是负数，那么代表从右往左数，第N个分隔符右边的所有内容。



### 21.





















