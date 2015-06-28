---
layout: post
title:  GitHub에 홈페이지 만들기
date:    2012/08/24 07:18
categories: github
---

GitHub에 공짜로 개인 홈페이지 만드는 방법을 설명 드리겠습니다.

리포지토리를 하나 만듭니다. 'home'이나 'homepage'와 같은 이름이 좋겠지요? 이 리포지토리는 웹 사이트 생성을 위한 일종의 더미입니다.

생성 후, 리포지토리 관리 메뉴 중 'Admin'을 선택하고, 'GitHub Pages' 부분으로 가서 'Automatic Page Generator'를 선택합니다.

홈페이지 구성에 필요한 기본적인 내용을 채우고 'Continue to Layouts' 버튼을 누릅니다.

몇 가지 디자인 중에 하나를 누르고 'Publish'를 누르면 끝입니다!

이 과정을 거치면 리포지토리에 'gh-pages'라는 브랜치가 생깁니다. 이 브랜치는 GitHub에서 "리포지토리 홍보용 웹 페이지"라는 특별한 의미가 있습니다.

웹 페이지를 바꾸고 싶다면 GitHub 웹 사이트에서 직접 고치면 됩니다. 소규모 웹 사이트를 운영할 때는, 웹 서버 호스팅 받는 것보다 훨씬 편합니다.

GitHub의 아이디가 cybaek이고 리포지토리 이름이 home이라면 약 10분 안에 http://cybaek.github.com/home 이라는 웹 사이트가 자동으로 생깁니다. (404 페이지가 나와도 당황하지 마시고 10분 정도 기다려보세요)

http://cybaek.com/ 과 같은 커스텀 도메인 주소에 매핑하는 것도 역시 쉽고 간단합니다.

자기 도메인 DNS에 cybaek.com의 CNAME으로 cybaek.github.com을 등록합니다. 그리고 리포지토리의 루트에 CNAME이라는 파일을 만든 다음(DNS 서버에 작업하는 것이 아닙니다. 진짜 CNAME이라는 파일을 만드는 것입니다) 내용에 cybaek.com을 적으면 됩니다. 간단하지요? ^^

수 분 지난 후 http://cybaek.com/에 접속하면 http://cybaek.github.com/home과 같은 내용이 보이는 것을 확인할 수 있습니다.

돈내고 호스팅할 필요 없겠지요? ^^

참고:
* https://help.github.com/categories/20/articles
* https://help.github.com/articles/setting-up-a-custom-domain-with-pages

