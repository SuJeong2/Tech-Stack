# 네트워크 인터페이스 계층
*written by sohyeon, hyemin 💡*

<br>

## 목차
### [1. 네트워크 인터페이스 계층이란?](#1-네트워크-인터페이스-계층이란-1)
### [2. MAC 어드레스](#2-MAC-어드레스-1)
### [3. 이더넷](#3-이더넷-1)
### [4. 네트워크 허브](#4-네트워크-허브-1)
### [5. 무선 LAN](#5-무선-LAN-1)
### [6. ARP](#6-ARP-1)
### [7. FTTx와 xDSL](#7-FTTx와-xDSL)
### [8. PPP와 PPPoE](#8-PPP와-PPPoE)

<br>

## 1. 네트워크 인터페이스 계층이란?
`네트워크 인터페이스 계층`은 네트워크의 하드웨어를 제어하는 부분이다.    
하드웨어는 네트워크 어댑터나 LAN 케이블, 광 케이블을 말한다.  
이러한 하드웨어들을 제어하면서 `상위의 인터넷 계층이 하위의 하드웨어 동작에 대해서는 신경쓰지 않고 동작할 수 있도록 만들어주는 것`이 네트워크 인터페이스 계층의 역할이다.  

<br>

## 2. MAC 어드레스
### MAC 어드레스란?
`MAC 어드레스`는 네트워크 장비에 부여된 식별 번호다.  
```
MAC 어드레스는 제조사 식별 번호(24비트) + 제조사에서 정의한 식별 번호(24비트)로 이루어져 있다.
제조사 식별 번호: 어댑터 제조사를 식별하는 번호
제조사에서 정의한 식별 번호: 제조사가 생산한 제품들끼리 중복되지 않도록 부여하는 번호
```

### 수신지 주소로 사용하는 MAC 어드레스
MAC 어드레스는 유선 LAN의 이더넷이나 무선 LAN 외에도 단거리 통신에 사용되는 블루투스와 같은 다양한 데이터 통신에서 활용된다.  
네트워크 인터페이스 계층이 보내는 데이터를 `프레임(frame)`이라고 부르는데, 이 프레임 안에 송신지와 수신지의 MAC 어드레스 정보가 들어간다.  
```
----------------------------------------------------------------------
 프리앰블 | 수신지 MAC 어드레스 | 송신지 MAC 어드레스 | 길이/타입 | 데이터 본체 | FCS
----------------------------------------------------------------------

프리앰블: 데이터가 시작하는 것을 표시한다.
데이터 본체: IP 패킷 등이 여기에 들어간다.
FCS: 오류 방지 정보가 여기에 들어간다.
```

### IP 어드레스와 MAC 어드레스의 차이점
`MAC 어드레스`의 역할은 데이터를 전달할 목적지를 가리킨다는 점에서 IP어드레스와 유사하다.  

하지만,   `IP 어드레스`는 최종 목적지가 한번 설정되면 전송 과정 중에 변경되지 않지만, `MAC 어드레스`는 전송 과정 중에 통신 경로상에 다음 장비의 어드레스로 교체된다는 점이 다르다.  

<br>

## 3. 이더넷
`이더넷`은 하나의 인터넷 회선에 유/무선 통신장비 공유기, 허브 등을 통해 다수의 시스템이 랜선 및 통신포트에 연결되어 통신이 가능한 네트워크 구조를 말한다. 이더넷은 현재 가장 많이 사용되는 유선 LAN의 규격으로, 기술이 발전함에 따라 점점 더 많은 데이터를 고속으로 처리할 수 있게 개선되고 있다.  

### 주요 이더넷 규격
| 규격 이름 | 특징 |
|:---:|:---:|
| 10BASE-T | 트위스트 페어 케이블을 사용하고 10Mbps로 통신한다. |
| 100BASE-TX | 트위스트 페어 케이블을 사용하고 100Mbps로 통신한다. |
| 1000BASE-T | 트위스트 페어 케이블을 사용하고 1000Mbps로 통신한다. |
| 1000BASE-X | 광섬유 케이블을 사용하고 LX, SX, FX 등의 규격이 있다. 이들 규격은 케이블 종류나 전송 거리에 차이가 있다. |
* 100BASE-TX와 같이 규격 표기 방법에서 앞에 나오는 숫자는 전송 속도를, BASE는 신호의 변조 방식을, 마지막 알파벳은 케이블의 종류를 의미한다.  
* 주파수가 높은 신호는 쉽게 감쇠하기 때문에 전송 속도가 고속인 규격에서는 가능한 한 주파수가 높아지지 않도록 제한하는 대신 케이블 자체를 고급 사양으로 사용하고 있다.  

