# Spring 환경세팅 및 설명

##

## 1. 초기세팅 및 다운로드

https://start.spring.io 여기서 편하게 프로젝트 초기 세팅 가능함

### 1.1 https://start.spring.io 접속

### 1.2 각종 세팅

- 그래들 선택
- java 선택
- 버전 선택 (뒤에 알파뱃같은거 안붙는 최신버전을 선택했다.)
- Group적는다 (나는 com.sghaha 로 했다)
- Artifact적는다 (나는 Jpabook 으로 했다)

### 1.3 Dependencies 추가

- spring web
- thymeleaf
- jpa
- h2 (mysql사용할거면 이거 안해도됨)
- validation
- lombok

### 1.4 다운로드

generate를 누르면 다운로드 받아진다. 적당한 곳에 압축풀어준다.

##

##

## 2. 인텔리제이 import

나의 환경 : 인텔맥 + 인텔리제이 엔터프라이즈 (프록시환경 아님)

### 2.1 인텔리제이 실행

### 2.2 Open - 아까받은 - build.gradle 파일 연다

### 2.3 open as Project

처음 열면 라이브러리 다운로드 엄청 한다.

### 2.4 대충 설명

- .idea 파일 : 인텔리제이가 사용하는 설정파일
- build.gradle : start.spring.io에서 설정한 디펜던시들이 적혀있는걸 볼 수 있다.
- 로그 날길때 logback + slf4j조합으로 많이들 남기는데, 이 두개는 spring-starter-logging에 들어있고 그건또 spring-starter에 들어있다.
- resources/static/index.html 여기가 welcome 페이지 이다. (근데 잘 안쓸듯)
- 참고 : spring-boot-devtools를 설치하면 대충 서버 재시작 없이해도된다는데 난 적용안함.

##

##

## 3. Github

### 3.1 깃헙에 레포지토리 생성

꼭 README.md 파일 '없이'만든다.   
퍼블릭/프라이빗은 본인 선택

### 3.2 first 커밋

아마 아래와 비슷하게 repo화면에 뜰거다 그걸 복사해서   
인텔리제이 터미널에서 날리자.    
jpabook디렉토리에서 날리자

```
echo "# jpabook" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/sghaha/jpabook.git
git push -u origin main
```

제대로 되었다면 repo에 README.md파일 하나 푸시 되었을 것이다.

### 3.3 나머지 파일 푸시

대충 인텔리제이 Commit탭에서 하면된다.

##

##

## 4. Lombok 플러그인 설치

- 세팅에서 plugins 들어가서 lombok찾아서 enable되어있나 확인
- 세팅에서 annotation processors찾아서 enable annotation processors 체크 한다.

##

##

## 5.코딩 컨벤션 적용하기

### 5.1 다운로드

https://github.com/google/styleguide intellij-java-google-style.xml 다운로드

### 5.2 적용

- File > Settings...(Ctrl + Alt + S) > Code Style > 톱니바퀴 선택 > Import Scheme > IntelliJ IDEA code
  style XML을 선택
- 적용한 Code Style을 확인한 후 Apply 버튼을 클릭

- File > Settings...(Ctrl + Alt + S) > Code Style > Java > Tabs and Indents에서 Tab Size와 Indent를 4로
  수정한 후 Apply 버튼을 클릭
  use tab character 체크

- 검사할때는 옵션+커맨드+L

### 5.3 저장할 때 자동 적용되게

- Setting - Tools - Actions on Save 에 Reformat Code체크

##

##

## 6. 빌드하는법

### 6.1 빌드

```
./gradlew build
```

/build/libs 에 빌드됨

### 6.2 빌드된걸 실행

```
java -jar hello-spring-0.0.1-SNAPSHOT.jar
```

##

##

## 7. 의존관계 살펴보기

그래들 의존관계를 살펴볼땐 아래의 명령어를 날려보자

```
./gradlew dependencies —configuration compileClasspath
```

##

##

## 8. View

나중에는 스프링을 백엔드로만 쓸거라 프론트엔드를 따로 만들겠지만   
여기선 임시로 Thymeleaf를 쓸 거다.   
JSP랑 비슷한건데

