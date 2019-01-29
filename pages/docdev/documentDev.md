---
title: EDISON 문서 작성 가이드
tags: []
keywords: EDISON 문서
summary: "EDISON 문서 작성 방법을 정리한 가이드 입니다. EDISON 문서는 Jekyll 기반으로 작성되었으며 documentation-theme-jekyll 테마를 기반으로 문서가 구성되어 있습니다. 본 문서에서는 EDISON 문서를 작성하기 위한 개발환경 구축 방법 및 문서 작성 그리고 페이지 추가 방법에 대해서 정리하였습니다."
sidebar: docdev_sidebar
permalink: docdev_intro.html
folder: docdev
hide_sidebar: true
---

## 시작하기 전에 ...

본 페이지는 루비 기반에 정적 페이지를 만들어주는 [Jekyll](https://jekyllrb-ko.github.io/docs/home)을 사용하고 있으며, [Jekyll Documentation theme](https://idratherbewriting.com/documentation-theme-jekyll/index.html) 기반으로 작성하였습니다. 보다 자세한 내용은 해당 문서를 참고하시기 바랍니다.


## 설치하기

 - [Mac에서 환경 구축하기](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_mac.html)
 - [Window에서 환경 구축하기](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_windows.html)
 - [Docker로 사이트 운영하기](https://idratherbewriting.com/documentation-theme-jekyll/index.html#running-the-site-in-docker)

### Ruby 설치

 - [Unix 계열 Ruby 설치](https://www.ruby-lang.org/ko/documentation/installation/#other-systems)
 - [Windows Ruby 설치](https://www.ruby-lang.org/ko/documentation/installation/#rubyinstaller)

### Jekyll, Bundle 설치

```
gem install jekyll bundler
```

### EDISON Documentation 설치

```
git clone https://github.com/sp-edison/sp-edison.github.io.git
cd sp-edison.github.io
bundle install
bundle update jekyll-remote-theme
```

### 빌드 & 서버 실행

```
bundle exec jekyll serve
```

명령어 실행시 문서의 빌드가 진행됩니다. 생성된 문서들은 ```_site```에 생성됩니다. 빌드 과정이 완료되면 웹서버가 구동되며 [http://127.0.0.1:4000](http://127.0.0.1:4000)을 통해 접근 가능합니다. 


## solverDev 문서 구조 설명

solverDev 문서를 구성하고 있는 파일들은 다음 디렉토리에 위치해 있습니다. 

| 종류 | 위치 | 설명 |
|--|--|--|
| 문서(Markdown) 파일 위치 | ```pages/solverDev/``` | solverDev 문서의 md 파일이 저장된 위치 입니다. |
| 사이드바 위치 | ```_data/sidebars/solverdev_sidebar.yml``` | solverDev의 사이드바가 저장된 위치입니다. |
| 이미지 위치 | ```images/solverdev/```| solverDev 문서에서 사용되는 이미지가 저장된 위치입니다. |

  
## 문서 구조

{% include image.html file="docdev/docDev_image1.jpg" %}

### 문서 파일 예시 

solverDev의 문서 파일 중 ```pages/solverDev/01_introduction/00_Intro.md```에 대해 설명합니다. 보다 자세한 내용은 [documentation-theme-jekyll의 pages 설명 문서](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_pages.html#where-to-save-pages)를 참고하시기 바랍니다.

#### Frontmatter

```yaml
---
title: EDISON 플랫폼 소개
tags: [EDISON, Platform]
keywords:
summary: "EDISON 플랫폼은 웹 브라우저 접속만으로 C, C++, Fortran, MPI, Python등으로 코딩된 Science Apps(시뮬레이션 SW)을 활용할 수 있는 환경을 제공합니다. 본 문서는 Science App 개발자들을 위한 개발 문서로 EDISON 플랫폼에서 시뮬레이션 SW를 개발하는 방법에 대해서 소개하고자 합니다."
sidebar: solverdev_sidebar
permalink: solverdev_intro.html
folder: solverDev
---
```

```md

## EDISON 플랫폼 소개

EDISON 플랫폼은 웹 브라우저 접속만으로 C, C++, Fortran, MPI, Python등으로 코딩된 Science Apps(시뮬레이션 SW)을 활용할 수 있는 환경을 제공합니다. 본 문서는 Science App 개발자들을 위한 개발 문서로 EDISON 플랫폼에서 시뮬레이션 SW를 개발하는 방법에 대해서 소개하고자 합니다.


## PDF로 다운 받기

<a target="\_blank" class="noCrossRef" href="{{ "pdf/solverdev.pdf"}}"><button type="button" class="btn btn-default" aria-label="Left Align"><span
    class="glyphicon glyphicon-download-alt" aria-hidden="true"></span> PDF Download</button></a>

## Science App 등록 절차

개발자 권한 신청 및 발급

Bulb 서버 접속 - Code upload & Compile - 실행 파일 압축

사이언스 앱스토어 > 앱 관리 > 앱 등록 - 앱 정보 입력 - 실행환경 정보 입력 - 입/출력 포트 정보 입력 - 앱테스트

서비스 요청 -> 관리자 승인 -> 서비스!

```


## 윈도우 설치 Tip
1. ruby 설치 : 2.5 버전 설치. 2.6버전은 jekyll 설치 과정에 오류있음
```
https://github.com/oneclick/rubyinstaller2/releases/download/rubyinstaller-2.5.3-1/rubyinstaller-devkit-2.5.3-1-x64.exe
```

1. Jekyll, Bundle 설치 SSL 오류 발생의 경우
``` 
gem install rubygems-update --source http://rubygems.org/ 
update_rubygems --no-ri --no-rdoc
gem uninstall rubygems-update -x
gem install jekyll bundler 
```

1. bundle exec jekyll serve 실행에서 scss 파일 오류 발생의 경우
```
윈도우 제어판 > 시스템 로캘 변경 > Beta : UTF-8 사용 선택
```


## data 관련 매뉴얼 작성 Tip
- pages/datadev : 개발자 매뉴얼
- pages/user/data : 사용자 매뉴얼 데이터 부분
- pages/user/mat : 소재 포털 사용자 매뉴얼 
- images/data : 그림 파일 위치 