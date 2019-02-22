---
title: 시뮬레이션 결과 데이터 조회
tags: []
keywords:
summary: ""
sidebar: user_sidebar
permalink: user_data_dataset.html
folder: user_data
---

## 데이터셋이란? 
시뮬레이션 결과 데이터는 EDISON 플랫폼에서 데이터셋(Dataset)이라는 개념으로 표현됩니다. 

데이터셋의 정의(개념)는 다음 링크를 참조하십시오. [링크](./user_data_intro.html)



## 데이터셋 상세보기
1. 메뉴의 `콘텐츠/데이터` - `데이터 탐색기`로 이동 합니다.
1. `Data Browser` 검색을 통해 원하는 컬렉션을 선택합니다.
1. 컬렉션 상세보기 화면에서 `Dataset 탭`을 선택하여 해당 컬렉션에 포함된 데이터셋들을 리스팅합니다. 
1. 원하는 데이터셋을 선택합니다. 이때 보여지는 화면은 아래와 같습니다. 


- `Information 탭` : 시뮬레이션 결과 데이터에 대한 요약정보와 가시화된 내용을 보여줍니다. 
   이 페이지는 기본적으로 `View Designer` 툴을 통해 솔버가 개발자가 생성하고 제공합니다. 솔버 개발자가 제공하지 않는 경우 이 탭은 존재하지 않습니다. 

    {% include image.html file="data/dataset/dataset_info.png" %}

- `File 탭` : 시뮬레이션 결과 데이터 파일들을 리스팅하고 다운로드 할 수 있습니다. 

    {% include image.html file="data/dataset/dataset_file.png" %}

- `Metadata 탭` : 서술형 메타데이터와, 생성이력 메타데이터를 볼수 있습니다. 

    {% include image.html file="data/dataset/dataset_metadata.png" %}

- `Comment 탭` : 별점과 게시된 사용자 의견을 보여줍니다.  



## 데이터셋 수정 
데이터셋에 대한 수정은 되도록이면 피할 것을 권장하며, 필요한 경우 제목(Title ) 등을 수정할 수 있습니다. 

1. 상기의 데이터셋 상세보기 페이지로 이동합니다. 
1. `Metadata 탭`을 선택합니다.
1. 맨 하단의 `Edit` 버튼을 선택합니다. 
1. 제목(title), 컬렉션(collection), Description(설명)을 수정한 후 하단의 `Save` 버튼을 누릅니다. 


## 데이터셋 삭제

데이터셋에 대한 삭제는 되도록 피할 것을 권장합니다.

데이터셋을 생성한 소유자만 삭제가 가능합니다. 

1. 상기의 데이터셋 상세보기 페이지로 이동합니다. 
1. `Metadata 탭`을 선택합니다.
1. 맨 하단의 `Delete` 버튼을 선택합니다. 