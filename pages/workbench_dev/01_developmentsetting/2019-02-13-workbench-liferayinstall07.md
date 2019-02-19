---
title: SDK 설정
keywords:
sidebar: workbench_sidebar
summary: "본 문서는 워크벤치 기반 전후처리기 개발을 위한 매뉴얼입니다."
permalink: workbenchsetting7.html
tags: [workbench]
folder: workbench
---

## SDK 설정
Liferay 6.2에서 개발되어 추가되는 개발 모듈은 포틀릿(portlet) 단위로 구성되어 플러그인 처럼 추가 될 수 있습니다. 따라서 개발 모듈에 대한 전체 디렉토리인 Liferay Plufins SDK Directory를 설정할 수 있습니다.

### 1. Import SDK 폴더
처음으로 DeveloperStudio에서 Project Explorer 부분에서 사용자 마우스 우클릭을 합니다. 그 후 Import 메뉴의 하위 메뉴에서 Import를 선택합니다.
아래 그림과 같이 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/49.png" %}<br>

### 2. Liferay Plugins SDK Directory 선택
Import를 선택하면 아래와 같은 팝업창이 나타나게 됩니다. 이 중에서 Liferay 하위 메뉴에서 `Liferay Plugins SDK Directory`를 선택합니다. 그리고 난 후 Next 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/50.png" %}<br>

### 3. SDK 디렉토리 설정
SDK 디렉토리를 자동으로 DeveloperStudio에서는 인식이 가능합니다. 아래 그림과 같이 아무런 SDK 디렉토리가 설정되어 있지 않으면, 다음 단계로 넘어갈 수가 없습니다.
{% include image.html file="workbench_dev/liferayinstall/51.png" %}<br>
SDK Directory는 초반에 다운받은 Liferay SDK 6.2의 압축을 푼 폴더가 됩니다. 아래 그림과 같이 `liferay-plugins-sdk-6.2`를 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/52.png" %}<br>
적절한 폴더가 선택되면 아래 그림과 같이 처음과는 다르게 SDK 설정을 마칠 수 있는 `Finish` 버튼이 활성화 됩니다. Finish버튼을 선택하고 설정을 종료합니다.
{% include image.html file="workbench_dev/liferayinstall/53.png" %}<br>


### 4. 서버 연결
SDK의 import 과정이 모두 끝나게 되면, 서버와 연결을 설정해야 합니다.
SDK 폴더 내 `build.properties` 파일 내 tomcat 서버의 연결을 설정하는 부분이 존재하는데 해당 폴더 위치를 다운 받은 Liferay tomcat 서버와 연결시켜야 합니다.
기본으로 설정되어 있는 서버의 위치는 `app.server.parent.dir=${sdk.dir}/../bundles`로 설정되어 있습니다. 해당 내용은 아래 그림에서 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/54.png" %}<br>
현재 서버와 SDK가 설치된 위치의 관계는 다음 그림과 같습니다.
{% include image.html file="workbench_dev/liferayinstall/55.png" %}<br>
해당 내용을 바탕으로 서버의 위치를 설정하면 `app.server.parent.dir=${sdk.dir}/../liferay-portal-6.2-ce-ga6`값으로 변경해야 합니다.
변경된 내용을 저장하면 다음 그림과 같은 화면을 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/56.png" %}<br>

### 5. ivy url 설정
SDK 폴더 내 ivy 에러 해결을 위해 `plugin-sdk/ivy-settings.xml` 파일 내 ivy url을 수정해 줘야 합니다.
해당 내용은 아래와 같습니다.
```xml
<ivysettings>
    <settings defaultResolver="default" />

    <resolvers>
        <!-- remove -->
        <!-- <ibiblio m2compatible="true" name="liferay-public" root="http://cdn.repository.liferay.com/nexus/content/groups/public" /> -->
        <!-- add -->
        <ibiblio m2compatible="true" name="liferay-public" root="https://repository.liferay.com/nexus/content/repositories/public" />
        <ibiblio m2compatible="true" name="local-m2" root="file://${user.home}/.m2/repository" />

        <chain dual="true" name="default">
            <resolver ref="local-m2" />

            <resolver ref="liferay-public" />
        </chain>
    </resolvers>
</ivysettings>
```
최근 URL 인식이 안되는 경우가 있습니다. 해당하는 경우 다음 링크에서 파일을 다운받아 압축을 풀어서 SDK 폴더 내에 `.ivy`에 덮어씌워 실행을 하면 에러를 처리할 수 있습니다.
- [.ivy](/OSPLibrary/.ivy.zip)
 <a href='/OSPLibrary/.ivy.zip'>.ivy</a><br>

### 6. 그 외 설정
SDK 폴더 내 `build.properties` 내부에 compiler와 관련된 내용을 수정해야 합니다.
해당 내용은 아래 그림과 같습니다.
{% include image.html file="workbench_dev/liferayinstall/24.png" %}<br>
{% include image.html file="workbench_dev/liferayinstall/25.png" %}<br>

수정해야 하는 내용은 다음 표와 같습니다.



| 수정 전                           | 수정 후                            |
|:----------------------------------|:-----------------------------------|
| ant.build.javac.source=1.6        | ant.build.javac.source=1.6         |
| ant.build.javac.target=1.6        | ant.build.javac.target=1.7         |
