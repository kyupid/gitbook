# Tips



#### 컬럼 생성시에 DATETIME 타입 default로 현재시간 주는 방법

```sql
create table hello (
  dt datetime default CURRENT_TIMESTAMP not null
)
```

* 5.6버전이상에서만 동작함
