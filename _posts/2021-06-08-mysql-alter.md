---
title: mysql 컬럼명 변경, 컬럼 타입 변경, 컬럼 추가, 컬럼 삭제
tags: MYSQL QUERY ALTER DATABASE
---
## 컬럼명 변경
ALTER TABLE ```테이블명``` CHANGE ```기존컬럼명``` ```변경할컬럼명``` ```컬럼타입```;
```
mysql> ALTER TABLE user CHANGE score score int;
```

## 컬럼 순서변경
ALTER TABLE ```테이블명``` MODIFY ```기존컬럼명``` ```변경할컬럼명``` ```컬럼타입```;
```
mysql> ALTER TABLE user MODIFY nickname varchar(64) AFTER user_id
```

## 컬럼 디폴트값 변경
ALTER TABLE ```테이블명``` ALTER COLUMN ```변경할컬럼명``` SET DEFALUT ```디폴트값```;
```
mysql> ALTER TABLE user ALTER COLUMN age SET DEFAULT 10;
```

## 컬럼 타입변경
ALTER TABLE ```테이블명``` MODIFY ```컬럼명``` ```변경할컬럼타입```;
```
mysql> ALTER TABLE user MODIFY score varchar(64);
```

## 컬럼 추가
ALTER TABLE ```테이블명``` ADD ```추가할컬럼명``` ```컬럼타입``` DEFAULT ```디폴트값```;
ALTER TALBE ```테이블명``` ADD COLUMN ```추가할컬럼명``` ```컬럼타입``` DEFAULT ```디폴트값``` ```컬럼위치```;
```
mysql> ALTER TABLE klass ADD coast int DEFAULT 100;
mysql> ALTER TABLE klass ADD COLUMN ranking INT(10) DEFAULT 0 AFTER user_id;
mysql ALTER TABLE rank ADD COLUMN test INT(10) DEFAULT 1 FIRST;
```

## 컬럼 삭제
ALTER TABLE ```테이블명``` DROP COLUMN ```컬럼명```;
```
mysql> ALTER TABLE user DROP COLUMN age;
```
---
