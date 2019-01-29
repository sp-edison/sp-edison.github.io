---
title: 시뮬레이션 데이터 View Designer
tags: []
keywords:
summary: ""
sidebar: datadev_sidebar
permalink: datadev_view_design.html
folder: datadev
---

## 데이터 View 생성

1. 메뉴의 `Tool` - `View Designer`로 이동 합니다.

1. `Create` 버튼을 클릭하여 뷰 생성 화면으로 이동 합니다. 

    {% include image.html file="data/datadev_view_manage/datadev_view_design_001.png" %}

2. View Designer 전체적인 설명

    {% include image.html file="data/datadev_view_manage/datadev_view_design_guide_1.png" %}

   ```
   도구막대 : 데이터타입을 지정하고 샘플용 데이터셋을 선택 할 수 있는 기능, 하단의 도구는 순서대로 미리보기, 되돌리기, 다시실행, 전체화면, 다운로드, 가이드, 저장 기능
   템플릿 페이지 : 뷰 레이아웃을 미리 지정해 놓은은 템플릿 페이지를 불러오는 기능
   컴포넌트 : 뷰를 꾸미기 위한 각종 컴포넌트들로 뷰 영역에 Drag&Drop 하여 편집 할 수 있는 컴포넌트 영역
   뷰 영역 : 실제 뷰를 편집하는 영역
   컴포넌트 설정 : 각 컴포넌트별로 특정 옵션이 있을경우 해당 영역에 표시됨
   컴포넌트 기본 설정 : 모든 컴포넌트에 기본적으로 적용되는 옵션으로 뷰를 상세편집시 사용
   ```

    {% include image.html file="data/datadev_view_manage/datadev_view_design_guide_2.png" %}

   ```
   미리보기 : 편집중인 뷰를 미리보기 하는 기능 (상단의 데이터셋을 선택하면 실제 데이터를 확인 할 수 있음)
   되돌리기 : 편집중에 한단계 뒤로 되돌리는 기능
   다시실행 : 편집중 되돌렸던기능 다시 실행 기능
   전체화면 : 뷰편집 모드를 전체화면으로 전환
   다운로드 : 해당 뷰 소스를 다운로드
   가이드 : 뷰컴포넌트에 대한 가이드를 확인
   저장 : 뷰를 작성후 저장 하는 기능
   ```

    {% include image.html file="data/datadev_view_manage/datadev_view_design_guide_3.png" %}

   ```
   이동(Drag&Drop) : 해당 컴포넌트의 위치를 이동하는 기능
   상위컴포넌트선택 : 여러 컴포넌트가 조합되어 있는경우 상위 컴포넌트를 선택할때 사용
   상단으로이동 : 컴포넌트의 위치를 상단으로 이동
   하단으로이동 : 컴포넌트의 위치를 하단으로 이동
   복사 : 동일한 컴포넌트를 복사하여 하단에 하나더 생성
   삭제 : 선택한 컴포넌트를 삭제
   ```

3. 좌측 `Layout` 영역에서 `Grid Row(4:8)` 컴포넌트를 뷰 영역으로 Drag&Drop 합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_002.png" %}

4. 좌측 `Layout` 영역에서 `Panel` 컴포넌트를 `Grid Row(4:8)` 의 좌측 영역으로 Drag&Drop 합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_003.png" %}

5. `Panel` 컴포넌트 상단을 `더블클릭` 하여 타이틀을 입력 합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_004.png" %}

6. `Panel` 컴포넌트 하단에 `Non-border Table` 컴포넌트를 Drag&Drop 합니다. 

7. 컴포넌트를 클릭하면 우측 `컴포넌트 설정` 영역에 해당 컴포넌트의 설정 항목이 표시되고 다음과 같이 조절합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_005.png" %}

8. `Non-border Table` 상단에 제목을 입력하고 하단에는 메타 데이터를 입력하기 위해 `데이터 타입`과 `Preview 데이터셋` 을 선택 합니다.

9. 상단의 `Select` 버튼을 클릭하고 해당 데이터타입의 `Choose` 버튼을 클릭

    {% include image.html file="data/datadev_view_manage/datadev_view_design_006.png" %}

10. Preview 할 데이터셋을 `Choose` 버튼을 클릭하여 선택

    {% include image.html file="data/datadev_view_manage/datadev_view_design_007.png" %}

11. Preview 데이터셋을 선택하면 좌측 컴포넌트 영역 밑으로 `Metadata` 와 `Reference` 영역이 생성됨

     ```
     Metadata : 해당 데이터셋의 `DescriptiveMetadata` 로 Drag&Drop 하여 사용함. 또는 {{dm.metadata_name}} 형식으로 직접 입력 해도됨
     Reference : 해당 데이터셋의 `Descriptive Metadata Schema` 로 Drag&Drop 하여 사용하면 Preview시 메타데이터명 옆에 `?` 표시가 되고 클릭시 설명 페이지(wiki)로 이동한다.
     ```

12. `Metadata` 를 뷰영역으로 Drag&Drop 한다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_008.png" %}

13. 나머지 항목도 동일한 방식으로 채움, 다음은 Library 영역에서 `jsmol` 컴포넌트를 `Grid Row(4:8)` 의 좌측 영역으로 Drag&Drop 합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_009.png" %}

14. 컴포넌트를 클릭하면 우측 `컴포넌트 설정` 영역에 해당 컴포넌트의 설정 항목이 표시되고 다음과 같이 조절합니다. 컴포넌트 설정 항목 밑으로 기본적인 설정 옵션이 있는데 Size 를 조절하기 위해 Width: 100%, height : 495px 로 조절합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_010.png" %}

15. 해당 컴포넌트별 상세 설정 방법은 [데이터 뷰 컴포넌트] 를 참조

16. 작성을 완료 하면 `도구 막대` 영역에서 `미리보기` 버튼을 클릭하여 작성된 뷰를 확인 할 수 있습니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_011.png" %}

17. 작성이 완료되면 `저장` 버튼을 클릭하고 Title, Description을 작성 후 `Save` 버튼을 눌러 저장 합니다.

    {% include image.html file="data/datadev_view_manage/datadev_view_design_012.png" %}

[데이터 뷰 컴포넌트]: datadev_view_component.html	"데이터 뷰 컴포넌트"