### 프레임의 시작을 알리는 프리앰블
수신 측의 네트워크 어댑터는 전압의 높낮이가 변화하는 신호를 받아 0과 1의 디지털 신호로 복호화한다. 이때 전압이 변화하는 타이밍에 맞춰 신호를 분석하려면 어디부터가 시작인지 기준점을 알아야 한다.  
프레임 앞부분에는 `프리앰블(preamble)`이라고 하는 패턴을 두어 신호의 시작을 알 수 있도록 만들어져 있다.  
프리앰블은 길이가 상당히 긴 편이라서 통신 중에 앞부분의 데이터를 잃어버리더라도 1010이 일정 횟수 반복되다 마지막이 10101011로 끝나면 프레임의 시작이라고 인식한다.  
<br>

## 4. 네트워크 허브
### 네트워크 허브의 동작 방식
유선 LAN에서는 `네트워크 허브`라는 장비에 케이블을 연결해서 네트워크를 구성한다.  
`네트워크 허브`는 수신한 데이터를 다른 컴퓨터에게 전송하며, `리피터 허브, L2 스위치(스위칭 허브), L3 스위치` 등이 있다.  

### (1) L2 스위치  
`L2 스위치(스위칭 허브)`는 포트에 연결된 각 호스트의 MAC 어드레스를 기억해 두었다가 통신할 당사자 간에만 데이터를 전달하기 때문에 통신 과정에서 다른 호스트가 보내는 패킷 신호와의 충돌을 피할 수 있다.  

#### L2 스위치가 통신하는 방식
* 수신지의 MAC 어드레스를 확인한 후에 수신 측의 LAN 포트에만 신호를 보낸다.  
* LAN 포트가 독립적으로 구성되어 있어서 동시에 여러 신호를 보낼 수 있다.  

### (2) 브로드캐스트 도메인
`브로드캐스트 도메인(broadcast domain)`이란, 수신지의 주소가 브로드캐스트 어드레스일 때 데이터가 전달되는 범위를 말한다.  
예를 들어, L2 스위치로 네트워크를 구성하였다면 `네트워크 전체`가 브로드캐스트 도메인이 된다.  

네트워크에 연결된 호스트의 수가 많을 경우, DHCP나 OS의 파일 공유와 같은 브로드캐스트 통신이 자주 사용되면 네트워크 내에 대량의 패킷이 발생해서 망이 혼잡해질 수도 있다.  

#### 리피터 허브와 콜리전 도메인
L2 스위치가 보급되기 전에는 한 개의 호스트에서 수신한 데이터를 다른 모든 호스트에게 전달하는 `리피터 허브`를 많이 사용했었다.  
모든 호스트가 회선을 공유하고 있는 형태라서 여러 대의 호스트가 동시에 통신하게 되면 네트워크상에서 신호가 충돌할 수 있는데, 이렇게 충돌이 발생할 수 있는 범위를 `층돌 도메인(콜리전 도메인)`이라고 불렀다.  

### (3) L3 스위치
`L3 스위치`는 OSI 참조 모델 중 네트워크 계층에 해당되고, TCP/IP 모델에서는 인터넷 계층의 기능까지 수행할 수 있는 네트워크 장비다.  
`L3 스위치의 대표적인 기능`은 `VLAN(Virtual LAN)`을 꼽을 수 있는데, 이 기능은 LAN을 몇 개의 가상적인 네트워크로 분할해서 통신 효율을 높이기 위해 사용한다. VLAN을 구성하면 브로드캐스트 패킷을 VLAN 내의 호스트 범위로만 제한하여 전달할 수 있다.  
* 같은 장비의 포트에 연결되어 있어도 서로 다른 네트워크처럼 구성할 수 있다.  
* VLAN별로 서로 다른 IP 어드레스를 가지는 네트워크를 만들 수 있다.  
* VLAN 내의 통신 방식은 L2 스위치와 같으며, 라우터처럼 라우팅을 하면서 네트워크를 넘나들 수 있다.  
<br>

## 5. 무선 LAN
전파를 이용해서 네트워크를 구성하는 `무선 LAN`의 정식 규격명은 `IEEE 802.11`이다.  
무선 LAN 에서는 다른 통신 장비가 전파를 발신하고 있지 않은 것을 확인한 후, 통신을 시작하는 `CSMA/CA(Carrie Sense Multiple Access with Collision Avoidance)` 방식을 사용한다.

### 주요 LAN 규격
| 규격 이름 | 특징 |
|:---:|:---:|
| IEEE 802.11 | 기본이 되는 규격. 프레임의 구성 형태 등을 정의하고 있음 |
| IEEE 802.11a | 5GHz 대역을 사용하며, 최대 54Mbps까지 통신 가능 |
| IEEE 802.11b | 2.4GHz 대역을 사용하며, 최대 11Mbps까지 통신 가능 |
| IEEE 802.11g | 2.4GHz 대역을 사용하며, OFDM 방식으로 최대 11Mbps까지 통신 가능 |
| IEEE 802.11n | 여러 개의 안테나를 사용하여 최대 600Mbps까지 통신 가능 |

