---
title: Material Data View
tags: []
keywords:
summary: ""
sidebar: mat_sidebar
permalink: mat_search_view.html
folder: mat
categories: materials
---

## 개요
 - Material Data View는 `Data` - `Data Browse`, `Data Search`, `Advanced Search` 데이터 검색 또는 `Analysis` - `Material Explorer` 검색 도구를 활용하여 검색된 소재 데이터를 표현하는 뷰 페이지 입니다.

## 다양한 검색 방법을 지원하는 Material Data View


### Data Browse

 - 먼저 `Data` 탭의 - `Data Browse` 메뉴를 선택하면 다음과 같은 타일 형태의 소재 데이터 컬렉션들을 확인할 수 있습니다. 컬렉션 썸네일 이미지, 이름, 키워드 등을 통해 대략적인 내용을 한눈에 파악할 수 있습니다.
 
 - 우측 하단의 `Create` 버튼을 클릭하여 플랫폼에 또 다른 컬렉션을 업로드하고 등록할 수 있습니다.

    {% include image.html file="data/mat_search_view_01.png" caption="Tile 형태의 Data Collection" %}

 - 컬렉션을 선택하면 컬렉션 뷰 페이지로 이동합니다. 데이터 컬렉션은 `Info`, `Dataset`, `Paper`, `Detail`, `Comment` 총 다섯개의 탭으로 구성됩니다.
    {% include image.html file="data/mat_search_view_02.png" caption="OQMD Data Collection - Info." %}
    {% include image.html file="data/mat_search_view_03.png" caption="OQMD Data Collection - Dataset" %} 
    {% include image.html file="data/mat_search_view_04.png" caption="OQMD Data Collection - Paper" %} 
 
 - `Detail` 탭에서 해당 컬렉션의 Access Control 및 컬렉션 수정 및 삭제가 가능합니다.
   {% include image.html file="data/mat_search_view_05.png" caption="OQMD Data Collection - Detail" %}

 
 - `Dataset` 탭에서 특정 데이터셋을 선택하면 다음과 같이 해당 소재의 주요 메타데이터를 표현하는 뷰 페이지를 확인할 수 있습니다.
 - 소재 뷰는 `Material Information`, `File`, `Metadata`, `Comments` 탭으로 구성되어 있습니다. `Material Information` 탭에서는 해당 소재의 조성, 에너지, 질량 등의 기초적인 물성 데이터 뿐 아니라 해당 유닛 셀 내의 원자의 위치 정보 등을 확인할 수 있으며 JSmol 컴포넌트를 이용한 실시간 웹 시각화 기능을 지원합니다. 이와 같은 데이터 표현 뷰 페이지는 플랫폼 내의 `View Designer` 를 활용하여 연구자가 직접 구성할 수 있습니다.
   {% include image.html file="data/mat_search_view_06.png" caption="Material Information 뷰 예제 - As2WO 데이터셋" %}
 
 - `File` 탭을 클릭하여 해당 데이터셋의 시뮬레이션 결과 및 메타데이터들을 다운로드하여 열람할 수 있습니다. 또한 `Metadata` 탭을 클릭하여 `DescriptiveMetadata`를 확인하고 해당 데이터셋의 수정 및 삭제 기능을 수행할 수 있습니다.
   {% include image.html file="data/mat_search_view_10.png" caption="File 뷰 예제 - As2WO 데이터셋" %}


### Data Search
 - `Data` - `Data Search`를 통한 데이터 검색은 아래 예제와 같이 좌측에 패싯 검색을 지원하며 해당하는 컬렉션의 리스트를 우측에 보여줍니다.
   {% include image.html file="data/mat_search_view_07.png" caption="Data Search" %}

 - `Title`, `ID`, `Description`, `Title+Description` 을 통한 통합 검색이 지원됩니다.   
   {% include image.html file="data/mat_search_view_08.png" caption="통합 검색 지원" %}


### Advanced Search
 - `Data` - `Advanced Search`를 사용한 `Lucene Query` 형태의 질의를 통해 보다 세밀한 타입의 데이터들을 검색할 수 있습니다.
   {% include image.html file="data/mat_search_view_09.png" caption="Advanced Search를 통한 전문 검색 지원" %}


