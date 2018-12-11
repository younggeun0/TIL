## linux 05 - 관리자와 일반사용자, 사용자 추가

##### 2018-12-05

---

### 관리자와 일반사용자

* **super(root) user**
    * 관리자
* **user**
    * 일반유저
* **sudo** - 관리자 권한 실행 명령어

```bash
# 유저명이 root고 '$'가 아니라 '#'이면 super유저
root@~# 
```

![01](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/05/01.png?raw=true)

```bash
# super유저로 변경하기
su - root

# super 유저 락걸기
sudo passwd -l root

# super 유저 락풀기
sudo passwd -u root
```

---

### 사용자 추가
	
* 필요시 검색해서 자세한 기능 사용

```bash
# 유저 추가
sudo useradd -m 유저명

# 유저 비번설정
sudo passwd 유저명

# 유저 변경
su - 유저명

# sudo 권한주기, 자세한 내용은 매뉴얼 참조 man usermod
sudo usermod -a -G sudo

# 유저 나가기
exit
```

---

### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)
