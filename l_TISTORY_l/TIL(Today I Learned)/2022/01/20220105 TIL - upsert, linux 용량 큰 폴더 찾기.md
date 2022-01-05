#   UPSERT : UPDATE + INSERT


##   UPSERT
-   UPSERT : 중복되는 값이 있다면 update 없다면 insert 를 하는 명령어

-   사용법

```sql
INSERT INTO user_refresh_token (user_id, refresh_token)
VALUES (#{userId}, #{refreshToken}) ON DUPLICATE KEY
UPDATE refresh_token = #{refreshToken}
```

-   참조 : [UPSERT](https://devlog-wjdrbs96.tistory.com/365)


##   MERGE INTO
-   merge into : oracle의 경우는 UPSERT명령어가 MERGE INTO 이다.  
    명령어만 다르고 동작은 동일하다.

-   사용법

```sql
MERGE INTO dest_table_name [alias]
            USING (source_table_name or  view or subquery) [alias]
            ON (join condition)
WHEN MATCHED THEN
     UPDATE SET col1 = value1[, col2 = value2…]
WHEN NOT MATCHED THEN
     INSERT [(col1, col2, ... coln)] VALUES(value1, value2 ... valuen)
```

```sql
MERGE INTO tablename USING dual ON ( val3 = in_val3 )
WHEN MATCHED THEN 
	UPDATE SET val1 = in_val1, val2 = in_val2
WHEN NOT MATCHED THEN 
	INSERT VALUES (in_val1, in_val2, in_val3)
```

#   Linux 폴더 용량 큰 순서대로 나열

-   du -sh (경로) 
    해당 경로에 있는 모든 파일용량의 총합을 나타냄. 

-   du -h (경로) |sort -h
    해당 경로에 있는 모든 파일과 폴더의 용량을 용량 단위를 사용하여 표기한다.
    이 때, 표기되는 순서는 폴더 이름 1순위, 파일이름 2순위로 나열되며, 경로 내의 폴더에 있는 폴더에 있는 파일조차 모두 표기된다. (전부 표기)

-   du -h (경로) |sort -h |tail -10
    해당 경로에 있는 모든 파일과 폴더의 용량을 용량 단위를 사용하여 표기한다.
    이 때, 용량이 큰 폴더가 아래로 가게 되며, 해당 경로에서 가장 큰 10개만 아래에서 위로 출력이 된다.

-   find / -type f  -exec du -h {} + | sort -h | tail -30
    전체 경로에서 용량이 가장 큰 파일 30개 나열한다.

-   du -ckxh | sort -nr
    해당 경로에 있는 폴더 및 파일을 문자열의 수치 값에 따라 비교합니다.

-   du -ch (경로) --max-depth=1 |sort -hr
    해당 경로에 있는 폴더 및 파일을 디렉토리 1 기준(숫자가 높을 수록 많이 표기됨. 간략화는 숫자 낮게. 추천 1)으로
    위에서부터 아래로 나열하는 것

-   ls -lh 
    현재 경로의 파일 용량

##  Sort 옵션
-h : human-numeric-sort 파일크기에 따라 정렬한다. du 의 -h 옵션에 대응한다.
-n : numeric-sort 단순히 문자열의 수치 값에 따라 비교한다. K M 이 섞인다.
-r : reverse  역순으로 정렬

##  du 옵션
-s : 옵션은 하위 디렉토리를 보여주지 않으며 하위 디렉토리까지 포함한 전체 용량을 표시해 준다. (총 사용량만 표시한다)
-a : 각 하위 디렉터리에 포함된 파일까지 포함해서 출력함.
-S : 하위 경로를 합쳐서 표기하지말고 나눠서 표기한다.
-h : 용량을 K, M, G와 같은 용량단위로 표기한다.
-c : 모든 파일의 디스크 사용정보를 보여주고 나서 합계를 보여준다

-   df : 시스템에 마운트된 디스크의 사용 정보
    `df -h`

참조 : [폴더 용량 큰 순서대로 나열 명령어](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sung_mk1919&logNo=221495950308)
