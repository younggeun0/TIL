## linux 06 - 권한, 그룹

##### 2018-12-07

---

### 권한(Permission)

*** User에게 File과 Directory에 대한 제한을 주는 것**
    * Read & Write & Excute
    * 다른 유저가 다른유저의 파일에 접근했을때 Permission denied

* 타입(파일 또는 디렉토리)/ 엑세스모드(오너-그룹-아더)// 오너, 그룹// 생성일 / 파일또는디렉토리명
    * **엑세스모드(access mode)**
        * **r** - read
        * **w** - write        
        * **x** - excute
* **chmod(change mod)**

![01](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/06/01.png?raw=true)

```bash
# 파일의 권한 변경, other의 read를 삭제
chmod o-r perm.txt

# other에게 read권한 부여
chmod o+r perm.txt

# other에게 write권한 부여
chmod o+w perm.txt

# user 권한변경, 자기자신도 권한제한 부여할 수 있음
chmod u-r perm.txt

# hi-machine.sh(특정파일)에 실행권한 부여
chmod u+x hi-machine.sh

# octal mode를 사용하면 한번에 여러 권한부여가능(위키참조)
# execute only는 모드 '1' => -x-x-x = 111
chmod 111 perm.txt

# write only는 2
chmod 222 perm.txt
```

![02](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/06/02.png?raw=true)


* **디렉토리 권한**
  
```bash
# perm이란 디렉토리에 other가 읽는 권한을 부여한 것
chmod o-r perm

# 파일이랑 권한제어 똑같음
```

* **재귀적 권한부여**

```bash
# -R을 붙여서 해당 디렉토리 내 모든 파일에 같은 권한부여가 가능
chmod -R o+w perm
```

---

### Group

* 파일과 디렉토리를 여러 사용자들이 공동으로 관리할 수 있는 방법
* **권한을 주고 싶은 사람들(other)을 묶은 것 => group**
* 자주사용하는  기능이 아니기 때문에 검색으로 해결
* 그룹 설정하면 쉘을 재접속필요

```bash
# 그룹생성
groupadd 그룹명

# 그룹에 유저추가
useradd-G 그룹명 유저명

#usermodify, 그룹에 유저 추가
usermod -a -G 그룹명 유저명  
```

```bash
# 파일이나 디렉토리의 그룹 owner나 그룹 바꾸기
chown {-R} [user]{:group} [file|directory]
sudo chown 기존그룹명:변경할그룹명 파일또는디렉토리
```


---

### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)
