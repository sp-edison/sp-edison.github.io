---
title: Visualization Chart
tags: []
keywords:
summary: ""
sidebar: mat_sidebar
permalink: mat_analysis_vc.html
folder: mat
---

## 개요

- `Visualization Chart`는 연구자가 직접 파라미터로 x축, y축, z축을 구성하여 포털에 등록되어있는 시뮬레이션 데이터들의 상관성을 분석하는 툴입니다.
- 연구자들은 구축된 데이터에 대한 경향성을 분석하는 경우가 많은데, 이 툴을 사용하여 데이터 타입별로 제공하는 필드들을 구성하여 3D로 Floating한 차트를 구성하여 분석할 수 있습니다.

## Visualization Chart

1. 메뉴의 `Analysis` - `Visualization Chart` 혹은 도구 아이콘 `Visualization Chart`을 클릭하여 이동 합니다.

{% include image.html file="data/image00284.png" caption="소재 특화 사이트 Visualization Chart 메뉴" %}

## 화면 소개

1. Chart 왼쪽 차트구성 도구를 이용하여 시뮬레이션 데이터들의 상관성을 분석하겠습니다.
1. 먼저 `DataType`을 선택합니다. `DataType`을 선택하면 아래 `X`, `Y`, `Z` 축을 구성할 수 있는 변수들이 설정되는데, 이 때 설정되는 변수들은 선택한 타입에 따라 달라집니다.
1. `Activation`은 `Z`축을 구성하여 3D 차트로 나타낼지에 대한 옵션입니다.
1. `Max length`를 설정하여 최대 나타낼 시뮬레이션 데이터 점들의 수를 조정할 수 있습니다.
1. 구성정보를 모두 입력하였다면, `Make Chart`를 클릭하여 차트를 생성합니다. 

{% include image.html file="data/image00285_0.png" caption="차트 구성" %}

## 차트 구성 결과 조회

1. `Make Chart` 버튼을 클릭하여 차트 구성 도구로 아래와 같은 차트가 생성되었습니다.
    {% include image.html file="data/image00285_1.png" caption="차트 구성 결과" %}
1. 카테고리 변수를 클릭하여 특정 조건의 `카테고리` 레인지 검색으로 `필터링`이 가능합니다.
    {% include image.html file="data/image00285_2.png" caption="카테고리 필터링" %}
1. 차트는 `Make Chart` 버튼을 클릭하여 최대 3개까지 구성하여 비교 분석할 수 있습니다.
    {% include image.html file="data/image00285_3.png" %}
    {% include image.html file="data/image00285_4.png" %}
    {% include image.html file="data/image00285_5.png" caption="최대 3개 차트 구성 가능" %}