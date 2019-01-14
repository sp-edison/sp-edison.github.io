---
title: HANDSHAKE
permalink: /event_handshake.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary: 초기 워크벤치를 실행하면서 필요한 편집기와 분석기 모듈들을 호출합니다. 해당 편집기와 분석기는 실행되기 전에 HANDSHAKE 이벤트를 워크벤치로부터 받아 현재 상태 및 아이디를 등록을 하게 됩니다.
---

### OSP HADNSHAKE 이벤트
초기 워크벤치를 실행하면서 필요한 편집기와 분석기 모듈들을 호출합니다. 해당 편집기와 분석기는 실행되기 전에 HANDSHAKE 이벤트를 워크벤치로부터 받아 현재 상태 및 아이디를 등록을 하게 됩니다.


해당 HANDSHAKE 등록 과정에서 편집기 또는 분석기 모듈은 워크벤치의 아이디를 등록하게 되며, 앞으로 발생되는 이벤트에 대해 이벤트를 보내고자 하는 목적지의 주소와 같은 역할을 하게 됩니다.

- 샘플 예제
```javascript
Liferay.on(
  	OSP.Event.OSP_HANDSHAKE,
  	function(e){
  		var myId = '<%=portletDisplay.getId()%>';
  		if( e.targetPortlet !== myId ){
  			return
  		}
  		console.log('[NGLViewer]OSP_HANDSHAKE: ['+e.portletId+', '+new Date()+']');
  		<portlet:namespace/>connector = e.portletId;

  		if( e.mode )
  			<portlet:namespace/>action = e.mode;
  		else
  			<portlet:namespace/>action = 'VIEW';
  		var events = [
  			OSP.Event.OSP_EVENTS_REGISTERED,
  			OSP.Event.OSP_LOAD_DATA
  		];
  		var eventData = {
  			portletId: myId,
  			targetPortlet: <portlet:namespace/>connector,
  			data: events
		};
		Liferay.fire( OSP.Event.OSP_REGISTER_EVENTS, eventData );
	}
);
```
