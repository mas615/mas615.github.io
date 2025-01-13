---
layout: post
title: An exhibit of Markdown2
subtitle: Each post also has a subtitle
categories: markdown
tags:
  - example
  - markdown
---

#### 9.1.2. Identifying and Exploiting Directory Traversals

1. 옵시디언을 어떻게 쓰는줄 몰라서 일단 원래있던 게시물을 수정해본다.
2. 디렉토리 탐색 식별 및 활용112
3. 이미 했네 ㅋㅋ

## 9.1.3. Encoding Special Characters
특수문자 인코딩

```java
../../
```
등의 스크립트는 웹 애플리케이션 동작을 남용하는 알려진 방법이기 때문에 웹서버, 웹 애플리케이션 방화벽 또는 웹 애플리케이션 자체에 의해 필터링됩니다.

다행히도 우리는 URL 인코딩, 퍼센트 인코딩 이라고 불리는 우회방법을 사용하여 필터링을 우회할 수 있다.

1. 이 섹션에서는 URL 인코딩을 사용하여 VM #1의 Apache 2.4.49에서 디렉토리 트래버설 취약성을 악용했습니다. 취약한 Apache 웹 서버에서 디렉토리 트래버설을 통해 /opt/passwords 파일 의 내용을 표시하려면 Burp 또는 curl을 사용합니다 . 디렉토리 트래버설 공격에는 URL 인코딩을 사용하는 것을 잊지 마세요. 파일의 출력에서 ​​플래그를 찾으세요.

```shell
curl http://192.168.50.16/cgi-bin/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
```

![](/assets/images/posts/2018-12-05-an-exhibit-of-markdown%202/1e2f37042219927559bbf236b3e92a62_MD5.jpeg)

2. 2. Grafana는 VM #2의 포트 3000에서 실행 중입니다. 실행 중인 버전은 이전 섹션과 동일한 디렉토리 트래버설 취약성에 취약합니다. 성공적인 디렉토리 트래버설 공격을 수행하는 데 URL 인코딩이 필요하지 않지만, **/etc/passwd** 의 내용을 표시하기 위해 요청의 다른 문자를 URL 인코딩하는 것을 실험해 보세요 . URL 인코딩을 활용한 작동 요청이 있으면 **/opt/install.txt** 의 내용을 표시하여 플래그를 얻으세요 .
	1. 파이썬 스크립트가있다.
		1. https://www.exploit-db.com/exploits/50581
	2. 아래와 같이 사용이 가능하다./![](/assets/images/posts/2018-12-05-an-exhibit-of-markdown%202/5fcd1ce9b43a62153c41b11bf4e3780b_MD5.jpeg)
	3. 위 스크립트는 플러그인 정보를 임의로 입력하여 공격하는 툴인거같다.
	4. 주의할점은 host명에 http://를 꼭 붙어야한다.
	5. 하지만 문제에서는 URL인코딩을 해서 해보라고 하니 해보자.![](/assets/images/posts/2018-12-05-an-exhibit-of-markdown%202/9cfa836d421c3b93d053f369d090a8f8_MD5.jpeg)
	6. 아주 잘된다.
	7. 위와 같은 방법으로  **/opt/install.txt** 도 탐색이 가능하고, 그안에 플래그가 있다.

## 9.2. File Inclusion Vulnerabilities
1. 파일 포함 및 디렉토리 트레버셜 취약점의 차이점 알아보기
2. 파일 포함 취약점에 대한 이해 얻기.
3. 코드 실행을 얻기 위해 로컬 파일 포함(LFI) 을 활용하는 방법을 이해합니다.
4. PHP래퍼 사용법 살펴보기.
5. RFI(원격 파일 포함) 공격을 수행하는 방법을 알아보세요.

## 9.2.1. Local File Inclusion (LFI)
로컬파일 인클루전은 디렉토리 트레버셜과 비슷하지만 해당 파일에 접근시 안에 있는 code가 실행 될 수 있다는 차이점이 있다.


