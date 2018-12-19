## git 01 - 기본 용어

##### 2018-12-19

---

### SCM

* **Source Code Management, 버전관리**
* 동일한 정보에 대한 여러 버전을 관리하는 것
  * [위키 정의](https://ko.wikipedia.org/wiki/%EB%B2%84%EC%A0%84_%EA%B4%80%EB%A6%AC)

---

### GIT

* 소스코드를 효과적으로 관리하기 위해 개발된 **'분산형 버전 관리 시스템'**

---

### Remote Repository & Local Repository

*** Remote Repository**
  * 파일이 원격 저장소 전용 서버에서 관리, 여러 사람이 함께 공유하기 위한 장소
* **Local Repository**
  * 내 PC에 파일이 저장되는 개인 전용 저장소

---

### commit

* **git이 관리하는 repository의 변경을 기록하는 것.**
* 각 커밋엔 영문/숫자로 이루어진 40자리 고유 이름이 붙는다.
* 커밋시 comment를 필수로 입력
  
---

### Work Tree(작업 트리), Index

* **git에서 디렉토리를 지칭하는 말**
* 커밋을 수행 전 Repository와 Work Tree 사이에 존재하는 공간을 **'Index(인덱스)'**라 함.
  * Work Tree에서 수행한 내용은 **stage(또는 staging)**을 통해 **Index**에 등록되고 commit을 사용하게되면 Repository로 넘어간다.
    * repository에 변경 사항을 기록하기 위해선 기록하고자 하는 모든 변경사항들이 'Index' 공간에 존재해야 함.
  * **Index**란 공간이 있기 때문에 Work Tree에 모든 파일을 repository에 올리는게 아니라 **원하는 변경사항만 선택적으로 올릴 수 있다.**


