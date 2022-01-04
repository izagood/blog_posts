#   2022.01.03_TIL 계획, spring task scheduler

#   TIL 계획

TIL은 Today I Learned의 약자로 오늘 배운 내용을 정리하는 것이다.

매일 배운 내용을 작성만 하고 복습하지 않는다면 의미 없는 기록에 불과하기에 배운 내용을 일정주기로 복습하려고 한다.

주간, 월간, 년간으로 배운 내용을 복습할 예정이고

이를 위해서

**WIL(Weekly I Learned) : 주 단위 복습**  
**MIL(Monthly I Learned) : 월 단위 복습**  
**AIL(Annually I Learned) : 년 단위 복습**  

을 진행하려고 한다.

WIL은 **매주 일요일까지**
MIL은 **매월 마지막주 일요일까지**
AIL은 **매년 마지막월 마지막주 일요일까지** 

작성한다.

점진적으로 복습하여 단순 기록만이 아니라 기억으로도 옮기려고 한다.

---

#   Spring task : scheduler

오랜만에 배치를 수행하여야 하는 개발이 생겼다.

매일 오전 9시에 수행하여야 한다.

일반적으로 배치 수행이라고 하지만 실제로는 Spring Task의 scheduler를 사용한다.

Spring batch가 있으나 batch는 batch Job에 중점을 둔 것 같다.

배치는 spring task scheduler + spring batch로 구성하였다.

quartz 스케줄러를 사용하여 DB 클러스터링도 가능하지만 학습중이다.

참고 : [스케줄러 테스트](https://skout90.github.io/2017/07/07/Spring/scheduler/)

##  cron

크론은 스케줄러를 설정할 떄 일정 주기로 실행하도록 하는 표현식을 말한다.

크론은 아래와 같이 표현되는데 각 자리수는 아래 표와 같은 의미를 가지고 있다.

```
* * * * * * *
```

|초|분|시|일|월|요일|연도|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|0 - 59|0 - 59|0 -23|1 - 31|1 - 12|0 - 6|생략가능



#til #202201 #stream #spring #task #batch #scheduler