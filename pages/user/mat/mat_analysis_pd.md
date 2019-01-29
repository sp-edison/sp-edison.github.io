---
title: Phase Diagram
tags: []
keywords:
summary: ""
sidebar: mat_sidebar
permalink: mat_analysis_pd.html
folder: mat
---

## 개요

- `Phase Diagram`은 Multicomponent system의 열역학적 상 평형도를 나타내며, 재료의 가공 및 반응과 관련한 기본 소재 측면에 대하여 유용하게 분석할 수 있는 툴입니다.
- 선택한 원소들이 포함된 모든 소재들을 한 눈에 볼 수 있으며, 각 소재들의 상관관계와 안정성 등을 살펴 볼 수 있습니다.

## Phase Diagram

1. 메뉴의 `Analysis` - `Phase Diagram` 혹은 도구 아이콘 `Phase Diagram`을 클릭하여 이동 합니다.

{% include image.html file="data/image00275.png" caption="소재 특화 사이트 Phase Diagram 메뉴" %}

## 원소기호 조합

1. 주기율표에서 원소 기호를 선택하여 조합합니다. 

{% include image.html file="data/image00276.png" caption="주기율표 소개" %}

> 입력 창 오른쪽의 ‘Reset’ 버튼을 통해 이전 검색 결과를 초기화할 수 있습니다.
> {% include image.html file="data/image00277.png" caption="선택한 원소기호 초기화" %}

## 분석 결과 조회

1. `Search` 버튼을 클릭합니다. (원소 기호는 최소 2개 이상 선택해야 합니다.)

{% include image.html file="data/image00278.png" caption="Phase Diagram 검색" %}

> 분석 결과 조회 후 오른쪽의 `Periodic Table Close` 버튼을 클릭하여 주기율표를 숨길 수 있습니다.
> {% include image.html file="data/image00279.png" caption="주기율표 보이기/감추기" %}

## 분석 결과 보기

1. 선택한 원소의 조합으로 데이터베이스에 등록된 시뮬레이션 데이터들의 상관관계가 나타납니다.
1. 분석 결과 오른쪽 목차에서 `Id`를 클릭하여 해당 시뮬레이션 데이터의 상세 정보를 조회할 수 있습니다.

{% include image.html file="data/image00280.png" caption="시뮬레이션 데이터 상관관계 분석" %}

> 조회 결과 우측의 `Compounds` 하단의 `stable’, `Unstable` 탭을 클릭하여 해당 목차를 확인 할 수 있습니다.
> {% include image.html file="data/image00281.png" caption="Compounds stable/Unstable 전환" %}