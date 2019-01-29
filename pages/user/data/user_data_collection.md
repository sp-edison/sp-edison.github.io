---
title: 데이터 컬렉션 관리
tags: []
keywords:
summary: ""
sidebar: user_sidebar
permalink: user_data_collection.html
folder: user_data
---


## 기본 개념

관련된 개념들은 다음 링크를 참조하십시오. [링크](./user_data_intro.html)

<br>
## Collection 상세보기

### Collection 리스트

컬렉션 내용의 상세보기를 위해서는 Collection Browser를 통해 리스팅되는 컬렉션들 중 하나를 선택합니다. 

컬렉션 상세보기 창에서 보여주는 주요 탭들은 다음과 같습니다. 

- `Info 탭` : 컬렉션 데이터들을 설명하는 웹페이지입니다. 
- `Dataset 탭` : 컬렉션에 포함된 데이터셋(dataset)들을 리스트합니다. 
- `Paper 탭` : 컬력션과 관련된 대표 논문을 보여줍니다. 
- `Detail 탭` : 컬렉션 관리를 위한 상세정보를 보여줍니다. 키워드, 소유자, 라이선스, 생성일, 접근제어권한 등
- `Comment 탭` : 별점과 게시된 사용자 의견을 보여줍니다.  


{% include image.html file="data/data_search/collection_detail.png" %}

<br>

### Collection 접근제어

컬렉션 상세보기 `Detail 탭`에서 볼 수 있는 Permission은 이 컬렉션에 대한 접근제어 권한을 나타냅니다. 

컬렉션에 대한 접근제어 권한은 컬렉션에 포함된 데이터셋들에게도 적용됩니다. 

{% include image.html file="data/data_search/collection_ac.png" %}

<br>

컬렉션 접근의 주체는 다음과 같이 구분됩니다. 

- `Allowed User` : `Detail` 창에서 설정할 수 있는 소유자와 거의 유사한 권한을 갖는 사용자를 말합니다. 
- `Community Member` : 같은 커뮤니티에 소속된 사용자를 말합니다. 
- `non-Community Member` : 계정을 갖는 모든 사용자를 말합니다.
- `Guest` : 로그인하지 않은 사용자를 말합니다. 

<br>

컬렉션 접근 권한은 다음과 같이 구분되며, 아래로 갈수로 강한 권한입니다. 

- `Null` : 아무런 권한이 없음
- `Read Collection` : 해당 컬렉션과 데이터셋들을 읽고 접근할 수 있음
- `Create Dataset` : 해당 컬렉션에 데이터셋을 생성할 수 있음
- `Update Dataset` : 해당 컬렉션의 내용을 수정할 수 있음
- `Delete Collection` : 해당 컬렉션을 삭제할 수 있음

컬렉션이 신규 생성되었을 때의 기본적인 권한은 모든 사용자들이 읽거나 접근할 수 있으며, `Allowed User`와 생성한 본인만 내용을 수정할 수 있습니다. `Allowed User`는 해당 컬렉션의 `Detail 탭`에서 설정 가능합니다. 

<br>

## Collection 생성
새로운 컬렉션을 생성하기 위해서는 Collection Browser 맨 밑의 `Create` 버튼을 선택합니다.  
컬렉션 생성에 필요한 정보는 아래와 같습니다. 

- `Title` : 컬렉션 제목 
- `Community` : 컬렉션의 소속 커뮤니티; CEM(구조동역학) ,CFD(전산열유체), CHEM(계산화학), CMED(전산의학), CSE(), DESIGN(전산설계), MQCP(전파위성), NANO(나노물리), UE(도시환경), GUEST(구분없음)
- `Keyword` : 키워드
- `Description` : 컬렉션 설명

`Title`과 `Community`는 필수 입력값입니다.

상기 항목들을 입력한 이후에 하단의 `Save` 버튼을 선택합니다. 

{% include image.html file="data/data_search/collection_create.png" %}



<br>

## Collection 수정
### Collection Thumbnail 수정
Collection의 Thumbnail은 Collection Browser에서 보이는 이미지를 말합니다. 

