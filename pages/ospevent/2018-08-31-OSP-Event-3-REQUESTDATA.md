---
title: REQUEST DATA EVENT
permalink: /event_requestdata.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary:
---

### OSP REQUEST DATA 이벤트
사용자가 서버에 저장된 파일을 선택하거나 새로운 데이터를 로드하고자 할 때, 분석기나 편집기에서는 새로운 데이터를 요청해야 합니다. 따라서 분석기나 편집기에서는 새로운 데이터를 요청하는 이벤트를 발생시키고, 해당 이벤트를 받아 새로운 데이터를 받아오게 됩니다.
- 샘플 예제
```javascript
Liferay.on(
		OSP.Event.OSP_REQUEST_DATA,
		function(e){
			var myId = '<%=portletDisplay.getId()%>';
			if( e.targetPortlet === myId ){
				var iframe = document.getElementById('<portlet:namespace/>TBox');
				var eventData = {
						portletId: myId,
						targetPortlet: e.portletId,
						data: {
							type_: OSP.Enumeration.PathType.FILE_CONTENT,
							context_: iframe.contentWindow.getParameters(),
							params: e.params
						}
				}				
				Liferay.fire(OSP.Event.OSP_RESPONSE_DATA, eventData);
			}
		}
);
```
