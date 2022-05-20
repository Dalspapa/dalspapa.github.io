# 쉘

<br/> 

## 🍕 환경변수

<br/>

### 🍺 `echo $SHELL`
---

- 현재 사용하는 쉘을 보여줌.

- ***`$` 가 붙으면 환경변수***

### 🍺 `env`
---

- 환경변수의 창구
- 어떤 변수의 어떤 값이 들어가 있는지 확인 가능

### 🍺 `chsh -l`
---
- Change Shell 의 약어
- 바꿀 쉘의 리스트를 보여줌

<br/>
<br/>

## 🍕 bash 로그인시 일어나는 일

<br/>

### 🍺 `vi /etc/profile`
---

*`/etc` 밑의 파일은 열어서 볼 수는 있지만, 수정 불가*

- `#` 으로 시작하는 것은 주석문
- 함수들로 이루어져 있음

<br/>

### 🍺 bash 로그인시 실행되는 파일들
---

1. `/etc/profile` 
   - etc 디렉토리에 있는 profile 파일을 읽는다.

2. `/etc/profile.d/*.sh`
    - profile.d 디렉토리에 있는 sh파일을 읽어 나간다.

3. 🍜 `~/.bash_profile` 
    - '`.`' 으로 시작하는 파일은 숨김파일
    - 환경 변수와 bash가 수행될 때 실행되는 프로그램을 제어하는 지역적인 시스템 설정과 관련된 파일
    - 환경 변수들은 오직 해당 사용자에게만 한정
    - 이 파일은 전역적인 설정 파일인 /etc/profile이 수행된 다음 곧바로 수행
     
4. 🍜 `~/.bashrc` 
    - 별칭(alias)과 bash가 수행될 때 실행되는 함수를 제어하는 지역적인 시스템 설정과 관련된 파일
    - 별칭과 함수들은 오직 해당 사용자에게만 한정

5. 🍜 `~/.bash_logout`
   - 사용자가 로그 아웃하기 바로 직전에 실행하는 프로그램에 관한 bash의 지역적인 시스템 설정과 관련된 파일

6. 🍜 `~/.bash_history`
   - 사용했던 명령어 기록

<br/>

**.bash_profile**
> `cd ~`
>
> `vi .bash_profile`

```
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific enviroment and startup programs

PATH=$PATH:$HOME/.local/bin:$HOME/bin

NAME="이은사"
AGE=31

export PATH
```

> `:wq` 로 저장

- `#` 은 주석
- `[]` 대괄호 안에 있는 것이 조건문
- `-f` 파일의 존재 여부를 물어봄
- 참이면 `then` 밑에 구절 실행
- `.` 찍혀있고 파일이름이 있음. 그 파일을 인클루드.
- `PATH` 라는 변수에 값 `$PATH:$HOME/.local/bin:$HOME/bin`
- 원하는 변수 설정할 수 있음.

<br/>

**저장한 `.bash_profile` 변수 읽기**

```
[j@localhost ~]$ vi .bash_profile
[j@localhost ~]$ echo $AGE

[j@localhost ~]$ echo $NAME

[j@localhost ~]$ . ~/.bash_profile
[j@localhost ~]$ echo $AGE
31
[j@localhost ~]$ echo $NAME
이은사
```

> `. ~/.bash_profile` 명령어로 재설정 해야 나옴.
>> 로그아웃 후 로그인과 같은 효과

<br/>

**부모쉘 자식쉘 (`bash`명령어)**

```
[j@localhost ~]$ . ~/.bash_profile
[j@localhost ~]$ echo $NAME
이은사
[j@localhost ~]$ echo $AGE
31

[j@localhost ~]$ bash

[j@localhost ~]$
[j@localhost ~]$ echo $NAME

[j@localhost ~]$ . ~/.bash_profile
[j@localhost ~]$ echo $AGE
31
[j@localhost ~]$
```

> `bash` 명령어로 자식쉘 생성
> > 부모쉘의 설정된 변수가 자식쉘에 영향을 미치지 않음
> > >즉, **지역변수**

<br/>

**전역변수화 시키기 (`export`명령어)**

