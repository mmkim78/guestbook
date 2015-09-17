# guestbook
[![Build Status](https://travis-ci.org/clojure-study/guestbook.svg?branch=master)](https://travis-ci.org/clojure-study/guestbook)
## 접속주소
http://52.68.124.223:3000/

## 개발 시작하기

    $ git clone https://github.com/clojure-study/guestbook.git
    $ cd guestbook
    $ lein run migrate
    $ lein run

실행 후 웹 브라우저로 [http://localhost:3000](http://localhost:3000) 에 접속하여 확인


## PostgreSQL 데이터베이스 연동하기

#### project.clj 수정하기
`:database-url`가 2개 있는데 모두 수정하기.
```clojure
:databse-url "jdbc:postgresql://호스트이름(또는 주소):포트번호/데이터베이스이름?user=이름&password=비밀번호"
```

#### db.clj 수정하기
`db-spec`에서 `:subname`, `:user`, `:password`를 위의 `:database-url`의 내용에 맞춰 수정하기 


## 배포하기
#### 빌드
    $ cd guestbook
    $ lein uberjar
    
#### 파일 업로드
    $ scp -i "clojurestudy-aws.pem" target/guestbook.jar ec2-user@52.68.124.223:~/target
여기에서 path는 배포자의 개발 환경에 따라 다를 수 있음

#### 서버 재시작
ssh로 접속하여 screen 세션에 들어감
    
    $ ssh -i "clojurestudy-aws.pem" ec2-user@52.68.124.223
    $ screen -r

서버 정지하고 다시 시작

    Ctrl + c
    $ java -jar target/guestbook.jar

세션에서 나옴    
    
    Ctrl + a + d
