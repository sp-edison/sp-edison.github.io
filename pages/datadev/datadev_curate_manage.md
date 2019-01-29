---
title: 데이터 큐레이션 모듈 관리
tags: []
keywords:
summary: ""
sidebar: datadev_sidebar
permalink: datadev_curate_manage.html
folder: datadev
---

## 데이터 큐레이션 모듈 관리

1. 사이트 상단의 `Tool` - `Curation Manager`로 이동합니다. 

    {% include image.html file="data/image00144.png" %}




## 큐레이션 모듈 검색
1. 검색창에 검색할 내용을 입력한 후 `Search` 버튼을 클릭합니다. 
    {% include image.html file="data/image00145.png" %}
2. 데이터가 있는 경우 아래와 같이 검색 결과가 나타납니다.
    {% include image.html file="data/image00146.png" %}


## 큐레이션 모듈 상세보기
1. 목록에서 상세보기 할 큐레이션의 `Title`을 클릭합니다.
    {% include image.html file="data/image00147.png" %}
- `simple` Type 상세화면 : Title, Curation Type, Data Type, SubCurationModule, Description 항목으로 구성됩니다.
    {% include image.html file="data/datadev_curate_manage_04.png" %}
- `container` Type 상세화면 : Title, Curation Type, Data Type, Image, argument, Description 항목으로 구성됩니다.
    {% include image.html file="data/datadev_curate_manage_12.png" %}
- `compostion` Type 상세화면: Title, Curation Type, Data Type, SubCurationModule, Description 항목으로 구성됩니다.
    {% include image.html file="data/datadev_curate_manage_03.png" %}



## 큐레이션 모듈 수정 및 삭제
- 큐레이션 모듈 상세 페이지 하단의 `Edit` 버튼을 클릭 합니다.
    {% include image.html file="data/image00160.png" %}
### 1. SIMPLE Type 수정
1. SIMPLE 모듈 정보 수정 후 입력 양식 하단의 `Save`버튼을 클릭 합니다.
2. 저장 후 `Validate`, `TEST`버튼을 이용하여 오류 여부를 확인할 수 있습니다.
    {% include image.html file="data/datadev_curate_manage_05.png" %}
3. 아래 화면은 `Validate`버튼을 이용하여 검증 후 성공 시 라인번호가 초록색으로 변경 됩니다.
    {% include image.html file="data/image00162.png" %}
4. 아래 화면은 `Validate`버튼을 이용하여 검증 후 실패시 라인번호 빨간색으로 표기되며 오류 내용을 툴팁에서 확인할 수 있습니다.(검증 실패시 `TEST` 버튼을 이용한 시험은 진행할 수 없습니다.)
    {% include image.html file="data/image00163.png" %}
5. 아래 화면은 `TEST` 버튼을 클릭하여 TEST할 시뮬레이션 데이터를 선택할 수 있는 Dataset Popup 페이지가 나타납니다. 우측 Choose 버튼을 클릭하여 선택합니다.
    {% include image.html file="data/image00180.png" %}
6. 선택한 시뮬레이션 데이터로 TEST를 진행하며, 성공이나 실패 시에 아래와 같은 Success/Error Dialog 창이 나타납니다.
    {% include image.html file="data/image00181.png" caption="SUCCESS" %}
    {% include image.html file="data/image00174.png" caption="FAILS" %}
7. TEST 후 아래와 같은 ViewMetadata Popup 창이 나타나고, 성공 시 처리된 데이터들을 더블클릭하여 다운로드한 후에 파일을 열어서 데이터를 확인할 수 있습니다.
    {% include image.html file="data/image00183.png" %}
8. dm.json 파일을 내려받아 열어보면 아래와 같은 데이터를 확인할 수 있습니다.
    {% include image.html file="data/image00184.png" %}
9. 결과 팝업의 DescriptiveMetadata 항목과 같은 데이터임을 확인할 수 있습니다.
10. TEST 실패 시에 아래와 같은 ViewMetadata Popup 창이 나타나고, error.log를 더블클릭하여 다운로드한 후에 파일을 열어서 Error 로그를 확인할 수 있습니다.
    {% include image.html file="data/image00175.png" %}
11. 아래와 같이 Error 로그를 확인할 수 있습니다.
    {% include image.html file="data/datadev_curate_manage_15.png" %}

