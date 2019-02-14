---
title: Liferay 설치 파일 다운로드
keywords:
summary: "본 문서는 워크벤치 기반 전후처리기 개발을 위한 매뉴얼입니다."
sidebar: workbench_sidebar
permalink: workbenchsetting1.html
tags: [workbench]
folder: workbench
---
EDISON 포털 기반 워크벤치에서 동작하는 전후처리기 개발을 진행하기 위해서는 다음과 같은 파일들을 설치해야 합니다. 해당 파일을 다운받아 개발환경에 맞게 설치해 주시기 바랍니다.

## Liferay 설치 파일 다운로드
Liferay 설치를 위해서는 필수적으로 3가지의 파일이 필요합니다. 해당 파일들은 오픈소스로 누구나 다운받아 개인 사용자 PC에 설치 할 수 있습니다.<br>
설치해야 하는 리스트는 다음과 같습니다.
- [Liferay Portal Tomcat 6.2.6](https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.5%20GA6/)
- [Liferay Plugin SDK 6.2.6](https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.5%20GA6/)
- [Liferay IDE](https://sourceforge.net/projects/lportal/files/Liferay%20IDE/3.4.0/)

### Liferay SDK와 Portal Tomcat 다운로드
다운로드 링크로 가게 되면 다음과 괕은 화면을 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/1.png" %}<br>
현재 EDISON 플랫폼에서 사용하고 있는 워크벤치 기반 전후처리기를 개발하기 위해서는 서로 버전을 통일해야 합니다. 따라서 현재 EDISON 플랫폼에서 사용중인 `Lifeary Plugin SDK 6.2.6` 버전과
`Liferay Portal tomcat 6.2.6` 버전을 다운받아 사용합니다.

### 포틀릿 개발을 위한 개발 도구 다운로드
Liferay IDE 다운로드 링크를 따라가면 아래 그림과 같은 화면으로 이동하게 됩니다.
{% include image.html file="workbench_dev/liferayinstall/2.png" %}<br>
위의 그림과 같이 Liferay IDE는 윈도우 운영체제, 맥운영체제, 리눅스 운영체제를 지원하고 있습니다. 현재 사용중인 운영체제에 맞는 IDE를 다운받아 사용하면 됩니다.

### 다운로드 파일 확인
현재 다운로드 받은 세 개의 파일을 확인하면 다음 그림과 같습니다.
{% include image.html file="workbench_dev/liferayinstall/3.png" %}<br>
윈도우 운영체제를 기반으로 설치를 진행하는 화면입니다. 정상적인 파일을 다운받게 되었으면, SDK, tomcat, IDE 설치 파일 세 개의 파일을 다운 받으셔야 합니다.

### JDK 1.7 설치
Liferay 6.2 버전에서 원활한 개발을 위해서는 JDK 1.7 버전에서의 실행 환경을 구성해야 합니다.
JDK 설치 파일을 확인하고 운영체제에 맞게 다운받아 설치하시기 바랍니다.
- [JDK 1.7](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html)

### ANT 1.9 설치
Liferay 6.2 버전에서 개발된 포틀릿을 웹 포털에 설치(deploy) 하기 위해서는 Ant 버전 1.9를 설치해야 합니다. 해당 ant 1.9를 운영체제에 맞게 다운받아 설치하시기 바랍니다.
JDK 설치 파일을 확인하고 운영체제에 맞게 다운받아 설치하시기 바랍니다.
- [ANT 1.9](https://ant.apache.org/bindownload.cgi)

모든 파일의 다운로드 및 설치가 끝나면 해당 설정하는 방법은 다음 매뉴얼을 참고하시기 바랍니다.
