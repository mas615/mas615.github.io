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
2. 디렉토리 탐색 식별 및 활용
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

![](assets/images/posts/2018-12-05-an-exhibit-of-markdown%202/1e2f37042219927559bbf236b3e92a62_MD5.jpeg)

2. 2. Grafana는 VM #2의 포트 3000에서 실행 중입니다. 실행 중인 버전은 이전 섹션과 동일한 디렉토리 트래버설 취약성에 취약합니다. 성공적인 디렉토리 트래버설 공격을 수행하는 데 URL 인코딩이 필요하지 않지만, **/etc/passwd** 의 내용을 표시하기 위해 요청의 다른 문자를 URL 인코딩하는 것을 실험해 보세요 . URL 인코딩을 활용한 작동 요청이 있으면 **/opt/install.txt** 의 내용을 표시하여 플래그를 얻으세요 .
	1. 파이썬 스크립트가있다.
		1. https://www.exploit-db.com/exploits/50581
	2. ![](assets/images/posts/2018-12-05-an-exhibit-of-markdown%202/5fcd1ce9b43a62153c41b11bf4e3780b_MD5.jpeg)
	3. 위 스크립트는 

