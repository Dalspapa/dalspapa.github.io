# `alias` : 명령어 별칭

<br/>

## 핑테스트 `alias` 적용
---

```
[j@localhost ~]$ alias pt='ping -c3 8.8.8.8'
[j@localhost ~]$ pt
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=35.3 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=34.5 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=42.4 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 34.570/37.456/42.430/3.538 ms
```

> `alias pt='ping -c3 8.8.8.8'`
> 
> `pt` 명령어만 입력해도 핑테스트 가능

<br/>

## `alias` 만 입력
---

```
[j@localhost ~]$ alias
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias pt='ping -c3 8.8.8.8'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

> 지정된 `alias` 명령어들을 확인할 수 있다.

<br/>

## `unalias`
---

```
[j@localhost ~]$ unalias pt
```

> 지정된 `alias` 삭제

<br/>

## `ls` 명령어
---

```
TEST  a.out  aa  b  bb  bbb  dd  ddd  down  p  s  t.c
[j@localhost ~]$ ls --color=auto
TEST  a.out  aa  b  bb  bbb  dd  ddd  down  p  s  t.c

// 파일 : 파란색 / 디렉토리 : 흰색으로 표시
```

> `ls` 명령어는 디폴트로 `alias` 되어있음
>
> `ls --color=auto`

### `alias` 미적용된 `ls`
---

```
[j@localhost ~]$ \ls
TEST  a.out  aa  b  bb  bbb  dd  ddd  down  p  s  t.c
[j@localhost ~]$
```

> '\' 백슬러시 붙히면 색상 적용되지 않음.
> 
> 원래 unix `ls` 명령어는 색상 표시 x
> 
> `ls -l` 구분 위해 `-l` 옵션 붙힘
>
> d: directory / - : file / l : symbolic link

<br/>

***💡 새로운 세션에서는 적용된 alias가 해제 됨.***

<br/>
<br/>

# `history` : 명령어 역사

*방금 전에 내가 내린 명령어 보여줌*

<br/>

```
[j@localhost ~]$ history
    1  who
    2  cal
    3  date
    4  ps -ef
    5  rpm -qa | grep
    6*
    7  rpm -qa | mail
    8  rpm -qa | httpd
    9  rpm -qa | gcc
   10  rpm -qa | grep mail
   11  rpm -qa | grep httpd
   12  rpm -qa | grep gcc
   13  history
```

> 📌 TIP
> 
> 위쪽 방향기로 방금 전에 내린 명령어 불러올 수 있음.
> `Ctrl + P` 로 위쪽 방향키 역할 가능
> 
> `Ctrl + N` 넥스트, 아래 방향키 역할
> 
> *키보드 방향키 까지 가지 않고 코딩 가능*
 
<br/>

## [ !숫자 ] `!123` 
---

```
[j@localhost ~]$ history
    1  who
    2  cal
    3  date
    4  ps -ef
    5  rpm -qa | grep
    6*
    7  rpm -qa | mail
    8  rpm -qa | httpd
    9  rpm -qa | gcc
   10  rpm -qa | grep mail
   11  rpm -qa | grep httpd
   12  rpm -qa | grep gcc
   13  history
   14  A=500
   15  B="boss"
   16  echo $A
   17  echo $B
   18  unset A
   19  echo $A
   20  ping -c3 8.8.8.8
   21  history
[j@localhost ~]$ !20
ping -c3 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=54.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=74.0 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=58.8 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2007ms
rtt min/avg/max/mdev = 54.836/62.561/74.025/8.272 ms
[j@localhost ~]$
```

> `history` 명령어에 붙어 있는 번호를 이용해 빠르게 명령 내릴 수 있다.
> 
> `!20` : 20 번째에 해당하는 핑테스트 실행됨.

<br/>

## [ `!!` ] bangbang 명령어
---

```
[j@localhost ~]$ !!
ping -c3 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=45.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=57.6 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=66.0 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 45.821/56.505/66.007/8.287 ms
```

> `!!` :  방금 전에 내린 명령어 실행됨

<br/>

## [ !첫문자열 ] `!p`
---

```
[j@localhost ~]$ !d
date
2022. 05. 19. (목) 16:37:50 KST
```

> 가까운 명령어 중 해당 문자열과 가장 매칭되는 명령어를 찾아줌

## [ history 숫자 ] `history 5`
---

```
[j@localhost ~]$ history 5
   20  ping -c3 8.8.8.8
   21  history
   22  ping -c3 8.8.8.8
   23  date
   24  history 5
```

> 최근 사용한 명령어 중 끝에서 5개 불러옴.

<br/>

## [ `echo $HISTRSIZE` ]
---

```
[j@localhost ~]$ echo $HISTSIZE
1000
[j@localhost ~]$
```

> 보관하는 히스토리 갯수 출력해줌. (stack에 보관)

<br/>
<br/>

## 쉘 프로그래밍
---

```
[j@localhost ~]$ A=500
[j@localhost ~]$ B="boss"
[j@localhost ~]$ echo $A
500
[j@localhost ~]$ echo $B
boss
```

>`$` 는 변수를 뜻함.
>> `echo $A`
>>> "A가 갖고 있는 값이 무엇이니?"

```
[j@localhost ~]$ unset A
[j@localhost ~]$ echo $A

[j@localhost ~]$
```

> [ `unset` 명령어 ] 로 변수 해제

<br/>

## HISTTIMEFORMAT 변수에 시간 담기 
---

```
[j@localhost ~]$ HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "
[j@localhost ~]$ history
    1  2022-05-19 16:19:04 who
    2  2022-05-19 16:19:05 cal
    3  2022-05-19 16:19:06 date
    4  2022-05-19 16:19:16 ps -ef
    5  2022-05-19 16:19:29 rpm -qa | grep
    6* 2022-05-19 16:19:46
    7  2022-05-19 16:19:59 rpm -qa | mail
    8  2022-05-19 16:20:07 rpm -qa | httpd
    9  2022-05-19 16:20:15 rpm -qa | gcc
   10  2022-05-19 16:20:33 rpm -qa | grep mail
   11  2022-05-19 16:20:39 rpm -qa | grep httpd
   12  2022-05-19 16:20:44 rpm -qa | grep gcc
   13  2022-05-19 16:20:56 history
   14  2022-05-19 16:22:46 A=500
   15  2022-05-19 16:22:57 B="boss"
   16  2022-05-19 16:23:01 echo $A
   17  2022-05-19 16:23:07 echo $B
   18  2022-05-19 16:26:00 unset A
   19  2022-05-19 16:26:07 echo $A
   20  2022-05-19 16:30:42 ping -c3 8.8.8.8
   21  2022-05-19 16:30:47 history
   22  2022-05-19 16:31:12 ping -c3 8.8.8.8
   23  2022-05-19 16:37:50 date
   24  2022-05-19 16:41:15 history 5
   25  2022-05-19 16:42:41 echo $HISTSIZE
   26  2022-05-19 16:46:03 HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "
   27  2022-05-19 16:46:25 history
```

> `HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "`
> 
> 해당 명령어 내린 날짜와 시간을 알 수 있다.