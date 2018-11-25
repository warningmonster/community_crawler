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


## Python3 설치
Repository를 yum에 추가
<pre><code>
$sudo yum install -y https://centos7.iuscommunity.org/ius-release.rpm
</code></pre>

yum search로 python 3.x 버전 확인
아래 명령어를 수행하면 python3으로 시작하는 라이브러리들을 확인할 수 있습니다.
<pre><code>
$ yum search python3
</code></pre>

필요 라이브러리들 설치
<pre><code>
$ sudo yum install -y python36u python36u-libs python36u-devel python36u-pip
</code></pre>

Python 설치 및 버전 확인
<pre><code>
$ python -V
Python 2.7.5

$ python3.6 -V
Python 3.6.4
</code></pre>

기본적으로 python 명령어는 Python 2.x를 가리키고 있기 때문에 Alias 수정으로 이를 변경해줍니다.

Alias 수정
먼저 Python 3.x가 설치되어 있는 디렉토리 위치를 찾습니다.
<pre><code>
$ which python3.6 /usr/bin/python3.6 
</code></pre>

그 다음 현재 Alias 확인을 합니다.
<pre><code>
$ ls -l /bin/python*
</code></pre>

Alias 수정을 합니다.
<pre><code>
$ sudo unlink /bin/python
$ sudo ln -s /bin/python3.6 /bin/python3
$ sudo ln -s /bin/python3.6 /bin/python
$ sudo ln -s /bin/pip3.6 /bin/pip
</code></pre>

## 설치
- ln -s $(pwd)/pre-commit $(pwd)/.git/hooks/
- cp env.dist.dev .env
- python3 -m venv venv
- source venv/bin/activate .
- pip install -r requirement.txt


## License
MIT (http://www.opensource.org/licenses/mit-license.php)
