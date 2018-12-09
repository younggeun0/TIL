## linux 02 - sudo, package manager, CLI, wget, git, IO Redirection

##### 2018-11-27

---

### sudo

* **super user do**
* 임시로 권한이 필요할때 사용
    * 다운로드 시

```bash
# 절대 사용하면 안되는 명령어 이처럼 모든 디렉토리 삭제가능..
sudo rm -rf /

# 사용할땐 앞에 'sudo'를 붙인다.
# 이런식으로 설치
sudo apt-get install git 
```

---

### package manager

* 패키지매니저는 없는 프로그램을 받아 설치할때 사용
  * apt, yum 등이 존재

```bash
# 패키지매니저를 이용해서 업데이트할 수 있는 목록 업데이트
sudo apt-get update

# 목록중에서 설치가능한 프로그램 출력, htop이란 프로그램 패키지 목록 검색
sudo apt-cache search htop

# htop 다운로드받고 설치
sudo apt-get install htop

# htop 업그레이드
sudo apt-get upgrade htop 

# 설치된 모든 프로그램 업그레이드
sudo apt-get upgrade

# 설치된 프로그램 삭제
sudo apt-get remove htop
```

---

### GUI VS CLI

* **GUI**
    * 그래픽 UI
    * 쉽다
* **CLI**
    * 커맨드라인 UI
    * 자원 점유가 적다
    * **순차적 실행**이라는 강점을 갖는다

```bash
mkdir why 
cd why

# 위에 두개의 명령을 하나로 합칠 수 있다.(순차적 실행)
# ';'로 명령을 이을 수 있다.
mkdir why;cd why

# ls 옵션내용이 많음 그 중 sort내용만 보고 싶을땐 |(파이프)
ls --help | grep sort 
# 계속 |로 원하는 내용을 한정시킬 수 있음
ls --help | grep sort | grep file

# |를 사용하면 앞 프로그램의 출력을 뒤 프로그램의 입력으로 연결할 수 있다
# 현재 프로세스 목록 중에 해당 단어를 포함한 결과를 출력
ps aux | grep 어떤단어
```

---

### 파일 다운로드 프로그램 wget

```bash
wget 받을파일url
mv 파일명 변경할파일명

# 위처럼 다운받고 파일명을 변경하지않고 한번에 가능(--help 참고)
wget -O 파일명 받을파일url
```

---

### git

* 버전관리 프로그램
* github 오픈소스 프로그램 허브
    * 개발자 협업 사이트

```bash
# git 설치
sudo apt-get install git

# git 설치된지 확인하기
git

#github 프로그램 받는법
git clone 오픈소스프로젝트url 저장할디렉토리명
```

---

### IO Redirection

* input, output의 결과의 방향을 바꾸는 것

```bash
# 명령어의 결과를 '>'로 모니터출력(기본출력)을 파일출력으로 redirect 시킴(txt파일로 저장)
ls -l > log.txt
```

![01]()


* 유닉스에선 출력은 **stdout, stderr** 두가지로 출력됨 
* '>'는 stdout을 redirection한 것
  * **stdout**은 옵션 1이었음(생략가능)
  * **stderr**를 redirect하기위해선 2를 사용
  * 그림같이 input이 들어와 output으로 나가는 것을 **IO Stream**이라 한다

```bash
# 1이 생략되어 있었음
ls -a 1> result.txt

rm name.txt 2> result.txt 
```

![02]()

* **프로그램**
  * 하드에 저장된 코드
  * 프로그램은 여러개의 프로세스를 가질 수 있다.
    * **프로세스**
      * 프로그램이 살아난 상태

```bash
# cat 을 사용하면 사용자가 입력하는 값을 받아서 출력(ctrl+d로 종료)
cat

# 사용자의 입력이 stdin, 이처럼 파일의 내용을 리다이렉션해서 cat의 입력값(arguments)으로 줄 수 있음
cat < hello.txt

# head는 위에 10줄을 출력
head linux.txt

# -n 옵션쓰면 한줄 출력
head -n1 linux.txt

# 위 1줄 출력은 아래와 같이 나타낼 수 있다(리다이렉션), argument로 linux.txt를 준거
head -n1 < linux.txt 

# 위 결과를 다른 파일에 저장하고 싶으면 또 리다이렉션
head -n1 < linux.txt > one.txt

# 결과 확인
cat one.txt
```

```bash
# 아래와 같이 두번 사용하면 결과를 덮어씀
ls -al > result.txt
ls -al > result.txt

# 결과를 추가하고 싶으면 append '>>', 기존 내용에 추가한다.
ls -al >> result.txt

# 명령 중간에 취소하고 싶으면 Ctrl+C
^C

# '<<'는 여러개의 입력을 하나로 합치는 것(쓰는 일 거의 없다..)
# mail은 해당 메일로 이메일을 보내는 유틸(설치필요)
mail younggeun0@mme.dongguk.edu << eot
> hi
> its young
> eot
# 종료됨, << eot의미는 eot만나면 종료된다는 의미

# /dev/null은 유닉스계열의 일종의 쓰레기통, 리다이렉션한 내용을 날릴때 사용
ls -al > /dev/null
```

---

### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)
