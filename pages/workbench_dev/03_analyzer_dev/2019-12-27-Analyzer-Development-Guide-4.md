---
title: "Wrapper 파일"
permalink: workbench_analyzerguide4.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
summary: 에디슨 워크벤치 기반 후처리기(Post-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 분석기(Post-Processor) 개발 매뉴얼 입니다.

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

## 2. view.jsp 파일 코드 설정

view.jsp 파일은 워크벤치 시뮬레이션 서비스와 연계되어 데이터를 주고받고, 실제 가시화를 담당하는 부분을 독립적으로 동작할 수 있도록 지원합니다.
워크벤치 시뮬레이션 서비스에서 사용자의 이벤트에 따라 이벤트를 전송하고, 이벤트를 주고 받는 부분을 담당하고 있습니다.<br>

### 2.1. 기본 설정
처음으로 워크벤치 시뮬레이션 서비스와 연계되어 데이터를 주고 받거나 시뮬레이션 데이터를 전송받기 위해서는 아래와 같이 `OSPVisualizerUtil`과 `OSPVisualizerConfig`의 라이브러리들을 가져와야 합니다.
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
`id="<portlet:namespace/>menu"` 태그 안에 포함되어 있다. 사용자의 로컬 컴퓨터에서 지정한 파일을 쓸 때는 `Open local file`메뉴를 선택하고, 서버에 존재하는 파일을 불러올 때는 `Open Server file`메뉴를 선택하면, 내부 지정된 서버 파일 익스플로러를 호출하게 됩니다.


```html
<div class="container-fluid osp-visualizer">
 <div class="row-fluid osp-header">
 <div class="col-sm-10">
	<div id="<portlet:namespace/>title" class="osp-title"></div>
 </div>
 <div class="col-sm-2 osp-menu" id="<portlet:namespace/>menu">
	<div class="dropdown text-right">
		<button class="btn btn-primary dropdown-toggle" type="button" data-toggle="dropdown">
			Menu<span class="caret"></span>
		</button>
		<!-- Link or button to toggle dropdown -->
		<ul class="dropdown-menu dropdown-menu-right">
			<li><a href="#" id="<portlet:namespace/>openLocalFile">
				<i class="icon-file"></i>Open local file</a></li>
			<li><a href="#" id="<portlet:namespace/>openServerFile">
				<i class="icon-file"></i>Open Server file</a></li>
			<li><a href="#" id="<portlet:namespace/>download">
				<i class="icon-download-alt"></i> Download</a></li>
		</ul>
	</div>
 </div>	
 </div>
 
 <div class="row-fluid osp-frame">
  <iframe class ="col-sm-12 osp-iframe-canvas" 
		id="<portlet:namespace/>canvas" style="<%=visualizerConfig.getDisplayStyle()%>"
		src="<%=request.getContextPath()%>/html/testvisualizer/load_visual.jsp">
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
/***********************************************************************
 * Global variables and initialization section
 ***********************************************************************/
 var <portlet:namespace/>canvas = document.getElementById('<portlet:namespace/>canvas');

 var <portlet:namespace/>config = {
	namespace: '<portlet:namespace/>',
	displayCanvas: <portlet:namespace/>canvas,
	portletId: '<%=portletDisplay.getId()%>',
	connector: '<%=visualizerConfig.connector%>',
	menuOptions: JSON.parse('<%=visualizerConfig.menuOptions%>'), 
	resourceURL: '<%=serveResourceURL%>',
	eventHandlers: {
		'OSP_LOAD_DATA': <portlet:namespace/>loadDataEventHandler,
		'OSP_RESPONSE_DATA':<portlet:namespace/>responseDataEventHandler,
		'OSP_INITIALIZE': <portlet:namespace/>initializeEventHandler
	},
	loadCanvas: <portlet:namespace/>loadCanvas,
	procFuncs:{
		readServerFile: function( jsonData ){
			console.log('Custom function for readServerFile....');
		}
	}
};
 
 var <portlet:namespace/>visualizer;
 $('#<portlet:namespace/>canvas').load(function(){
 	<portlet:namespace/>visualizer = OSP.Visualizer(<portlet:namespace/>config);
 	<portlet:namespace/>processInitAction( JSON.parse( '<%=visualizerConfig.initData%>' ) );
 });
```



### 2.4. script 내 글로벌 함수 설정
2.3 절이서 설정된 바와 같이, 파일에 대한 처리 부분을 포함하는 함수인 `<portlet:namespace/>loadCanvas`와 포틀릿의 타이틀을 설정하는 `<portlet:namespace/>setTitle` 함수, 
가시화 모듈의 초기화를 담당하는 함수인 `<portlet:namespace/>processInitAction`의 함수 정의가 포함되어 있습니다. <br>
`<portlet:namespace/>visualizer.callIframeFunc` 함수의 경우, 해당 이벤트가 발생하였을 때, `<iframe>` 태그에서 호출하는 가시화 모듈 내에 존재하는 데이터 로딩 가시화 함수를 지정합니다.<br>

`loadVisualFile`함수는 실제 가시화를 담당하는 부분의 함수를 의미합니다.


```html
/***********************************************************************
 * Canvas functions
***********************************************************************/
function <portlet:namespace/>loadCanvas( jsonData, changeAlert ){
	
	switch( jsonData.type_ ){
	case OSP.Enumeration.PathType.FILE:
	    <portlet:namespace/>visualizer.readServerFileURL();
		break;
	case OSP.Enumeration.PathType.FOLDER:
	case OSP.Enumeration.PathType.EXT:
	    <portlet:namespace/>visualizer.readFirstServerFileURL();
		break;
	case OSP.Enumeration.PathType.URL:
		<portlet:namespace/>setTitle(jsonData.name_);
		<portlet:namespace/>visualizer.callIframeFunc( 'loadVisualFile', null, jsonData.content_ );
		break;
	case OSP.Enumeration.PathType.CONTENT:
	case OSP.Enumeration.PathType.FILE_CONTENT:
		console.log('FILE_CONTENT Un supported yet.', jsonData);
		break;
	default:
		console.log('Un supported yet.', jsonData);
	}
}

function <portlet:namespace/>setTitle( title ){
	$('#<portlet:namespace/>title').html( '<h4 style="margin:0;">'+title+'</h4>' );
}

function <portlet:namespace/>processInitAction( jsonInitData ){
	if(jsonInitData && !jsonInitData.repositoryType_ ){
		// Do nothing if repository is not specified.
		// This means processInitAction will be performed OSP_SHAKEHAND event handler.
		return;  
	}
	
	if( !jsonInitData.user_ ){	
		jsonInitData.user_ = '<%=user.getScreenName()%>';
		jsonInitData.dataType_ = {
				name: 'any',
				version:'0.0.0'
		};
		jsonInitData.type_ = OSP.Enumeration.PathType.FOLDER;
		jsonInitData.parent_ = '';
		jsonInitData.name_ = '';
	}
	
	<portlet:namespace/>visualizer.processInitAction( jsonInitData, false );
}

```

### 2.5. 전체 코드

전체 코드를 확인하면 아래와 같습니다.<br>
```html
<%@page import="com.kisti.osp.util.OSPVisualizerUtil"%>
<%@page import="com.kisti.osp.util.OSPVisualizerConfig"%>
<%@include file="../init.jsp"%>

<portlet:resourceURL var="serveResourceURL"></portlet:resourceURL>
<%
OSPVisualizerConfig visualizerConfig = OSPVisualizerUtil.getVisualizerConfig(renderRequest, portletDisplay, user);
%>

<div class="container-fluid osp-visualizer">
	<div class="row-fluid osp-header">
		<div class="col-sm-10">
			<div id="<portlet:namespace/>title" class="osp-title"></div>
		</div>
		<div class="col-sm-2 osp-menu" id="<portlet:namespace/>menu">
			<div class="dropdown text-right">
				<button class="btn btn-primary dropdown-toggle" type="button" data-toggle="dropdown">
					Menu<span class="caret"></span>
				</button>
				<!-- Link or button to toggle dropdown -->
				<ul class="dropdown-menu dropdown-menu-right">
					<li><a href="#" id="<portlet:namespace/>openLocalFile"><i class="icon-file"></i>Open local file</a></li>
					<li><a href="#" id="<portlet:namespace/>openServerFile"><i class="icon-file"></i>Open Server file</a></li>
					<li><a href="#" id="<portlet:namespace/>download"><i class="icon-download-alt"></i> Download</a></li>
				</ul>
			</div>
		</div>	
	</div>
	<div class="row-fluid osp-frame">
		<iframe 
				class ="col-sm-12 osp-iframe-canvas" 
				id="<portlet:namespace/>canvas" style="<%=visualizerConfig.getDisplayStyle()%>"
				src="<%=request.getContextPath()%>/html/testvisualizer/load_visual.jsp">
		</iframe>
	</div>
</div>


<script>
/***********************************************************************
 * Global variables and initialization section
 ***********************************************************************/
 var <portlet:namespace/>canvas = document.getElementById('<portlet:namespace/>canvas');

 var <portlet:namespace/>config = {
			namespace: '<portlet:namespace/>',
			displayCanvas: <portlet:namespace/>canvas,
			portletId: '<%=portletDisplay.getId()%>',
			connector: '<%=visualizerConfig.connector%>',
			menuOptions: JSON.parse('<%=visualizerConfig.menuOptions%>'), 
			resourceURL: '<%=serveResourceURL%>',
			eventHandlers: {
					'OSP_LOAD_DATA': <portlet:namespace/>loadDataEventHandler,
					'OSP_RESPONSE_DATA':<portlet:namespace/>responseDataEventHandler,
					'OSP_INITIALIZE': <portlet:namespace/>initializeEventHandler
			},
			loadCanvas: <portlet:namespace/>loadCanvas,
			procFuncs:{
				readServerFile: function( jsonData ){
					console.log('Custom function for readServerFile....');
				}
			}
};
 
 var <portlet:namespace/>visualizer;
 $('#<portlet:namespace/>canvas').load(function(){
 	<portlet:namespace/>visualizer = OSP.Visualizer(<portlet:namespace/>config);
 	<portlet:namespace/>processInitAction( JSON.parse( '<%=visualizerConfig.initData%>' ) );
 });
 
/***********************************************************************
 * Canvas functions
***********************************************************************/
function <portlet:namespace/>loadCanvas( jsonData, changeAlert ){
	
	switch( jsonData.type_ ){
	case OSP.Enumeration.PathType.FILE:
	    <portlet:namespace/>visualizer.readServerFileURL();
		break;
	case OSP.Enumeration.PathType.FOLDER:
	case OSP.Enumeration.PathType.EXT:
	    <portlet:namespace/>visualizer.readFirstServerFileURL();
		break;
	case OSP.Enumeration.PathType.URL:
		<portlet:namespace/>setTitle(jsonData.name_);
		<portlet:namespace/>visualizer.callIframeFunc( 'loadVisualFile', null, jsonData.content_ );
		break;
	case OSP.Enumeration.PathType.CONTENT:
	case OSP.Enumeration.PathType.FILE_CONTENT:
		console.log('FILE_CONTENT Un supported yet.', jsonData);
		break;
	default:
		console.log('Un supported yet.', jsonData);
	}
}

function <portlet:namespace/>setTitle( title ){
	$('#<portlet:namespace/>title').html( '<h4 style="margin:0;">'+title+'</h4>' );
}

function <portlet:namespace/>processInitAction( jsonInitData ){
	if(jsonInitData && !jsonInitData.repositoryType_ ){
		// Do nothing if repository is not specified.
		// This means processInitAction will be performed OSP_SHAKEHAND event handler.
		return;  
	}
	
	if( !jsonInitData.user_ ){	
		jsonInitData.user_ = '<%=user.getScreenName()%>';
		jsonInitData.dataType_ = {
				name: 'any',
				version:'0.0.0'
		};
		jsonInitData.type_ = OSP.Enumeration.PathType.FOLDER;
		jsonInitData.parent_ = '';
		jsonInitData.name_ = '';
	}
	
	<portlet:namespace/>visualizer.processInitAction( jsonInitData, false );
}


/***********************************************************************
 * Window Event binding functions 
 ***********************************************************************/
 $('#<portlet:namespace/>selectFile').bind(
			'change', 
			function(event){
				var input = document.getElementById('<portlet:namespace/>selectFile');
				var reader = new FileReader();
		            
				reader.onload = function (e) {
					$('#<portlet:namespace/>canvas').each(function(){
						$(this).prop('contentWindow').loadVisualFile(e.target.result);
							
					});
			      
					<portlet:namespace/>setTitle(input.files[0].name);
				};
		            
				reader.readAsDataURL(input.files[0]);
			}
		);
 
$('#<portlet:namespace/>openLocalFile').click(function(){
	//$('#<portlet:namespace/>selectFile').click();
	<portlet:namespace/>visualizer.openLocalFileURL();
});

$('#<portlet:namespace/>openServerFile').click(function(){
	<portlet:namespace/>visualizer.openServerFile();
});

$('#<portlet:namespace/>download').click(function(){
	<portlet:namespace/>visualizer.downloadCurrentFile();
});

/***********************************************************************
 * Handling OSP Events and event handlers
 ***********************************************************************/
function <portlet:namespace/>loadDataEventHandler( data, callbackParams ){
	console.log('[<portlet:namespace/>loadDataEventHandler] ', data );
	<portlet:namespace/>visualizer.loadCanvas( data, false );
}

function <portlet:namespace/>responseDataEventHandler( data, callbackParams ){
	console.log('[<portlet:namespace/>responseDataEventHandler]', data, callbackParams);
	
	switch( callbackParams.procFunc ){
	case 'readServerFile':
		<portlet:namespace/>visualizer.runProcFuncs( 'readServerFileURL', data );
		break;
	}
}

function <portlet:namespace/>initializeEventHandler( data, callbackParams ){
	console.log('[<portlet:namespace/>initializeEventHandler] ');
	<portlet:namespace/>visualizer.callIframeFunc('clearVisual', null );
	<portlet:namespace/>setTitle('');
}


</script>
 
```