### 무선 LAN의 프레임 구조
무선 LAN에서도 통신할 때 주고받는 데이터를 프레임이라고 부른다.  
무선 LAN의 프레임에는 MAC 어드레스 필드가 4개나 되는데, 무선 LAN끼리 통신하는 경우와 무선 LAN 뒤에 유선 LAN이 연결되는 경우 등에 따라 MAC 어드레스 정보가 할당되는 방식이 달라진다.  
```
------------------------------------------------------------------------------------------------------------
 프리앰블 | PLCP 헤더 | 제어 정보 | MAC 어드레스1 | MAC 어드레스2 | MAC 어드레스3 | 일련번호 | MAC 어드레스4 | 데이터 본체 | FCS 
------------------------------------------------------------------------------------------------------------
                   |<-------------------------- IEEE 802.11 헤더 -------------------------->|
                   
PLCP 헤더: 신호의 변조 방식에 대한 정보가 들어간다
제어 정보: 통신을 제어하는 데 필요한 정보가 들어간다
일련번호: 데이터가 분할된 경우 일련번호를 표시한다
FCS: 프레임의 끝을 표시한다
```

### MAC 어드레스 정보의 설정 방식
무선 LAN의 통신에는 송신지와 수신지 사이를 무선 AP가 중계하게 된다.  따라서 프레임에는 송신지와 수신지의 MAC 어드레스 외에도 무선 AP의 MAC 어드레스 정보도 들어간다.  

```
(1) 무선 -> 무선
-----------------------------------------------------------------------------------------
 수신지 무선 클라이언트의 MAC 어드레스 | 송신지 무선 클라이언트의 MAC 어드레스 | 무선 AP의 MAC 어드레스 | 미사용 
-----------------------------------------------------------------------------------------

(2) 무선 -> 유선
-----------------------------------------------------------------------------------------
 무선 AP의 MAC 어드레스 | 송신지 무선 클라이언트의 MAC 어드레스 | 수신지 유선 클라이언트의 MAC 어드레스 | 미사용 
-----------------------------------------------------------------------------------------

(3) 유선 -> 무선
-------------------------------------------------------------------------------
수신지 무선 클라이언트의 MAC 어드레스 | 무선 AP의 MAC 어드레스 | 송신지 유선 MAC 어드레스 | 미사용 
-------------------------------------------------------------------------------

(4) 무선 AP를 경유해서 통신하는 경우
---------------------------------------------------------------------------------------------
수신지 무선 AP의 MAC 어드레스 | 송신지 무선 AP의 MAC 어드레스 | 수신지 유선 MAC 어드레스 | 송신지 유선 MAC 어드레스 
---------------------------------------------------------------------------------------------
```
<br>

## 6. ARP
`ARP(Address Resolution Protocol)`는 IP 어드레스 정보를 이용하여 해당 장비의 MAC 어드레스를 알아내는 프로토콜이다.  
송신 측 장비는 `요청 패킷`에 수신 측의 IP 어드레스를 설정한 후 네트워크 전체에 브로드캐스트한다. 이어 이 요청을 받은 호스트들 중 수신지의 IP 어드레스가 자신의 IP 어드레스와 동일한 장비는 자신의 MAC 어드레스를 `응답 패킷`에 설정하여 응답하게 된다. 결국, 송신지 장비는 수신지 장비의 IP 어드레스 정보를 사용하여 MAC 어드레스도 알 수 있게 된다.  

### ARP 헤더
ARP 헤더에는 MAC 어드레스를 물어보는 송신지의 어드레스 정보와 MAC 어드레스를 알 수 없는 목적지의 어드레스를 담을 수 있는 필드가 있다.

