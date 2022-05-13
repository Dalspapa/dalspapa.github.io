# 리눅스에서 C언어 코딩

### GCC 설치
---
1. gcc 설치 확인
    ```
    [j@localhost ~]$ gcc
    -bash: gcc: command not found
    ```

2. 루트 계정 전환 후 gcc 설치
    ```
    [j@localhost ~]$ su -
    암호:
    마지막 로그인: 수  5월 11 17:34:32 KST 2022 일시 tty1
    [root@localhost ~]# yum -y install gcc^C
    ```

3. 확인 후 로그아웃
    ```
    [root@localhost ~]# rpm -qa | grep gcc
    libgcc-4.8.5-44.el7.x86_64
    gcc-4.8.5-44.el7.x86_64
    [root@localhost ~]# gcc
    gcc: fatal error: no input files
    compilation terminated.
    [root@localhost ~]# exit
    logout
    ```
    
4. vim 진입 (확장자는 반드시 **.c**)
    ```
    [j@localhost ~]$ whoami
    j
    [j@localhost ~]$ vi t.c
    ```

<br/>

### vim에서 C Coding
---
`:se nu` vi에 행번호 붙히기.

```c
#include <stdio.h>

int main(void) {
    puts(" 재밌는 리눅스 \n");
    return 0;
}
```

`:wq` 코드 작성 후 저장 종료.

<br/>

#### 작성 파일 확인
---
**GCC**
: _원래는 GNU C Compiler를 의미 했지만 1999년부터 GNU Compiler Collection을 의미한다._

> 1. `[j@localhost ~]$ gcc t.c`
>> _gcc 컴파일 완료. (무소식이 희소식.)_
> 2. `[j@localhost ~]$ ls`
> `TEST  a.out  aa  b  bb  bbb  dd  ddd  p  s  t.c`
>> `a.out` 파일 확인.
> 3. `[j@localhost ~]$ a.out`
> `-bash: a.out: command not found`
>> _`a.out` 파일 진입 실패_
> 4. `[j@localhost ~]$ ./a.out`
> `재밌는 리눅스`<br/>
>> _`a.out` 파일 정상 실행됨._

<br/>

#### PATH=$PATH:.
---
> `[j@localhost ~]$ echo $PATH`
>> `/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/j/.local/bin:/home/j/bin`
>
> `[j@localhost ~]$ PATH=$PATH:.`
>
> `[j@localhost ~]$ echo $PATH`
>> `/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/j/.local/bin:/home/j/bin:.`
>
> `[j@localhost ~]$ a.out`
>> `재밌는 리눅스`
>> <br/>

<br/>

**❓ command not found** 
> **현재 위치`./`** path 명시하지 않았기 때문.

**❗ PATH=$PATH:.**
> "**`./`**" 생략하고 파일 접근 가능.
> **`/home/j/bin:.`**
_로그아웃 하면 설정 초기화 됨._

<br/>

#### gcc 컴파일 옵션
---
#### `gcc t.c -o FILENAME` 
- **`-o`** output의 약어.

> `[j@localhost ~]$ gcc t.c -o aa`
> `[j@localhost ~]$ ls`
>> `TEST  a.out  aa  b  bb  bbb  dd  ddd  p  s  t.c`
>
> `[j@localhost ~]$ aa`
>> `재밌는 리눅스`
>> <br/>
>
> `[j@localhost ~]$ a.out`
>> `재밌는 리눅스`
>> <br/>