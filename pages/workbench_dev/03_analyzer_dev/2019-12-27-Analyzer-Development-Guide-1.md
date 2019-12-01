---
title: "프로젝트 생성"
permalink: workbench_analyzerguide1.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
summary: 에디슨 워크벤치 기반 후처리기(Post-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 분석기(Post-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## Liferay 6.2 기반 프로젝트 구성
개발 환경은 아래와 같습니다.

- `liferay-developer-studio`
- `liferay-portal-6.2-ce-ga6`
- `liferay-plugins-sdk-6.2`




## 1. Liferay plugin Project  생성
liferay-developer-studio 환경에서 `Liferay Plugins Projects`를 생성합니다.
<br>이클립스 환경에서 New -> Liferay Plugin Project를 선택합니다.<br>

{% include image.html file="workbench_dev/analyzer_dev/1.png" %}
<br><br>프로젝트 이름을 작성하고 include sample code 체크를 해지합니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/2.png" %}
<br><br>프로젝트 이름을 작성하고 Liferay MVC를 선택하여 최종적으로 프로젝트 생성을 마무리 합니다.<br>

## 2. EDISON 워크벤치 연동을 위한 Analyzer 포틀릿 생성
EDISON 플랫폼의 워크벤치 연동을 위한 포틀릿을 생성합니다.
<br>생성된 Liferay Plugins Projects 내에 Liferay Portlet을 생성합니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/3.png" %}
<br><br>포틀릿 클래스명, 패키지명은 자유롭게 원하는 형태로 생성합니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/4.png" %}
<br><br>특별히 추가할 인터페이스가 없다면 Finish를 선택하고 포틀릿 생성을 완료합니다.


## 3. Library 설정
### SciencePlatform-hook-service.jar 라이브러리 추가 
EDISON 플랫폼에서 워크벤치와 연동을 위해서는 워크벤치 시뮬레이션 서비스와 연동이 가능하도록 라이브러리를 추가 해야 합니다 <br>
`SciencePlatform-hook-service.jar` 파일을 플러그인 프로젝트 내부에 `WEB-INF/lib` 폴더에 추가합니다.<br>
해당 라이브러리 파일은 다음 링크에서 다운받을 수 있습니다.<br>

- [SciencePlatform-hook-service.jar](OSPLibrary/SciencePlatform-hook-service.jar)

라이브러리 다운받아 추가하면 다음 그림과 같습니다.
{% include image.html file="workbench_dev/analyzer_dev/5.png" %}<br>

### jstl Dependency 추가
플러그인 프로젝트 내에 포함되어 있는 liferay-plugin-package.properties 파일에서 Portal Dependency Jars 에서 Add 버튼을 클릭하여 라이브러리를 추가합니다.<br>
liferay-plugin-package.properties 파일에 “jstl-api.jar”, “jstl-impl.jar” 파일을 추가합니다. <br>
{% include image.html file="workbench_dev/analyzer_dev/6.png" %}<br>

