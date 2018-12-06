---
title: REGISTERED EVENT
permalink: /event_registerd.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary:
---

### OSP REGISTERED 이벤트

- 샘플 예제
```javascript
Liferay.on(
	OSP.Event.OSP_EVENTS_REGISTERED,
	function(e){
		var myId = '<%=portletDisplay.getId()%>';
		if(e.targetPortlet === myId){
			console.log('[NGLViewer]Regestered'+e.portletId+' activated. '+new Date()+']');
		}
	}
);
```
