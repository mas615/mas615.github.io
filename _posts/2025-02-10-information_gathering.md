---
layout: post
title: 6. 정보수집
subtitle: Information Gathering
author: 마준영
categories: etc
tags:
  - oscp
---
# 6. 정보수집

침투 테스트(펜테스트, Penetration Test)의 목표는 보안 취약점을 찾아내어 고객 조직의 방어력을 향상시키는 것입니다. 기업의 네트워크, 장치, 소프트웨어는 시간이 지남에 따라 변화하기 때문에, 침투 테스트는 주기적으로 수행해야 합니다. 기업의 공격 표면(Attack Surface)은 다음과 같은 이유로 지속적으로 변화할 수 있습니다.

- 새로운 소프트웨어 취약점이 발견됨
- 내부 활동 중 발생한 설정 오류
- IT 재구성이 이루어지면서 새로운 공격 대상이 노출됨

또한, 다음과 같은 변경 사항이 발생하면 공격 표면이 더욱 넓어질 수 있습니다.

- 신규 직원의 채용
- 신제품 출시
- 새로운 기기 배포
- 인프라 확장
- 웹사이트 운영

이러한 이유로 침투 테스트는 정기적으로 다시 수행되어야 합니다.

본 학습 모듈에서는 **수동적 및 능동적 방법을 활용하여 클라이언트의 공격 표면을 체계적으로 매핑하는 방법**을 배우고, 침투 테스트의 전체 과정에서 이 정보를 활용하는 방법을 살펴봅니다.

## 6.1. 침투테스트 라이프 사이클
이 학습 단원에서는 아래와 같은 학습 목표를 다룹니다.

1. 침투 테스트 단계 이해
2. 각 단계 내에서 정보 수집의 역할 알아보기
3. 능동적 정보 수집과 수동적 정보 수집의 차이점 이해

회사의 보안 상태를 최대한 엄격하게 통제하려면 정지적으로 침투 테스트를 실시하고 대상의 IT 아키텍처에 큰 변화가 있을 때마다 테스트를 실시해야 합니다.

일반적인 침투 테스트는 다음 단계로 구성 됩니다.

- **범위 정의(Defining the Scope)**
- **정보 수집(Information Gathering)**
- **취약점 탐지(Vulnerability Detection)**
- **초기 침투(Initial Foothold)**
- **권한 상승(Privilege Escalation)**
- **수평 이동(Lateral Movement)**
- **보고서 작성 및 분석(Reporting/Analysis)**
- **교훈 도출 및 보완 조치(Lessons Learned/Remediation)**

본 모듈에서는 **범위 정의(Scoping)를 간단히 다룬 후, 정보 수집(Information Gathering)에 집중**할 것입니다. 나머지 단계에 대한 내용은 이후 과정에서 다룰 예정입니다.

**범위 정의(Scoping)**
침투 테스트의 범위를 정의하는 것은 **테스트할 IP 범위, 호스트, 애플리케이션을 정하는 과정**을 의미합니다. 이 과정에서 **테스트 대상과 비대상(Out-of-Scope) 항목을 명확히 구분**해야 합니다.

클라이언트와 테스트 범위 및 일정에 대한 합의를 마친 후, 두 번째 단계인 **정보 수집(Information Gathering)** 단계로 진행할 수 있습니다.

**정보 수집(Information Gathering) 단계**
이 단계에서는 **목표 대상(타겟)에 대한 최대한 많은 정보를 수집하는 것**이 목표입니다.

정보 수집을 시작하기 위해 먼저 **정찰(Reconnaissance)** 을 수행하며, 이를 통해 목표 조직의 **인프라, 자산, 인력 정보**를 파악할 수 있습니다. 이 과정은 두 가지 방식으로 수행됩니다.

1. **수동적 정보 수집(Passive Information Gathering)**
    
    - 대상과 **직접적인 상호작용 없이** 정보를 수집하는 방법
    - 공격자의 흔적을 남기지 않기 때문에 탐지를 피할 수 있음
