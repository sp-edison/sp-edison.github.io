---
title: 내 시뮬레이션 결과 공유
tags: [EDISON-Data, Platform, Upload]
keywords:
summary: "실행한 시뮬레이션 결과물들을 EDISON-Data 플랫폼에 영구 저장합니다. "
sidebar: user_sidebar
permalink: user_data_share.html
folder: user_data
---
## 시뮬레이션 결과 공유
데이터 업로드는 `저장할 시뮬레이션 선택 → Collection 생성 및 선택 → 업로드` 순서로 진행됩니다. 데이터를 올려주실 때에는 각 `경진대회 팀`마다, 혹은 각 `주제`마다 Collection을 하나씩 생성하시고, 해당 Collection에 시뮬레이션 데이터를 업로드해주시면 됩니다. 현재는 EDISON 포털에 등록된 솔버를 사용해서 시뮬레이션을 실행한 경우에만 데이터 플랫폼에 저장이 가능합니다.

- EDISON 로그인 후, 메뉴의 `My EDISON` 탭으로 이동합니다.
- 좌측의 `시뮬레이션 파일` 탭에서 저장을 원하는 시뮬레이션(Simulation) 혹은 잡(Job)을 선택합니다.
```
※ 시뮬레이션 실행 시 설정했던 [시뮬레이션 명- 잡 명]이 Dataset 이름으로 자동 저장되기 때문에, 시뮬레이션과 잡 이름을 다른 것들과 구분할 수 있는 의미 있는 값 (예, 시뮬레이션 주제, 파라미터 값)으로 변경해주시길 바랍니다. 시뮬레이션과 잡 이름은 워크벤치 (Workbench)에서 변경이 가능합니다.
```
- 저장할 시뮬레이션 혹은 잡을 선택 후, `Register & Share Data` 버튼을 누르면 저장할 Collection을 선택하라는 팝업이 뜹니다.
```
※ Simulation 목록에서 ‘Register & Share Data’ 버튼을 누르면 Simulation 하위의 성공적으로 종료된 모든 Job 들이 저장의 대상이 됩니다. 그리고 Job 목록에서 ‘Register & Share Data’ 버튼을 누르면 개별 Job이 저장의 대상이 됩니다.
```

{% include image.html file="data/user_data_share_01.png" caption="Save process" %}

- 최초 업로드 시, Collection을 생성하여야 하고 방법은 다음 그림과 같습니다.
```
※ Collection 명은 `논문 이름` 혹은 `주제 이름`으로 해주시면 되고, Community 명은 각 전문센터 커뮤니티로 선택해주시면 됩니다.
- 전산열유체 → CFD
- 구조동역학 → CSD
- 계산화학 → CHEM
- 나노물리 → NANO
- 전산의학 → CMED
- 전산설계 → DESIGN
- 도시환경 → UE
```
{% include image.html file="data/user_data_share_02.png" caption="Collection popup" %}
{% include image.html file="data/user_data_share_03.png" caption="Collection detail info" %}

- Collection 생성을 완료하고, 해당 Collection의 `Choose` 버튼을 누르면 저장이 진행됩니다. 성공적으로 저장이 완료되면 다음 그림과 같은 메시지가 뜰 것입니다.

{% include image.html file="data/user_data_share_04.png" caption="Save success" %}

- 이후의 업로드는 저장을 원하는 Simulation, Job에 대해서 `Register & Share Data` 버튼을 누르고 저장을 원하는 Collection의 `Choose` 버튼을 눌러 저장해주시면 됩니다.


## 제출된 데이터 상태 보기
데이터 업로드 작업 중 혹은 작업이 끝난 후, 제대로 저장이 되었는지 확인할 수 있는 페이지입니다. 다음 그림과 같이, `콘텐츠/데이터` 메뉴에서 `데이터 관리` 메뉴를 선택하시면 자신이 생성한 Collection과 성공, 실패, 대기 중인 Dataset의 개수를 확인할 수 있습니다. `Manage` 버튼을 누르면 각 Dataset의 상태를 개별적으로 확인하실 수 있습니다.

{% include image.html file="data/user_data_share_05.png" caption="Data Management" %}
{% include image.html file="data/user_data_share_06.png" caption="Dataset Detail" %}

## Collection 썸네일 이미지 등록
해당 Collection을 대표할 수 있는 썸네일 이미지를 등록합니다. 다음 그림과 같이 Collection 페이지에서 `Detail` 탭으로 이동합니다. `Edit` 버튼을 누르면 대표 이미지를 업로드할 수 있는 페이지로 이동합니다. 여기서 대표 이미지를 업로드해주시고 `Save` 버튼을 통해 저장해주시기 바랍니다.

{% include image.html file="data/user_data_share_07.png" caption="Move to detail tab" %}
{% include image.html file="data/user_data_share_08.png" caption="Thumbnail upload" %}

## Colection 논문 등록
저장한 시뮬레이션 결과들로부터 도출된 논문이 있다면 해당 논문을 등록합니다. 논문은 `PDF` 형식만 업로드 가능합니다. 논문 등록 절차는 다음 그림과 같이 Collection 페이지에서 `Paper` 탭으로 이동한 후 `Edit Paper` 버튼을 누르고 `파일 선택` 버튼을 눌러 논문을 선택합니다. 논문이 선택되면 `Upload Paper` 버튼을 눌러 논문을 업로드합니다.

{% include image.html file="data/user_data_share_09.png" caption="Paper upload" %}

## Collection 설명 페이지 등록
Collection은 어떤 주제에 대한 시뮬레이션들의 집합체를 의미합니다. 따라서 시뮬레이션들이 어떤 문제를 해결하고자 하였는지에 대한 설명이 Collection 메인 페이지에 나와 있었으면 합니다. 예를 들면, 경진대회에 제출한 논문의 내용을 적어주셔도 됩니다. 그럼 Collection을 디자인하는 방법에 대해서 설명드리겠습니다.
- `데이터 관리` 메뉴에서 생성한 Collection의 `Title을 클릭`하면 생성한 Collection 페이지로 이동합니다. 해당 페이지에서 `Info` 탭으로 이동하면 Collection을 처음 생성했기 때문에 빈 페이지일 것입니다. 여기서 `Edit Description` 버튼을 눌러 수정 페이지로 이동합니다.

{% include image.html file="data/user_data_share_10.png" caption="Move to Info tab" %}

- 수정 페이지로 이동한 후, 다음 그림과 같이 페이지를 꾸며주시면 됩니다. 일반적인 문서 작업처럼 텍스트, 이미지, 테이블, 링크 등을 활용하실 수 있습니다. 그리고 페이지 작성 중 틈틈이 저장하시기를 추천드립니다.

{% include image.html file="data/user_data_share_11.png" caption="Collection design" %}
