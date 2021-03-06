#   YAML, Docker

---

#   YAML

##  정의
XML, C, 파이썬, 펄, RFC2822에서 정의된 e-mail 양식에서 개념을 얻어 만들어진 '사람이 쉽게 읽을 수 있는' 데이터 직렬화 양식

##  요소
-   YAML 문자열은 UTF-8 또는 UTF-16과 같이 출력 가능한 유니코드 문자집합을 이용
-   공백 문자를 이용한 들여쓰기로 구조체를 구분한다. 그러나 탭문자를 들여쓰기에 사용하지 않는다.
-   **리스트**는 여러 줄에 쓸 때에는 하이픈(-)으로 시작하는 한 줄에 하나의 요소를 표현
    -   한 줄에 모아 쓸 때에는 대괄호([])를 이용하며 쉼표로 각 요소를 구분

```yaml
 --- # Favorite movies, block format
 - Casablanca
 - Spellbound
 - Notorious
 --- # Shopping list, inline format
 [Casablanca, Spellbound, Notorious]
```

-   **해쉬**는 콜론 기호를 이용해서 키:값의 형태로 한 줄에 하나를 표현하거나, 한 줄에 모아 쓸 때에는 중괄호({})를 이용하며 쉼표로 각 요소를 구분한다.

```yaml
 --- # Block
 name: John Smith
 age: 33
 --- # Inline
 {name: John Smith, age: 33}
```

-   간단한 값(스칼라 값)은 보통 아무 표시를 하지 않으나 따옴표("")나 작은 따옴표('')를 이용해 둘러쌀 수 있다.
-   따옴표 안에서 특수 문자는 C언어 스타일(역슬래쉬키와 함께쓰이는 제어문자 예. \n)로 표시
-   블록 값은 보존(|) 또는 접기(>)의 선택 지시자로 나눈다


### 참조
[YAML](https://ko.wikipedia.org/wiki/YAML)

---
#   Docker

##  WSL2
-   wsl 2 기반 엔진을 사용 하도록 설정 하면 동일한 컴퓨터의 Docker Desktop에서 Linux 및 Windows 컨테이너를 모두 실행할 수 있다
