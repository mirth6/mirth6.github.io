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
| 2    | 태블릿   | 99999 | 40          |
| 3    | 복숭아   | 29000 | 20          |
| 4    | 돼지고기 | 15000 | 30          |
| 5    | 고구마   | 10000 | 10          |
| 6    | 소고기   | 54000 | 30          |
| 7    | 딸기     | 18000 | 20          |
| 8    | 사과     | 32000 | 20          |
| 9    | 닭고기   | 19000 | 30          |

#### category

| id   | category_no | category |
| ---- | ----------- | -------- |
| 1    | 10          | 채소     |
| 2    | 20          | 과일     |
| 3    | 30          | 고기     |
|      |             |          |



## SQL

#### Select

```sql
select col1, col2 from 테이블 
```



#### distinct

: 중복제거

```sql
select distinct category_no
from food
```

>10  
>
>20
>
>30



#### order by

: 정렬

```sql
-- 가격기준 오름차순으로 정렬
select name, price
from food
order by price asc				-- 오름차순 asc, 내림차순 desc
```

>상추             3000
>
>고구마       10000
>
>돼지고기   15000
>
>...



#### join

1. inner join

```sql
select name, category
from food
join category
using (category_no);		 	  	-- join할 칼럼, alias사용 X

select name, category
from food f
join category c
on f.category_no = c.category_no;	-- join 조건

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



2. outer join

```sql
select name, food.category_no, category
from food
left outer join category
using (category_no);
```

>상추           10     채소
>
>태블릿       40
>
>복숭아       20     과일
>
>돼지고기   30     고기
>
>...



#### group by

```sql
-- 카테고리별 평균 가격이 10000보다 큰 상품 조회
select category_no, count(*), avg(price)
from food
group by category_no
having avg(price) > 10000			//group by의 조건절
```

>20    3    26333
>
>30    3    29333





#### subQuery

1. where절 subQuery

```sql
--사과와 같은 category_no를 가지고 있는 상품의 이름과 category_no를 출력
select name, category_no
from food
where category_no = (select category_no 
                     from food 
                     where name='사과')
```

>복숭아  20
>
>딸기      20
>
>사과      20



2. from절 subQuery

```sql
-- category_no가 20인 상품중에 price가 30000원 보다 큰 상품 출력
select name, category_no, price
from (select * from food where category_no = 20)
where price < 20000
```

> 딸기     20    18000







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



