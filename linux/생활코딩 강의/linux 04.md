## linux 03 - 백그라운드작업, 항상실행, 정기적 실행, shell Stratup script, 다중사용자

##### 2018-12-04

---

### 백그라운드 작업

* **전환작업(Alt+tab)**
* 어떤 일을 하다 **Ctrl+Z**를 누르면 **종료하지 않고 전환**
    * **fg** 명령하면 다시 앞으로 전환
* **jobs** 입력시 백그라운드로 돌린 실행중인 프로세스들이 떠있다.
    * **fg 프로세스명** 로 원하는 프로세스로 전환가능
    * ps로 **pid**파악 후 **kill pid**로 원하는 프로세스 종료

```bash
# 전환했던 프로세스를 다시 앞으로
fg 

# jobs 후 실행중인 특정 프로세스를 앞으로
fg 프로세스명

# ps 후 pid파악 후 특정 프로세스 종료
kill pid
```

```bash
# 시간이 오래 걸리는 작업을 실행하고 바로 백그라운드로 돌릴땐 '&'를 붙인다
# ls -alR / 모든 파일을 출력하므로 오래 걸림(&로 백그라운드로 돌리면 쉘을 계속 쓸 수 있다.)
ls -alR / > result.txt 2> error.log &
```

---

### daemon

* 항상 실행되는 프로세스
* **데몬형태의 프로그램들은 항상실행되고 있다는 특징**이 있음
  * 부팅시 자동실행
  * ls, mkdir, rm은 필요할때만 수행되는 프로그램들
  * 비유하자면 daemon은 냉장고(항상켜짐)/ ls 같은 명령어들은 티비(필요할때만 킴)
* **Web Server가 대표적인 데몬**
  * 실습은 CentOS로 했기 때문에 apt가 아니라 yum, 아래 명령과 조금 달랐음

```bash
# 아파치 웹서버 설치
sudo apt install apache2

# 설치됐는지 확인(윈도우 bash라 다른 위치에 저장되어 있었음..)
cd /etc/init.d/; ls;

#/init.d/ 데몬저장된 디렉토리
#아파치 실행
sudo service apache2 start

# ps로 확인
ps aux | grep apache2

# apache 종료
sudo service apache2 stop
```

---

### 정기적인 실행(cron)

* **정기적으로 명령을 시켜주는 도구**
* crontab expression 참고해서 vi이용해서 내용을 추가해주면 주기적인 작업을 시킬 수 있다.

```bash
# 크론 수정
crontab -e

# 크론에 추가했음 시간을 주기적으로 로그로 추가해주는 내용을 추가했음, 표준에러를 표준출력으로 보내줌
*/1 * * * * date >> date.log 2>&1

# 뒤쪽 내용을 쫒으면서 보여줌(ctrl+c로 빠져나옴)
tail -f date.log
```

---

### 쉘을 시작할 때 실행(shell startup script)

```bash
# 명령어에 별명붙이기, l만 입력해도 ls -al이 실행됨
alias l='ls -al'
alias ..='cd ..'
alias c='clear'
```

* 위 bash 명령어를 시작될 때 shell script를 시작시키면 반복안해도 됨

```bash
# shell check
echo $SHELL

# ~에 .bashrc에 bash 실행시 수행될 코드를 적으면 된다
```

![01](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/04/01.png?raw=true)

---

### 다중사용자

* **유닉스계열은 다중사용자 시스템**
    * 어렵고 보안문제 발생 가능,

```bash
# 자신을 식별하는 명령어 id
id

# 누가 접속했는지 확인하는 who
who
```

---


### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)
