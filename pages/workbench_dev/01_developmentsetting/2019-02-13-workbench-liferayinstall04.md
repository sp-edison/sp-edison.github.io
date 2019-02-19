---
title: JDK 1.7 설정
keywords:
summary: "본 문서는 워크벤치 기반 전후처리기 개발을 위한 매뉴얼입니다."
sidebar: workbench_sidebar
permalink: workbenchsetting4.html
tags: [workbench]
folder: workbench
---

## JDK 1.7 설정
DeveloperStudio에서 JDK 버전 설정을 위해 상위 메뉴중 `Window`메뉴를 선택하고 `Preferences`를 선택하여 Preferences설정 창을 엽니다.
{% include image.html file="workbench_dev/liferayinstall/19.png" %}<br>
Preferences창에서 `java` 탭 내에 `Installed JREs`에서 아래 그림과 같이 설정을 합니다.
{% include image.html file="workbench_dev/liferayinstall/29.png" %}<br>
기본적인 셋팅으로 JRE 1.8 버전으로 DeveloperStudio가 구동되게 되어 있습니다. 워크벤치 기반 전후처리기 개발을 위해서 JDK 1.7 기반으로 설정을 바꿔야 합니다. 해당 내용은 아래와 같습니다.<br>

1. Add 버튼 선택{% include image.html file="workbench_dev/liferayinstall/29.png" %}<br>
2. Standard VM 선택{% include image.html file="workbench_dev/liferayinstall/30.png" %}<br>
3. JRE home Directory 선택 {% include image.html file="workbench_dev/liferayinstall/31.png" %}<br>
4. JDK 1.7 버전이 설치된 디렉토리 선택 {% include image.html file="workbench_dev/liferayinstall/32.png" %}<br>
5. JDK 1.7 설정 Finish 선택 {% include image.html file="workbench_dev/liferayinstall/33.png" %}<br>
6. 설치된 JRE 리스트 중 JDK 1.7 버전 체크 및 Apply 버튼 클릭 {% include image.html file="workbench_dev/liferayinstall/34.png" %}<br>
7. Java Compiler 탭에서 아래 그림과 같이 설정 {% include image.html file="workbench_dev/liferayinstall/28.png" %}<br>
