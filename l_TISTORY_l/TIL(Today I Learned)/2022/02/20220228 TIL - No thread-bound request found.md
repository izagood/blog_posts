#   No thread-bound request found

##  원인

1. 쓰레드세이프하지 않은 메서드에서 사용
2. 실제 request가 없는 곳에서 사용했을 때
3. static 메서드에서 사용 했을 때

[No thread-bound request found](https://server0.tistory.com/100)