```
이더넷 헤더
-----------------------------------------------------
 프리앰블 | 수신지 MAC 어드레스 | 송신지 MAC 어드레스 | 길이/타입 
-----------------------------------------------------
수신지 MAC 어드레스: 요청할 때는 브로드캐스트 어드레스를 설정한다

ARP 헤더
-----------------------------------------------------------------------------------------------------------------------------------------------------
 하드웨어 타입 | 상위의 프로토콜 | MAC 어드레스의 길이 | IP 어드레스의 길이 | 오퍼레이션 코드 | 송신지 MAC 어드레스 | 송신지 IP 어드레스 | 목적지 MAC 어드레스 | 목적지 IP 어드레스 | FCS 
-----------------------------------------------------------------------------------------------------------------------------------------------------
송신지 IP 어드레스: MAC 어드레스를 물어본 송신지 호스트의 IP 어드레스를 설정한다
목적지 MAC 어드레스: 요청할 때는 0을 설정한다
목적지 IP 어드레스: MAC 어드레스를 알 수 없는 목적지 호스트의 IP 어드레스를 설정한다
```
### 프락시 ARP
`프락시(proxy) ARP`는 호스트 대신 라우터가 ARP에 대해 응답하는 기능을 말한다.  
보통 ARP 요청은 네트워크 내에 있는 호스트들에게는 브로드캐스팅되는 반면, 서브넷 마스크가 다른 호스트에 전달되지 않는다. 그래서 그 사이에 있는 라우터가 프락시 ARP 기능으로 자신의 MAC 어드레스를 대신 응답하여 데이터를 중계할 수 있게 만든다.  
<br>

## 7. FTTx와 xDSL
가정이나 사무실에서 인터넷 서비스 제공자까지의 통신에는 광섬유 케이블을 사용하는 FTTx나 금속 케이블을 사용하는 xDSL이 사용된다.  

### 광섬유 케이블을 사용하는 FTTx
광섬유 케이블에 레이저 빛을 쏘아 통신하는 광섬유 회선은 수 km 떨어진 원거리에서도 고속 통신이 가능하다.   
일반 가정까지 광 회선이 들어와 인터넷 서비스를 제공하는 방식은 `FTTH(Fiber To The Home)`이고, 광 회선이 어디까지 들어오느냐에 따라 명칭이 달라지는데, 통틀어서 `FTTx`라고 부른다.  

#### 인터넷 서비스 제공자에서 가입자까지 접속하는 방법
* 점유형
    - 인터넷 서비스 제공자에서 가정까지 한 개의 케이블로 연결된다
* 공유형
    - 여러 개의 신호를 한 개의 케이블로 보낸다
    - 광 신호를 분기한다
    - 자신에게 보내진 신호만 수신한다

### 금속 케이블을 사용하는 xDSL
통신 방식이나 속도, 거리에 따라 규격으로 구분하는데, 이를 통틀어서 `xDSL`이라고 부른다.  
주요 xDSL 규격에는 금속 케이블을 사용하는 통신 회선인 `ADSL(Asymmetric Digital Subscriber Line)`과 `VDSL(Very high Digital Subscriber Line)` 등이 있다.  

#### 전화 회선을 이용하는 ADSL
* 통신 거리는 1~3km이다. 
* 전화에서 사용하지 않는 높은 주파수로 디지털 신호를 전송한다.  
* 주파수별로 신호를 분기하고나 합친다. 
  
#### 옥외 배선에 사용되는 VDSL
* 통신 거리는 1.5km이다.  
* 인터넷 서비스 제공자까지는 원거리에도 고속 통신이 가능한 FTTx로 연결한다.  
* 각 방까지 VDSL로 배분한다.  

<br>

## 8. PPP와 PPPoE
### PPP
`PPP(Point to Point Protocol)`는 원격지에 있는 컴퓨터를 일대일로 연결하기 위한 프로토콜이다.  
`PPP`는 접속, 사용자 인증, 통신, 중단과 같은 단계로 통신한다.

#### PPP의 통신 과정
```
1. 접속: 모뎀으로 통신이 가능하게 되었다
2. 인증: 사용자 계정과 패스워드를 교환한다
3. 통신: 통신에 사용할 프로토콜이나 어드레스를 서로 맞춘다.
4. 종료: 통신이 끝나면 종료한다.

원격지에 있는 상대와 통신하기 때문에 통신하기로 한 상대가 맞는지, 어떤 방법으로 통신을 할지 등에 대한 정보를 서로 교환하고 확인이 끝난 후에 통신을 시작한다. 
```

### 이더넷에서 사용하는 PPPoE
이더넷을 사용하여 PPP 통신을 할 경우 `이더넷의 프레임 안에 PPP의 헤더를 넣은 PPPoE(PPP over Ethernet)`라는 프로토콜을 사용한다.  
```
--------------------------------------------------------------------------------------------
 프리앰블 | 수신지 MAC 어드레스 | 송신지 MAC 어드레스 | 길이/타입 | PPPoE 헤더 | PPP 헤더 | 데이터 본체 | FCS
--------------------------------------------------------------------------------------------

PPPoE 헤더는 버전, 타입, 코드, 세션 ID로 이루어져 있다.
코드: 접속 확인 시 사용한다
세션 ID: 접속 확인 시 정해지는 고유한 숫자 값

PPP 헤더는 접속, 인증, 정보 교환, 통신, 종료와 같은 단계를 표시하는 2바이트 값이 들어간다.
```

## Reference & Additional Resources
> TCP/IP 쉽게, 더 쉽게