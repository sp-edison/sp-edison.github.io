---
title: "text-editor 파일 설정"
permalink: workbench_editorguide5.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, editor]
folder: workbench
summary: 에디슨 워크벤치 기반 에디터(Pre-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 전처리기(Pre-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## 1. text-editor.jsp 파일 설정

이전 단계에서 실제 데이터를 가시화하는 후처리 모듈을 `<iframe>`태그 안에서 호출을 하였습니다.
해당 코드 부분은 다음과 같습니다.

```html
<iframe 
	class="col-sm-12 osp-iframe-canvas"  
	style="<%=visualizerConfig.getDisplayStyle()%>border:solid #eeeeee 1px;" 
	id="<portlet:namespace/>canvas" 
	src="<%=request.getContextPath()%>/html/TextEditor/text-editor.jsp">
</iframe>
```
<br>
위의 내용과 마찬가지로 현재 같은 폴더 내에 `text-editor.jsp` 파일을 새로 생성하여 가시화 하는 소스코드를 추가합니다.
기본적인 구조는 html 파일과 마찬가지로 동작할 수 있습니다. 외부 스크립트 라이브러리를 추가하고 싶은 경우에는 아래 코드와 같이 추가합니다.

```html
<script src="<%=request.getContextPath()%>/js/jquery/jquery-3.1.0.min.js"></script>
```

## 2. 데이터 입력 처리 함수 설정
아래의 코드는 데이터 입력을 처리하는 함수를 포함하고 있습니다. `visualizer-wrapper`에서 호출되는 함수들이 포함되어 있습니다.

- `setNamespace` : 포틀릿의 고유 아이디인 namespace를 설정
- `disable` : 입력 데이터를 바꾸지 못하도록 설정
- `setContent` : 입력 데이터를 에디터 영역에 설정
- `getContent` : 현재 입력된 데이터를 가져옴
- `fireDataChangedEvent` : 사용자의 입력이 변경됨에 따라 이벤트를 발생시켜 서버에 저장하도록 함


 <br>
```html
/***********************************************************************
	 * Functions called by wrapper jsp 
	 ***********************************************************************/
	function setNamespace( ns ){
		namespace = ns;
	} 
	
	function disable( flag ){
		$('#canvas').prop('readonly', flag );
	}
	
	function setContent( content ){
		//console.log( content );
		$('#canvas').val( content );
	}
	
	function getContent(){
		return 	$('#canvas').val();
	}
	
	function fireDataChangedEvent( content ){
		setTimeout(
				function(){
					if( namespace ){
						window.parent[namespace+'fireDataChangedEvent']( content );
					}
					else{
						fireDataChangedEvent( content );
					}
				},
				10
			);
	}
	 
	
	$('#canvas').on('change', function(){
		fireDataChangedEvent( this.value );
	});
```


## 3. 전체 코드


전체 코드를 확인하면 다음과 같습니다.
```html
<!DOCTYPE>

<html>
<head>
	<script src="<%=request.getContextPath()%>/js/jquery/jquery-3.1.0.min.js"></script>
	<script src="<%=request.getContextPath()%>/js/jquery/jquery-ui-1.12.1.custom/jquery-ui.min.js"></script>
	<link rel="stylesheet" type="text/css" href="<%=request.getContextPath()%>/js/jquery/jquery-ui-1.12.1.custom/jquery-ui.min.css"/>
	
	<style>
	body {
		margin: 0;
		padding: 0;
	}
	.inner-canvas {
		margin: 0;
		padding: 0;
		width:100%;
		height:100%;
		overflow:none;
	}
	
	.inner-canvas .canvas {
		margin: 0;
		padding: 0;
		width:100%;
		height:100%;
		border:none;
		resize:none;
		overflow:none;
	}
	
	</style>
</head>
<body style="height: 100%;">
	<div class="inner-canvas">
		<textarea id="canvas" class="canvas"></textarea>
	</div>
	<script>
	$(document).ready(function(){
// 		$('body').height(document.documentElement.clientHeight );
	});
	
	var namespace;
	var disabled = false;
	
	/***********************************************************************
	 * Functions called by wrapper jsp 
	 ***********************************************************************/
	function setNamespace( ns ){
		namespace = ns;
	} 
	
	function disable( flag ){
		$('#canvas').prop('readonly', flag );
	}
	
	function setContent( content ){
		//console.log( content );
		$('#canvas').val( content );
	}
	
	function getContent(){
		return 	$('#canvas').val();
	}
	
	function fireDataChangedEvent( content ){
		setTimeout(
				function(){
					if( namespace ){
						window.parent[namespace+'fireDataChangedEvent']( content );
					}
					else{
						fireDataChangedEvent( content );
					}
				},
				10
			);
	}
	 
	
	$('#canvas').on('change', function(){
		fireDataChangedEvent( this.value );
	});
	</script>
</body>
</html>
```


샘플 코드는 아래의 링크를 통해 다운로드 받을 수 있습니다.
- [OSPTextEditorExample-portlet.zip](OSPLibrary/OSPTextEditorExample-portlet.zip)