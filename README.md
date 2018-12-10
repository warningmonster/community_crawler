[![Build Status](https://travis-ci.org/james-song/community_crawler.svg?branch=master)](https://travis-ci.org/james-song/community_crawler)

# 커뮤니티 크롤러
대한민국 커뮤니티에 올라오는 많은 게시물 중에서 덧글이 일정량 이상인 글들에 한해서만 크롤링하여 저장하는 머신 입니다.

## 사용 가능한 커뮤니티 목록 
- 클리앙 [모두의공원](http://clien.net/cs2/bbs/board.php?bo_table=park)
- 뽐뿌 [자유게시판](http://www.ppomppu.co.kr/zboard/zboard.php?id=freeboard)
- 웃대 [베스트오브베스트](http://www.todayhumor.co.kr/board/list.php?table=bestofbest)
- slrclub [자유게시판](http://www.slrclub.com/bbs/zboard.php?id=free)
- 루리웹 [유머 베스트 게시판](http://bbs.ruliweb.com/best/selection)
- 루리웹 [핫딜 게시판](http://bbs.ruliweb.com/market/board/1020)
- 루리웹 [취미 게시판](http://bbs.ruliweb.com/hobby)

## 개발 환경
- python 3.x
- [Mongodb](https://www.mongodb.org)

## git 설치
- sudo yum install git

## Python3 설치  
(http://snowdeer.github.io/python/2018/02/20/install-python3-on-centos/)    

Repository를 yum에 추가   
~~~
$sudo yum install -y https://centos7.iuscommunity.org/ius-release.rpm
~~~

yum search로 python 3.x 버전 확인
아래 명령어를 수행하면 python3으로 시작하는 라이브러리들을 확인할 수 있습니다.   
~~~
$sudo yum search python3
~~~

필요 라이브러리들 설치   
~~~
$ sudo yum install -y python36u python36u-libs python36u-devel python36u-pip
~~~

Python 설치 및 버전 확인   
~~~
$ python -V
Python 2.7.5

$ python3.6 -V
Python 3.6.4
~~~

기본적으로 python 명령어는 Python 2.x를 가리키고 있기 때문에 Alias 수정으로 이를 변경해줍니다.

Alias 수정
먼저 Python 3.x가 설치되어 있는 디렉토리 위치를 찾습니다.   
~~~
$ which python3.6 /usr/bin/python3.6 
~~~

그 다음 현재 Alias 확인을 합니다.   
~~~
$ ls -l /bin/python*
~~~

## Alias 수정을 합니다.
### 아래 명령어는 설치할 거 다 하고 합시다.  
### yum에서 사용하는 python 문법이 모두 2.x로 되어 있어 아래 3.6으로 변경하고 나서 yum 설치시 에러남.

~~~
$ sudo unlink /bin/python
$ sudo ln -s /bin/python3.6 /bin/python3
$ sudo ln -s /bin/python3.6 /bin/python 
  ㄴ yum을 망가트림
     sudo vi /usr/bin/yum 으로 해서 맨 윗줄의 python을 python2.7같이 버전 명시해서 수정 필요
     #!/usr/bin/python → #!/usr/bin/python2.7 (2018.12.10 메모)
     ㄴ 이렇게 하면 yum은 구동은 되나, yum download 시에 에러남.
        그냥 2.x대로 원복하고 나중에 3.x와 연결하는게 낫겠네...(2018.12.10 메모)

         ** 원복 (python이라는 이름을 2.7 즉 구버전과 다시 연결)
         - sudo unlink /bin/python
         - sudo ln -s /bin/python2.7 /bin/python
         ** 설치 다했으면 다시 python이라는 이름을 3.x python과 연결
         - sudo unlink /bin/python
         - sudo ln -s /bin/python2.7 /bin/python
         ** 졸라 귀찮음...(2018.12.10 메모)
                                                
$ sudo ln -s /bin/pip3.6 /bin/pip 
~~~

## 소스 복제
git clone github 주소   
ex) git clone https://github.com/warningmonster/community_crawler.git

## 설치
~~~
- cd ./commutiy_crawler
- ln -s $(pwd)/pre-commit $(pwd)/.git/hooks/
- cp env.dist.dev .env
- python3 -m venv venv
- source venv/bin/activate . <---- 모듈 실행할때마다 다시 해줘야 함.(2018.11.25 메모) 
- pip install -r requirement.txt
  ㄴ 옛날 버전이라고 pip 업그레이드하라고 메시지 나옴(2018.12.10 메모)
      You are using pip version 9.0.3, however version 18.1 is available.
      You should consider upgrading via the 'pip install --upgrade pip' command.
- pip install --upgrade pip
~~~

## 실행명령어
~~~
[aaa@bbb community_crawler]$ python serve.py
2018-11-25 05:14:09,403 - crawler.main - INFO - crawler start
~~~



## 원격의 mongodb 접속하기
~~~
# 먼저 /etc/hosts 파일에 mongodb라고 등록해놓았다.  
# public network이 아니라 private network 주소이다.
# 이건 구글클라우드를 사용해서 있는 거고, 일반적으로는 public network 주소 밖에 없다.   
[aaa@seoul chat-bot]$ cat /etc/hosts|grep mongodb
10.146.0.3 mongodb1


[aaa@seoul chat-bot]$ cat test.sh
mongo -u test -p test --host mongodb1:27017 --authenticationDatabase simple-bot
                             ㄴ 서버IPL포트
~~~
