---
title: "Wrapper 파일"
permalink: workbench_editorguide4.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, editor]
folder: workbench
summary: 에디슨 워크벤치 기반 에디터(Pre-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 전처리기(Pre-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## 1. init.jsp 파일 설정
공통적으로 사용되는 태그라이브러리들을 설정합니다.
포틀릿에서 사용되는 공용 태그 라이브러리 및 포틀릿관련 오브젝트들을 사용할 수 있도록 설정을 추가합니다.
`/html/`폴더에 `init.jsp`파일을 추가하고 아래와 같은 코드를 추가합니다.

```html
<%@ taglib uri="http://java.sun.com/portlet_2_0" prefix="portlet" %>
<%@ taglib uri="http://alloy.liferay.com/tld/aui" prefix="aui" %>
<%@ taglib uri="http://liferay.com/tld/ui" prefix="liferay-ui" %>
<%@ taglib uri="http://liferay.com/tld/theme" prefix="theme" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://liferay.com/tld/security" prefix="liferay-security" %>
<%@ taglib uri="http://liferay.com/tld/portlet" prefix="liferay-portlet" %>

<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>


<portlet:defineObjects />
<theme:defineObjects />
```

## 2. visualizer_wrapper.jsp 파일 코드 설정

visualizer_wrapper.jsp 파일은 워크벤치 시뮬레이션 서비스와 연계되어 데이터를 주고받고, 사용자 입력 데이터를 서버 시뮬레이션 서비스에 전송하는 컨트롤 부분을 담당하고 있다.
워크벤치 시뮬레이션 서비스에서 사용자의 이벤트에 따라 이벤트를 전송하고, 이벤트를 주고 받는 부분을 담당하고 있습니다.<br>

### 2.1. 기본 설정
처음으로 워크벤치 시뮬레이션 서비스와 연계되어 데이터를 주고 받거나 시뮬레이션 데이터를 전송 하기 위해서는 아래와 같이 `OSPVisualizerUtil`과 `OSPVisualizerConfig`의 라이브러리들을 가져와야 합니다.
`OSPVisualizerUtil`과 `OSPVisualizerConfig`에서는 워크벤치 시뮬레이션 서비스에서 제공하는 다양한 이벤트와 이벤트 처리 함수가 정의되어 있으며, 해당 부분을 `import` 하기만 하면 시뮬레이션 서비스와 연계되어 사용자에게 가시화 하는 모듈을 제공할 수 있습니다.<br>
또한 이전 단계에서 정의한 포틀릿의 구성 정보를 지정하여 포틀릿의 너비와 높이, 메뉴 선택 등을 설정할 수 있습니다. 아무런 값이 지정되어 있지 않다면 기본적으로 제공되는 기본 설정이 포틀릿 구성정보로 지정되며, 워크벤치와 연동되어 동작을 할 때에는 워크벤치에서 지정한 값으로 구성 정보가 지정됩니다.<br>
코드를 확인하면 다음과 같습니다.

```html
<%@page import="com.kisti.osp.util.OSPVisualizerUtil"%>
<%@page import="com.kisti.osp.util.OSPVisualizerConfig"%>
<%@include file="../init.jsp"%>

<portlet:resourceURL var="serveResourceURL"></portlet:resourceURL>
<%
OSPVisualizerConfig visualizerConfig = OSPVisualizerUtil.getVisualizerConfig(renderRequest, portletDisplay, user);
%>
```

### 2.2. iframe 설정
실제 가시화를 담당하는 부분은 사용자에게 시뮬레이션 결과 데이터를 워크벤치 서비스에서 전송받아 데이터를 가시화 하는 모듈을 포함하고 있습니다.
후처리기 가시화 모듈을 지정하는 부분은 `<iframe>` 태그 안에 존재하고 있습니다. <br>
위에 `html` 태그들은 워크벤치 시뮬레이션 서비스와 호환되기 위해 스타일 이미지들을 지정한 내용입니다. 또한 워크벤치 시뮬레이션 서비스와 연계되기 위해 메뉴로 지정되는 부분은 
`id="<portlet:namespace/>menu"` 태그 안에 포함되어 있다. 

메뉴의 대한 설명은 다음의 표와 같습니다.



| 메뉴명             | 동작 기능                                                                        |
|:------------------|:---------------------------------------------------------------------------------|
| sample            |  시뮬레이션에 지정된 샘플데이터를 가져와 시뮬레이션 입력으로 선택함                   |
| Open local file   |  사용자의 로컬 컴퓨터 파일을 가져오기 위한 파일 익스플로러 선택                       |
| Open Server file  |  서버 파일의 리스트를 보여주는 서버 파일 익스플로러가 실행 됨                         |
| Save              |  현재 편집한 내용을 서버 내 시뮬레이션 입력으로 저장함                               |
| Save as...        |  현재 편집한 내용을 서버 내 시뮬레이션 입력으로 새로운 이름을 지정하여 저장함          |
| Save at local     |  현재 편집한 내용을 로컬 사용자의 컴퓨터에 저장함                                    |
| Download          |  현재 데이터를 다운로드함                                                          |

```html
<div class="container-fluid osp-visualizer">
 <div class="row-fluid osp-header">
	<div class="col-sm-10">
	  <div id="<portlet:namespace/>title" class="osp-title"></div>
	  </div>
	  <div class="col-sm-2 osp-menu"  id="<portlet:namespace/>menu">
		<div class="dropdown text-right">
			<button class="btn btn-primary dropdown-toggle" type="button" data-toggle="dropdown">
				Menu<span class="caret"></span>
   			</button>
			<ul class="dropdown-menu dropdown-menu-right">
             <li><a href="#" id="<portlet:namespace/>sample"><i class="icon-file"></i>Sample</a></li>
             <li><a href="#" id="<portlet:namespace/>openLocalFile"><i class="icon-file"></i>Open local file</a></li>
             <li><a href="#" id="<portlet:namespace/>openServerFile"><i class="icon-file"></i>Open Server file</a></li>
             <li><a href="#" id="<portlet:namespace/>save"><i class="icon-file"></i>Save</a></li>
             <li><a href="#" id="<portlet:namespace/>saveAs"><i class="icon-file"></i>Save as...</a></li>
             <li><a href="#" id="<portlet:namespace/>saveAtLocal"><i class="icon-file"></i>Save at local</a></li>
             <li><a href="#" id="<portlet:namespace/>download"><i class="icon-download-alt"></i> Download</a></li>					
			</ul>
		 </div>
	  </div>	
	</div>

 <div class="row-fluid osp-frame">
	<iframe 
		class="col-sm-12 osp-iframe-canvas"  
		style="<%=visualizerConfig.getDisplayStyle()%>border:solid #eeeeee 1px;" 
		id="<portlet:namespace/>canvas" 
		src="<%=request.getContextPath()%>/html/TextEditor/text-editor.jsp">
	</iframe>
 </div>
</div>
```


### 2.3. script 내 글로벌 변수 설정

다음 코드는 자바 스크립트 내의 기본값을 설정하는 부분입니다.
`<portlet:namespace/>config`는 `JSON`형태를 지정하는 부분으로 기본적인 워크벤치 시뮬레이션 서비스와 연동되어 설정되어야 하는 데이터 내부 소스를 포함하고 있습니다.
내용을 정리하면 다음과 같습니다.


| 객체명             | 동작 기능                                                            | 기본 값                                                       |
|:------------------|:---------------------------------------------------------------------|:--------------------------------------------------------------|
|namespace          |  포틀릿 고유의 아이디를 설정                                           | `'<portlet:namespace/>'`                                       |
|displayCanvas      |  그림을 그리는 부분인 iframe 아이디를 설정                              | `<portlet:namespace/>canvas `                                |
|portletId          |  포틀릿의 아이디를 설정                                                | `'<%=portletDisplay.getId()%>' `                                |
|connector          |  앞서 설정한 visualizerConfig 값 연결 설정                             | `'<%=visualizerConfig.connector%>' `                            |
|menuOptions        |  사용하려는 메뉴를 설정                                                | `JSON.parse('<%=visualizerConfig.menuOptions%>') `              |
|resourceURL        |  파일 전송을 위한 serveResourceUrl 값 설정                             | `'<%=serveResourceURL%>'`                                       |
|eventHandlers      |  사용하려는 이벤트 설정                                                | `'OSP_LOAD_DATA', 'OSP_RESPONSE_DATA', 'OSP_INITIALIZE'`        |
|loadCanvas         |  워크벤치와 호환되어 파일을 읽어오기 위한 함수 설정                      | `<portlet:namespace/>loadCanvas`                                |
|procFuncs          |  개발자가 임의로 지정한 함수/visualizer 함수보다 우선순위를 가짐         |  `readServerFile: function( jsonData ) `                        |

두 번째로 `visaalizer`라이브러리에서 제공하는 기본적인 값들을 설정하는 부분이 포함되어 있습니다.

```html
//***********************************************************************
 * Global variables and initialization section
 ***********************************************************************/
 console.log( '== LIFERAY ==', Liferay );
 
var <portlet:namespace/>canvas = document.getElementById('<portlet:namespace/>canvas');
var <portlet:namespace/>disabled = JSON.parse( '<%=visualizerConfig.disabled%>');

var <portlet:namespace/>config = {
			namespace: '<portlet:namespace/>',
			displayCanvas: <portlet:namespace/>canvas,
			portletId: '<%=portletDisplay.getId()%>',
			connector: '<%=visualizerConfig.connector%>',
			menuOptions: JSON.parse('<%=visualizerConfig.menuOptions%>'), 
			resourceURL: '<%=serveResourceURL%>',
			eventHandlers: {
					'OSP_LOAD_DATA': <portlet:namespace/>loadDataEventHandler,
					'OSP_REQUEST_DATA':<portlet:namespace/>requestDataEventHandler,
					'OSP_RESPONSE_DATA':<portlet:namespace/>responseDataEventHandler,
					'OSP_INITIALIZE': <portlet:namespace/>initializeEventHandler,
					'OSP_DISABLE_CONTROLS': <portlet:namespace/>disableControlsEventHandler
			},
			loadCanvas: <portlet:namespace/>loadCanvas,
			procFuncs:{
				readServerFile: function( jsonData ){
					console.log('Custom function for readServerFile....');
				}
			},
			disabled: JSON.parse( '<%=visualizerConfig.disabled%>')
};

var <portlet:namespace/>visualizer;
$('#<portlet:namespace/>canvas').load(function(){
	<portlet:namespace/>visualizer = OSP.Visualizer(<portlet:namespace/>config);
	<portlet:namespace/>processInitAction( JSON.parse( '<%=visualizerConfig.initData%>' ), false );
});
```



### 2.4. script 내 글로벌 함수 설정
2.3 절이서 설정된 바와 같이, 파일에 대한 처리 부분을 포함하는 함수인 `<portlet:namespace/>loadCanvas`와 포틀릿의 타이틀을 설정하는 `<portlet:namespace/>setTitle` 함수, 
가시화 모듈의 초기화를 담당하는 함수인 `<portlet:namespace/>processInitAction`의 함수 정의가 포함되어 있습니다. <br>
`<portlet:namespace/>visualizer.callIframeFunc` 함수의 경우, 해당 이벤트가 발생하였을 때, `<iframe>` 태그에서 호출하는 가시화 모듈 내에 존재하는 데이터 로딩 가시화 함수를 지정합니다.<br>


```html
/***********************************************************************
 * Canvas functions
 ***********************************************************************/
function <portlet:namespace/>loadCanvas( jsonData, changeAlert ){
	console.log( 'jsonData: ', jsonData, changeAlert );
	
	switch( jsonData.type_){
		case OSP.Enumeration.PathType.FILE:
			<portlet:namespace/>visualizer.readServerFile( jsonData, changeAlert );
			break;
		case OSP.Enumeration.PathType.CONTENT:
		case OSP.Enumeration.PathType.FILE_CONTENT:
			if( jsonData.name_ )
				<portlet:namespace/>setTitle( OSP.Util.mergePath(jsonData.parent_, jsonData.name_) );
				<portlet:namespace/>setTextEditorContent( Liferay.Util.unescapeHTML(jsonData.content_) );
			if( !<portlet:namespace/>disabled && changeAlert )
				<portlet:namespace/>visualizer.fireDataChangedEvent();
			break;
		case OSP.Enumeration.PathType.DLENTRY_ID:
			<portlet:namespace/>visualizer.readDLFileEntry(changeAlert);
			break;
		case OSP.Enumeration.PathType.URL:
			alert( 'Un-supported yet.');
			changeAlert = false;
			break;
		default:
			console.log('Path Type Error: Cannot display with this path type', jsonData );
			changeAlert = false;
			return;
	}
	
};

function <portlet:namespace/>setTitle( title ){
	$('#<portlet:namespace/>title').html( '<h4 style="margin:0;">'+title+'</h4>' );
};

function <portlet:namespace/>processInitAction( jsonInitData, changeAlert ){
	
	if( !jsonInitData.repositoryType_ ){
		// Do nothing if repository is not specified.
		// This means processInitAction will be performed OSP_SHAKEHAND event handler.
		return;  
	}
	
	jsonInitData.user_ = jsonInitData.user_ ? jsonInitData.user_ : '<%=user.getScreenName()%>';
	jsonInitData.type_ = jsonInitData.type_ ? jsonInitData.type_ : OSP.Enumeration.PathType.CONTENT;
	jsonInitData.parent_ = jsonInitData.parent_ ? jsonInitData.parent_ : '';
	jsonInitData.name_ = jsonInitData.name_ ? jsonInitData.name_ : '';
	
	<portlet:namespace/>visualizer.processInitAction( jsonInitData, changeAlert );
}

```

### 2.5. Editor 개발자 함수 정의

Editor는 사용자가 입력한 데이터 값을 처리하여 워크벤치 기반 시뮬레이션 서비스의 입력값을 업데이트 하는 역할을 합니다. 이러한 과정에서 사용자가 입력한 데이터를 워크벤치 시뮬레이션 서비스에 전송하는 역할을 하는 함수가 필요합니다.
`<portlet:namespace/>fireDataChangedEvent` 함수는 사용자가 입력한 데이터 값을 워크벤치에 전달해 주는 역할을 합니다. `<iframe>`에서 호출하는 `jsp`모듈 내부에서 사용자 UI 입력을 받거나 특정 사용자 입력에 따라 호출되는 함수입니다.
또한 `<portlet:namespace/>setTextEditorContent`함수는 샘플데이터나 시뮬레이션이 종료된 경우 서버에서 데이터를 전송받게 됩니다. 이러한 데이터를 전송받아 Editor에 데이터를 설정하는 함수입니다.

```html
 /***********************************************************************
  * Functions called by iframe jsp 
  ***********************************************************************/
function <portlet:namespace/>fireDataChangedEvent( content ){
	console.log('fireDataChangedEvent in text editor wrapper...');
	<portlet:namespace/>visualizer.fireDataChangedEvent({
		type_: 'content',
		content_: content 
	});
};

/***********************************************************************
  * Functions which call iframe functions 
  ***********************************************************************/
function <portlet:namespace/>setTextEditorContent( content ){
	<portlet:namespace/>visualizer.callIframeFunc('setContent', null, content );
}

```

### 2.6. 이벤트 함수 정의
사용자의 각 이벤트를 처리하는 코드입니다. 메뉴로 제공되는 sample, Open local file, Open Server file, Save, Save as..., Save at local, Download의 메뉴를 선택하였을 때 처리하는 함수를 정의한 내용입니다.
기본적으로 워크벤치 시뮬레이션 서비스에서 제공되는 함수는 `<portlet:namespace/>visualizer`에서 호출되는 형태를 가지고 있습니다. 특별한 경우를 제외하고는 모두 라이브러리에서 제공되는 함수를 사용합니다.


```html
/***********************************************************************
 * Window Event binding functions 
 ***********************************************************************/

$('#<portlet:namespace/>sample').click(function(){
	if( <portlet:namespace/>disabled )
		return;
	
	<portlet:namespace/>visualizer.fireRequestSampleContentEvent();
});

$('#<portlet:namespace/>openLocalFile').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.openLocalFile( true );
});

$('#<portlet:namespace/>openServerFile').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.openServerFile(null, true);
});

$('#<portlet:namespace/>save').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.callIframeFunc('getContent', function( content ){
		<portlet:namespace/>visualizer.saveAtServer(content);
	});
});

$('#<portlet:namespace/>saveAs').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.saveAtServerAs();
});

$('#<portlet:namespace/>saveAtLocal').click(function(){
	<portlet:namespace/>visualizer.callIframeFunc('getContent', function( content ){
		<portlet:namespace/>visualizer.saveAtLocal(content, 'text/plain');
	});
});

$('#<portlet:namespace/>download').click(function(){
	<portlet:namespace/>visualizer.downloadCurrentFile();
});

```

### 2.7. 이벤트 처리 함수
아래의 코드는 이벤트를 처리하는 함수 입니다. 
- `<portlet:namespace/>loadDataEventHandler` : 데이터를 로드하는 이벤트를 처리
- `<portlet:namespace/>requestDataEventHandler` : 데이터를 로드해 달라고 요청하는 이벤트 처리
- `<portlet:namespace/>responseDataEventHandler` : 데이터 요청에 대한 응답 이벤트 처리
- `<portlet:namespace/>initializeEventHandler` : 데이터 초기화 이벤트 처리
- `<portlet:namespace/>disableControlsEventHandler` : 작업이 끝난 시뮬레이션의 입력값을 변경시키지 못하도록 처리



```html
/***********************************************************************
 * Handling OSP Events and event handlers
 ***********************************************************************/
function <portlet:namespace/>loadDataEventHandler( data, params ){
	console.log('[<portlet:namespace/>loadDataEventHandler] ', data, params );
	
	<portlet:namespace/>visualizer.loadCanvas( data, params.changeAlert );
}

function <portlet:namespace/>requestDataEventHandler( data, params ){
	console.log('[<portlet:namespace/>requestDataEventHandler]', data, params);
	<portlet:namespace/>visualizer.callIframeFunc('getContent', function(content){
		<portlet:namespace/>visualizer.fireResponseDataEvent({content_: content}, params );
	});
}

function <portlet:namespace/>responseDataEventHandler( data, params ){
	console.log('[<portlet:namespace/>responseDataEventHandler]', data, params);
	
	switch( params.procFunc ){
	case 'readServerFile':
		<portlet:namespace/>visualizer.runProcFuncs( 'readServerFile', data, true );
		break;
	case 'saveAtServerAs':
		<portlet:namespace/>visualizer.callIframeFunc('getContent', function(content){
			<portlet:namespace/>visualizer.runProcFuncs( 'saveAtServerAs', data.parent_, data.name_, content );
			<portlet:namespace/>setTitle( OSP.Util.mergePath( data.parent_, data.name_) );
		});
		break;
	}
}

function <portlet:namespace/>initializeEventHandler( data, params ){
	console.log('[<portlet:namespace/>initializeEventHandler] ', data, params );
	
	<portlet:namespace/>visualizer.processInitAction(null, false);
	
	<portlet:namespace/>visualizer.callIframeFunc('setContent', null, '' );
	<portlet:namespace/>setTitle('');
}

function <portlet:namespace/>disableControlsEventHandler( data, params ){
	console.log('[<portlet:namespace/>disableControlsEventHandler] ');
	<portlet:namespace/>disabled = params.disabled;
	<portlet:namespace/>visualizer.disabled( params.disabled );
	<portlet:namespace/>visualizer.callIframeFunc('disable', null, params.disabled);
}
```


### 2.8. 전체 코드

전체 코드를 확인하면 아래와 같습니다.<br>
```html
<%@page import="com.kisti.osp.util.OSPVisualizerConfig"%>
<%@page import="com.kisti.osp.util.OSPVisualizerUtil"%>
<%@ include file="../init.jsp" %>

<portlet:resourceURL var="serveResourceURL"></portlet:resourceURL>
<%
OSPVisualizerConfig visualizerConfig = OSPVisualizerUtil.getVisualizerConfig(renderRequest, portletDisplay, user);
%>

<div class="container-fluid osp-visualizer">
	<div class="row-fluid osp-header">
		<div class="col-sm-10">
			<div id="<portlet:namespace/>title" class="osp-title"></div>
		</div>
		<div class="col-sm-2 osp-menu"  id="<portlet:namespace/>menu">
			<div class="dropdown text-right">
				<button class="btn btn-primary dropdown-toggle" type="button" data-toggle="dropdown">
					Menu<span class="caret"></span>
   				</button>
				<ul class="dropdown-menu dropdown-menu-right">
                       <li><a href="#" id="<portlet:namespace/>sample"><i class="icon-file"></i>Sample</a></li>
                       <li><a href="#" id="<portlet:namespace/>openLocalFile"><i class="icon-file"></i>Open local file</a></li>
                       <li><a href="#" id="<portlet:namespace/>openServerFile"><i class="icon-file"></i>Open Server file</a></li>
                       <li><a href="#" id="<portlet:namespace/>save"><i class="icon-file"></i>Save</a></li>
                       <li><a href="#" id="<portlet:namespace/>saveAs"><i class="icon-file"></i>Save as...</a></li>
                       <li><a href="#" id="<portlet:namespace/>saveAtLocal"><i class="icon-file"></i>Save at local</a></li>
                       <li><a href="#" id="<portlet:namespace/>download"><i class="icon-download-alt"></i> Download</a></li>					
				</ul>
			</div>
		</div>	
	</div>
	<div class="row-fluid osp-frame">
		<iframe 
				class="col-sm-12 osp-iframe-canvas"  
				style="<%=visualizerConfig.getDisplayStyle()%>border:solid #eeeeee 1px;" 
				id="<portlet:namespace/>canvas" 
				src="<%=request.getContextPath()%>/html/TextEditor/text-editor.jsp">
		</iframe>
	</div>
</div>

<script>
/***********************************************************************
 * Global variables and initialization section
 ***********************************************************************/
 console.log( '== LIFERAY ==', Liferay );
 
var <portlet:namespace/>canvas = document.getElementById('<portlet:namespace/>canvas');
var <portlet:namespace/>disabled = JSON.parse( '<%=visualizerConfig.disabled%>');

var <portlet:namespace/>config = {
			namespace: '<portlet:namespace/>',
			displayCanvas: <portlet:namespace/>canvas,
			portletId: '<%=portletDisplay.getId()%>',
			connector: '<%=visualizerConfig.connector%>',
			menuOptions: JSON.parse('<%=visualizerConfig.menuOptions%>'), 
			resourceURL: '<%=serveResourceURL%>',
			eventHandlers: {
					'OSP_LOAD_DATA': <portlet:namespace/>loadDataEventHandler,
					'OSP_REQUEST_DATA':<portlet:namespace/>requestDataEventHandler,
					'OSP_RESPONSE_DATA':<portlet:namespace/>responseDataEventHandler,
					'OSP_INITIALIZE': <portlet:namespace/>initializeEventHandler,
					'OSP_DISABLE_CONTROLS': <portlet:namespace/>disableControlsEventHandler
			},
			loadCanvas: <portlet:namespace/>loadCanvas,
			procFuncs:{
				readServerFile: function( jsonData ){
					console.log('Custom function for readServerFile....');
				}
			},
			disabled: JSON.parse( '<%=visualizerConfig.disabled%>')
};

var <portlet:namespace/>visualizer;
$('#<portlet:namespace/>canvas').load(function(){
	<portlet:namespace/>visualizer = OSP.Visualizer(<portlet:namespace/>config);
	<portlet:namespace/>processInitAction( JSON.parse( '<%=visualizerConfig.initData%>' ), false );
});
	
/***********************************************************************
 * Canvas functions
 ***********************************************************************/
function <portlet:namespace/>loadCanvas( jsonData, changeAlert ){
	console.log( 'jsonData: ', jsonData, changeAlert );
	
	switch( jsonData.type_){
		case OSP.Enumeration.PathType.FILE:
			<portlet:namespace/>visualizer.readServerFile( jsonData, changeAlert );
			break;
		case OSP.Enumeration.PathType.CONTENT:
		case OSP.Enumeration.PathType.FILE_CONTENT:
			if( jsonData.name_ )
				<portlet:namespace/>setTitle( OSP.Util.mergePath(jsonData.parent_, jsonData.name_) );
			
			<portlet:namespace/>setTextEditorContent( Liferay.Util.unescapeHTML(jsonData.content_) );

			if( !<portlet:namespace/>disabled && changeAlert )
				<portlet:namespace/>visualizer.fireDataChangedEvent();
			break;
		case OSP.Enumeration.PathType.DLENTRY_ID:
			<portlet:namespace/>visualizer.readDLFileEntry(changeAlert);
			break;
		case OSP.Enumeration.PathType.URL:
			alert( 'Un-supported yet.');
			changeAlert = false;
			break;
		default:
			console.log('Path Type Error: Cannot display with this path type', jsonData );
			changeAlert = false;
			return;
	}
	
};

function <portlet:namespace/>setTitle( title ){
	$('#<portlet:namespace/>title').html( '<h4 style="margin:0;">'+title+'</h4>' );
};

function <portlet:namespace/>processInitAction( jsonInitData, changeAlert ){
	
	if( !jsonInitData.repositoryType_ ){
		// Do nothing if repository is not specified.
		// This means processInitAction will be performed OSP_SHAKEHAND event handler.
		return;  
	}
	
	jsonInitData.user_ = jsonInitData.user_ ? jsonInitData.user_ : '<%=user.getScreenName()%>';
	jsonInitData.type_ = jsonInitData.type_ ? jsonInitData.type_ : OSP.Enumeration.PathType.CONTENT;
	jsonInitData.parent_ = jsonInitData.parent_ ? jsonInitData.parent_ : '';
	jsonInitData.name_ = jsonInitData.name_ ? jsonInitData.name_ : '';
	
	<portlet:namespace/>visualizer.processInitAction( jsonInitData, changeAlert );
}


 /***********************************************************************
  * Functions called by iframe jsp 
  ***********************************************************************/
function <portlet:namespace/>fireDataChangedEvent( content ){
	console.log('fireDataChangedEvent in text editor wrapper...');
	<portlet:namespace/>visualizer.fireDataChangedEvent({
		type_: 'content',
		content_: content 
	});
};

/***********************************************************************
  * Functions which call iframe functions 
  ***********************************************************************/
function <portlet:namespace/>setTextEditorContent( content ){
	<portlet:namespace/>visualizer.callIframeFunc('setContent', null, content );
}

/***********************************************************************
 * Window Event binding functions 
 ***********************************************************************/

$('#<portlet:namespace/>sample').click(function(){
	if( <portlet:namespace/>disabled )
		return;
	
	<portlet:namespace/>visualizer.fireRequestSampleContentEvent();
});

$('#<portlet:namespace/>openLocalFile').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.openLocalFile( true );
});

$('#<portlet:namespace/>openServerFile').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.openServerFile(null, true);
});

$('#<portlet:namespace/>save').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.callIframeFunc('getContent', function( content ){
		<portlet:namespace/>visualizer.saveAtServer(content);
	});
});

$('#<portlet:namespace/>saveAs').click(function(){
	if( <portlet:namespace/>disabled )
		return;

	<portlet:namespace/>visualizer.saveAtServerAs();
});

$('#<portlet:namespace/>saveAtLocal').click(function(){
	<portlet:namespace/>visualizer.callIframeFunc('getContent', function( content ){
		<portlet:namespace/>visualizer.saveAtLocal(content, 'text/plain');
	});
});

$('#<portlet:namespace/>download').click(function(){
	<portlet:namespace/>visualizer.downloadCurrentFile();
});

/***********************************************************************
 * Handling OSP Events and event handlers
 ***********************************************************************/
function <portlet:namespace/>loadDataEventHandler( data, params ){
	console.log('[<portlet:namespace/>loadDataEventHandler] ', data, params );
	
	<portlet:namespace/>visualizer.loadCanvas( data, params.changeAlert );
}

function <portlet:namespace/>requestDataEventHandler( data, params ){
	console.log('[<portlet:namespace/>requestDataEventHandler]', data, params);
	<portlet:namespace/>visualizer.callIframeFunc('getContent', function(content){
		<portlet:namespace/>visualizer.fireResponseDataEvent({content_: content}, params );
	});
}

function <portlet:namespace/>responseDataEventHandler( data, params ){
	console.log('[<portlet:namespace/>responseDataEventHandler]', data, params);
	
	switch( params.procFunc ){
	case 'readServerFile':
		<portlet:namespace/>visualizer.runProcFuncs( 'readServerFile', data, true );
		break;
	case 'saveAtServerAs':
		<portlet:namespace/>visualizer.callIframeFunc('getContent', function(content){
			<portlet:namespace/>visualizer.runProcFuncs( 'saveAtServerAs', data.parent_, data.name_, content );
			<portlet:namespace/>setTitle( OSP.Util.mergePath( data.parent_, data.name_) );
		});
		break;
	}
}

function <portlet:namespace/>initializeEventHandler( data, params ){
	console.log('[<portlet:namespace/>initializeEventHandler] ', data, params );
	
	<portlet:namespace/>visualizer.processInitAction(null, false);
	
	<portlet:namespace/>visualizer.callIframeFunc('setContent', null, '' );
	<portlet:namespace/>setTitle('');
}

function <portlet:namespace/>disableControlsEventHandler( data, params ){
	console.log('[<portlet:namespace/>disableControlsEventHandler] ');
	<portlet:namespace/>disabled = params.disabled;
	<portlet:namespace/>visualizer.disabled( params.disabled );
	<portlet:namespace/>visualizer.callIframeFunc('disable', null, params.disabled);
}
</script>
```
