---
title: 시뮬레이션 데이터 타입 관리
tags: []
keywords:
summary: ""
sidebar: datadev_sidebar
permalink: datadev_datatype_manage.html
folder: datadev
---

## 데이터 타입 검색


1. 메인 메뉴 `Data` - `Data Type`을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_01.png" %}

1. DataType 목록을 확인 할 수 있고 클릭하여 상세화면을 확인 할 수 있습니다.

    {% include image.html file="data/datadev_datatype_manage_02.png" %}

## 데이터 타입 등록

1. DataType의 목록에서 `Create` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_03.png" %}

1. 왼쪽의 대표이미지를 등록하기 위해 `select` 버튼을 클릭하여 이미지를 선택 합니다.

    {% include image.html file="data/datadev_datatype_manage_04.png" %}

1. `DataType`에 대한 정보(`DataType`, `Description`, `Curate Required`, `File Validation Rule`)를 입력 필드에 입력합니다.

    {% include image.html file="data/datadev_datatype_manage_05.png" %}

1. `Descriptive Metadata Schema` 항목에서 `add`, `remove` 버튼을 클릭하여 입력합니다. 또는 엑셀(xlsx)로 작성한 목록을 `import` 버튼을 클릭하여 입력 할 수 있습니다.

    {% include image.html file="data/datadev_datatype_manage_06.png" %}

1. `View` 항목은 View Designer로 해당 DataType에 등록된 View를 입력 할 수 있기 때문에 저장 후 수정 화면에서 등록 할 수 있습니다. 입력이 완료되면 `Save` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_07.png" %}

## 데이터 뷰 상세보기    

1. 목록에서 `DataType` 항목을 선택합니다.

    {% include image.html file="data/datadev_datatype_manage_02.png" %}

1. DataType의 상세 화면입니다. 상단에 대표 이미지와, Title, Description을 확인 할 수 있고 File Validation Rule, Descriptive Metadata Schema 를 확인할 수 있습니다. 

    {% include image.html file="data/datadev_datatype_manage_08.png" %}

1. 상세 화면의 하단 부분에 `Edit` 버튼을 클릭하여 DataType을 수정 할 수 있고, View 항목에서 `Preview`를 클릭하여 ViewDesigner에서 설정한 화면을 확인 할 수 있습니다.

    {% include image.html file="data/datadev_datatype_manage_09.png" %}

1. DataType 상세 화면에서 View 항목의 `Preview` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_10.png" %}

1. Preview 화면 상단의 Dataset 입력 필드의 `Select` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_11.png" %}
 
1. Dataset의 목록에서 Preview할 Dataset을 `Choose` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_12.png" %}

1. 선택된 Dataset에 설정된 View페이지의 Preview 화면을 확인 할 수 있습니다.

    {% include image.html file="data/datadev_datatype_manage_13.png" %}

## 데이터 뷰 등록

1. DataType 상세 화면에서 `Edit` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_14.png" %}

1. 수정할 DataType 정보를 입력하고 View 항목에서 `add` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_15.png" %}

1. View Designer에서 해당 DataType에 설정한 View 목록에서 `Choose` 버튼을 클릭 합니다.

    {% include image.html file="data/datadev_datatype_manage_16.png" %}

1. VIew를 여러개 등록시 화면에 보이는 탭의 순서를 변경 하려면 목록을 `Drag&Drop` 하여 조절 할 수 있습니다. 추가가 완료 되면 `Save` 버튼을 클릭합니다.

    {% include image.html file="data/datadev_datatype_manage_17.png" %}

## 데이터 큐레이션 모듈 등록

1. DataType의 Edit 페이지에서 처리 모듈을 등록할 수 있습니다. 처리 모듈을 등록하기 위해서는 먼저 DataType을 등록한 후에 Edit 페이지에서 처리 모듈을 등록해야 합니다. 이제 처리 모듈을 등록할 `DataType`을 목록에서 선택하여 상세 보기 페이지로 이동합니다.

    {% include image.html file="data/datadev_datatype_manage_18.png" %}

1. 상세 보기 페이지에서는 하단 `Edit` 버튼을 클릭하여 Edit 페이지로 이동합니다.

    {% include image.html file="data/datadev_datatype_manage_19.png" %}

1. Edit 페이지 하단의 Curation 항목에서 `Select` 버튼을 클릭하여 새로운 처리 모듈 팝업을 호출합니다.

    {% include image.html file="data/datadev_datatype_manage_20.png" %}

1. Curation Popup 팝업 페이지가 나타나면, 적용할 처리 모듈을 오른쪽 `Choose` 버튼을 클릭하여 선택합니다.

    {% include image.html file="data/datadev_datatype_manage_21.png" %}


1. 아래와 같이 선택한 처리 모듈이 등록된 것을 확인할 수 있습니다. 하단 `Save` 버튼을 클릭하여 설정을 완료합니다.

    {% include image.html file="data/datadev_datatype_manage_22.png" %}