---
title: AI 플랫폼 검색 - 프로그래밍 코드
tags: []
keywords:
summary: ""
sidebar: ai_sidebar
permalink: ai_search_code.html
folder: ai
---

## 개요
 - 이 사이트는 AI 플랫폼에서 활용할 수 있는 프로그래밍 코드(노트북)를 검색하는 역할을 수행합니다.

### 검색 메인
 - (1) `Search` - `AI code`를 클릭하여 AI 코드 검색 메인 페이지를 호출합니다.
 - (2) 통합 검색 바를 지원하여 `Title`, `ID`, `Description`, `Title + description`등의 검색어를 통해 코드를 검색할 수 있습니다.
 - (3) `Public Notebook`, `My Notebook` 탭을 이용하여 코드를 검색할 수 있습니다. `My Notebook` 탭의 `Share` 버튼을 클릭하여 원하는 코드를 다른 사용자에게 공개할 수 있습니다.
 - (4) `Language`, `Task`, `Algorithm`을 이용한 패싯 검색을 지원합니다.
 - (5) 검색된 코드들을 타일 형태로 확인할 수 있습니다.
 - 특정 코드를 선택하면 세부 내용을 확인할 수 있습니다.
    {% include image.html file="data/ai_search_code_01.png" caption="AI 코드 검색 메인 페이지" %}
    {% include image.html file="data/ai_search_code_02.png" caption="AI 코드 검색 마이 페이지" %}

### 세부 코드
 - 세부 정보를 표현하는 뷰 페이지는 다음과 같이 구성되어 있습니다.
 - (1) 탭 구성: `Info`, `Code`, `Data`, `File`, `Metadata`, `Comments`

		`Info`: 대략적인 정보를 설명합니다. 권한이 있는 경우 이 페이지에서 편집이 가능합니다.

		`Code`: 프로그래밍 코드를 열람할 수 있습니다. `Fork Notebook` 버튼을 통해 내 개발 환경으로 해당 데이터셋 및 코드를 복사하여 실행할 수 있습니다.

		`Data`: 해당 코드의 데이터 파일을 열람합니다.

		`File`: 해당 코드의 파일을 열람합니다.

		`Metadata`: 해당 코드의 메타데이터를 확인할 수 있습니다. 권한이 있는 경우 이 페이지에서 메타데이터를 수정 및 삭제할 수 있습니다.

		`Comments`: 해당 코드에 대한 사용자들의 평가와 코멘트를 확인할 수 있는 페이지입니다.