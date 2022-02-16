# oracle lock mode

오라클에 lock이 걸려있을때 어떤 유형의 lock이 발생하였는지 

LOCKED_MODE 로 알 수 있다.

---

Lock mode. The numeric values for this column map to these text values for the lock modes for table locks:

0 - NONE: lock requested but not yet obtained

1 - NULL

2 - ROWS_S (SS): Row Share Lock

3 - ROW_X (SX): Row Exclusive Table Lock

4 - SHARE (S): Share Table Lock

5 - S/ROW-X (SSX): Share Row Exclusive Table Lock

6 - Exclusive (X): Exclusive Table Lock

See Also: Oracle Database Concepts for more information about lock modes for table locks

### 참조

[8.39 V$LOCKED_OBJECT](https://docs.oracle.com/database/121/REFRN/GUID-3F9F26AA-197F-4D36-939E-FAF1EFD8C0DD.htm#REFRN30125)

#   DB 모니터링

toad, orange

