---
title: "파일 탐색기 설정"
permalink: workbenchanalyzerguide6.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---



### 파일 메뉴 설정
기본적으로 분석기를 EDISON 워크벤치와 연동을 하면서 필요한 파일 메뉴는 3가지 입니다. 현재 대부분의 워크벤치와 연동된 파일 메뉴는 로컬 파일 불러오기, 서버 파일 불러오기, 현재 파일 다운로드하기 가 있습니다.
이러한 파일 메뉴와 더불어 실제 파일을 불러와 가시화하는 가시화 부분을 호출하는 `iframe`도 같이 포함하여 정의합니다. 이러한 파일 메뉴는 이전 포스트에서 설정되어 있는 [osp-analyzer.css](../analyzerguide3)에서 정의되어 있는 스타일을 사용합니다.

다음은 파일 메뉴를 설정하기 위한 html 태그 코드입니다.
```javascript
<div class="container-fluid osp-analyzer">
	<div class="row-fluid header">
		<div class="col-sm-10" id="<portlet:namespace/>title"></div>
		<div class="col-sm-2" >
			<div class="dropdown">
				<button class="btn btn-primary dropdown-toggle" type="button" data-toggle="dropdown">
					Menu<span class="caret"></span>
				</button>
				<!-- Link or button to toggle dropdown -->
				<ul class="dropdown-menu dropdown-menu-right">
					<li ><a href="javascript:$('#<portlet:namespace/>selectFile').click();"><i class="icon-folder-open"> Open local...</i></a></li>
					<li><a href="javascript:<portlet:namespace/>openFileExplorer();"><i class="icon-folder-open"> Open server...</i></a></li>
					<li><a href="javascript:<portlet:namespace/>downloadCurrentFile();"><i class="icon-download-alt"> Download</i></a></li>
				</ul>
			</div>
		</div>
	</div>
	<div class="row-fluid canvas" id="<portlet:namespace/>canvasFrame">
		<iframe class ="col-sm-12 iframe-canvas" id="<portlet:namespace/>canvas"  src="<%=request.getContextPath()%>/html/testanalyzer/loadAnalyzer.jsp" style="border:0">
		</iframe>
	</div>
</div>
```

### 파일 다이얼로그 추가
서버와 연동되는 파일 처리를 위한 서버 파일 리스트를 볼 수 있는 다이얼로그를 띄울 수 있는 태그를 추가합니다.


또한 서버의 파일 리스트를 볼 수 있는 서버 파일 탐색기를 호출하게 됩니다. 이 서버 사이드 파일 탐색기는 EDISON 플랫폼에 탑재되어 있으며, 분석기를 개발하려면 호출하기만 하면 됩니다. 호출하는 함수는 `OSPFileExplorerportlet`로서 자바스크립트로 정의되어 있습니다.


```javascript
<div id="<portlet:namespace/>hiddenSection" class="osp-analyzer hidden">
	<div id="<portlet:namespace/>fileExplorer" class="panel panel-primary ui-draggable" style="padding:0px;margin-bottom:0px;">
		<!-- title -->
		<div class="panel-heading">
			<button type="button" class="close" data-dismiss="modal" aria-hidden="true" id='<portlet:namespace/>closeDialog'>&times;</button>
			<h4>Select a File</h4>
		</div>

		<!-- content -->
		<div class="panel-body" id="<portlet:namespace/>file-explorer-content" style="height: 81%"></div>


		<!-- bottom -->
		<div class="panel-footer">
			<div class="ui-dialog-buttonset">
				<input class="btn btn-primary" id="<portlet:namespace/>file-explorer-ok" type="button" value="OK">
				<input class="btn" id="<portlet:namespace/>file-explorer-cancel" type="button" value="Cancel">
			</div>
		</div>

	</div>
	<input type="file" id="<portlet:namespace/>selectFile"/>
</div>
```


### 파일 메뉴 이벤트 처리
- 로컬 파일 처리 함수

```javascript
$('#<portlet:namespace/>selectFile').bind(
	'change',
	function(event){
		var input = document.getElementById('<portlet:namespace/>selectFile');
		var reader = new FileReader();

		reader.onload = function (e) {
			$('#<portlet:namespace/>canvas').each(function(){
				$(this).prop('contentWindow').loadJSMolFile(e.target.result);
			});
	        console.log("[JSMOL] local file test : ", input);
			console.log("[JSMOL] local file test2 : ", input.files[0]);


			<portlet:namespace/>setTitle(input.files[0].name);
		};

		reader.readAsDataURL(input.files[0]);
	}
);
```

