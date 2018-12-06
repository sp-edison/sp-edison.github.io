---
title: LOAD DATA EVENT
permalink: /event_loaddata.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary:
---


### OSP LOAD DATA 이벤트
편집기 또는 분석기에서 데이터를 로드할 때 사용되는 이벤트로, 서버에 저장되어 있는 파일을 로드하거나 시뮬레이션 결과 데이터를 로드할 때 쓰이는 이벤트입니다.

사용자가 서버쪽 파일을 선택하거나 시뮬레이션이 성공적으로 종료되는 상황에서 워크벤치에서 이벤트를 발생시키며, 이벤트 데이터 내 파일 경로에 따라 파일을 읽어 들이는 프로세스를 거쳐 사용자에게 보여줍니다.

- 샘플 예제
```javascript
Liferay.on(
	'OSP_LOAD_DATA',
	function(e){
		var myId = '<%=portletDisplay.getId()%>';
		console.log("[ATOM EDITOR] OSP LOAD DATA :", myId, e.targetPortlet );
		if( e.targetPortlet !== myId )	return;

		<portlet:namespace/>initData = e.data;
		if( ! <portlet:namespace/>initData.repositoryType_){
			<portlet:namespace/>initData.repositoryType_ = 'USER_HOME';
		}
		<portlet:namespace/>loadEPDEditor( OSP.Util.toJSON(<portlet:namespace/>initData) );
		<portlet:namespace/>initializeFileExplorer();
	}
);
```
