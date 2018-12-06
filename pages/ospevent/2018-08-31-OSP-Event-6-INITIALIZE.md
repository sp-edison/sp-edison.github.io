---
title: INITIAIZE EVENT
permalink: /event_initialize.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary:
---

### OSP INITIAIZE 이벤트
워크벤치가 실행된 이후, 초기화 값을 셋팅하는 이벤트 입니다. 워크벤치가 실행되고 시뮬레이션 실행 환경이 구성되고 난 뒤, 각 편집기나 분석기에서는 필요한 값들의 초기화를 진행하는데 이 때 사용되는 이벤트입니다.

- 샘플 예제
```javascript
Liferay.on(
	'OSP_INITIALIZE',
	function(e){
		var myId = '<%=portletDisplay.getId()%>';
		if( e.targetPortlet !== myId )	return;
		<portlet:namespace/>initializeFileExplorer();
	}
);
```