```
[j@localhost ~]$ bash
[j@localhost ~]$
[j@localhost ~]$ echo $NAME

[j@localhost ~]$ . ~/.bash_profile
[j@localhost ~]$ echo $AGE
31
[j@localhost ~]$ exit
exit
[j@localhost ~]$ export AGE
[j@localhost ~]$ bash
[j@localhost ~]$ echo $AGE
31
[j@localhost ~]$ echo $NAME

[j@localhost ~]$
```

> `export AGE` 로 인해 AGE 변수가 전역화 되었음.
> > `echo $AGE` 명령어 입력시 변수 값 출력됨.
> 
> 계정 재접속시 설정한 변수나 함수 유지되게 할 수 있음.

<br/>

**알리아싱 적용시키기**

`vi .bashrc` 에디터 접근

```
# .bashrc

# Source global definitions
if [ -f /etcbashrc ]; then
        . /etc/bashrc
fi

# Uncomment the following line if you don't like systemctl's auo-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions

alias h='history'
alias c='clear'
alias pt='ping -ping c3 8.8.8.8'

```

>`. ~/.bashrc` 로 재실행
>> 새로 로그인해도 알리아싱 잘 됨

<br/>

**`.` 생략하고 파일 읽기**

> `vi .bash_profile`

```
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific enviroment and startup programs

PATH=$PATH:$HOME/.local/bin:$HOME/bin:.

NAME="이은사"
AGE=31

export PATH
```

- `PATH=$PATH:$HOME/.local/bin:$HOME/bin`
- `PATH=$PATH:$HOME/.local/bin:$HOME/bin:.`
-  패스정보 뒤에 접근자 붙혀줌 `:.`

```
[j@localhost ~]$ ls
TEST  a.out  aa  b  bb  bbb  dd  ddd  down  p  s  t.c
[j@localhost ~]$ aa
 재밌는 리눅스

[j@localhost ~]$

```

<br/>
<br/>
<br/>

## 🍕 리눅스 쉘(bash)

<br/>

### 🍺 쉘 종류
---

-   쉘(shell)
    -   운영체제 커널과 사용자 사이를 이어주는 역할
    -   사용자의 명령을 해석하고, 커널에 명령을 요청해주는 역할  

<br/>

-   유닉스/리눅스 쉘 종류
    -   Bourne-Again Shell (bash) : GNU 프로젝트의 일환(sh의 클론)으로 개발됨, 리눅스 거의 디폴트
    -   Bourne Shell (sh)
    -   C Shell (csh)
    -   Korn Shell (ksh) : 유닉스에서 가장 많이 사용됨
    -   Z Shell : 비교적 최근의 쉘 종류

<br/>
<br/>

###  🍺 리눅스 기본 명령어 정리
---

-   리눅스 명령어는 결국 쉘이 제공하는 명령어임
-   리눅스 기본 쉘이 bash 이므로, **bash에서 제공하는 기본 명령어**를 배우는 것임  
      
    
- 🍟  **whoami : 로그인한 사용자 ID를 알려줌**
    
    ```
    # whoami
    root
    ```
    
- 🍟  **passwd : 로그인한 사용자 ID의 암호 변경**
    
    ```
    # passwd
    Enter new UNIX password:
    Retype new UNIX password:
    passwd: password updated successfully
    ```
    
- 🍟  **pwd : 현재 디렉토리 위치**
    
    ```
    # pwd
    /
    ```
    
- 🍟  **cd : 디렉토리 이동**
    

    ```
    # pwd
    /etc
    # cd ~
    # pwd
    /root
    # cd -
    # pwd
    /etc
    ```

- 🍟  **ls : 파일 목록 출력**

    ```
    # ls -al
    total 32
    drwxr-xr-x 4 root root 4096 Oct  3 09:51 .
    drwxr-xr-x 1 root root 4096 Oct  4 03:52 ..
    drwxr-xr-x 2 root root 4096 Oct  3 09:47 conf.d
    -rwxr-xr-x 1 root root  120 Jul 19 19:28 debian-start
    -rw------- 1 root root  317 Oct  3 09:47 debian.cnf
    lrwxrwxrwx 1 root root   24 Oct  3 09:47 my.cnf -> /etc/alternatives/my.cnf
    -rw-r--r-- 1 root root  839 Jan 21  2017 my.cnf.fallback
    -rw-r--r-- 1 root root  682 Feb  3  2017 mysql.cnf
    drwxr-xr-x 2 root root 4096 Oct  3 12:47 mysql.conf.d
    ```