* 이것의 장점 : 그냥 파일을 열어도 브라우저에서 열린다. jsp는 그냥 쌩 파일을 부라우저에서 열만 안열린다.
* 단점 : 메뉴얼을 좀 봐야한다.

### 8.1 적용 예제

HelloController.java

### 8.2 html파일 바뀌었을때 알아서 서버 재시작 하게

build.gradle에 추가

```
implementation 'org.springframework.boot:spring-boot-devtools'
```

인텔리J : 메뉴 build - Recompile하면 서버 재시작 없이 html만 컴파일 된다.

##

##

## 9. 참고

스프링에서 어떻게 개발할지 잘 모를 떄   
https://spring.io에서 가이드에 들어가자   
여기서 jpa, RESTful 같은거 찾아서 돌려보면 좋다.     
근데 영어다

##

##

## 10. h2 database

테스트 할때 좋아서 일단 h2를 깔지만 나중에나는 mysql로 전환할거다.

### 10.1 설치

1) https://www.h2database.com/html/download-archive.html
2) 1.4.200을 추천하더라. 더 올리면 뭔가 안되는듯.
3) Zip파일 다운로드, 압축 풀고
4) 실행파일 권한 변경(맥)

```
chmod 755 h2.sh
```

### 10.2 실행

```
./h2.sh
```

조금 지나면 웹브라우저가 뜬다.   
잘 안될때가 있는데 이럴때는   
브라우저 주소창에 jdbc:h2:~/jpabook 로 바꿔주고, test는 jpabook,   
사용자명 root   
비번 123

### 10.3 실행 후

~/jpabook.mv.db가 뜬다

* 만약에 다시 설치한다면 꼭 이파일을 지우자
* 그렇지 않으면 아래 오류가 난다.   
  General error: ""The write format 1 is smaller than the supported format 2
  [2.0.206/5]"" [50000-202] HY000/50000

### 10.4 진입 설정 변경

url을 아래와 같이 바꾸자

```
jdbc:h2:tcp://localhost/~/jpabook
```

- 이렇게 안하면 동시에 애플리케이션이랑 웹콘솔이랑 접근하면 충돌이 나는 경우가 있다고 한다.

### 10.5 JPA와 DB 설정, 동작확인

application.properties를 지우고 application.yml을 만들자. 야믈파일 형식도 지원하나보다

* main/resources/application.yml 에 아래내용 복사

```
spring:
  datasource:
    url: jdbc:h2:tcp://localhost/~/jpabook
    username: root
    password: 123
    driver-class-name: org.h2.Driver
  # 이 설정들은 스프링부트 메뉴얼에 가서 봐야한다.
  # https://spring.io/projects/spring-boot#learn
  # https://docs.spring.io/spring-boot/docs/current/reference/html/
  jpa:
    hibernate:
      ddl-auto: create #어플리케이션 실행 시점에 테이블을 drop하고 create함
    properties:
      hibernate:
        #show_sql: true  # show_sql : 옵션은 System.out 에 하이버네이트 실행 SQL을 남긴다. 로거로 남기는게 더 좋아서 이건 주석
        format_sql: true

logging.level:
  org.hibernate.SQL: debug  #org.hibernate.SQL : 옵션은 logger를 통해 하이버네이트 실행 SQL을 남긴다.
  # org.hibernate.type: trace
```

### 10.6 쿼리 파라미터 로그 남기기

* application.yml 마지막에 이거 추가

```
org.hibernate.type: trace
```

### 10.7 인텔리제이 JPA세팅

(맥 + 인텔리제이 엔터프라이즈 버전 기준)   
File - Project Structure - Modules클릭 - 메인 펼쳐서 JPA있는지 확인



##

##

## 11. MYSQL

### 11.1 build.gradle 추가

```
runtimeOnly 'mysql:mysql-connector-java'
```

### 11.2 application.yml 수정

```
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:[포트]/[스키마]?serverTimezone=Asia/Seoul
    username: [아이디]
    password: "[패스워드]" 
```

### 11.3 table 초기화 전략 바꾸기

application.yml을 아래와 같이 수정해서 뜰때마다 테이블 다시 만드는거 안하게 바꾼다. 어짜피 나는 test할땐 인메모리 h2쓴다.

``` 
jpa:
  hibernate:
    ddl-auto: none
```


