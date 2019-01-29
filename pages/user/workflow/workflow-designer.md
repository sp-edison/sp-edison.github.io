---
title: 워크플로우 편집기 매뉴얼
tags: [workflow]
keywords: workflow
summary: "워크플로우 편집기 사용자 매뉴얼"
sidebar: user_sidebar
permalink: /workflow_workflow-designer.html
folder: workflow
---

## 워크플로우 편집기

### [워크플로우 편집기 URL](http://www.edison.re.kr/web/portal/workflow-workbench) 

### 워크플로우 생성

1. 화면 좌측 상단의 `New` 메뉴 클릭한다.
1. `Title`과 `Description` 을 입력하고 `Create` 버튼을 클릭한다.
<br>
{% include image.html file="user/workflow/designer_main_01.png"%}
<br>

### 워크플로우 편집

#### 워크플로우 편집 시작

1. 화면 좌측 `Apps` 메뉴를 클릭하여 `사이언스 앱 선택 도구`를 생성한다.
1. `사이언스 앱 선택 도구`에서 워크플로우에서 사용하고자 하는 앱을 선턱하여 좌측 `워크플로우 캔버스`로 드래그 한다.
<br>
{% include image.html file="user/workflow/designer_main_02.png"%}
<br>

1. `Search` 기능을 이용하여 사이언스 앱을 좀 더 편리하게 선택할 수 있습니다.
<br>
{% include image.html file="user/workflow/designer_main_15.png"%}
<br>


#### 사이언스 앱 연결

1. 2개 이상의 `사이언스 앱`을 연결하여 순차적으로 동작하는 워크플로우를 생성할 수 있습니다.
<br>
{% include image.html file="user/workflow/designer_main_16.png"%}
<br>
1. 연결된 `Output Port`의 출력은 `Input Port`의 입력으로 사용되며, 동일한 `Data Type`을 가지는 `Port`끼리만 연결 됩니다.
1. 하나의 `Output Port` 출력은 `n`개의 사이언스 앱의 `Input Port`로 사용될 수 있습니다.
<br>
{% include image.html file="user/workflow/designer_main_17.png"%}
<br>

#### Sample File 등록 및 Default Editor 선택

- 사이언스 앱의 `Input Port`를 `더블 클릭`하여 `Sample File` 및 `Default Editor`를 설정할 수 있습니다.
<br>
{% include image.html file="user/workflow/designer_main_18.png"%}
<br>

##### Sample File

1. 워크플로우에서 사용되는 `사이언스 앱`은 앱 자체에 등록되어 있는 `Sample File` 이외에 워크플로우 작성과정에서 Sample File를 설정할 수 있습니다.
1. 등록된 `Sample File`는 워크플로우를 `사이언스 앱`으로 등록하여 공개할 때, 다른 사용자들에게 공유됩니다.
1. 등록된 `Sample File`는 워크플로우 `실행` 시 사용자가 선택하여 `Input Port`의 입력값으로 사용할 수 있습니다.

##### Default Editor

1. 워크플로우에서 `Input Port` 입력에 사용할 `Default Editor`를 선택하여 워크플로우 실행 시 `사이언스 앱`의 입력 데이터를 저장할 수 있습니다.
1. 설정된 `Default Editor`는 워크플로우 편집기에서만 수정할 수 있습니다.  

### 워크플로우 저장

1. 워크플로우를 모두 작성하였다면 좌측 상단 `Save` 버튼을 클릭하여 작성된 워크플로우를 저장할 수 있다.
1. 또한, `Ctrl + s` 단축키를 이용하여 워크플로우를 저장할 수 있다.
1. 성공적으로 워크플로우가 저장되면 우측 상단에 `성공적으로 워크플로우를 저장하였습니다` 라는 메시지가 출력됨을 확인할 수 있다.
1. `Save As` 메뉴를 통해 현재 생성된 워크플로우가 아닌 새로운 워크플로우를 생성함과 동시에 저장할 수 있다.
<br>
{% include image.html file="user/workflow/designer_main_03.png"%}
<br>

### 워크플로우 불러오기

1. 화면 좌측 `Open` 메뉴를 클릭하여 `워크플로우 저장 목록`을 생성한다.
1. 목록에서 불러오고자 하는 워크플로우를 클릭하여 선택한 후, `워크플로우 저장 목록` 하단의 `Open` 버튼을 클릭한다.
<br>
{% include image.html file="user/workflow/designer_main_04.png"%}
<br>

### 워크플로우 Rename / Duplicate / Delete / Setting

#### Rename

1. 화면 좌측 `Open` 메뉴를 클릭하여 `워크플로우 저장 목록`을 생성한다.
1. 목록에서 이름을 변경하고자 하는 워크플로우를 클릭하여 선택한 후, `워크플로우 저장 목록` 하단의 `Rename` 버튼을 클릭한다.
1. 생성된 팝업에 변경하고자 하는 워크플로우 이름을 입력하고 `Save` 버튼을 클릭한다.
<br>
{% include image.html file="user/workflow/designer_main_05.png"%}
<br>

#### Duplicate

1. 목록에서 복사하고자 하는 워크플로우를 클릭하여 선택한 후, `워크플로우 저장 목록` 하단의 `Duplicate` 버튼을 클릭한다.
1. 생성된 팝업에 복사된 워크프로우의 이름을 입력하고 `Save` 버튼을 클릭한다.
<br>
{% include image.html file="user/workflow/designer_main_06.png"%}
<br>

#### Delete

1. 목록에서 삭제하고자 하는 워크플로우를 클릭하여 선택한 후, `워크플로우 저장 목록` 하단의 `Delete` 버튼을 클릭한다.
<br>
{% include image.html file="user/workflow/designer_main_07.png"%}
<br>

#### Setting

1. 워크플로우가 로딩된 상태에서는 `Setting` 메뉴에서 워크플로우의 `이름`, `설명`을 수정할 수 있고, `삭제`가 가능하다.
<br>
{% include image.html file="user/workflow/designer_main_10.png"%}
<br>

### 워크플로우 사이언스 앱 등록

#### 워크플로우 사이언스 앱

- 생성된 워크플로우를 `사이언스 앱`으로 등록하여 공개 및 공유할 수 있습니다.
- 공개된 워크플로우는 EDISON의 다른 사용자들에 의해 자유롭게 실행될 수 있습니다.
<br>
{% include image.html file="user/workflow/designer_main_12.png"%}
<br>

#### 사이언스 앱 등록 과정

1. `사이언스 앱`으로 등록하고자 하는 워크플로우를 작성한 후 좌측 `Register App` 메뉴를 클릭하여 `사이언스 앱` 등록 화면으로 이동합니다.
1. EDISON에서 사용하고 있는 여타 앱과 마찬가지로 `이름`, `버전` 등의 정보를 입력하여 `사이언스 앱`으로 등록합니다.
1. 등록된 사이언스 앱을 `서비스 요청`하여 공개할 수 있습니다.
1. `서비스`된 이후의 워크플로우는 수정할 수 없으며 `Duplicate`하여 수정 및 버전관리할 수 있습니다.
<br>
{% include image.html file="user/workflow/designer_main_13.png"%}
<br>
<br>
{% include image.html file="user/workflow/designer_main_14.png"%}
<br>

### 워크플로우 실행

- 작성된 워크플로우는 별도의 다른 과정 없이 `Execute` 버튼을 클릭하여 [워크플로우 실행](/workflow_workflow-executor.html) 메뉴로 이동한 후 실행할 수 있습니다.

<br>
{% include image.html file="user/workflow/designer_main_09.png"%}
<br>

<br><br><br>
