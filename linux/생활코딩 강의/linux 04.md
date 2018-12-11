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

### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)
