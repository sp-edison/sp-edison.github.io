---
title: Material Explorer
permalink: mat_search_explorer.html
sidebar: mat_sidebar
categories: materials
tags: []
keywords:
folder: mat
summary: ""
---

## 개요
 - Material Explorer는 연구자들이 관심있는 소재 시뮬레이션 데이터를 포털에서 쉽게 찾을 수 있도록 특화된 검색 도구 입니다. 주기율표를 모티브로 한 원소 기호 검색에서부터 화학식 검색, 그리고 사용자 입력 구조 파일 검색 등의 다양한 검색 방식을 지원합니다.

## Material Explorer
 - `Home` 또는 `Analysis`의 - `Material Explorer` 를 클릭하여 이동합니다.

    {% include image.html file="data/mat_search_explorer_01.png" caption="Materials Explorer" %}

## 검색 방식 설정
 - 원소 기호 검색
 `by Element` 검색 방식을 선택한 후 원하는 원소들을 아래 주기율표에서 선택한 후 `Search` 버튼을 클릭합니다.

    {% include image.html file="data/mat_search_explorer_02.png" caption="Elements 검색의 예"%}

 - 화학식 검색
 `by Formula` 검색 방식을 선택한 후 원하는 화학식을 검색창에 입력합니다. `[Hill System](https://en.wikipedia.org/wiki/Chemical_formula#Hill_system)`을 따르는 `Reduced Formula` 형태의 검색문을 사용합니다.

 - 구조 검색
  `by Structure` 검색 방식을 선택한 후 사용자가 직접 `POSCAR` 데이터 타입의 구조 파일을 업로드하여 검색할 수 있습니다.

## 검색 결과 조회

 - 검색 결과는 주기율표 아래에 생성됩니다. 또한 우측 상단의 `Periodic Table Close` 버튼을 활용하여 검색 결과를 한눈에 확인할 수 있습니다. 상단의 `density`, `# of Elements`, `Bandgap`, `Volume` 로 구성된 패싯 사이드바(Facet Sidebar)를 활용하여 구체화된 세부 검색을 수행할 수 있습니다.
 {% include image.html file="data/mat_search_explorer_03.png" caption="검색 결과" %}