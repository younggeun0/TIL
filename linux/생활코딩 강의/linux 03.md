## linux 03 - shell과 kernal, shell script, 디렉토리의 구조, 프로세스모니터링, 파일 찾는법

##### 2018-12-04

---

### shell & kernal

![01](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/03/01.png?raw=true)


* **shell - 껍데기, kernal - 코어**
    * 유저가 linux 명령을 하면 쉘에게 입력하는 것
    * 쉘이 해석해서 커널이 이해할 수 있는 방식으로 전달
        * 커널이 하드웨어 제어 후 결과를 쉘에게 쉘이 유저에게 전달해서 처리
* 커널을 유저가 직접 제어를 못 하므로 쉘을 통해 명령을 입력하면 쉘이 대신 전달, 처리를 해준다.

```bash
# 뒤에 들어온 문자를 출력해주는 기능을 하는 echo
echo "hello"

# 해당 쉘을 출력해줌 (-bash)
echo $0

# 다른 쉘을 사용해보기위해 zsh 설치
sudo apt-get install zsh

# 설치후 zsh실행, echo $0로 zsh 실행 후 명령어가 zsh을 통해 커널에 전달되는걸 확인가능
zsh
echo$0
```

* bash vs zsh
    * **부모는 같음**, zsh이 추가기능을 가짐(더 추가기능을 가지는 oh my zsh)
    * bash나 zsh나 다 프로그램

---

### Shell Script

* **쉘에서 실행되는 스크립트**
* 쉘 스크립트를 사용하면 쉘을 통해 명령을 실행시키는 여러가지 작업을 한번에 순차적으로 실행가능
    * **재사용 가능**

```bash
# 반복된 작업이 아래와 같을 때, 이를 쉽게 반복가능하게 할 쉘스크립트 작성
# - script 디렉토리 생성, script내에 bak 디렉토리 생성, a.log, b.log, c.log 생성
# - bak에 a.log, b.log, c.log를 카피

mkdir script
cd script/
touch a.log b.log c.log
mkdir bak 
cp *.log bak
ls -l bak

# bash의 설치 위치 확인하기
ls /bin
```

* **운영체제는 #!(Shebang)을 보고 /bin/bash 란 프로그램를 통해 해석되어야 한다고 해석**
* backup이란 파일 생성
    * bak 디렉토리가 존재하지 않는다면 bak 을 만들고
        * 조건문 종료 fi, 이제 bak디렉토리가 존재하므로 확장자가 log인 파일을 bak에 복사한다

* shell script 내용
```bash
#!/bin/bash

if ! [ -d bak ]; then
    mkdir bak
fi
cp *.log bak
```

```bash
# 실행전 권한부여
chomod +x backup

# 실행
./backup
```

---

### 디렉토리의 구조(Linux Directory Structure)

* **/** 최상위 디렉토리(root)
  * **bin** - user binaries
  	* 실행가능한 프로그램들이 저장되어있는 곳
  * **sbin** - system binaries
  	* 시스템 프로그램들이 저장
  * **etc** - configuration files
  	* 설정파일들이 저장
  * **dev** - device files
  * **proc** - process information
  * **var** - variable files
  	* 변경될 정보를 담는 곳
  * **tmp** - temporary files
  	* 임시파일들 저장되는 곳
  * **home** - home directories
  	* 개인파일 저장하는 곳
  * **boot** - boot loader files
  * **lib** - system libraries
  * **opt** - optional add-on application
  * **mnt** - mount directory
  * **media** - removable media devices
  * **srv** - service data
  * **usr**
  	* bin - 일반적인 설치프로그램들이 usr밑에 설치됨
  	* 이젠 usr아닌 **home**으로 유저데이터를 담고 사용

---

### 프로세스

* 프로그램을 실행해서 메모리에 적재되고 프로세서에 의해 처리되고 있는 상태
    * **실행중인 프로그램**
* **스토리지** - 가격 쌈, 저장용량 큼
* **메모리** - 가격 비쌈, 저장용량 작음
* 스토리에 깔린 프로그램을 메모리에 적재, 실행중인 프로그램이 메모리에 상주하면서 cpu가 읽어들어서 처리

![02](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/03/02.png?raw=true)

### 프로세스 모니터링

* **ps** - 프로세스 리스트를 보여주는 명령어
    * **ps aux** - 백그라운드 돌아가는 프로세스도 출력

```bash
# ps aux의 결과를 grep이 받아서 top을 검색한  결과 출력
ps aux | grep top 
```

![03](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/03/03.png?raw=true)

* **pid는 식별자**
    * **kill**로 정지 시킬 수 있다.

```bash
sudo kill pid번호
```


* **top** 은 기본으로 설치된 프로세스 모니터링하는 프로그램
    * 업그레이드 버전이 **htop**

```bash
# install
sudo apt install htop
```

* **htop**
    * 항목을 더블클릭하면 해당 항목순으로 정렬이 됨
    * Command는 어떤 내용으로 실행됐는지 기록된 것
    * RES는 실제적인 메모리 사용량
        * MEM은 메모리 사용 %
    * 위에 1~8은 8개의 cpu코어를 뜻함
    * Load average는 cpu점유율(1분,5분,15분간 평균치)
        * 대기중인 프로세스가 얼마나 되는지 확인 가능한 것
        * 코어수에 따라 다른 값을 가짐

![04](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/03/04.png?raw=true)

---

### 파일 찾는 법

* **locate 와 find**
  * 파일을 찾는 법
  * **locate는 디렉토리를 뒤지지 않고 DB로 검색(훨씬 빠르게 검색)**
    * locate가 사용하는 DB를 **mlocate**라고 함
        * sudo updatedb 를 통해현재 디렉토리내 정보들을 업데이트

```bash
# .log에 해당하는 모든 파일의 디렉토리를 출력
locate *.log
```

* **find는 실제로 데이터를 검색**
  * **시간이 더 오래걸림**
  * 가장 많이 사용되는 명령어 중 하나
	* **/** - 루트디렉토리부터 찾겠다
	* **.** - 현대디렉토리에서 찾겠다
	* **~** - 홈디렉토리에서 찾겠다
  * 설명서 + 온라인 검색예제를 통해 추가공부(필요시)

```bash
# 참고
find --help 

# 루트 디렉토리부터 이름에서 log인 모든 파일을 찾겠다. sudo 해줘야 다 검색함
find / -name *.log
```

### whereis와 $PATH

* **whereis**
    * **실행파일**을 검색해줌

```bash
whereis 파일명
```

![05](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/03/05.png?raw=true)

* **$PATH**
    * ls는 /bin/ls에 존재하는데 어디서든 명령이 실행되는 이유는 PATH란 변수 때문
    * PATH는 리눅스, 유닉스계열에서 기본으로 갖고 있음
    * OS는 **PATH변수**에 담긴 디렉토리들을 검색, 해당 실행파일이 있는지 차례대로 검색
        * 발견시 실행
    * 이런 변수를 **환경변수**라고 한다.

![06](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/03/06.png?raw=true)

---

### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)

[linux directory structure](https://www.thegeekstuff.com/2010/09/linux-file-system-structure/)