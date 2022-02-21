# 오라클 CASE WHEN 표현식 사용법

보통 사용할때 IF문 방식을 주로 사용했는데 SWITCH문 방식도 유용해 보인다.

만족하는 조건이 없으면 NULL을 리턴한다.

## IF 문 방식
```sql
SELECT
    CASE WHEN TEST_COLUMN = '1' THEN '일'
         WHEN TEST_COLUMN = '2' THEN '이'
         ELSE '나머지'
    END AS test
FROM
    TEST_TABLE
```

## SWITCH 문 방식
```sql
SELECT
    CASE TEST_COLUMN
        WHEN '1' THEN '일'
        WHEN '2' THEN '이'
        ELSE '나머지'
    END AS test
FROM
    TEST_TABLE
```


### 참조

[오라클 CASE WHEN 표현식 사용법](https://gent.tistory.com/311)