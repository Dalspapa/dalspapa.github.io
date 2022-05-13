# 리눅스에서 권한 (Permission)

- 읽기 Read `r` - **`4`**
- 쓰기 Write `w` - **`2`**
  - 생성
  - 삭제
  - 수정
- 실행 Execute `x` - **`1`**

<br/>
<br/>

## 소유주 / 소유그룹 / Others
---

```
[j@localhost ~/down]$ whereis cal
cal: /usr/bin/cal /usr/share/man/man1/cal.1.gz
[j@localhost ~/down]$ ll /usr/bin/cal
-rwxr-xr-x. 1 root root 37688 10월  1  2020 /usr/bin/cal
[j@localhost ~/down]$ chmod 644 /usr/bin/cal
chmod: changing permissions of `/usr/bin/cal': 명령을 허용하지 않음
```

**`-rwxr-xr-x. 1 root root 37688 10월  1  2020 /usr/bin/cal`**
- `root root 37688` 
  - `root` 소유주 
  - `root` 소유그룹 
  - `37688` Others 로 나누어져 있음.   
  <br/>
- `-rwxr-xr-x.` ***3글자**씩 끊어서 권한과 맵핑됨.* 
  - 가장 처음 `-` file을 나타냄.
  - `rwx` 소유주는 읽기, 쓰기, 실행 권한 모두 갖고 있음.
  - `r-x` 소유그룹은 읽기, 실행 권한을 갖고 있음.
  - `r-x` 나머지 사람들도 읽기, 실행 권한을 갖는다.

<br/>

**`chmod 644 /usr/bin/cal`**
- `chmod` ChangeMode
- `644` 루트 권한을 `6` 그룹은 `4` 그 외도 `4`로 설정
  
<br/>
<br/>

## 🤷‍♂️ 숫자 의미
---

### ex) `drwxr-xr--.`
- `d` Directory
- `r` Read 권한은 2의 제곱인 **4**
- `w` Write 권한은 **2**
- `x` Execute 권한은 **1**

**💡 숫자로 변경 !**
- 루트 (`rwx`) 는 모든 권한을 갖고 있기 떄문에 `4+2+1` 해서 **7**
- 루트 그룹은 (`r-x`) 읽기, 실행 권한만 갖고 있기 때문에 `4+1` = **5**  
- 그 외 권한은 (`r--`) 읽기 권한만 갖고 있기 때문에 `4+0+0` = **4**

✌ `drwxr-xr--.` 는 **`754`** 로 표현 가능 하다.

> **`chmod 644 /usr/bin/cal`**
> > 캘린더의 권한을
>>
> > **루트**는 *읽기, 쓰기* 가능
> >
> > **루트 그룹**은 *읽기*만 가능
> >
> > **Others** 도 *읽기*만 가능
> >
> > 하게 변경한다는 뜻.
>
> `chmod` 명령어는 root계정에서만 가능.