### 2. CONTAINER Type 수정
1. CONTAINER은 docker Image 명과 Agrgument등을 수정 후 하단의 `Save`버튼을 클릭 합니다.
    {% include image.html file="data/datadev_curate_manage_13.png" %}
2. 아래 화면은 수정 화면 하단의  `Validate` 버튼을 이용하여 검증 후 성공이나 실패 시에 아래와 같은 Success/Error Dialog 창이 나타납니다.
    {% include image.html file="data/image00181.png" caption="SUCCESS" %}
    {% include image.html file="data/datadev_curate_manage_06.png" caption="FAILS" %}
3. `TEST` 버튼을 클릭하면, TEST할 시뮬레이션 데이터를 선택할 수 있는 Dataset Popup 페이지가 나타납니다. 우측 Choose 버튼을 클릭하여 선택합니다.
    {% include image.html file="data/image00180.png" %}
4. 선택한 시뮬레이션 데이터로 TEST를 진행하며, 성공이나 실패 시에 아래와 같은 Success/Error Dialog 창이 나타납니다.
    {% include image.html file="data/image00181.png" caption="SUCCESS" %}
    {% include image.html file="data/image00174.png" caption="FAILS" %}
5. TEST 후 아래와 같은 ViewMetadata Popup 창이 나타나고, 성공 시 처리된 데이터들을 더블클릭하여 다운로드한 후에 파일을 열어서 데이터를 확인할 수 있습니다.
    {% include image.html file="data/image00183.png" %}
6. dm.json 파일을 내려받아 열어보면 아래와 같은 데이터를 확인할 수 있습니다.
    {% include image.html file="data/image00184.png" %}
7. 결과 팝업의 DescriptiveMetadata 항목과 같은 데이터임을 확인할 수 있습니다.
8. TEST 실패 시에 아래와 같은 ViewMetadata Popup 창이 나타나고, error.log를 더블클릭하여 다운로드한 후에 파일을 열어서 Error 로그를 확인할 수 있습니다.
    {% include image.html file="data/image00175.png" %}
9. 아래와 같이 Error 로그를 확인할 수 있습니다.
    {% include image.html file="data/image00176.png" %}

### 3. COMPOSTION Type 수정
1. COMPOSITION은 기존 큐레이션 모듈을 재 선택 및 삭제 후 하단의 `Save`버튼을 클릭 합니다.
    {% include image.html file="data/datadev_curate_manage_14.png" %}
2. `TEST` 버튼을 클릭하면, TEST할 시뮬레이션 데이터를 선택할 수 있는 Dataset Popup 페이지가 나타납니다. 우측 Choose 버튼을 클릭하여 선택합니다.
    {% include image.html file="data/image00180.png" %}
3. 선택한 시뮬레이션 데이터로 TEST를 진행하며, 성공이나 실패 시에 아래와 같은 Success/Error Dialog 창이 나타납니다.
    {% include image.html file="data/image00181.png" caption="SUCCESS" %}
    {% include image.html file="data/image00174.png" caption="FAILS" %}
4. TEST 후 아래와 같은 ViewMetadata Popup 창이 나타나고, 성공 시 처리된 데이터들을 더블클릭하여 다운로드한 후에 파일을 열어서 데이터를 확인할 수 있습니다.
    {% include image.html file="data/image00183.png" %}
5. dm.json 파일을 내려받아 열어보면 아래와 같은 데이터를 확인할 수 있습니다.
    {% include image.html file="data/image00184.png" %}
6. 결과 팝업의 DescriptiveMetadata 항목과 같은 데이터임을 확인할 수 있습니다.
7. TEST 실패 시에 아래와 같은 ViewMetadata Popup 창이 나타나고, error.log를 더블클릭하여 다운로드한 후에 파일을 열어서 Error 로그를 확인할 수 있습니다.
    {% include image.html file="data/image00175.png" %}
8. 아래와 같이 Error 로그를 확인할 수 있습니다.
    {% include image.html file="data/datadev_curate_manage_16.png" %}

### 큐레이션 모듈 삭제
1. 큐레이션 모듈 상세 또는 수정 페이지 하단의 `Delete`버튼을 클릭 합니다.
    {% include image.html file="data/datadev_curate_manage_17.png" %}