- 서버 파일 처리 함수
`initializeFileExplorer` 함수는 서버 파일 탐색기를 호출하기 위해 초기값을 설정하는 코드입니다.

```javascript
function <portlet:namespace/>initializeFileExplorer(){
if( $.isEmptyObject(<portlet:namespace/>initData) ||(
  <portlet:namespace/>initData.type() !== OSP.Enumeration.PathType.FILE &&
  <portlet:namespace/>initData.type() !== OSP.Enumeration.PathType.FOLDER &&
  <portlet:namespace/>initData.type() !== OSP.Enumeration.PathType.EXT ))	return;

var eventData = {
            portletId: '<%=portletDisplay.getId()%>',
            targetPortlet: <portlet:namespace/>fileExplorerId,
            data: OSP.Util.toJSON(<portlet:namespace/>initData)
};

Liferay.fire( 'OSP_LOAD_DATA', eventData );
}
```

`openFileExplorer`함수는 사용자가 서버 파일 오픈 메뉴를 선택하였을 때, 다이얼로그형태로 사용자에게 서버쪽 파일 리스트를 탐색한 내용을 업데이트 하여 보여주는 함수 부분입니다.

```javascript
function <portlet:namespace/>openFileExplorer(){
	AUI().use('liferay-portlet-url', function(A){
		if($("#<portlet:namespace/>file-explorer-content").children().length > 0){
			$<portlet:namespace/>fileExplorerDialogSection.dialog("open");
		}else{
			var inputData;
			if(	!$.isEmptyObject(<portlet:namespace/>initData) && (
				<portlet:namespace/>initData.type() === OSP.Enumeration.PathType.FILE ||
				<portlet:namespace/>initData.type() === OSP.Enumeration.PathType.FOLDER ||
				<portlet:namespace/>initData.type() === OSP.Enumeration.PathType.EXT )){
				inputData = <portlet:namespace/>initData;
			}
			else{
				inputData = new OSP.InputData();
				inputData.repositoryType( '<%=OSPRepositoryTypes.USER_HOME.toString()%>' );
				inputData.type( OSP.Enumeration.PathType.FOLDER );
				inputData.parent('');
				inputData.name('');
			}

			var dialogURL = Liferay.PortletURL.createRenderURL();
			dialogURL.setPortletId(<portlet:namespace/>fileExplorerId);
			dialogURL.setParameter('inputData', JSON.stringify(inputData));
			dialogURL.setParameter('mode', 'VIEW');
			dialogURL.setParameter('eventEnable', false);
			dialogURL.setParameter('connector', '<%=portletDisplay.getId()%>');
			dialogURL.setWindowState('<%=LiferayWindowState.EXCLUSIVE%>');

			$("#<portlet:namespace/>file-explorer-content").load( dialogURL.toString());
			$<portlet:namespace/>fileExplorerDialogSection.dialog("open");
		}
	});
}
```


- 현재 파일 다운로드
현재 선택되어 있는 파일을 다운로드 하는 함수입니다.

```javascript
function <portlet:namespace/>downloadCurrentFile(){
console.log("[testView] Download current data", <portlet:namespace/>currentData);
if( $.isEmptyObject(<portlet:namespace/>currentData) ||
  <portlet:namespace/>currentData.type() !== OSP.Enumeration.PathType.FILE )
  return;

var filePath = <portlet:namespace/>currentData;
var data = {
  <portlet:namespace/>command: "DOWNLOAD_FILE",
  <portlet:namespace/>pathType: filePath.type_,
  <portlet:namespace/>repositoryType: filePath.repositoryType_,
  <portlet:namespace/>parentPath: filePath.parent_,
  <portlet:namespace/>fileName: filePath.name_
};


var base = '<%=serveResourceURL.toString()%>';
var sep = (base.indexOf('?') > -1) ? '&' : '?';
var url = base + sep + $.param(data);

location.href = url;
<portlet:namespace/>loadXXXXFile( <portlet:namespace/>currentData );
}
```
