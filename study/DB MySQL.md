# DB MySQL

alter table 테이블명 add 컬럼명 타입 옵션;



UPDATE `ssafy`.`keyword` SET `end_date` = '2020-01-31' WHERE (`keyword_no` = '9');



##### 컬럼추가

ALTER TABLE 테이블명 ADD(컬럼명 데이타타입(사이즈));







##### 

## 테이블

#### food

| id   | name     | price | category_no |
| ---- | -------- | ----- | ----------- |
| 1    | 상추     | 3000  | 10          |
| 2    | 복숭아   | 29000 | 20          |
| 3    | 돼지고기 | 15000 | 30          |
| 4    | 고구마   | 10000 | 10          |
| 5    | 소고기   | 54000 | 30          |
| 6    | 딸기     | 18000 | 20          |
| 7    | 사과     | 32000 | 20          |
| 8    | 닭고기   | 19000 | 30          |

#### category

| id   | category_no | category |
| ---- | ----------- | -------- |
| 1    | 10          | 채소     |
| 2    | 20          | 과일     |
| 3    | 30          | 고기     |



## SQL

#### Select

```sql
select col1, col2 from 테이블 
```



#### order by

```sql
select name, price
from food
order by price
```

>상추             3000
>
>고구마       10000
>
>돼지고기   15000
>
>...



#### like

```sql
select name
from food
where name like '%기'
```

> 돼지고기
>
> 소고기
>
> 딸기
>
> 닭고기



```sql
select name
from food
where name like '__기'
```

>소고기
>
>닭고기





#### join

```sql
select name, category
from food
join category
using (category_no);

select name, c.category_no
from food f, category c
where f.category_no = c.category_no;
```

> 상추           채소
>
> 복숭아       과일
>
> 돼지고기   고기
>
> ...



#### group by

```sql
select count(*), category
from food
group by category
```

>
>
>