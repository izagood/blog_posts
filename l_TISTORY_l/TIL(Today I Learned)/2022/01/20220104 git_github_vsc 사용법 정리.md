#   1. git
-   git : 버전(형상) 관리 시스템이다.

##  설치방법

1. [git 다운로드](https://git-scm.com/downloads "깃 다운로드")

1.  git 설치

1.  git 초기 설정
    -   git을 설치하고 아래 설정의 최초 1회 해야한다.  

    -   **이름_입력**, **이메일_입력** 부분만 수정한다.  
    ```
    $ git config --global user.name "이름_입력"
    $ git config --global user.email 이메일_입력
    ```

    참조 : [git 초기 설정 링크](https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)


#   2. github
-   github : git 저장소의 호스팅 웹 서비스  

[깃허브](https://github.com/ "github")  

-   git의 자주 사용되는 명령어 링크 : [git cheat sheet](https://training.github.com/downloads/ko/github-git-cheat-sheet/)  

-   github commit history (a.k.a. 잔디심기)  
    블로그와 함께 개발자의 학습 정도를 파악하기 위해 자주 참조한다.  

    commit history를 외부 웹사이트에 쉽게 삽입할 수 있는 API도 있다. ( [gschart API](https://ghchart.rshah.org/izagood) )  


#   3. VS Code github 연동

1.  왼쪽 하단 사람 아이콘 클릭
1.  github 아이디로 로그인
1.  브라우저에서 권한 수락
1.  Ctrl+Shift+P 단축키로 Git : Clone 


#   VS Code 단축키

VS Code의 단축키는 extensions로 eclipse의 단축키로 변경하지 않고 그대로 사용하는 것이 좋은 것 같다.  

eclipse를 제외하고는 sublime text에서부터 사용된 단축키를 많이 사용하기 때문에  

VS Code의 단축키에 익숙해지면 코딩 테스트 사이트들의 에디터 단축키에 자동으로 익숙해진다.  

##  VS Code의 특이한 단축키

### e.g. 모두 저장 (Ctrl+K -> S)

모두 저장의 경우 Ctrl + K -> S 인데 한글인 경우 ㄴ이 입력된다.  

왼쪽 아래
```
(Ctrl+K) was pressed. Waiting for second key of chord...
```
같은 상태이면 영문으로 변경 후 S 를 입력하면 모두 저장된다.  

####    단축키 검색창
Ctrl + K -> Ctrl + S 를 입력하면 단축키 검색창이 열린다.  

---

#   DB Lock
-   Lock은 트랜잭션 처리의 순차성을 보장하기 위한 방법

-   공유 Lock
    -   공유 lock 끼리는 동시 접근 가능
-   베타 Lock
    -   데이터를 변경할 때 사용
    -   베타 lock은 해제될 때까지 다른 트랜젝션(읽기 포함)이 해당 리소스에 접근할 수 없다.

참조 : [DB Lock](https://sabarada.tistory.com/121)


#   트랜젝션
-   DB는 트랜젝션 단위로 처리된다.


참조 : [트랜젝션과 격리성](https://sabarada.tistory.com/117)