- 🍟  **와일드 카드**
    -   `*` 는 임의 문자열
    -   `?` 는 문자 하나

    ```
    # ls debi* -al
    -rwxr-xr-x 1 root root 120 Jul 19 19:28 debian-start
    -rw------- 1 root root 317 Oct  3 09:47 debian.cnf
    ```

- 🍟  **cat : 파일 보기**
    
    ```
    # cat mysql.cnf
    mysql.cnf 파일 내용이 출력됨
    ```
    
- 🍟  **head/tail** : head 는 파일 시작부분, tail 은 끝 부분을 보여줌
    
    ```
    # head mysql.cnf
    mysql.cnf 파일 앞부분만 출력됨 (기본적으로 출력 라인 수가 10으로 정해져 있음)
    # tail mysql.cnf
    mysql.cnf 파일 뒷부분만 출력됨 (기본적으로 출력 라인 수가 10으로 정해져 있음)
    ```
    
- 🍟  **more** : 파일 보기 (화면이 넘어갈 경우, 화면이 넘어가기 전까지 보여줌)
    
    ```
    # more mysql.cnf
    mysql.cnf 파일 내용이 출력됨
    ```
    
- 🍟  **rm** : 파일 및 폴더 삭제
    
    -   주로 사용하는 명령어 형태: rm -rf
    -   r 옵션: 하위 디렉토리를 포함한 모든 파일 삭제
    -   f 옵션: 강제로 파일이나 디렉토리 삭제  
          
        
- 🍟  **man**
    -   manual이라는 의미. man rm을 입력하면 메뉴얼이 나옴

<br/>
<br/>

### 🍺 리눅스 리다이렉션(redirection) 과 파이프(pipe)
---

-   **standard stream**
    -   command 로 실행되는 process 는 세 가지 스트림을 가지고 있음
        -   표준 입력 스트림 (standard input stream)
        -   표준 출력 스트림 (standard output stream)
        -   오류 출력 스트림 (standard error stream)
    -   모든 스트림은 일반적인 plain text로 console 에 출력하도록 되어 있음  
          
        
-   **리다이렉션(redirection)**
    -   스트림 흐름을 바꿔주는 것으로 > 또는 < 을 사용함
    -   예
        1.  `ls > files.txt`
            -   ls 로 출력되는 표준 출력 스트림의 방향을 files.txt 로 바꿔줌 (files.txt 에 ls 로 출력되는 결과가 저장됨)
        2.  `head < files.txt`
            -   files.txt 의 파일 내용이 head 라는 파일의 처음부터 10 라인까지 출력해주는 명령으로 넣어짐 (files.txt 의 앞 10 라인이 출력됨)
        3.  `head < files.txt > files2.txt`
            -   files.txt 의 파일 내용이 head 로 들어가서, files.txt 의 앞 10 라인을 출력
            -   head 의 출력 스트림은 다시 files2.txt 로 들어감
            -   head 는 files.txt 내용을 출력하지 않고, 해당 출력 내용이 다시 files2.txt 에 저장됨(결과적으로 files.txt 의 앞 10 라인이 files2.txt에 저장됨)
        4.  기존 파일에 추가는 `>>` 또는 `<<` 사용
            -   `ls >> files.txt`
            -   기존에 있는 files.txt 파일 끝에, ls 출력 결과를 추가해줌

  

