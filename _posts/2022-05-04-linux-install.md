
# Linux 기초 지식
## GNU
_'Gnu is Not Unix'_ 를 의미하는 재귀적 약어.
- 유닉스와 완벽하게 호환하는 소프트웨어 시스템.
- 모든 이가 자유롭게 사용할 수 있도록 작성.
## 리눅스란?
1991년 핀란드 헬싱키의 대학생이었던 **Linus Torvalds**가 Minix라는 유닉스 클론을 IBM PC에 호환될 수 있도록 개발한 GNU 운영체제.
- 누구나 자유롭게 사용할 수 있는 운영체제.
- 여러 사용자(Multi-user)가 동시에 사용할 수 있는 환경 제공.
- 다중 작업(Multi Tasking) 및 가상 터미널(Virtual Terminal) 환경 지원.
- GUI 방식의 X-Windows 지원
- CPU 구애가 없는 운영체계.
- 강력하면서 안정적인 네트워크를 지원하는 운영체계.
- 하드웨어 드라이버 설정 및 하드웨어 사용이 매우 쉬움.
- 이식성이 강한 운영체계.
	+ 리눅스는 유닉스 표준인 POSIX (Portable Operating System Interface for Computer Environments) 표준에 따라 개발됨.
- 다양한 배포판 지원.

# Linux 설치
가상머신 **VirtualBox**를 이용한 **CentOS 7** 버전 설치. 
## Oracle VM VirtualBox
> ### [VirtualBox](https://www.virtualbox.org/wiki/VirtualBox)  6.1.34 platform packages
## CentOS 7 (X-windows)
>### [CentOS-7-x86_64-NetInstall-2009.iso](http://ftp.kaist.ac.kr/CentOS/7.9.2009/isos/x86_64/CentOS-7-x86_64-NetInstall-2009.iso "CentOS-7-x86_64-NetInstall-2009.iso"

## 설치과정
```
	1. VirtualBox에서 새로만들기 클릭.
	2. 이름 : CentOS7 / Red Hat (64-bit) -> 다음 클릭
	3. 메모리 크기 / 하드 디스크 / 물리적 하드 / 파일 위치 및 크기 
	   모두 기본 디폴트 값으로 설치 -> 만들기 클릭
	4. 설정 -> 저장소 -> 컨트롤러 : IDE -> 비어 있음 -> 광학 드라이브 아이콘 -> 
	   디스크 파일 선택 -> ISO파일 찾아서 선택 -> 확인 -> 시작
```
OS상에서 설치 과정
```
1. Install CentOS 7 선택
2. 파일 -> 환경설정 -> 입력 -> 가상 머신 탭에서 
   호스트 키 조합 단축키를 F12로 변경 (가상머신 밖으로 나갈 때 F12키 사용)
3. 설치 언어 선택
4. KDUMP 활성화 해제 / Security Policy 끄기 
5. 네트워크 및 호스트명 -> 이더넷 연결 -> 호스트 이름 설정 (디폴트 값으로 설정)
6. Root : 암호 : r 
7. 사용자  :  j  /  암호 j

기초 수업 기준으로 강좌 따라가며 설치 하였습니다.
```
  설치 완료 후 CHECK !
 ```
  localhost login : root
  Password : r

  localhost login : j
  Password : j

사용한 명령어
whoami : 로그인한 사용자 확인.
exit : 새로운 사용자로 로그인하기 위해 나가기. Ctrl + D 가능.
df -h : 하드디스크 파티션 정보
rpm -qa | nl : package 설치 수 301.
ping 8.8.8.8 : 핑테스트. 외부 네트워크 연결 확인. 확인 후 Ctrl + C로 끊어줌.
```

# 리눅스 기초 명령어 

## **💻 필수 명령어들 요약**

-   **1. ls - 현재 위치의 파일 목록 조회**
-   **2. cd - 디렉터리 이동**
-   **3. touch - 0바이트 파일 생성, 파일의 날짜와 시간을 수정**
-   **4. mkdir - 디렉터리 생성**
-   **5. cp - 파일 복사**
-   **6. mv - 파일 이동**
-   **7. rm - 파일 삭제**
-   **8. cat - 파일의 내용을 화면에 출력, 리다이렉션 기호('>')를 사용하여 새로운 파일 생성**
-   **9. redirection - 화면의 출력 결과를 파일로 저장**
-   **10. alias - 자주 사용하는 명령어들을 별명으로 정의하여 쉽게 사용할 수 있도록 설정**

## **🔎 명령어 옵션과 설명**

#### **1. ls (List segments) : 현재 위치의 파일 목록 조회**

-   **ls -l : 파일의 상세정보**
-   **ls -a : 숨김 파일 표시**
-   **ls -t : 파일들을 생성시간순(제일 최신 것부터)으로 표시**
-   **ls -rt : 파일들을 생성시간순(제일 오래된 것부터)으로 표시**
-   **ls -f : 파일 표시 시 마지막 유형에 나타내는 파일명을 끝에 표시**  
    **('/' : 디렉터리, '*' : 실행파일, '@' : 링크 등등,,,)**

#### **2. cd (Change directory) :디렉터리 이동**

