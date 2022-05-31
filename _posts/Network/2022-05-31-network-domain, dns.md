# 🍕 Domain(도메인)
---

*도메인은 웹 브라우저를 통해 특정 사이트에 진입을 할 때, IP 주소를 대신하여 사용하는 주소.*

- 도메인을 이용해서 한눈에 파악하기 힘든 IP 주소를 보다 분명하게 나타낼 수 있다.
- 만약 IP 주소가 지번 또는 도로명 주소라면, 도메인 이름은 해당 주소에 위치한 상호로 볼 수 있다.

<br/>

## 👉 터미널에서 도메인의 IP 주소를 확인하는 방법
---

터미널에서 명령어 `nslookup`으로 해당 홈페이지의 IP 주소를 확인할 수 있다.
 
<br/>
<br/>
<br/>
 
# 🍕 DNS(Domain Name System)

*웹사이트의 IP 주소와 도메인 주소를 이어주는 환경/시스템*

- 네트워크 상에 존재하는 모든 PC에 IP 주소 존재.
  - 로컬 PC를 나타내는 127.0.0.1 은 localhost 로 사용 가능.
  - 그 외의 모든 도메인 이름은 일정 기간 동안 대여하여 사용.

<br/>

- 도메인 이름을 사용했을 때 입력한 도메인을 실제 네트워크상에서 사용하는 IP 주소로 바꾸고 해당 IP 주소로 접속하는 과정 필요.
  - 이러한 과정, 전체 시스템을 DNS(도메인 네임 시스템)라고 함
  - 이러한 시스템은 전세계적으로 약속된 규칙을 공유

<br/>

- 상위 기관에서 인증된 기관에게 도메인을 생성하거나 IP 주소로 변경할 수 있는 ‘권한’을 부여.
  - DNS는 상위 기관과 하위 기관과 같은 ‘계층 구조’를 가지는 분산 데이터베이스 구조

<br/>
<br/>

## 🍺 DNS의 구성요소
---

*도메인 수가 많기 때문에 DNS 서버 종류를 계층화해서 단계적으로 처리*

<br/>

- **Root DNS Server** 
  - ICANN(국제인터넷주소관리기구)이 직접 관리하는 서버
  - TLD DNS 서버 IP들을 저장해두고 안내하는 역할

<br/>

- **TLD(최상위 도메인) DNS Server** 
  - 도메인 등록 기관(Registry)이 관리하는 서버.
  - Authoritative DNS 서버 주소를 저장해두고 안내하는 역할. 
  - 어떤 도메인 묶음이 어떤 Authoritative DNS Server에 속하는지 아는 이유는 도메인 판매 업체(Registrar)의 DNS 설정이 변경되면 도메인 등록 기관(Registry)으로 전달이 되기 때문.

<br/>

- **Authoritative(권한) DNS Server**
  - **Second-Level Domain(SLD) DNS Server** 라고도 함
  - 실제 개인 도메인과 IP 주소의 관계가 기록/저장/변경되는 서버.
  - 일반적으로 도메인/호스팅 업체의 ‘네임서버’를 말하지만, 개인 DNS 서버 구축을 한 경우에도 여기에 해당.

<br/>

- **Recursive(반복) DNS Server (Resolver)**
  - 인터넷 사용자가 가장 먼저 접근하는 DNS 서버. 
  - 한 번 거친 후 얻은 데이터를 일정 기간(TTL/Time to Live) 동안 캐시라는 형태로 저장해 두는 서버. 
     - (위 3개의 DNS 서버를 매번 거친다면 효율이 낮을 수밖에 없음.) 
  - 직접 도메인과 IP 주소의 관계를 기록/저장/변경하지는 않고 캐시만을 보관. 
  - ISP DNS : 통신사 DNS 서버. ex) `KT/LG/SK` 등 사용자가 실제 쓰는 DNS서버
   - Public DNS : 브라우저 우회 용도로 쓰임 ex) `구글퍼블릭dns`, `클라우드플레어`

<br/>

> *브라우저는 캐시가 저장된 Recursive 서버 사용*
> 
> *실제 네임서버를 설정하는 곳은 Authoritative 서버*

<br/>
<br/>

## 🍺 DNS 동작 방식
---


1. 브라우저에서 "EUNSA.COM"을 검색 

<br/>

2. 사용하고 있는 통신사 **`[ISP DNS Server]`** 에 도메인 주소에 해당하는 IP 주소 요청. (브라우저 기본 DNS 설정은 통신사 DNS 서버)

<br/>

3. `[ISP DNS Server]`에 **캐시 데이터가 없을 경우** **`[Root DNS Server]`** 로 [`TLD DNS Server`]의 IP 주소 요청.

   - `[Root DNS Server]`는 `[TLD DNS Server]`의 주소만 관리.
   - 캐시 데이터 있을 경우, 브라우저에 바로 해당 IP주소 안내

<br/>

4. `[Root DNS Server]`로부터 `[ISP DNS Server]`가 응답을 받으면 **`[TLD DNS Server]`** (도메인 등록기관 (Registry) com, org, net 등) 에게 어디로 가야 하는지 다시 요청.

<br/>

5. `[TLD DNS Server]` 는 **`[Authoritative DNS Server]`** (도메인 판매업체 (Registrar) 가비아, 후이즈, 아마존 등) 에서 해당 도메인이 관리되고 있는지 확인하고 `[ISP DNS Server]` 에 안내(응답).

<br/>

6. `[ISP DNS Server]`는 **`[Authoritative DNS Server]`** 에게 또 다시 어디로 갈지 요청.

<br/>

7. **`[Authoritative DNS Server]`** 는 “eunsa.com = 12.123.123.123”이라는 정보를 확인하고 이 IP를 `[ISP DNS Server]`에 전달(응답). 동시에 `[ISP DNS Server]`는 해당 정보를 **캐시**로 기록.

