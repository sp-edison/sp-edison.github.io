---
title: REQUEST DATA CHANGED EVENT
permalink: /event_datachanged.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary:
---


### OSP DATA CHANGED 이벤트
해당하는 포틀릿이 편집기인 경우, 사용자의 입력을 받게 됩니다. 사용자의 입력을 받아 입력 데이터가 변경되게 되면 해당 데이터의 변경을 워크벤치에 알려야 합니다.
따라서 사용자의 입력에 따라 변경된 데이터를 JSON의 형태로 이벤트를 발생시켜 워크벤치에 전달합니다.

- 샘플 예제
```javascript
function <portlet:namespace/>fireTextChangedEvent( data ){
		<portlet:namespace/>ViewStructure();

		var inputData = new OSP.InputData();
		inputData.type( OSP.Enumeration.PathType.FILE_CONTENT );
		if( $.isEmptyObject(<portlet:namespace/>initData) ){
			inputData.repositoryType('<%=OSPRepositoryTypes.USER_HOME.toString()%>');
		}
		else if( <portlet:namespace/>initData.repositoryType_ ){
			console.log("[ATOM EDITOR] test re[psotpry Type]]", <portlet:namespace/>initData);
			inputData.repositoryType(<portlet:namespace/>initData.repositoryType_);
		}
		else{
			inputData.repositoryType('<%=OSPRepositoryTypes.USER_HOME.toString()%>');
		}
		inputData.context( data );


		var eventData = {
		     			portletId: '<%=portletDisplay.getId()%>',
		     			targetPortlet: <portlet:namespace/>connector,
		     			data: OSP.Util.toJSON(inputData)
		};
		Liferay.fire( OSP.Event.OSP_DATA_CHANGED, eventData );
}
```