컬렉션을 생성한 이후 데이터를 대표하는 Thumbnail 이미지를 넣는 것을 권장합니다. 

Thumbnail 생성/수정은 컬렉션을 생성한 본인만 가능하며, 과정은 다음과 같습니다. 
1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Detail 탭`으로 이동합니다. 
1. 맨 하단의 `Edit` 버튼을 선택합니다. 
1. 아래 그림의 Thumbnail 이미지 `Select` 버튼을 누른 후 원하는 이미지를 선택합니다. 
   이미지의 크기는 50k 미만, 크기는 200X150을 권장합니다. 
1. 그리고 맨 밑의 `Save`를 선택하여 수정을 완료합니다. 

{% include image.html file="data/data_search/collection_edit_thumbnail.png" %}

<br>

### Collection Paper 수정
Collection의 Paper는 Collection에 포함된 데이터들을 활용하여 도출된 대표논문을 말합니다. 

컬렉션을 생성한 이후 데이터의 내용을 보다 잘 설명할 수 있는 논문을 입력하는 것을 권장합니다. 

1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Paper 탭`으로 이동합니다. 
1. 맨 하단의 `Edit Paper` 버튼을 누른 후 업로드 할 논문을 선택합니다. 
1. 그리고 맨 밑의 `Save`를 선택하여 수정을 완료합니다. 

<br>

### Collection Info 수정
컬렉션 내용의 상세보기의 첫번째 탭은 `Info` 탭은 컬렉션의 데이터들을 요약하여 설명하는 웹페이지입니다. 

되도록 컬렉션을 생성한 이후 데이터의 내용을 보다 잘 설명할 수 있는 `Info` 웹 페이지 작성을 권장합니다. 

1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Info 탭`에 있음을 확인합니다.  
1. 맨 하단의 `Edit Description` 버튼을 선택합니다. 
1. 아래와 같은 편집창에서 원하는 내용을 입력합니다. 
   상단의 아이콘 메뉴를 활용하여 그림, 유튜브 동영상 등을 입력할 수 있습니다. 
   필요한 경우 오른편 위쪽의 `source` 메뉴를 선택하여 HTML을 편집할 수 있습니다.  
   편집기의 보다 자세한 튜토리얼은 아래 동영상을 참고하시기 바랍니다. 
1. 그리고 맨 밑의 `Save`를 선택하여 수정을 완료합니다. 

<br>

{% include image.html file="data/data_search/collection_edit_info.png" %}

<br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/S1KbGhlwk0w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

### Collection 제목 및 설명 수정

1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Detail 탭`으로 이동합니다. 
1. 맨 하단의 `Edit` 버튼을 선택합니다. 
1. `Title` 혹은 `Description`을 수정합니다. 
1. 맨 밑의 `Save`를 선택하여 수정을 완료합니다. 

<br>

### Collection 접근제어 수정

1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Detail 탭`으로 이동합니다. 
1. 맨 하단의 `Edit` 버튼을 선택합니다. 
1. 하단의 `Permission`을 수정합니다. 
   접근제어 권한에 대한 설명은 상단의 `Collection 상세보기` 를 참조하세요.
1. 맨 밑의 `Save`를 선택하여 수정을 완료합니다. 

<br>

## Collection 별점 및 커맨트
1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Comment 탭`으로 이동합니다. 
1. `Rating`에서 별점 점수를 줄 수 있습니다.  
1. 그리고 `Comments`에 의견을 게시할 수 있습니다.  

<br>

## Collection 삭제
컬렉션에 데이터셋이 등록되어 있는 경우에는 삭제가 허용되지 않습니다. 

그러므로 삭제를 위해서는 데이터셋들을 모두 삭제한 이후 컬렉션을 삭제하십시오. 

컬렉션의 삭제는 해당 컬렉션과 관련된 Info 웹페이지, Paper, Thumbnail 등의 정보를 모두 삭제합니다.  

1. Collection Browser에서 원하는 컬렉션을 선택합니다. 
1. `Detail 탭`으로 이동합니다. 
1. 맨 하단의 `Delete` 버튼을 누릅니다.  