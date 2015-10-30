
### Tcollector Install
Execution of one terminal anymore
```sh
    cd /usr/local
    git clone git://github.com/OpenTSDB/tcollector.git
    cd tcollector
```
##### 'startstop' Changing the file
```sh
    vim startstop
```
Please comment cancel the portion of the '#TSD_HOST=dns.name.of.tsd' and Enter the Ip address.(4~5 line)
```sh
    TSD_HOST=192.168.X.X
```
### Tcollector Run - Execution of one terminal anymore
```sh
    ./startstop start

```
##### The connection with 'http://192.168.x.x:4242' in the web address bar


### tcollector Test

```sh
   # root 권한으로
   cd /usr/local/tcollector/collectors
   mkdir 0
   

```

#### test code 만들기 

```sh
   vim insert_test.py
```

```sh

#!/usr/bin/python

import sys
import urllib2
import time
from datetime import datetime, timedelta

while 1 :
    t = time.localtime()
    tsec = t.tm_sec
    if tsec%10!=0 :
            print tsec
            time.sleep(0.2)

    else :
        print "inha.test %d %d" % ( time.time(), tsec )
        time.sleep(0.1)

```

```sh
   # 실행해 보기
   python insert_test.py
   
   # 파일 권한 변경(참고 블로그 : http://blog.naver.com/radii26omg/220337573729)
   chmod 777 insert_test.py

   > ll 로 권한확인한다.
   ps -as | grep tcolle => tcolle에 관한것만 보여준다.
   
   
   # openTSDB GUI에서 확인
   # http://127.0.0.1:4242
   
   # log 파일 확인
   # 터미널에서 실행
   tail -f /var/log/tcollector.log
   => 에러나는거로그남겨준다
       tail : 맨마지막만보여준다
      
   
   # 터미닐에서 실행 - 특정 단어만 검색
   tail -f /var/log/tcollector.log | grep inha
```

#### 연습 1

```sh
   # 20초마다 100을 openTSDB에 저장하세요
   # 원하는 메트릭을 정하세요(예: cc_100)
```

#### 연습 2 : Tag 추가하기

```sh
   # 20초마다 100을 openTSDB에 저장하세요
   # 원하는 메트릭을 정하세요(예: cc_100)
   
   # insert_test.py 의 print 부분에 tag 를 추가하세요(Tag는 7개까지 추가 가능)
   print "inha.test %d %d id = %d" % ( time.time(), tsec, 1030 )
   
```