-   **파이프(pipe)**
    -   두 프로세스 사이에서 한 프로세스의 출력 스트림이 또다른 프로세스의 입력 스트림으로 사용될 때 쓰임
        >  `ls | grep files.txt`
            >>   ls 명령을 통한 출력 내용이 grep 명령의 입력 스트림으로 들어감
            >>
            >>   grep files.txt 는 grep 명령의 입력 스트림을 검색해서 files.txt 가 들어 있는 입력 내용만 출력해줌
            >>
            >>   따라서, ls 명령으로 해당 디렉토리/파일 중에 files.txt 파일이 있는지를 출력해줌
    - 🍟  **grep** : 검색 명령
        -   `grep [-option] [pattern] [file or directory name]`
            
            ```
            <option>
              -i : 영문의 대소문자를 구별하지 않는다.
              -v : pattern을 포함하지 않는 라인을 출력한다.
              -n : 검색 결과의 각 행의 선두에 행 번호를 넣는다(first line is 1).
              -l : 파일명만 출력한다.
              -c : 패턴과 일치하는 라인의 개수만 출력한다.
              -r : 하위 디렉토리까지 검색한다.
            ```
            
        -   사용 예
            -   grep python files.txt -> files.txt 라는 파일에서 python 라는 문구가 들어간 모든 행을 출력
            -   grep -n python files.txt -> files.txt 라는 파일에서 python 라는 문구가 들어간 모든 행을 라인까지 출력
            -   grep -r python foldername -> foldername 라는 폴더내의 모든 파일 중 python 라는 문구가 들어간 행을 출력
            -   grep -i python files.txt -> files.txt 라는 파일에서 python 라는 문구를 대,소문자 구분 없이 검색해서 출력
            -   grep -E "go|java|python" files.txt -> files.txt 라는 파일에서 go, java, 또는 python 이 있는 모든 행을 출력

<br/>
<br/>

### 🍺 리눅스 프로세스
---

-   **리눅스 프로세스**
    -   프로세스는 실행 중인 프로그램을 의미
        -   좀더 깊게 이해한다면!
            -   프로세스는 메모리에 적재된 코드(바이너리) 이미지와 가상화된 메모리(가상 메모리)의 인스턴스, 열린 파일 같은 커널 리소스, 관련된 사용자 정보와 같은 보안 정보, 하나 이상의 스레드를 포함
    -   리눅스는 프로세스가 프로그램 실행 단위 (스케쥴링 단위)
        -   프로세스 ID(pid) 라는 unique한 ID를 부여받고, pid를 활용해서 프로세스를 제어
    -   리눅스는 기본적으로 다양한 프로세스가 실행됨
        -   유닉스 철학과 관련: 각 프로그램은 하나의 일을 잘 할 수 있게 만들 고, 새로운 기능이 필요하면, 기존 프로그램에 추가하지 말고, 새로운 프로그램을 만들 것.
        -   여러 프로그램이 서로 유기적으로 각자의 일을 수행하면서 전체 시스템이 동작하도록 하는 모델  
              
<br/>            

-   **foreground process / background process**
    -  🍜 `foreground process` : 쉘(shell)에서 해당 프로세스 실행을 명령한 후, 해당 프로세스 수행 종료까지 사용자가 다른 입력을 하지 못하는 프로세스

    -  🍜 `background process` : 사용자 입력과 상관없이 실행되는 프로세스
        -   쉘(shell)에서 해당 프로세스 실행시, 맨 뒤에 & 를 붙여줌
        -   사용 예
            
            ```
            # find / -name '*.py' > list.txt &
            [1] 57
            ```
            
        -   [1] 은 작업 번호 (job number), 57 은 pid (process ID) 를 나타냄  
                          
<br/>

-   **foreground process 제어하기**
    
    - **🍟 `[CTRL] + z`** : foreground 프로세스를 실행 중지 상태(suspend 모드)로 변경
      - 맨 마지막 [CTRL] + z 로 중지된 프로세스는 bg 명령으로 background 프로세스로 실행될 수 있음
      - **🍟 `jobs` 명령어** : 백그라운드로 진행 또는 중지된 상태로 있는 프로세스를 보여줌
    
    ### find / -name '*.txt'
    ```
    ^Z
    [1]-  Stopped                 find / -name '*.txt'
    ```

    ### find / -name '*.py'
    ```
    ^Z
    [2]-  Stopped                 find / -name '*.py'
    ```

    ### jobs
    ```
    [1]-  Stopped                 find / -name '*.txt'
    [2]+  Stopped                 find / -name '*.py'
    ```

    ### bg
    ```
    [2]+ find / -name '*.py' &
    ```

    ```
    - [CTRL] + c : 프로세스 작업 취소 (해당 프로세스는 완전히 종료됩니다.)
    ```

