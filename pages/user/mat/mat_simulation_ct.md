---
title: Crystal Toolkit
tags: []
keywords:
summary: ""
sidebar: mat_sidebar
permalink: mat_simulation_ct.html
folder: mat
---

## 개요

- `Crystal Toolkit` 툴을 사용하면 소재 시뮬레이션 데이터셋 ID 또는 CIF 또는 POSCAR 파일 업로드를 통해 구조를 로드하고 원소를 대체하거나 제거하여 새로운 소재 구조를 생성 할 수 있습니다.
- 또한, 로드된 구조체의 수퍼셀 크기를 변경하기 위한 스케일링 행렬을 지정할 수도 있습니다.

## Crystal Toolkit

1. 메뉴의 `Analysis` - `Crystal Toolkit` 혹은 도구 아이콘 `Crystal Toolkit`을 클릭하여 이동 합니다.

{% include image.html file="data/image00266.png" caption="소재 특화 사이트 Crystal Toolkit 매뉴" %}

## 화면 소개

1. `Dataset`의 `Id` 값으로 검색하여 해당 시뮬레이션 데이터에 포함된 `Structure` 파일을 구조를 불러올 수 있습니다.
1. `Structure` 파일을 직접 업로드하여 해당 파일의 구조를 불러올 수도 있습니다.
1. 검색 유형과 값을 입력 후 `Search` 버튼을 클릭합니다.

{% include image.html file="data/image00267.png" caption="Dataset Id 검색" %}

> ### Structure 검색
> 검색창 좌측의 선택 창에서 `By Structure`를 선택합니다.
> {% include image.html file="data/image00268.png" caption="Structure 검색 : 검색 유형 선택" %}
> ‘파일 선택’ 버튼을 클릭 후 `Structure` 파일을 등록 후 `Submit` 버튼을 클릭합니다.
> {% include image.html file="data/image00269.png" caption="Structure 검색 : 파일 선택" %}

## 검색 결과 조회

1. `Material ID`나 `POSCAR` Structure 구조파일을 업로드하여 프로그램이 실행되면, 기본 `Supercell` 매트릭스 행렬과, `Substitute`의 기본 원소 정보, Crystal Data에 구조 정보, Lattice Parameters에 각각의 격자 상수와 각도, Final Structure에 각 원소의 점들에 대한 좌표값이 표시됩니다.

{% include image.html file="data/image00270_0.png" caption="Supercell Submit" %}

> ### 검색 결과 활용 하기
> ① 출력 결과 왼쪽 위의 수치를 변경한 후 `Supercell Submit` 버튼을 클릭하여 출력 결과를 변경할 수 있습니다.
> {% include image.html file="data/image00270.png" caption="Supercell Submit" %}
> ② 출력 결과 왼쪽의 `Substitute` 항목의 선택 창을 사용하여 원소를 변경하거나 삭제 할 수 있습니다.
> {% include image.html file="data/image00271.png" caption="Substitute Submit" %}
> ③ 출력 결과 오른쪽측의 `Structure Download`선택 창의 확장자를 선택하여 파일을 다운로드 할 수 있습니다.
> {% include image.html file="data/image00272.png" caption="Structure Download" %}
> ④ 출력 결과 오른쪽의 Simulation `Run` 버튼을 클릭하여 EDISON 시스템과 연계하여 시뮬레이션을 재 실행할 수 있습니다.
> {% include image.html file="data/image00273.png" caption="Simulation Run" %}
> {% include image.html file="data/image00274.png" caption="시뮬레이션 재실행 파라미터 설정" %}
 

