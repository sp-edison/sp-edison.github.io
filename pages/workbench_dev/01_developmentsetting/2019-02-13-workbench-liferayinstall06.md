---
title: ANT 1.9 설정
keywords:
summary: "본 문서는 워크벤치 기반 전후처리기 개발을 위한 매뉴얼입니다."
sidebar: workbench_sidebar
permalink: workbenchsetting6.html
tags: [workbench]
folder: workbench
---

## ANT 1.9 설정
기본적으로 DeveloperStudio에서 제공되는 Ant는 1.10 버전이며, Liferay 6 버전의 개발을 진행할 수 없습니다. 따라서 기본적인 Ant 설정을 삭제하고 추가적으로 필요한 Ant 1.9 버전을 설치합니다.

### 1. Preferences 설정
처음으로 DeveloperStudio에서 상위 메뉴에서 Window 하위 메뉴 중 Preferences 를 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/19.png" %}<br>

### 2. 기본 Ant 설정 삭제
Preferences 창에서 Ant 하위 메뉴 중 Runtime 메뉴를 선택하면 다음 그림과 같은 화면이 나오게 됩니다.
{% include image.html file="workbench_dev/liferayinstall/20.png" %}<br>
위의 표시된 내용과 같이 Ant의 Home Entries의 내용을 전체 선택 한 후, 기본 Ant 설정을 삭제합니다.

### 3. Ant Home 설정
모든 Default로 설정된 Ant 설정이 사라지면 아래와 같은 화면이 됩니다. 그림에서와 같이 `Ant Home...` 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/21.png" %}<br>
Ant Home 버튼을 선택하면 Ant가 설치된 디렉토리를 설정할 수 있습니다.
Ant 1.9가 설치된 디렉토리를 아래와 같이 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/22.png" %}<br>
디렉토리를 선택하고 확인 버튼을 누르면 자동으로 Ant Home Entries에 적용된 화면을 아래 그림과 같이 볼 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/23.png" %}<br>
