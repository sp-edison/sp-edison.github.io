---
title: 워크플로우 실행 매뉴얼
tags: [workflow]
keywords: workflow
summary: "워크플로우 실행 사용자 매뉴얼"
sidebar: user_sidebar
permalink: /workflow_workflow-executor.html
folder: workflow
---

## 워크플로우 실행

### 워크플로우 실행 메뉴로 이동

1. [워크플로우 편집기](http://www.edison.re.kr/web/portal/workflow-workbench)에서 편집된 워크플로우의 실행 화면으로 바로 이동할 수 있습니다.
<br>![capture](/images/user/workflow/designer_main_09.png "워크플로우 실행")<br>
1. [사이언스 앱스토어](http://www.edison.re.kr/web/portal/scienceappstore)에서 `사이언스 앱`으로 등록된 워크플로우를 선택하여 실행할 수 있습니다.(`Run` 버튼 클릭)    
<br>![capture](/images/user/workflow/exe_01.png "워크플로우 실행")<br>

###  Simulation 생성

1. 워크플로우를 실행하기 위해서는 `사이언스 앱`과 마찬가지로 `Simulation`을 먼저 생성해야 합니다.
1. `Simulation`의 제목을 입력하면, 실행을 위한 `Simulation Job` 하나가 자동 생성됩니다.
1. 하나의 `Simulation`은 `n`개의 `Simulation Job`을 포함할 수 있습니다.

<br>![capture](/images/user/workflow/exe_02.png "워크플로우 실행")<br>
<br>![capture](/images/user/workflow/exe_03.png "워크플로우 실행")<br>

### Simulation 관리 

1. `Simulation`은 워크플로우 실행의 기본 단위이며 `Simulations`메뉴에서 `New`/`Open`/`Rename`/`Delete` 버튼을 통해 각각 생성/불러오기/이름변경/삭제할 수 있습니다.
1. `Simulations` 팝업 상단의 검색 기능을 이용하여 편리하게 찾고자 하는 `Simulation`을 검색할 수 있습니다.
<br>![capture](/images/user/workflow/exe_04.png "워크플로우 실행")<br>



### Simulation Job 생성

1. 워크플로우 `Simulation`은 `Simulations Job` 단위로 실행되며, 실행 상태를 관리할 수 있습니다.
1. 생성된 `Simulation Job`의 `사이언스 앱`별 `Input Port` 와 `Output Port`는 화면 좌측에 목록 형태로 출력됩니다.
1. 또한, 우측 캔버스에서 워크플로우 흐름도 형태로 출력됩니다.
<br>![capture](/images/user/workflow/exe_05.png "워크플로우 실행")<br>
1. 좌측 목록에서 `사이언스 앱`의 `Input Port`와 `Output Port`로 마우스 오버할 때 선택된 포트로 이동하여 하일라이팅된 상태로 출력됩니다. 
1. 좌측 목록 또는 우측 캔버스에서 `Input Port` 또는 `Output Port`를 클릭할 경우 워크플로우의 실행 상태에 따라 해당 포트의 `Editor` 또는 `Analyzer`가 팝업 됩니다.
<br>![capture](/images/user/workflow/exe_06.png "워크플로우 실행")<br>

### Simulation Job 실행

1. 좌측 목록 또는 우측 캔버스에서 `Input Port`를 클릭하여 해당 포트의 `Editor` 팝업을 호출한 후 데이터를 입력합니다.
<br>![capture](/images/user/workflow/exe_08.png "워크플로우 실행")<br>
1. 데이터를 모두 입력하였다면 상단의 `Submit` 버튼을 클릭하여 `Simulation Job`을 제출 및 실행합니다.
1. 필요한 `Input Port`를 모두 입력하지 않았다면, 경고 메시지와 함께 해당 포트는 붉은 색으로 표시되며 `Simulation Job`은 제출되지 않습니다.
<br>![capture](/images/user/workflow/exe_07.png "워크플로우 실행")<br>
1. 성공적으로 `Submit` 하였다면 우측 캔버스에서 워크플로우의 실행 과정을 살펴볼 수 있습니다.
<br>![capture](/images/user/workflow/exe_09.png "워크플로우 실행")<br>

### Simulation Job 실행결과 확인

1. 좌측 목록 또는 우측 캔버스에서 `Output Port`를 클릭하여 해당 포트의 `Analyzer` 팝업을 호출한 후 실행 결과를 확인 또는 다운로드할 수 있습니다.
1. 워크플로우를 실행하는 중에도 각 사이언스 앱의 상태가 `Success`가 된다면 실행 결과를 확인할 수 있습니다.
<br>![capture](/images/user/workflow/exe_10.png "워크플로우 실행")<br>
1. 좌측 목록의 `Simulation Job` 제목 우측에 위치하는 `->`아이콘을 클릭하면 상세 실행내역을 조회할 수 있습니다.
<br>![capture](/images/user/workflow/exe_11.png "워크플로우 실행")<br>

### Simulation Job 재실행

1. `Simulation Job` 실행이 완전히 종료된 후에 입력값을 수정하여 `Simulation Job`을 재실행(`Rerun`)할 수 있습니다.
<br>![capture](/images/user/workflow/exe_12.png "워크플로우 실행")<br>
1. `Simulation Job` 재실행 시 `Success` 상태인 사이언스 앱에 한해서 재실행하지 않고 `Reuse` 기능을 이용해 이전 `Simulation Job` 실행 결과를 유지할 수 있습니다.
1. `Simulation Job` 재실행 시 `Success` 상태인 사이언스 앱을 `우클릭`하여  `ReUse` 메뉴를 선택한 후 `Simulation Job`을 재실행하면, 해당 사이언스앱은 바로 `Success` 상태로 전환되며 이후 작업이 진행됩니다.
<br>![capture](/images/user/workflow/exe_14.png "워크플로우 실행")<br>
<br>![capture](/images/user/workflow/exe_13.png "워크플로우 실행")<br>

### Simulation Job Pause / Resume

1. `Simulation Job`은 실행 도중 일시 정지할 수 있으며, 전체 `Simulation Job` 또는 단일 `사이언스 앱` 단위로 `Pause`할 수 있습니다.
1. 이미 `Running` 중인 `사이언스 앱`은 `Pause`할 수 없으며, `Simulation Job`을 `Pause`한 경우 `Running` 상태인 사이언스 앱을 제외한 나머지가 일시정지 됩니다.
<br>![capture](/images/user/workflow/exe_15.png "워크플로우 실행")<br>
1. 또한 `Simulation Job` 또는 단일 `사이언스 앱` 단위로 `Resume`하여 실행을 이어갈 수 있습니다.
<br>![capture](/images/user/workflow/exe_16.png "워크플로우 실행")<br>

### Simulation Job Copy

1. `Simulation Job`의 입력값을 유지한 채 실행결과를 초기화한 상태로 `Simulation Job`을 `Copy`할 수 있습니다.
<br>![capture](/images/user/workflow/exe_17.png "워크플로우 실행")<br>
1. `Simulation Job`의 `Copy`는 `Simulation Job`실행이 종료되지 않은 상태에서도 가능합니다.

### 워크플로우 재편집

- 워크플로우는 [워크플로우 편집기](/workflow_workflow-designer.html) 에서 재편집할 수 있습니다.
- 재편집된 워크플로우는 새롭게 생성된 `Simulation Job` 부터 적용되며 이전 `Simulation Job`은 편집 전의 워크플로우로 유지 실행 됩니다.
<br>![capture](/images/user/workflow/exe_18.png "워크플로우 실행")<br>

### 워크플로우 Export

- 워크플로우는 워크플로우 엔진에서 바로 실행할 수 있는 형태의 `json` 파일로 `Export`할 수 있습니다.
<br>![capture](/images/user/workflow/exe_19.png "워크플로우 실행")<br>

<br><br><br>