-   **cd [디렉터리 경로] : 이동하려는 디렉터리로 이동 (경로 입력 시 '[', ']'부분은 빼고 입력!)**
-   **cd ~ : 홈 디렉터리로 이동**
-   **cd / : 최상위 디렉터리로 이동**
-   **cd . : 현재 디렉터리**
-   **cd .. : 상위 디렉터리로 이동**
-   **cd - : 이전 경로로 이동**

#### **3. touch : 0바이트 파일 생성, 파일의 날짜와 시간을 수정**

-   **touch filename : filename의 파일을 생성**
-   **touch -c filename : filename의 시간을 현재시간으로 갱신**
-   **touch -t 202110291608 filename : filename의 시간을 날짜 정보(YYYYMMDDhhmm)로 갱신**  
    **(20211029160 => 2021.10.29.16:08)**
-   **touch -r oldfile newfile  :  **newfile**의 날짜 정보를  **oldfile****의 날짜 정보와 동일하게 변경****

#### **4. mkdir (Make dirctory) : 디렉터리 생성**

-   **mkdir dirname : dirname이라는 디렉터리 생성**
-   **mkdir dir1 dir2: 한 번에 여러 개의 디렉터리 생성**
-   **mkdir -p dirname/sub_dirname : dirname이라는 디렉터리 생성, sub_dirname이라는 하위 디렉터리도 생성**
-   **mkdir -m 700 dirname : 특정 퍼미션(권한)을 갖는 디렉터리 생성**

**<파일의 퍼미션>**

**8진수**

**2진수**

**권한**

**의미**

**0**

**000**

**---**

**아무 권한 없음**

**1**

**001**

**--x**

**실행 권한만 있음**

**2**

**010**

**-w-**

**쓰기 권한만 있음**

**3**

**011**

**-wx**

**쓰기,실행 권한 있음**

**4**

**100**

**r--**

**읽기 권한만 있음**

**5**

**101**

**r-x**

**쓰기,실행 권한 있음**

**6**

**110**

**rw-**

**읽기,쓰기 권한 있음**

**7**

**111**

**rwx**

**모든 권한 있음**

예를 들어 '777'의 경우 이진수로 111111111이고 rwxrwxrwx라는 의미를 가지므로 파일 소유자, 소유 그룹, 일반 사용자에게 읽기, 쓰기, 실행의 모든 권한을 주는 설정이다.

#### **5. cp (Copy) : 파일 복사**

-   **cp file1 file2 : file1을 file2라는 이름으로 복사**
-   **cp -f file1 file2 : 강제 복사(file2라는 파일이 이미 있을 경우 강제로 기존 file2를 지우고 복사 진행)**
-   **cp -r dir1 dir2 : 디렉터리 복사. 폴더 안의 모든 하위 경로와 파일들을 복사**

#### **6. mv  **(Move) :**  파일 이동**

-   **mv file1 file2 : file1 파일을 file2 파일로 변경**
-   **mv file1 /dir : file1 파일을 dir 디렉터리로 이동**
-   ****mv file1 file2 /dir : 여러 개의 파일을 dir 디렉터리로 이동****
-   ****mv /dir1 /dir2 : dir1 디렉터리를 dir2 디렉터리로 이름 변경****

#### **7. rm  **(Remove) :**  파일 삭제**

-   **rm file1 : file1을 삭제**
-   **rm -f file1 : file1을 강제 삭제**
-   **rm -r dir : dir 디렉터리 삭제 (디렉터리는 -r 옵션 없이 삭제 불가)**

#### **8. cat  ****(Catenate) :****  파일의 내용을 화면에 출력, 리다이렉션 기호('>')를 사용하여 새로운 파일 생성**

-   **cat file1 : file1의 내용을 출력**
-   **cat file1 file2 : file1과 file2의 내용을 출력**
-   **cat file1 file2 | more : file1과 file2의 내용을 페이지별로 출력**
-   **cat file1 file2 | head : file1과 file2의 내용을 처음부터 10번째 줄까지만 출력**
-   **cat file1 file2 | tail : file1과 file2의 내용을 끝에서부터 10번째 줄까지만 출력**

#### **9. redirection ('>', '>>') : 화면의 출력 결과를 파일로 저장**

**'>' 기호 : 기존에 있는 파일 내용을 지우고 저장  
'>>' 기호 : 기존 파일 내용 뒤에 덧붙여서 저장  
'<' 기호 : 파일의 데이터를 명령에 입력**

-   **cat file1 firle2 > file3 : file1, file2의 명령 결과를 합쳐서 file3라는 파일에 저장**
-   **car file4 >> file3 : file3에 file4의 내용 추가**
-   **cat < file1 : file1의 결과 출력**
-   **cat < file1 > file2 : file1의 출력 결과를 file2에 저장**

#### **10. alias : 자주 사용하는 명령어들을 별명으로 정의하여 쉽게 사용할 수 있도록 설정**

```
alias 별명 = '명령어 정의'
```

ex) alias lsa = 'ls -a' : lsa를 실행하면 -a 옵션을 갖는 ls를 실행합니다.

```
unalias lsa
```

unalias lsa : lsa라는 alias를 해제