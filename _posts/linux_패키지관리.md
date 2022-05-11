# 리눅스 패키지 관리

### 사용자 변경  
---
> *`su -`* 명령어로 변경. 암호는 root 암호.  

<br/>
### Redhat Package Manager
---
`rpm -qa | nl` : Redhat Package Manager -Query All | Number Line  

`rpm -qa > rpmList` : rpm 내용을 rpmList 이름으로 저장  

`rpm -qa | grep python` : rpm 내용 중 python이 포함된 내역 검색

<br/>
### 네트워크 테스트
---
`ping -c3 8.8.8.8` : 패킷 3개 주고 받아보면서 테스팅.  

<br/>
### FTP / VIM 조회 및 설치, 삭제
---
- **YUM 명령어로 설치**  
    - `yum -y install ftp`  
    - `yum -y install vim`  

- **설치 후 조회**  
    - `rpm -qa | grep ftp`  
    - `rpm -qa | grep vim`  

- **삭제**  
    - `rpm -e ftp` : `-e`는 eraser의 약어.