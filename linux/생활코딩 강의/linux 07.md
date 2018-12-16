## linux 07 - 인터넷, 네트워크, 서버, 아파치, SSH, 포트, 도메인

##### 2018-12-07

---

### 인터넷, 네트워크, 서버

* domain name써서 어떤 웹페이지 접속 시도 시 request(요청)하면 해당 정보를 가진 서버가 respond(응답)를 한다.
    * **인터넷은 request와 respond가 지속적으로 이루어지는 것(컴퓨터들의 대화)**
    * **Client <-> Server**
* google.com 은 domain name
    * 핸드폰에서 전화번호는 ip address, 저장된 이름은 도메인 네임
    * **ip address를 사람이 기억하기 쉽게 만든게 도메인 네임.**

```bash
# ping으로 알아낸 ip address를 이용해서 접속하면 해당 도메인으로 접속하는 것과 같다.
ping google.com 
```

![01](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/07/01.png?raw=true)


* DNS 서버는 모든 ip address를 갖고 있다.
    * 클라이언트가 도메인 네임을 입력하면 **DNS서버에 먼저 들려서 ip address를 알아내고 이를 이용해서 원하는 사이트로 접속하는 것.**

* 자신의 ip 알아내기

```bash
# public address 확인 방법(웹 통해서 접속한 ip를 알려주는 것) 
curl ipinfo.io/ip

# private address 확인 방법 (컴퓨터의 실제 ip를 확인하는 것)
ip addr
```


* **통신사(ISP)가 회선을 제공해 줌**
    * 모든 인터넷 사용하는 전자기기들은 직접 통신사와 연결되는게 아니라 공유기(Router)를 붙여서 여러대가 인터넷을 사용할 수 있도록 만듦. (개별로 직접 연결하면 비싸니까)
    *** 문제는 Router라는 장치가 통신사가 제공하는 회선을 갖게됨.** 
        * private IP(사설 IP)라는 개념이 여기서 등장
        * **외부에 공개되는 IP가 public IP address**
        * **내부에서 사용되는 IP를 private IP address라 함**
    * curl을 통해 알아내는 주소는 Router가 가진 주소를 보고 알려준 public IP address
    * ip addr이란 명령어로 알아낸 IP address는 private IP(공유기에서 부여한 IP)
    * 공유기로 private IP address를 부여받아 사용한다면그 컴퓨터는 Server로 쓸 수 없다.
        * 사내전화처럼 라우터로 묶인 네트워크끼리는 통신이 가능


---

### 웹서버(아파치)

* 웹서버를 설치하면 내컴퓨터의 내용을 인터넷을 이용하는 클라이언트들에게 제공해줄 수 있게 됨
* **Client로 요청을 하기 위해선 Web Browser가 필요.**
    * 대표적인 Web Browser로는 firefox, ie, chrome 존재
    * **응답하기 위해선 Web Server란게 설치되어 있어야 함**
    * **항상 돌아가다가 요청이 들어오면 요청에 대한 정보를 찾고 response를 보냄**
    * 대표적인 Web Server는 Apache, nginx, IIS 등이 존재

![02](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/07/02.png?raw=true)



* 생활코딩 강의에선 우분투를 사용, 실습은 CentOS사용
  * apt가 아닌 yum이란 패키지 매니저를 사용
  * 인터넷 설정이 우선 네트워크 환결설정
    * [인터넷 환경설정](https://m.blog.naver.com/PostView.nhn?blogId=tequini&logNo=220977723865&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
    * [아파치 설치](https://suwoni-codelab.com/linux/2017/05/27/Linux-CentOS-Apache/)

* **127.0.0.1은 자기자신을 가리키는 ip = localhost**

---

### SSH

* **쉘을 원격으로 접속해서 제어하는 것**
* 서버시장, IoT에서 리눅스의 비중이 엄청 크기 때문에 리눅스가 중요한 것
    * 인터넷을 통해 다루는 컴퓨터들
* 웹서버와 SSH Server와 동일하다고 보면 됨(기능상)

![03](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/07/03.png?raw=true)

```bash
# ssh 이용해 접속, 22번 포트를 사용
ssh 이름@아이피주소
ssh -p 포트번호 이름@아이피주소
```

---

### 포트

* http://naver.com:80 
    * 80은 생략가능, 다른 번호를 입력하면 접속이 안됨
    * **웹서버는 80번 포트**로 연결되기로 정해져 있기 때문(프로토콜)
    * **ssh는 22번 포트**
    * ssh 기본 포트번호를 바꾸고 싶으면 /etc/ssh에 있는 sshd config파일에서 port번호를 바꿔주면 됨
* **1024까지의 포트는 Well-known port, 이미 정해진 포트**
    * 그 외 포트번호는 특별한 용도로 사용

![04](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/07/04.png?raw=true)


### 포트포워딩 (port forwarding)

* **공유기를 쓰면 ISP에서 준 public IP를 라우터가 갖고 라우터는 여러 기기들에게 DHCP로 IP를 부여해줌(private IP) 근데 외부에서 private IP로 접근을 못 한다!**
    * 라우터에도 port가 존재, **외부에서 특정 port로 접근했을 때 서버를 가진 private IP의 port로 포워딩 하는것. 이게 포트 포워딩**
    * **공유기가 갖는 IP를 default gateway**라 한다.
        * 내부에서 밖으로 나갈때 지나는 관문이니까

![05](https://github.com/younggeun0/TIL/blob/master/linux/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9%20%EA%B0%95%EC%9D%98/img/07/05.png?raw=true)

```bash
# default gateway 알아내기
ip route
```

---

### 도메인(Domain)

* **DNS(Domain Name System)**
* **클라이언트가 도메인을 입력 후 서버에 접속하려고 하면 이미 알고 있는 DNS 서버에 가서 ip를 묻는다. 그리고 알게된 ip주소를 이용해서 서버에 접속한다.**
* 과거에는 hosts file이란게 존재했었음
    *** DNS 서버가 없었을 땐 hosts file에 존재하는 ip를 가지고 접속을 했었다.**
* etc/hosts 파일에 ip와 도메인을 추가해두면 해당 도메인 입력시 입력한 ip로 바로 접속.
  * 때문에 **hosts파일은 해커들의 표적이 됨**
* **하나의 서버는 하나의 도메인과 매칭이됨**
    * 서버가 여러개일 시 각각 도메인을 구입해야함(불편, 비용비쌈)
    * **도메인 앞에 서브도메인을 붙여 각각 다른 서버를 찾아가면서 한 도메인을 재사용하는 방법이 있음** 
    * 도메인 구입한 사이트(설정 페이지)에서 각각 이름과 다른 ip부여가능
* 해당 도메인을 접속할 땐
    * DNS 서버에 접속
    * DNS 서버는 root DNS server의 주소를 알고 있다. 
        * root DNS 서버는 전세계에 흩어진 서버(안정성, 성능을 위해)
        * DNS서버는 .com, .net 등 의 정보를 저장한 서버를 물어봄
        * 그리고 받아온 정보로 해당 도메인.com, 도메인.net을 물어봄
        * 그럼 원하는 도메인과 연결된 서버의 목록을 알려주고 ip를 알려줌

---

### 자료 출처

[생활코딩 리눅스](https://opentutorials.org/course/2598)