2. **능동적 정보 수집(Active Information Gathering)**
    
    - **대상 인프라를 직접 탐색하여 정보를 수집하는 방법**
    - 더 많은 정보를 얻을 수 있지만, 공격자의 활동이 탐지될 가능성이 높음

**능동적 정보 수집은 공격자의 발자국(흔적)을 많이 남기므로**, 보안 시스템에 탐지될 위험을 줄이기 위해 **가능하면 수동적 방법을 우선적으로 활용**하는 것이 좋습니다.

또한, 정보 수집(Enumeration)은 **초기 정찰 단계에서 끝나는 것이 아니라, 침투 테스트가 진행되는 동안 지속적으로 수행되어야 합니다.**

- 초기에 수집한 정보 외에도,
- **침투 과정에서 얻은 새로운 데이터(예: 취약한 서비스, 내부 시스템 정보, 계정 정보 등)를 추가로 분석하며 공격 표면을 확장**해야 합니다.

본 모듈에서는 **수동적 정찰(Passive Reconnaissance)** 부터 시작하여, 이후 **목표 시스템과 상호작용하며 정보를 수집하는 능동적 정찰(Active Reconnaissance)** 방법까지 학습하게 됩니다.

## 6.2. 수동적 정보 수집

이 학습 단원에서는 다음과 같은 학습 목표를 다룹니다:

- 두 가지 패시브 정보 수집 접근법 이해하기
- 오픈소스 인텔리전스(OSINT)에 대해 배우기
- 웹 서버 및 DNS 패시브 정보 수집 이해하기
### **패시브 정보 수집(Passive Information Gathering)이란?**

패시브 정보 수집은 **오픈소스 인텔리전스(Open-source Intelligence, OSINT)**라고도 불리며, 특정 대상(Target)에 대한 공개적으로 이용 가능한 정보를 수집하는 과정입니다.  
이 과정에서는 대상과 직접 상호작용하지 않고 정보를 수집하여 **우리의 흔적(footprint)을 최소화하는 것**이 중요합니다.

이를 수행하는 방법에는 두 가지 접근 방식이 있습니다.

#### **1) 엄격한 패시브 정보 수집 (Strict Interpretation)**

- 대상과 **직접적인 접촉 없이** 정보를 수집하는 방법
- 제3자로부터 정보를 얻을 수 있지만, 대상 시스템이나 서버에는 접속하지 않음
- **완벽한 익명성을 유지**할 수 있지만, 수집할 수 있는 정보가 제한될 가능성이 있음

#### **2) 느슨한 패시브 정보 수집 (Looser Interpretation)**

- **일반 인터넷 사용자가 할 수 있는 범위 내에서** 대상과 상호작용하는 방법
- 예를 들어, 대상의 웹사이트에서 **회원가입**을 하는 것은 가능하지만, 보안 취약점을 테스트하는 것은 금지됨
- 이 방식은 정보를 더 많이 얻을 수 있지만, 일정 수준의 노출 위험이 있음

**이 모듈에서는 두 번째(느슨한) 접근 방식을 사용할 것입니다.**  
즉, 특정 대상과 직접적으로 접촉하지는 않지만, 인터넷 사용자의 일반적인 행동 범위 내에서 정보를 수집합니다.

### **패시브 정보 수집의 특징**

패시브 정보 수집은 **선형적인 과정이 아니라 순환적인 과정**입니다.  
즉, 한 단계에서 얻은 정보가 다음 단계를 결정하며, 여러 번 반복될 수 있습니다.

패시브 정보 수집의 최종 목표는 다음과 같습니다:

- **공격 표면(Attack Surface) 확장:** 대상의 보안 취약점을 보다 명확하게 파악
- **피싱(Phishing) 공격 보조:** 소셜 엔지니어링 공격의 성공률 증가
- **비밀번호 추측(Password Guessing) 보조:** 계정 탈취 가능성 향상

**이 모듈에서는 개별 시나리오를 실습하기보다는 관련 도구와 기법을 배우는 데 집중합니다.**

## 6.2.1. Whois 열거

