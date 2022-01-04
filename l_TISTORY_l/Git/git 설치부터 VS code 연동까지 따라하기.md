#   순서
1.  git 설치 및 초기 설정
1.  github repository(저장소) 생성
1.  github VS Code 연동 


#   1. git 설치 및 초기 설정
-   git : 버전(형상) 관리 시스템이다.

##  설치방법

1. [git 다운로드](https://git-scm.com/downloads "깃 다운로드")

1.  다운로드 받은 git 설치
    1.  아래 선택 사항 이외에는 (Recommended) next 클릭
    1.  editor : use Vim ~
        -   vim에 익숙해지도록 선택
    1.  new repositories : Override the default branch ~~ 선택 -> main -> next 
        -   github에서는 master/slave에 대한 표현이 노예제를 연상시키므로 중립적인 의미인 main을 master 대신 사용하고 있다.
    1.  HTTPS : OpenSSL library
    1.  line ending : Windows-style
    1.  emulator : MinTTY
    1.  git pull : Default
    1.  credential helper : Git Credential Manager Core
    1.  experimental options : 선택 안함

1.  git 설치 되었는지 확인
    -   Win키 + R -> cmd
    ```cmd
    $ git --version
    ```
    -   버전이 출력되었다면 정상적으로 설치되었다.

1.  git 초기 설정
    -   git을 설치하고 아래 설정의 최초 1회 해야한다.  

    -   **이름_입력**, **이메일_입력** 부분만 수정한다.  
    ```
    $ git config --global user.name "이름_입력"
    $ git config --global user.email 이메일_입력
    ```

    참조 : [git 초기 설정 링크](https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)


#   2. github repository(저장소) 생성
-   [github](https://github.com/ "github") : git 저장소의 호스팅 웹 서비스  

1.  github 접속하여 계정 생성 또는 로그인

1.  계정 프로필 확인
    1.  오른쪽 상단 클릭
    1.  Your profile 클릭
    1.  github 계정의 전반적인 상황을 볼 수 있다.

1.  저장소(repository) 생성
    1.  오른쪽 상단 2번째 '+' 버튼 클릭
    1.  New repository
    1.  Repository name 입력
    1.  public / private 선택
        -   public : 모두에게 공개되는 저장소
            -   다른 사람과 공유하기 위한 정보
            -   오픈소스 프로젝트 등
        -   private : 나만 볼 수 있는 저장소
            -   개인적으로 정리하는 정보
            -   개인적인 프로젝트 등
    1.  Add a README file
        -   저장소에 대한 설명서
    1.  Create repository

-   git의 자주 사용되는 명령어 링크 : [git cheat sheet](https://training.github.com/downloads/ko/github-git-cheat-sheet/)  

-   github commit history (a.k.a. 잔디심기)  
    블로그와 함께 개발자의 학습 정도를 파악하기 위해 자주 참조한다.  

    commit history를 외부 웹사이트에 쉽게 삽입할 수 있는 API도 있다. ( [gschart API](https://ghchart.rshah.org/izagood) )


#   3. github VS Code 연동
-   [VS code 다운로드](https://code.visualstudio.com/download)

1.  VS code 설치하기
    -   다운로드 받은 설치파일을 next로 단순 설치

1.  github 연동하기

    1.  왼쪽 하단 사람 아이콘 클릭
    1.  github 아이디로 로그인
    1.  브라우저에서 권한 수락

1.  github 저장소 clone 하기 : 로컬로 가져오기

    1.  Ctrl+Shift+P 단축키
    1.  Git : Clone 선택
    1.  원하는 저장소(repository) 선택
        1.  또는 Clone 하고자 하는 저장소에서 Code(초록 버튼) 클릭
        1.  HTTPS url 복사
        1.  저장소 입력창에 붙여넣기

---

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