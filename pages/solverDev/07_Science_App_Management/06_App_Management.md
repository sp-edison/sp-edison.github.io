---
title: 사이언스 앱 관리하기
tags: 
keywords:
sidebar: solverdev_sidebar
permalink: solverdev_management_app_management.html
folder: solverDev
--- 

자신이 등록한 사이언스 앱은 My EDISON > 사이언스 앱 에서 관리할 수 있습니다. 소유 앱과 관리 앱을 분류하여 조회할 수 있으며, 탭을 통해 목록을 조회할 수 있습니다. 앱의 상태는 작성중, 서비스요청, 공개, 비공개 4단계로 나누어지며,

{% include image.html file="solverdev/08/management.png" %}

앱 검색이 필요한 경우 Filter 버튼을 클릭하고, 검색하고자 하는 내용을 입력하거나 리스트를 선택하면 됩니다.

{% include image.html file="solverdev/08/management2.png" %}


### 앱 업그레이드

공개된 앱의 경우 앱 상세보기 페이지로 이동하면, 앱을 업그래이드 하거나 비공개로 전환할 수 있습니다. 
{% include image.html file="solverdev/08/app_upgrade.png" %}
- (1) 업그레이드를 클릭하면 아래와 같은 팝업이 나타납니다.
- (2) 업그레이드 항목을 선택합니다.
|항목|설명|
|--|--|
|Release|컨텐츠 추가 또는 주요 기능의 추가, 변경 시 선택|
|Major|간단한 기능의 추가, 변경 시 선택|
|Minor|버그 수정 등 간단한 변경 시 선택|
- (3) 업그레이드할 버전을 작성한 후 `UPGRADE` 버튼을 클릭합니다.
  * 업그레이드를 클릭하면 현재 버전의 앱 관리 정보는 비공개로 변경되며, 생성된 앱 관리 정보는 실행 파일 정보를 제외한 나머지 정보가 기존 버전과 동일합니다. 

