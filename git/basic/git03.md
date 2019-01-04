## git 03 - remote repository folk 후 pull request를 사용한 협업방법

##### 2019-01-04

---

### 선행작업

* git, github desktop 설치

### 작업기준 remote repository folk

* 예를 든 경우는 younggeun0/logAnalysisApp
  * folk하면 자신의 계정 remote repository에 복사됨

### remote upstream(가져온 기준 repository) 설정

* folk한 자신의 repository에서 작업 수행 후 merge를 위한 작업

```bash
git remote add upstream younggeun0/logAnalysisApp.git 
```

### folk한 repository를 local repository에 다운로드

* repository 에서 git clone

```bash
git clone  https://github.com/사용자명/logAnalysisApp.git
```

### 작업 수행 전 upstream remote repository에서 최신 내용을 적용시킴

```bash
# upstream의 내용을 pull -> 자신의 master로
git pull upstream master
```

### 가져온 remote repository 내용을 이용하여 작업 수행

* 가능하면 branch로 작업하는게 버전관리하기 수월
* 작업 완료하면 commit, push로 자신의 remote repository 내용 업데이트
    * git Desktop GUI 이용하면 쉬움

### 작업기준 repository인 younggeun0/logAnalysisApp으로 Pull Request

* 작업을 완료 후 작업기준인 upstream과 합치기 위해 하는 것
* 깃허브 사이트 자신의 logAnalysisApp repository에서 pull request 
    * 작업기준 repository의 관리자가 내용을 확인 후 merge처리하면 작업기준에 반영됨