<br/>
    
-   **프로세스 중지시키기**
    
    -  🍟 **kill** 명령어
        -   사용법
            1.  kill % 작업 번호(job number)
            2.  kill 프로세스 ID(pid)
            3.  작업 강제 종료 옵션 -9
                -   예
                    
                    ```
                    # find / -name '*.py' > list.txt &
                    [1] 57
                    # kill -9 57
                    ```
                    
<br/>

-   **프로세스 상태 확인**
    
    -   🍟 **ps** 명령어

    -   사용법 : `ps [option(s)]`

    -   option(s)
        
        ```
        -a : 시스템을 사용하는 모든 사용자의 프로세스 출력 (보통 aux 와 같이 u, x 옵션과 함께 사용)

        -u : 프로세스 소유자에 대한 상세 정보 출력

        -l : 프로세스 관련 상세 정보 출력
        
        -x : 터미널에 로그인한 후 실행한 프로세스가 아닌 프로세스들도 출력함. 주로 데몬 프로세스(daemon process)까지도 확인하기 위해 사용함. 본래 ps 명령은 현재 쉘(shell)에서 실행한 프로세스들만 보여주기 때문에 이 옵션을 사용하는 경우가 많음

        -e : 해당 프로세스와 관련된 환경 변수 정보도 함께 출력

        -f : 프로세스 간 관계 정보도 출력
        ```

    -   ❗ **데몬 프로세스(`daemon process`)** : daemon은 악마를 의미함. 사용자 모르게 시스템 관리를 위해 실행되는 프로세스로 보통 시스템이 부팅될 때 자동 실행 (예: ftpd, inetd 등) </pre>

    -   ps 출력 정보 항목
        
        ```
        USER : 프로세스를 실행시킨 사용자 ID

        PID : 프로세스 ID

        %CPU : 마지막 1분 동안 프로세스가 사용한 CPU시간의 백분율

        %MEM : 마지막 1분 동안 프로세스가 사용한 메모리 백분율

        VSZ : 프로세스가 사용하는 가상 메모리 크기

        RSS : 프로세스에서 사용하는 실제 메모리 크기

        TTY : 프로세스와 연결된 터미널 포트

        STAT : 프로세스 상태

        START : 프로세스가 시작된 시간

        TIME : 현재까지 사용된 CPU 시간(분:초)

        COMMAND : 명령어
        ```

<br/>    

-   **프로세스 실행 권한**
    
    -   🍟 **sudo 명령어** : root 계정으로 로그인 하지 않은 상태에서 root 권한이 필요한 명령을 실행할 수 있도록 하는 프로그램
        -   기본 사용법
            -   sudo 명령어
        -   사용 예
            -   `sudo apt-get update`
        -   /etc/sudoers 설정 파일에서 다음과 같이 설정을 변경할 수 있음
            
            (visudo 를 쉘에서 명령하면, 해당 설정 파일이 오픈되어 수정 가능함, 물론 통상 root 권한으로 수정)

            1. 특정 사용자가 sudo를 사용할 수 있도록 설정
                ```
                userid       ALL=(ALL)       ALL
                ```

            2. 특정 그룹에 포함된 모든 사용자가 sudo를 사용할 수 있도록 설정
                ```
                %group        ALL=(ALL)       ALL
                ```

            3. 패스워드 생략 설정
                ```
                %group        ALL=(ALL)       NOPASSWD: ALL
                userid        ALL=(ALL)       NOPASSWD: ALL
                ```

<br/>    

-   **주로 사용하는 프로세스 명령** (적어도 이 명령은 편하게 사용해야 함)
    - 🍟 `ps aux | grep 프로세스명` : 프로세스가 실행 중인지를 확인하고, 관련 프로세스에 대한 정보 출력
    
    - 🍟 `kill -9 프로세스 ID(pid)` : 해당 프로세스를 강제로 죽임
    
    - 🍟 `명령 &` : 터미널에서 다른 작업을 해야하거나, 프로세스 실행에 오랜 시간이 걸릴 경우 background 로 실행
    
    - 🍟 `[CTRL] + z` : 프로세스 중지
    
    - 🍟 `[CTRL] + c` : 프로세스 종료(실행 취소)