# 리눅스 디렉토리 구조

---
## /
- 기본 계층 모든 파일 시스템 계층의 기본인 루트 디렉토리
- 최상위 디렉토리로 모든 디렉토리들의 시작점.
- 모든 디렉토리들을 절대경로로 표기할 때에 이 디렉토리부터 시작해야 함.
- 파티션 설정 시 반드시 존재하여야 함.
- 주의! `/` 와 `/root` 는 완전히 다른 것임.

---
## /bin
_일반 사용자들이 사용하는 명령어(cat, ls, cp 명령어 등) 집합._
**bin -> usr/bin**
> **bin** : Binary 약자. 실행 파일들을 모아둠.
> **->** : Symbolic link. 윈도우식으로 _바로가기 링크_ 라고 이해.
> **usr/bin** : bin이 가르키는 usr/bin이 진짜.

---
## /boot
_Booting과 관련된 파일 모음 / **kernel** 여기 들어 있음._
> **Kernel** : _Linux® 커널은 Linux 운영 체제(OS)의 주요 구성 요소이며 컴퓨터 하드웨어와 프로세스를 잇는 핵심 인터페이스입니다. 그리고 두 가지 관리 리소스 사이에서 최대한 효과적으로 통신합니다._
#### 커널의 기능
1. **메모리 관리** : 메모리가 어디에서 무엇을 저장하는 데 얼마나 사용되는지를 추적합니다.
2. **프로세스 관리** : 어느 프로세스가 중앙 처리 장치(CPU)를 언제 얼마나 오랫동안 사용할지를 결정합니다.
3. **장치 드라이버** : 하드웨어와 프로세스 사이에서 중재자/인터프리터의 역할을 수행합니다.
4. **시스템 호출 및 보안** : 프로세스의 서비스 요청을 수신합니다.

---
## /dev
_Device 약자 / **장치 파일**(키보드, 모니터, 하드디스크, USB 등) 을 의미._ 

---
## /etc
- 시스템 설정의 설정 파일을 담고 있음.
- 윈도우의 제어판이나 레지스트리에 해당됨.

---
## /home
_저장된 파일, 개인 설정, 기타 등을 포함한 사용자의 홈 디렉토리_
- 윈도우의 C:\Users 에 해당됨.
- useradd 라는 명령어로 새로운 사용자를 생성하면 대부분 사용자의 ID 와 동일한 이름의 디렉토리가 자동으로 생성됨.

---
## /lib
_library의 약자 / 관련된 공유 라이브러리 / 윈도우식으로 dll(4bit)같은 것들이 들어 있음._
- /bin/ 과 /sbin/ 에 있는 바이너리용 라이브러리.
- 주의! 함부로 삭제 시세 시스템이 멈출 수가 있음.

---
## /media
_CD-ROM 과 같은 이동식 미디어의 마운트 지점
(2004년 FHS-2.3 에서 적용됨)_

---
## /mnt
_임시로 마운트되는 파일 시스템_

---
## /opt
_리눅스 이외에 추가로 사용할 응용 소프트웨어 패키지_

---
## /proc
_Process 약자 / 메모리 상태의 설정값들 저장 / 하드디스크가 아닌 메모리 상태._
- 프로세스 및 커널 정보를 파일로 제공하는 가상 파일 시스템.
- 리눅스에서는 procfs 마운트에 해당되며 윈도우의 장치관리자에 해당됨.
- 일반적으로 자동으로 시스템에 의해 생성되고 채워짐.
- 실제 운용 상태를 정확하게 파악할 수 있는 중요한 정보를 제공함.
(여기에 존재하는 파일들 가운데 현재 실행 중인 커널의 옵션값을 즉시 변경할 수 있는 파라미터 파일들이 있기 때문에 시스템 운용에 있어 매우 중요한 의미를 가짐)
- 대부분 읽기 전용이나 일부 파일 중에는 쓰기가 가능한 파일이 존재하는데 이러한 파일들에 특정 값을 지정하면 커널 기능이 변하게 됨.

---
## /root
_시스템 최고관리자인 Root 사용자의 Home Directory_

---
## /run
_런타임 변수 데이터 / 마지막 부팅 이후 실행 중인 정보._
- ex. 현재 로그인 한 사용자 및 실행 중인 데몬.
- 이 디렉토리의 파일은 부팅 시 제거되어야 함.
그러나 이 디렉토리는 임시 파일 시스템(tmpfs)으로 제공하는 시스템에서는 필요하지 않음.

---
## /sbin
_Super User Binary. / 시스템 관리자가 사용하는 명령어 집합._
- 필수 시스템 바이너리.
ex. init, ip, route
- 주로 시스템 관리자들이 사용하는 시스템 관리자용 명령어를 저장하고 있는 디렉토리.
(/sbin – 대부분 root 사용자용, /bin - 공동)

---
## /srv
_웹 서버 스크립트 및 데이터, FTP 서버가 제공하는 데이터, 버전 제어 시스템용 저장소와 같은 시스템에서 제공하는 사이트별 데이터_
_(2004년 FHS-2.3 에서 적용됨)_

---
## /sys
_장치, 드라이버 및 일부 커널 기능에 대한 참조된 정보._

---
## /tmp
- 임시 디렉토리 (/var/tmp 참고) / 윈도우의 temp 폴더 같은 개념.
- Sticky bit / 끝에 t 옵션이 들어가 있음.
- 일반 사용자 자신의 홈 디렉토리 이외에 사용할 수 없으나 tmp는 사용 가능.
- 공용 디렉토리 – 시스템을 사용하는 모든 사용자들이 공동으로 사용하는 디렉토리
(ex. MySQL 에서 사용하는 소켓 파일(mysql.sock)이나 Apache 에서 사용하는 세션 파일(session file) 등이 생성되기도 함)
- 시스템의 일반적인 사용자 또는 각종 프로세스에서 사용되는 파일들이 생성되는 위치
- _웹해킹에 사용되는 파일이 업로드 되는 위치이므로 주의가 요구되는 디렉토리_

---
## /usr
_읽기 전용 사용자 데이터가 있는 보조 계층 구조_
- Uinix System Resource의 약자. 
- 주요(다중) 사용자의 유틸리티와 애플리케이션을 포함하고 있음.
- 윈도우의 C:\Program Files 에 해당되지만 리눅스에서는 더 큰 의미를 가짐.
- 프로그램 설치하면 이 곳에 존재. 
- 용량 가장 큼.

---
## /var
_시스템 운용 중에 생성되었다가 삭제되는 데이터를 일시적으로 저장하기 위한 디렉토리_
- variable의 약자.
- 가변적인 파일.
- 웹 서비스, HTTP 서비스, HTML 문서 같은 것이 여기에 있음.
- 일반적인 시스템의 정상적인 작동 중에 내용이 계속 변경될 것으로 예상되는 파일.
(로그 파일, 스풀 파일, 임시 이메일 파일)

---

