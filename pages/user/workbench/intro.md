---
title: WorkBench 소개
tags: [EDISON, WorkBench]
keywords:
summary: "사이언스 앱의 수행 환경인 WorkBench는 웹 브라우저의 접속 만으로 시뮬레이션 수행에 필요한 도구 및 분석기를 제공 합니다. 본 문서는 시뮬레이션 수행을 위한 유저 매뉴얼로 EDISON 플랫폼내에서 WorkBench를 활용 하는 방법에 대해서 소개하고자 합니다."
sidebar: user_sidebar
permalink: user_workbench_intro.html
folder: user/workbench
---

## WorkBench 소개
 - WorkBench에 대한 소개 입니다.
### WorkBench 화면 구성
- WorkBench의 화면 구성에 대하여 설명 입니다.

<!-- Workbench 이미지 삽입 -->
{% include image.html file="user/workbench/workbench.png" caption="워크벤치" %}

(1) Job Controller 영역 <br/>
(2) Dash Board 영역<br/>
(3) Layout 영역
### Job Controller 영역
- 작업 상태에 따른 작업 관리를 지원 하는 영역 입니다.
<!-- Job Controller 이미지 삽입 -->
{% include image.html file="user/workbench/job_controller.png" caption="Job Controller" %}

#### 시뮬레이션
```Simulation```
>시뮬레이션 목록을 조회 할 수 있습니다.

```Edit ```
> 현재 선택한 시뮬레이션에 대하여 이름 변경 및 삭제 할 수 있는 화면을 조회 합니다.

#### 작업
```New```
> 새로운 작업을 생성 합니다.

```Save```
> 현재 선택된 작업을 저장 합니다.

```Copy```
> 선택된 작업을 복사 할 수 있습니다.<br/>
>해당 기능을 통하여 현재 작업을 복사 할 시뮬레이션 목록을 조회 할수 있습니다.

```Delete```
> 선택된 작업을 삭제 할 수 있습니다.

```Select```
> WorkFlow에서 Workbench 실행 시 성공한 작업에 대하여 WorkFlow에 작업을 적용 할 수 있습니다.

#### 작업 수행
```Submit```
> 필수 입력 데이터 검증 후 선택된 작업을 실행 합니다.

```Cancel```
> 작업이 수행중일 상태일 경우 해당 작업을 취소 합니다.

```Log```
> 작업이 수행중이거나 종료 후 로그를 조회 할 수 있습니다.

```Download```
> 작업이 성공 하였을 경우 결과 파일의 목록 및 폴더를 조회 및 다운로드 하는 화면을 조회 합니다.

#### 사이언스 앱
```Manual```
> 사이언스 앱의 매뉴얼을 다운로드 합니다.<br/>
> 해당 작업은 사이언스 앱의 개발자가 매뉴얼을 업로드 하였을 경우에 동작 합니다.

```OpenData```
> 성공한 작업에 대하여 데이터 저장소에 해당 작업 내용을 저장 하는 화면을 조회 합니다.


### Dash Board 영역
- 선택한 시뮬레이션의 작업 목록 조회 및 포트 목록을 조회 하는 영역 입니다.
- 작업에 대한 상세 정보를 조회 할 수 있습니다.
- 포트 선택 시 해당 포트에 대한 입력기 또는 분석기를 조회 할 수 있습니다.
- 포트에 대한 조회는 현재 작업 상태에 따라 제한 될 수 있습니다.
<!-- Dash Board 이미지 삽입 -->
{% include image.html file="user/workbench/dashboard.png" caption="Dash Board" %}

### Layout 영역
- 사이언스 앱에서 설정된 Layout 구성을 기반으로 입력기/분석기를 조회 하는 영역 입니다.
- Layout 영역내에서 사용자는 특정 부분에 대한 크기를 제어 할 수 있습니다.
<!-- Layout 이미지 삽입 -->
{% include image.html file="user/workbench/layout.png" caption="Layout" %}

## 시뮬레이션 관리
- 시뮬레이션은 작업의 그룹을 관리 하는 단위 입니다. 현재 WorkBench에서는 선택된 시뮬레이션의 관리 및 목록에 대한 관리 기능을 제공 하고 있습니다.
### 화면
- 선택된 시뮬레이션의 관리
    - 이름 변경 및 삭제 기능을 제공 합니다.
    <!-- 시뮬레이션 수정 이미지 삽입-->
    {% include image.html file="user/workbench/simulation_edit.png" caption="시뮬레이션 수정" %}
- 시뮬레이션 목록에서의 관리
    - 현재 선택된 사이언스앱을 수행한 시뮬레이션 목록을 출력 합니다.
    - 입력, 이름 변경, 삭제, 데이터 저장소에 성공한 시뮬레이션 작업 데이터 저장 기능을 제공 합니다.
    <!-- 시뮬레이션 목록 이미지 삽입-->
    {% include image.html file="user/workbench/simulation_list.png" caption="시뮬레이션 목록" %}

## 작업 관리
- 작업은 유저가 수행한 내용에 대한 정보 입니다.
- 작업에 대한 상태에 따라 결과 파일 조회 및 다운로드, 입력기, 분석기에 대한 조회를 수행 할 수 있습니다.
- 입력기와 분석기는 작업 상태에 따라 입력 및 조회가 제한 될 수 있습니다.
<!-- 작업 관리 이미지 삽입-->
{% include image.html file="user/workbench/job_edit.png" caption="작업 상세 정보" %}