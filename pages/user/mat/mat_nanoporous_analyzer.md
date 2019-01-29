---
title: Nanoporous Analyzer
tags: []
keywords:
summary: ""
sidebar: mat_sidebar
permalink: mat_nanoporous_analyzer.html
folder: mat
---

## 개요

- `Nanoporous Analysis`는, 유사 구조 소재를 추천해주는 분석기로써, 특정 조건으로 유사한 소재끼리 그룹화하여 표현한 그래프입니다.
- 예를 들어, 나노전자소재의 구멍의 갯 수에 따른 그룹화한 구조를 확인할 수 있습니다.

## Nanoporous Analyzer

1. 메뉴의 `Analysis` - `Nanoporous Analyzer`를 클릭하여 이동합니다.

{% include image.html file="data/image00313.png" caption="소재 특화 사이트 Nanoporous Analyzer 메뉴" %}

## 화면 소개

1. `Dataset`의 `Id` 값으로 검색하여 해당 시뮬레이션 데이터에 포함된 `Structure` 파일의 구조가 포함된 클러스터의 위치를 확인할 수 있습니다.
1. `Structure` 파일을 직접 업로드하여 해당 파일과 유사한 구조가 포함된 클러스터의 위치를 확인할 수 있습니다.
1. 검색 유형과 값을 입력 후 `Search` 버튼을 클릭합니다.

{% include image.html file="data/image00314_0.png" caption="Dataset Id 검색" %}

> ### Structure 검색
> 검색창 좌측의 선택 창에서 `By Structure`를 선택합니다.
> {% include image.html file="data/image00314_1.png" caption="Structure 검색 : 검색 유형 선택" %}
> ‘파일 선택’ 버튼을 클릭 후 `Structure` 파일을 등록 후 `Submit` 버튼을 클릭합니다.
> {% include image.html file="data/image00314_2.png" caption="Structure 검색 : 파일 선택" %}

## 검색 결과 조회

1. `Material ID`나 Nanoporous `Structure` 구조파일을 업로드하여 프로그램이 실행되면, 아래와 같이 로딩 액션이 나타나는데, Structure 구조의 복잡도에 따라 수 초 ~ 수 분이 소요됩니다.
    {% include image.html file="data/image00315_0.png" caption="Dataset ID 검색 실행 로딩" %}
1. 프로그램 실행이 완료되면, 아래와 같이 해당 클러스터에 화살표 표시가 나타납니다.
    {% include image.html file="data/image00315_1.png" caption="Dataset ID 검색 완료" %}

## 검색 결과 상세 보기
    
1. Nanoporous Analyzer는 마우스로 줌, 아웃 등 시각적인 제어가 가능합니다.
    - 마우스 왼쪽 클릭 후 드레그 : 화면의 이동
    - 마우스 스크롤 : 줌 인/줌 아웃
    {% include image.html file="data/image00316_0.png" caption="Nanoporous Explorer" %}
1. 왼쪽 `CLUSTER DETAILS` 버튼을 클릭하면 아래와 같이 클러스터 상세 보기 창이 나타나며, 보고싶은 클러스터를 마우스 오버하면 해당 클러스터의 상세 정보를 확인할 수 있습니다.    
    {% include image.html file="data/image00316_1.png" caption="Cluster details" %}    
1. 왼쪽 `MAPPER SUMMARY` 버튼을 클릭하면 그래프에 대한 상세 정보를 확인할 수 있으며, 하단에 전체 클러스터의 색상별 분포도를 확인할 수 있습니다. 각각의 Structure에 대한 **탄소 흡착률에 따라 색상으로 구분**하는데, 왼쪽의 클러스터 상세 정보에서 마우스 오버한 해당 클러스터에 속한 멤버들에 대한 분포도를 확인할 수 있습니다. 
    {% include image.html file="data/image00316_2.png" caption="Mapper summary" %}
1. 이후, 마우스로 클러스터 상세 정보를 스크롤하여 각각의 멤버들의 정보를 확인할 수 있으며, 해당 멤버의 타이틀을 클릭하여 Nanoporous 소재 상세 정보 페이지로 이동이 가능합니다. 
    {% include image.html file="data/image00316_3.png" caption="Member 상세 보기" %}
1. Nanoporous 소재 상세 보기    
    {% include image.html file="data/image00318.png" caption="Nanoporous 소재 상세 보기" %}

## 기타 기능 소개

1. `FULLSCREEN` 버튼을 클릭하여 전체화면으로 좀 더 넓고 편하게 볼 수 있으며, `HELP` 버튼을 클릭하여 기타 정보를 확인할 수 있습니다.
    {% include image.html file="data/image00317_0.png" caption="Full screen" %}
1. `Print mode`, `Nodes glow`, `Tight layout` 이팩트 적용
    {% include image.html file="data/image00317_0.png" caption="Print mode" %}