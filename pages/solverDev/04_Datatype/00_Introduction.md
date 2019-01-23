---
title: Datatype
tags: 
keywords:
sidebar: solverdev_sidebar
permalink: solverdev_management_datatype.html
folder: solverDev
--- 


사이언스 앱에서 생성되는 다양한 데이터의 형태를 구분하는 요소입니다. 데이터 형태를 편집할 수 있는 편집기(Editor)와 분석할 수 있는 분석기(Analyzer)를 지정할 수 있으며, 앱을 등록하는 과정에서 입출력 포트를 생성하는 경우, 각 포트별로 데이터 타입을 지정해야 합니다.

{% include image.html file="solverdev/03/image01_app_component.png" caption="사이언스 앱 구성요소 (a) 해석기 (b) 데이터 타입" %}


> 예를 들어 흔히 사용하는 텍스트 파일을 하나의 데이터 타입으로 등록할 수 있습니다.
> 아래 그림은 편집기는 TEXT_EDITOR를 지정하고, 분석기는 OSPTextViewer로 설정한 ```text``` 데이터 타입을 조회한 결과 입니다.
>

{% include image.html file="solverdev/05/datatype1.png" caption="text 데이터 타입" %}


## Datatype 생성

My EDISON > Datatype 관리 > 추가를 통해 신규 Datatype을 생성할 수 있습니다.

{% include image.html file="solverdev/05/datatype_1.png" caption="Datatype 생성" %}

> 데이터 타입 생성전 검색을 통해 생성하고자 하는 데이터 타입을 찾아볼 수 있습니다.

(1) 데이터 타입의 이름을 작성합니다.

(2) 데이터 타입의 샘플 데이터 파일을 등록합니다.

(3) Editor, Analyzer 목록을 선택합니다.

(4) 데이터 타입을 저장합니다.
- Editor 목록의 SDE 항목이 클릭되지 않은 경우 (4)에 `저장`버튼이 나타납니다.
- Editor 목록의 SDE 항목을 클릭할 경우 (4)에 `다음`버튼이 나타나며 다음 과정을 진행합니다.

데이터 타입 생성은 데이터타입의 이름과 설명 그리고 사용하려고 하는 편집기(Editor)와 분석기(Analyzer)지정하여 생성할 수 있습니다. 여러개의 편집기와 분석기를 선택할 수 있으며, 기본 값을 지정해 주어야 합니다.

{% include image.html file="solverdev/05/datatype_2.png" caption="Datatype의 Editor 지정" %}

(5) SED의 경우 INPUTDECK 항목을 작성 및 수정할 수 있습니다.

(6) `View Structure` 버튼을 클릭하여 (7)화면과 같이 현재 INPUTDECK 구조를 확인할 수 있습니다.

(7) 현재 INPUTDECK 구조를 다운로드 받을 수 있으며, JSON 형식의 파일을 업로드하여 (5)의 데이터를 수정할 수 있습니다.
