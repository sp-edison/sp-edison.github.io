---
title: Liferay IDE 설치
keywords:
ssummary: "본 문서는 워크벤치 기반 전후처리기 개발을 위한 매뉴얼입니다."
sidebar: workbench_sidebar
permalink: workbenchsetting2.html
tags: [workbench]
folder: workbench
---

## Liferay IDE 설치
Liferay 기반 개발을 진행하기 위해서는 통합 개발 환경인 IDE(Integrated Development Environment, IDE)를 의미하며, Liferay 개발자를 위해 liferay 플랫폼을 기반으로 하는 개발 환경을 제공합니다.
해당 IDE는 Liferay에서 이클립스를 기반으로 개발 환경을 구축해 놓은 파일을 다운받아 설정을 하고 개발환경을 구성합니다.
<br>
이전 매뉴얼에서 확인했듯이 `[Liferay IDE](https://sourceforge.net/projects/lportal/files/Liferay%20IDE/3.4.0/)`에서 파일을 다운받아 설치합니다.
윈도우 운영체제를 기반으로 설치 방법을 진행하겠습니다.

### 1. 관리자 권한으로 실행
다운로드 받은 IDE 설치 파일을 마우스 오른쪽 클릭을 하여 관리자 권한으로 실행합니다.
{% include image.html file="workbench_dev/liferayinstall/4.png" %}<br>

### 2. JDK 1.8 기반으로 실행
개발 환경 설치를 시작하면 설치되는 IDE의 실행 환경인 JVM의 버전을 설치합니다.
{% include image.html file="workbench_dev/liferayinstall/5.png" %}<br>
실제 개발 환경을 설정할 때에는 개발 IDE 내부의 개발 환경을 JDK 1.7 버전으로 수정하게 됩니다.

### 3. 설치 내용
설치를 시작하면 아래 그림과 같은 화면을 확인할 수 있습니다. Nxet를 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/6.png" %}<br>

다음으로는 설치할 위치를 설정합니다. 기본적으로 윈도우 운영체제에서는 `C:\Program Files (x86)\LiferayProjectSDKwithDevStudioCommunityEdition` 폴더가 기본으로 설정되어 있습니다.
크게 변경되는 내용이 없으면 바로 Nxet 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/7.png" %}<br>

Install Command Like Tools 체크를 한 상태로 Next 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/8.png" %}<br>

Skip proxt configuration 체크를 한 상태로 Next 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/9.png" %}<br>

다음으로 모든 설치 준비가 완료되었다는 화면을 확인할 수 있습니다. 다시 설정하고 싶은 내용이 없으면  Next 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/10.png" %}<br>

설치하고 완료되면 아래와 같은 화면을 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/11.png" %}
{% include image.html file="workbench_dev/liferayinstall/12.png" %}<br>
위와 같이 설치가 완료되면 Finish 버튼을 선택하여 설치를 종료합니다.

### 4. 설치 확인
실제 설치된 위치인 `C:\Program Files (x86)\LiferayProjectSDKwithDevStudioCommunityEdition` 폴더에 가서 설치 내용을 확인하면 아래 그림과 같습니다.
{% include image.html file="workbench_dev/liferayinstall/13.png" %}
다운받은 Liferay IDE 설치 파일을 이용하여 설치를 진행하면 위의 그림과 같이 두개의 폴더가 설치된 것을 확인할 수 있습니다.
두 개의 폴더 중 IDE 환경은 `liferay-developer-studio`의 파일에 설치되어 있습니다. 해당 폴더를 들어가면 아래와 같은 설치된 파일들을 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/14.png" %}

### IDE 실행 환경 설정
처음 실행 환경을 설정어할 때, 기본 IDE 파일 실행 메모리가 매우 작아 원활한 실행 환경 설정을 위해 실행 환경 값을 변경합니다. 폴더 내 파일중 `DeveloperStudio.ini`파일의 내용을 수정합니다.
- 기본 환경 설정<br>
처음 기본으로 설정된 구성 환경 파일은 아래와 같습니다.
```terminal
-startup
plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.551.v20171108-1834
-product
com.liferay.ide.studio.ui.product
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
384M
-showsplash
com.liferay.ide.studio.ui
-vmargs
-Dosgi.requiredJavaVersion=1.8
-Xms40m
-Xmx1024m
-Dsun.java2d.noddraw=true
```

- 수정된 환경 설정<br>
수정해야 하는 내용은 아래와 같습니다.
```terminal
-startup
plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.551.v20171108-1834
-product
com.liferay.ide.studio.ui.product
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
512M
-showsplash
com.liferay.ide.studio.ui
-vmargs
-Dosgi.requiredJavaVersion=1.8
-Xms1024m
-Xmx2048m
-Dsun.java2d.noddraw=true
```
수정되는 내용은 메모리 사용량을 약간 늘리는 내용입니다. 각 컴퓨터의 사양에 맞춰 적당한 크기로 늘려 주시기 바랍니다.
`--launcher.XXMaxPermSize 512M`, `-Xms1024m`, `-Xmx2048m`의 내용을 수정하였으며, 원활한 개발을 위한 최소한의 메모리 사용량을 기준으로 수정하였습니다.