<br/>

8. `[ISP DNS Server]`는 브라우저에게 "12.123.123.123" IP 주소를 안내.

<br/>

9.  브라우저는 "12.123.123.123" IP 주소를 갖고 있는 `[Hosting server]` 에게 웹사이트를 출력하라고 요청

<br/>

10. 웹사이트 출력

<br/>

> `[Browser]` 에서 "EUNSA.COM"을 검색 --> `[ISP DNS Server]` 요청 
> > 캐시데이터 확인 --> 캐시데이터 없을 경우 --> 
> 
> > > `[ISP DNS Server]` --> `[Root DNS Server]` 요청
> > > > `[TLD DNS Server]` 의 주소값(com / net / org 네임서버 등) 응답
> 
> > > `[ISP DNS Server]` --> `[TLD DNS Server]` 요청 
> > > > `[Authoritative DNS Server]` 주소값(가비아 네임서버 등) 응답
> 
> > > `[ISP DNS Server]` --> `[Authoritative DNS Server]` 요청
> > > > `[해당 도메인의 실제 IP 주소]` 응답
>
> > `[ISP DNS Server]` --> `[Browser]`에 `[해당 도메인의 실제 IP 주소]` 응답
> 
> `[Browser]` --> `[Hosting server]` 요청 
> > `[Hosting server]` --> `[Browser]` 화면 출력 (응답)

<br/>

- DNS는 전세계적인 거대한 분산 시스템
- 도메인 네임 스페이스는 이러한 DNS가 저장 관리하는 계층적 구조를 의미
- 도메인 네임 서페이스는 최상위에 루트 DNS 서버가 존재
- 그 하위로 연결된 모든 노드가 연속해서 이어진 계층 구조 (디렉토리 구조 비슷)

<br/>
<br/>

## 🍺 DNS Query
---

- DNS 클라이언트와 DNS 서버는 DNS 쿼리를 교환.
- DNS 쿼리는 Recursive(재귀적) 또는 Iterative(반복적)로 구분.

<br/>

### 🍟 Recursive Query (재귀적 질의)

- Recursive DNS Server (Resolver)에서 수행 (ISP DNS Server)
- 결과물(IP 주소)를 돌려주는 작업.(결과적으로 Recursive 서버가 Recursive 쿼리를 웹 브라우저 등에게 돌려주는 역할)
- Recursive 쿼리를 받은 Recursive 서버는 Iterative 하게 권한 있는 네임 서버로 Iterative 쿼리를 보내서 결과적으로 IP 주소를 찾게 되고 해당 결과물을 응답.

<br/>

### 🍟 Iterative Query (반복적 질의)

- TLD / SLD(Authoritative) DNS Server에서 수행
- Recursive DNS 서버가 다른 DNS 서버에게 쿼리를 보내어 응답을 요청하는 작업
- Recursive 서버가 권한 있는 네임 서버들에게 반복적으로 쿼리를 보내서 결과물(IP 주소)를 알아내는 과정
  - Recursive 서버에 이미 IP 주소가 캐시 되어있다면 이 과정은 생략됨.

<br/>
<br/>

### 동작 과정
---

> 웹 브라우저에 도메인 입력
>> 웹 브라우저 방문기록 확인
>>> 브라우저 캐시 확인
>>> OS 캐시 확인
>>> 라우터 캐시 확인
>>> ISP 캐시 확인 (Recursive DNS Server)
>
>> ISP에서 DNS Iterative하게 쿼리를 날린다.
>>> ISP는 Authoritative DNS 서버에서 최종적으로 IP 주소를 응답받는다.
>>>
>>> ISP는 해당 IP 주소를 캐시한다.
>>
> 웹 브라우저에게 응답

<br/>
<br/>

## 🍺 DNS 레코드 종류
---

- **SOA(Start of Authority)** : 권한 시작 지정하고, 권한이 있는 서버를 가리킴.
- **A(Host Record)** : FQDN과 32비트의 IPv4 주소를 연결.
- **AAAA(IPv6호스트)** : FQDN과 128비트의 IPv6 주소를 연결.
- **CNAME(Alias Record)** : 실제 도메인 이름과 연결괴는 가상 도메인 이름(별칭)
- **MX(Mail Exchane Record)** : 주어진 사서함에 도달할 수 있는 라우팅 정보 제공.
- **SRV(Service Resources)** : 비슷한 TCP/IP 서비스를 제공하는 다수의 서버 위치 정보를 제공.
- **NS(Name Servers)** : 도메인 서버 목록을 지정.

<br/>
<br/>
<br/>

# 🍕 FQDN (Fully Qualified Domain Name)
---

*'절대 도메인 네임' 또는 '전체 도메인 네임' 이라고도 불리는 도메인 전체 이름을 표기하는 방식*

```
www.eunsa.com

www : 호스트
eunsa.com : 도메인 
FQDN : www.eunsa.com

FQDN ❓   
  👉 호스트와 도메인을 함께 명시하여 전체 경로를 모두 표기

PQDN ❓ (Partially Qualified Domain Name)
  👉 전체 경로명이 아닌 하위 일부 경로만으로 식별 가능하게 하는 이름.
  👉 일반적으로 왼쪽 끝의 호스트 네임 노드를 말함.
  👉 도메인에 따라 상대적인 네임이므로 Relative Domain Name 이라고도 부른다.
```

> 📌
> 
> 쿠버네티스의 경우 다른 Pod를 찾을 시 동일 네임스페이스 안에서 찾을 때에는 PQDN을 사용할 수 있지만,
> 
> 네임스페이스 외부에서 찾을 때에는 FQDN을 사용해야 한다.
