---
title: AI 플랫폼 검색 - 데이터셋
tags: []
keywords:
summary: ""
sidebar: ai_sidebar
permalink: ai_search_data.html
folder: ai
---

## 개요
 - 이 사이트는 AI 플랫폼에서 활용할 수 있는 데이터셋을 검색하는 역할을 수행합니다.

### 검색 메인
 - (1) `Search` - `AI Data`를 클릭하여 AI 데이터셋 검색 메인 페이지를 호출합니다.
 - (2) 통합 검색 바를 지원하여 `Title`, `ID`, `Description`, `Title + description`등의 검색어를 통해 데이터셋을 검색할 수 있습니다.
 - (3) `Public Dataset`, `My Dataset` 탭을 이용하여 데이터셋을 검색할 수 있습니다.
 - (4) `Community`, `Keyword`, `File Size`을 이용한 패싯 검색을 지원합니다.
 - (5) 검색된 데이터셋들을 타일 형태로 확인할 수 있습니다.
 - 특정 데이터셋을 선택하면 데이터셋의 세부 내용을 확인할 수 있습니다.
    {% include image.html file="data/ai_search_data_01.png" caption="AI 데이터셋 검색 메인 페이지" %}

### 세부 데이터셋
 - 데이터셋 세부 정보를 표현하는 뷰 페이지는 다음과 같이 구성되어 있습니다.
 - (1) 탭 구성: `Info`, `Csv Info`, `Notebook`, `File`, `Metadata`, `Comments`

		`Info`: 대략적인 정보를 설명합니다. 권한이 있는 경우 이 페이지에서 편집이 가능합니다.

		`Csv Info`: 아래 예제 그림에서 확인할 수 있는 뷰 입니다. 파일 정보를 나타내는 `File Info`, 데이터의 헤더 정보를 나타내는 `CSV Header`, 데이터의 간단한 분석이 가능한 `CSV DATA` 영역으로 나누어져 있습니다.

		`Notebook`: 해당 데이터셋을 이용해 작성된 연관 프로그래밍 코드(노트북)를 나타냅니다.

		`File`: 해당 데이터셋을 구성하는 파일과 메타데이터들을 열람 및 다운로드 할 수 있습니다.

		`Metadata`: 해당 데이터셋의 메타데이터를 확인할 수 있습니다. 만일 권한이 있다면 이 페이지에서 메타데이터를 수정 및 삭제할 수 있습니다.

		`Comments`: 해당 데이터셋에 대한 사용자들의 평가와 코멘트를 확인할 수 있는 페이지입니다.

 - (2) `CSV Header`의 데이터타입을 수정할 수 있습니다.
 - (3) 데이터셋 내부의 각 컬럼별로 한눈에 확인할 수 있는 간단한 분석을 수행합니다.막대 바 그래프를 선택하면 해당 컬럼의 데이터 분포를 확인할 수 있습니다. 숫자가 있는 가로 막대바 그래프를 선택하면 각 컬럼의 주요 성분의 개수를 간단히 확인할 수 있습니다.
 - (4) `New Kernel` 버튼을 클릭하면 이 데이터셋을 기반으로 AI 모델링을 수행할 수 있는 `Easy Analysis`로 자동으로 연결됩니다.
    {% include image.html file="data/ai_search_data_02.png" caption="AI 데이터셋 검색 세부 페이지" %}