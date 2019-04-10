---
title: 사용자 데이터셋을 이용하여 기계학습 모델 만들기
tags: []
keywords:
summary: ""
sidebar: ai_sidebar
permalink: ai_analysis_newdata.html
folder: ai
---

## 개요
 - `Upload new data and Analyze`는 사용자 데이터를 바탕으로 기계학습 모델을 생성해 볼 수 있는 손쉬운 인터페이스를 제공합니다.
 - 데이터 업로드 및 자동화된 메타데이터 파싱 과정을 제외하면 `Easy Analysis`와 기본적인 구조가 동일하게 구성되어 있습니다.

## Upload new data and Analyze   
 - `Analysis`의 - `Upload new data and Analyze` 를 클릭하여 이동합니다.  
   {% include image.html file="data/ai_analysis_newdata_01.png" caption="Upload new data and Analyze" %}
 
 - 이 사이트는 CSV 포멧의 데이터 파일을 지원합니다.
 - `Access level`을 `Public`으로 설정하면 해당 데이터셋이 자동으로 플랫폼에 등록되어 다른 사용자들이 검색 및 활용할 수 있습니다.
 - `License`는 `CC BY`, `CC BY-NC`, `CC BY-NC-SA`, `CC BY-ND`, `CC BY-SA` 중 선택할 수 있습니다.
 - `CSV delimete`는 업로드 될 CSV 파일의 구분자를 선택하는 옵션입니다. `Auto`, `Comma`, `Tab`, `Pipe` 형태의 구분자를 지원합니다.
 - `Keyword` 입력은 `Comma(,)`, 또는 `Tab`키를 이용하여 추가할 수 있습니다.
 - `파일 선택` 항목을 클릭하여 업로드할 CSV 파일을 선택합니다
 - 모든 과정이 마무리되면 `Save`버튼을 눌러 플랫폼에 데이터셋을 등록하고 `Next` 버튼을 눌러 다음 과정으로 넘어갑니다.

    {% include image.html file="data/ai_analysis_newdata_02.png" caption="File Upload" %}

 - 각 컬럼의 샘플 데이터 확인 및 `DataType`을 확인합니다. `Category`형 데이터일 경우 체크해두어야 범주화인코딩 코드가 자동으로 생성됩니다.
 - `Next`를 눌러 다음 과정으로 진행합니다.
    {% include image.html file="data/ai_analysis_newdata_03.png" caption="Datatype Selection" %}

 - 이후의 프로그래밍 코드 생성 순서는 `Easy Analysis`와 동일합니다. (1) 레이블 선택, (2) 알고리즘 선택, (3) 코드 미리보기 및 사용자 개발 환경 구동의 순서로 진행됩니다.