**Whois**는 TCP 기반의 서비스, 도구, 그리고 데이터베이스 유형으로, 특정 도메인에 대한 다양한 정보를 제공하는 역할을 합니다.  
이 정보를 통해 **도메인 등록 기관(Registrar), 네임 서버(Name Server), 등록자 정보(Registrant Information)** 등을 확인할 수 있습니다.

> 대부분의 Whois 정보는 **공개적(public)**으로 제공되지만, 일부 도메인 등록 기관은 사생활 보호 기능을 제공하며, 이를 이용할 경우 Whois 정보가 감춰질 수 있습니다.

#### Whois 조회 예제
아래 명령어를 통해 megacorpone.com 도메인의 정보를 조회하는 방법을 보여줍니다.
```bash
kali@kali:~$ whois megacorpone.com -h 192.168.50.251
```

#### 출력 예시
```yaml
Domain Name: MEGACORPONE.COM
Registry Domain ID: 1775445745_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.gandi.net
Registrar URL: http://www.gandi.net
Updated Date: 2019-01-01T09:45:03Z
Creation Date: 2013-01-22T23:01:00Z
Registry Expiry Date: 2023-01-22T23:01:00Z
...
Registrant Name: Alan Grofield
Registrant Organization: MegaCorpOne
Registrant Street: 2 Old Mill St
Registrant City: Rachel
Registrant State/Province: Nevada
Registrant Postal Code: 89001
Registrant Country: US
Registrant Phone: +1.9038836342
...
Name Server: NS1.MEGACORPONE.COM
Name Server: NS2.MEGACORPONE.COM
Name Server: NS3.MEGACORPONE.COM
```

### **Whois 조회를 통해 얻은 정보**

Whois 조회 결과에서 **유용한 정보**를 찾을 수 있습니다:

1. **도메인 등록자 정보**
    - **이름**: Alan Grofield
    - **소속 조직**: MegaCorpOne
    - **역할**: Megacorp One의 **IT 및 보안 디렉터**  
        → 이 정보는 보안 테스트 또는 공격을 수행하는 데 있어 유용할 수 있습니다.
2. **네임 서버 정보**    
    - **NS1.MEGACORPONE.COM**
    - **NS2.MEGACORPONE.COM**
    - **NS3.MEGACORPONE.COM**  
        → 네임 서버는 DNS 구성의 핵심 요소이므로 기록해 두어야 합니다.

#### IP주소로 Whois 조회 (Reverse Lookup)
만약 특정 IP 주소가 주어진다면 whois를 활용하여 해당 IP의 소유자 및 호스팅 서비스 제공자를 확인 할 수 있습니다.

```bash
kali@kali:~$ whois 38.100.193.70 -h 192.168.50.251
```

#### 출력 예시
```yaml
NetRange:       38.0.0.0 - 38.255.255.255
CIDR:           38.0.0.0/8
NetName:        COGENT-A
...
OrgName:        PSINet, Inc.
OrgId:          PSI
Address:        2450 N Street NW
City:           Washington
StateProv:      DC
PostalCode:     20037
Country:        US
Updated:        2015-06-04
```

### Whois조회를 통해 얻은 정보
**결과 분석**

- **해당 IP 주소는 "PSINet, Inc."라는 조직에서 소유**하고 있음
- **Washington D.C.에 위치**한 기업임
- IP 대역은 **CIDR 38.0.0.0/8**로 설정되어 있음

**활용 예시**

- **해당 IP가 어떤 서비스(웹, 이메일, API 등)를 운영하는지 분석 가능**
- **호스팅 제공 업체를 확인하여 보안 정책 분석**
- **IP 차단(Blacklisting) 목록과 비교하여 악성 도메인 여부 판단**

### 정리



# 오늘의 명령어
3. whois 도메인명 -h 192.168.50.251
	1. -h 192.168.50.251는 지정하지 않으면 자동으로 whois서버를 설정함, 하지만 특정 whois서버를 지정하고 싶을때 -h 옵션 사용
```bash
kali@kali:~$ whois megacorpone.com -h 192.168.50.251
```