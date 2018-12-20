## git 02 - 저장소 생성

##### 2018-12-20

---

### Git 버전 확인, 사용자 등록

```bash
# 설치된 git버전 확인하기
git --version
```

![01]()


* 설치한 git에 본인의 **사용자명과 메일주소** 등록하기
  * 등록한 정보는 나중에 변경이력에 표시됨
  * git 설정내역은 사용자 홈 폴더의 `.gitconfig` 파일에 기록됨. 
    * 직접 파일편집도 가능하지만 **config 명령어**를 이용해 설정가능

```bash
git config --global user.name "<사용자명>"
git config --global user.email "<메일주소>"
```

![02]()

---

### 새 Repository 생성

* **local repository**로 등록할 땐 해당 디렉토리에서 **'git init'**을 입력한다.

```bash
git init
```

![03]()

* **remote repository**는 github같은 사이트에서 생성한다.
  * github같은 경우 새 remote repository를 생성하면 초기 설정방법을 알려준다.

![04]()

---

### status, commit, add

* **status**는 git 관리 폴더의 work tree와 index 상태를 확인할 때 사용

```bash
git status
```

![05]()

* untracked files로 새로 만든 sample.txt가 확인가능, 처음 한번 인덱스에 등록하면 추적 대상으로 등록할 수 있다. 
  * 파일을 인덱스에 등록하는 명령어는 **add**

```bash
git add <file>..

# 파라미터에 '.'을 지정하면 모든 파일을 인덱스에 등록할 수 있음
git add .
```

![06]()

* commit 명령어를 실행해 index의 내용을 repository에 저장한다. ??
  
```bash
# 커밋 시 comment를 남길 수 있음
git commit -m "<comment>"
```



