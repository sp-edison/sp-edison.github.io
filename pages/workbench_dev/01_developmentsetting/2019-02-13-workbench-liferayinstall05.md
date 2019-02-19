---
title: tomcat 서버 설정
keywords:
summary: "본 문서는 워크벤치 기반 전후처리기 개발을 위한 매뉴얼입니다."
sidebar: workbench_sidebar
permalink: workbenchsetting5.html
tags: [workbench]
folder: workbench
---

## tomcat 서버 생성
이전 설정이 끝나고 다운 받은 Liferay 6.2 버전의 서버를 현재 DeveloperStudio와 연결해야 합니다. 아래의 그림과 같은 화면에서 아무런 서버가 연결되어 있지 않다면
`No servers are available. Click this link to create a new server...`의 문구를 왼쪽 하단부에서 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/18.png" %}<br>
해당 링크를 선택하면 새로운 서버를 연결시킬 수 있는 팝업 화면이 뜨게 됩니다.
{% include image.html file="workbench_dev/liferayinstall/35.png" %}<br>
위의 그림에서와 마찬가지로 EDISON 플랫폼 기반 전후처리기를 개발하기 위해서는 Liferay 6.2 버전의 서버를 설치해야 합니다. 따라서 `Liferay v6.2 Server (Tomcat 7)`을 선택하고 Next 버튼을 선택합니다.

### tomcat 디렉토리 연결
미리 다운받아놓은 파일 중에서 `liferay-portal-6.2-ce-ga6`의 압축을 풀면 해당 폴더 내에 포털(서버) 실행을 위한 파일들이 존재합니다.
해당 폴더 내 `tomcat-7.0.62` 폴더를 선택하여 Liferay Tomcat directory로 설정합니다.
 또한 서버 실행을 위한 자바 환경 파일은 이전에 설치되어 있는 jdk 1.7 버전인 `jdk1.7.0_79`을 선택합니다. 해당 설정이 모두 끝나면 Next 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/37.png" %}<br>
{% include image.html file="workbench_dev/liferayinstall/36.png" %}<br>
크게 설정할 내용은 아직 없으므로 Next 버튼을 선택합니다.
{% include image.html file="workbench_dev/liferayinstall/38.png" %}<br>
따로 설정할 내용은 없으므로 Finish 버튼을 선택하여 서버 생성을 종료합니다.
{% include image.html file="workbench_dev/liferayinstall/39.png" %}<br>

### 서버 Overview 설정
서버 생성을 종료하면 아래 그림과 같이 서버가 생성된 화면을 확인할 수 있습니다.
{% include image.html file="workbench_dev/liferayinstall/40.png" %}<br>
그림에서 왼쪽 하단부 Server 부분의 생성된 Liferay v6.2의 서버를 더블 클릭하면 현재 생성된 서버의 오버뷰(Overview)를 확인할 수 있습니다.
오버뷰에서 수정해야 하는 내용은 다음과 같습니다.

| 수정 내용          | 수정 전               | 수정 후                            |
|:-------------------|:----------------------|:-----------------------------------|
|Memory args         | -Xmx1024m             | -Xmx1024m --XX:MaxPermSize=512m    |
|User timezone       |  GMT                  | KST                                |


수정이 완료된 후 서버 Overview 내용은 다음 그림과 같습니다.
{% include image.html file="workbench_dev/liferayinstall/41.png" %}<br>

### 서버 실행 설정
서버의 실행 환경 설정을 위해 서버의 Overview 파일에서 `Open Luanch Configuration`링크를 선택합니다. 해당 링크를 선택하면 아래 그림과 같은 화면이 팝업으로 뜨게 됩니다.
{% include image.html file="workbench_dev/liferayinstall/45.png" %}<br>
{% include image.html file="workbench_dev/liferayinstall/46.png" %}<br>
해당 팝업은 실행 환경에서 변수를 지정할 수 있습니다. 해당 변수를 지정하기 위해 다음 그림과 같이 변수를 설정하고 저정합니다.


| 변수 명          | 내용                                          | 의미                                     |
|:-----------------|:----------------------------------------------|:-----------------------------------------|
|JAVA_HOME         | C:\Program Files\Java\jdk1.7.0.79             | 설치된 JDK 1.7 폴더 경로                 |
|PATH              |  C:\Program Files\Java\jdk1.7.0.79\bin        | 설치된 JDK 1.7 폴더 내 bin 폴더 경로     |

변수를 지정하는 그림은 아래와 같습니다.
{% include image.html file="workbench_dev/liferayinstall/47.png" %}<br>
{% include image.html file="workbench_dev/liferayinstall/48.png" %}<br>

### Portal 서버 세부 설정
서버에 추가적으로 설정해야 하는 내용이 있습니다. 따라서 해당 서버의 오른쪽 클릭을 하여 뜨는 메뉴 중에서 `Create Portal Settings File`을 선택하면 자동으로 설정 파일이 생성되게 됩니다.
오른쪽 클릭을 했을 때 뜨는 화면은 아래 그림과 같습니다.
{% include image.html file="workbench_dev/liferayinstall/42.png" %}<br>

### 데이터 베이스 연결
서버와 연결해야하는 데이터베이스가 존재한다면, 해당 `portal-ext.properties`에서 설정이 가능합니다.
Mysql 데이터베이스 시스템을 기준으로 연결해야하는 데이터 베이스인 `myDataBase`의 명으로 존재한다면 다음 예시와 같이 설정 할 수 있습니다.

```java
#
# MySQL
#
# Local
jdbc.default.driverClassName=com.mysql.jdbc.Driver
jdbc.default.url=jdbc:mysql://localhost/myDataBase?useUnicode=true&characterEncoding=UTF-8&useFastDateParsing=false
jdbc.default.username=root
jdbc.default.password=********(해당 패스워드)
```

### 파일 익스플로러 지원을 위한 디렉토리 설정
현재 EDISON 포털의 워크벤치를 기반으로 전후처리기를 개발한다면, 해당 전후처리기 개발을 위한 파일 익스플로러의 지원이 필요합니다. 따라서 파일 익스플로러 연결을 위한 몇 가지 설정이 필요합니다.
현재 EDISON 서버 내의 파일 연결을 위한 설정입니다.
```java
portlet.add.default.resource.check.enabled=false

osp.root.dir.path=/EDISON/LDAP
osp.user.root.dir.path=/EDISON/LDAP/DATA
```
위와 같이 해당 내용을 설정한 후, 파일 익스플로러와 연결되어 전후처리기가 동작하는 설정을 하기 위해서는 현재 서버가 위치하는 드라이브 하위에 다음과 같은 폴더 및 디렉토리 구조를 생성해야 합니다.
편집기 분석기에서 서버 파일을 클릭하면 아래의 경로의 파일이 보입니다.

```java
/EDISON/LDAP/DATA/[screen name]/repository
```

즉 만약 현재 사용자의 Screen Name 이 `edisonadm`이고, 톰캣 서버가 존재하는 드라이브가 D 드라이브에 존재한다면 아래 그림과 깉은 폴더 구조를 미리 생성해 놓아야 합니다.
{% include image.html file="workbench_dev/liferayinstall/44.png" %}<br>
