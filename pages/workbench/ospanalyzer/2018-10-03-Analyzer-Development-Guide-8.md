---
title: "공용 함수"
permalink: workbench_analyzerguide8.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---


### 공용함수
이벤트에 대한 응답이나 데이터를 처리하고 실제 가시화를 하기 위한 공용 함수들이 필요합니다. 예를 들어 워크벤치와 연동되어 시뮬레이션을 수행할 때, 시뮬레이션이 종료되고 결과를 확인하기 위해서는 워크벤치에서 데이터를 로드하라는 OSP_LOAD_DATA 이벤트를 분석기에 보내게 됩니다.

해당 이벤트를 해석하고 데이터를 로드하는 함수를 정의하고 로드된 데이터를 통해 시뮬레이션 분석을 위한 가시화를 진행할 수 있습니다. 따라서 데이터를 처리하고 파일을 분석하는 내용에 대한 공용 함수를 정의합니다.

분석기에서 사용되는 함수의 종류와 설명은 아래와 같습니다.

| 함수명                              | 정의                                                                                                                                        |
|:------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------|
|loadXXXXXXFile(OSPInputData)         |  실제 서버쪽의 파일을 읽어오는 방법에 대한 정의<br>Output 포트의 path 타입에 따라 케이스를 나누고 처리 방법에 대한 정의가 되어 있음         |
|getFirstFileName(OSPInputData)       |  Output 포트의 파일 타입이 폴더이거나 확장자일 경우 해당 결과 result 폴더에서 첫 번 째 파일을 읽어오도록 정의                               |
|drawXXXXXXView()                     |  서버와 연동되어서 선택된 파일을 실제 뷰 부분의 iframe 내부로 전달하여 가시화 함                                                            |
|initializeFileExplorer()             |  서버와 연결된 파일 익스플로러 초기값 설정                                                                                                  |
|DownloadCurrentFile()                |  현재 사용자가 파일 익스플로러에서 선택한 파일을 다운로드                                                                                   |


### loadXXXXXXFile(OSPInputData)
```javascript
function <portlet:namespace/>loadTestviewFile( inputData ){
	<portlet:namespace/>currentData = inputData;
	console.log("[testView] Load Data : input Data ", inputData);
	switch( inputData.type() ){
	case OSP.Enumeration.PathType.FILE:
	    <portlet:namespace/>drawView( inputData );
		break;
	case OSP.Enumeration.PathType.FOLDER:
	case OSP.Enumeration.PathType.EXT:
	    <portlet:namespace/>getFirstFileName( inputData );
	    // serveResourceUrl.setParameter('command', 'READ_FIRST_FILE');
		break;
	case OSP.Enumeration.PathType.URL:
		alert('Un supported yet.'+inputData.type());
		break;
	default:
		alert('Un supported yet.'+inputData.type());
	}
}
```
### drawXXXXXXView()
```javascript
function <portlet:namespace/>drawView( inputData ){
    setTimeout(
	    function(){
	    	var iframe = document.getElementById('<portlet:namespace/>canvas');
	    	var iframeDoc = iframe.contentDocument || iframe.contentWindow.document;

	    	console.log( '[testView]iframeDoc.readyState : ', iframeDoc.readyState);
	    	if (  iframeDoc.readyState  == 'complete' && iframe.contentWindow.drawTestViewer ) {

	    		console.log("[testView]  Load data in draw");
	    	    AUI().use('liferay-portlet-url', function(a) {
	                <portlet:namespace/>currentData = inputData.clone();
	                if( !<portlet:namespace/>currentData.repositoryType() )
	                	<portlet:namespace/>currentData.repositoryType('<%=OSPRepositoryTypes.USER_JOBS.toString()%>');

	    	        var serveResourceUrl = Liferay.PortletURL.createResourceURL();

	    	        serveResourceUrl.setPortletId('<%=portletDisplay.getId()%>');
	    	        serveResourceUrl.setParameter('command', 'GET_FILE');
	    	        serveResourceUrl.setParameter('repositoryType', <portlet:namespace/>currentData.repositoryType());
	    	        serveResourceUrl.setParameter('pathType', inputData.type());
	    	        serveResourceUrl.setParameter('parentPath', inputData.parent());
	    	        serveResourceUrl.setParameter('fileName', inputData.name());
	    	        serveResourceUrl.setParameter('relative', inputData.relative());

	    	        console.log( '[testView]Draw Input Data : ', inputData);

		    	    iframe.contentWindow.drawTestViewer(inputData, serveResourceUrl.toString());

		    	    $('#<portlet:namespace/>title').html(inputData.name());
	    	    });
	    	}
	    	else{
	    		console.log("[testView] test esle : load data in draw");

	    		<portlet:namespace/>drawView( inputData );
	    	}
	    },
	    10
	);
}
```
### getFirstFileName(OSPInputData)
```javascript
function <portlet:namespace/>getFirstFileName( inputData ){
	console.log('[testView]get First File Name : ', inputData );

	var data = {
		<portlet:namespace/>command: 'GET_FIRST_FILE_NAME',
		<portlet:namespace/>pathType: inputData.type_,
		<portlet:namespace/>repositoryType: inputData.repositoryType_,
		<portlet:namespace/>parentPath: inputData.parent_,
		<portlet:namespace/>fileName: inputData.name_
	};
    console.log("[testView] laod get first file test : ", data);

	$.ajax({
		url: '<%= serveResourceURL.toString()%>',
		type: 'POST',
		data  : data,
		dataType : 'json',
		success: function(data) {
			console.log("[testView] get result data ", data);
			inputData.name( data.fileName );
			inputData.type( OSP.Enumeration.PathType.FILE );
			<portlet:namespace/>drawView( inputData );
			console.log("[testView] Get First File Data : ", inputData);
		},
		error:function(data,e){
			console.log('[testView]AJAX ERROR1-->', data);
			console.log('[testView]AJAX ERROR2-->', e);
		},
		complete: function( jqXHR, textStatus ){
			console.log('[testView]AJAX complete ', jqXHR);
		}
	});
}
```
### initializeFileExplorer()
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
### DownloadCurrentFile()
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
	<portlet:namespace/>loadJSMolFile( <portlet:namespace/>currentData );

}
```

### 최종 파일 구조
지금까지 기본 설정을 마친 후 최종적인 파일 구조는 다음 그림과 같습니다.
![imagetestYejin](/images/analyzerguide/17.png "프로젝트 최종구조")<br><br>
