---
title: "이벤트 처리 함수"
permalink: workbenchanalyzerguide7.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---


### 이벤트 처리
개발하려는 분석기는 Liferay 에서 제공하는 이벤트 전송 및 수신 함수(Liferay.on(), Liferay.fire())를 사용하여 워크벤치와 연동하여 동작합니다. 자바 스크립트 단위로 동작을 하기 때문에 개발하려는 분석기 내에 필요한 이벤트를 처리하고 발생시키는 루틴을 넣어야 합니다.

분석기에서 사용되는 이벤트의 종류와 설명은 아래와 같습니다.

| 이벤트명                            | 정의                                                                                        |
|:------------------------------------|:--------------------------------------------------------------------------------------------|
|OSP.Event.OSP_HANDSHAKE              |  초기 워크벤치에 해당 모듈을 등록 하고 초기 설정값을 워크벤치로 부터 받을 때 쓰는 이벤트    |
|OSP.Event.OSP_Event_REGISTERED       |  초기 OSP_HANDSHAKE에 대한 워크벤치의 결과 응답 이벤트                                      |
|OSP.Event.OSP_LOAD_DATA              |  특정 위치와 파일에 대한 데이터 로드 이벤트                                                 |
|OSP.Event.OSP_RESPONSE_DATA          |  사용자가 파일 익스플로러에서 선택한 파일에 대한 응답 이벤트                                |
|OSP.Event.OSP_REFRESH_OUTPUT_VIEW    |  포틀릿 아이디 공유를 위한 이벤트                                                           |
|OSP.Event.OSP_INITIALIZE             |  워크벤치에서 보내는 초기화 값 설정을 위한 이벤트                                           |

**이벤트처리함수** <br> 일단 개발하려는 분석기가 동작하기 위해서는 위의 이벤트를 워크벤치로부터 받아서 처리하는 루틴이 필수적으로 필요합니다. 따라서 기본으로 해당 이벤트를 처리하는 코드를 작성하고 나머지 가시화 및 분석을 위한 코드를 추가하는 것이 좋습니다.
{: .notice--info}

### OSP.Event.OSP_HANDSHAKE
처음 워크벤치가 실행되면서 각 포틀릿에게 OSP.Event.OSP_HANDSHAKE이벤트를 보내게 됩니다. 따라서 워크벤치와 연동되는 분석기를 개발하기 위해서는 OSP.Event.OSP_HANDSHAKE 이벤트를 받아서 다시 워크벤치에게 전달하는 루틴이 필요합니다.
아래 코드에서 볼 수 있듯이, OSP.Event.OSP_HANDSHAKE이벤트를 받아들이고 현재 동작중인 분석기를 워크벤치에 등록시키는 과정을 포함합니다.

```javascript
Liferay.on(
  	OSP.Event.OSP_HANDSHAKE,
  	function(e){
  		var myId = '<%=portletDisplay.getId()%>';
  		if( e.targetPortlet !== myId ){
  			return
  		}
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


### OSP.Event.OSP_Event_REGISTERED
OSP_HANDSHAKE 이벤트의 결과에 대한 이벤트입니다. 간단하게 이벤트를 받아들여 체크하는 정도의 코드만 추가하면 됩니다.

```javascript
Liferay.on(
	OSP.Event.OSP_EVENTS_REGISTERED,
	function(e){
		var myId = '<%=portletDisplay.getId()%>';
		if(e.targetPortlet === myId){
			console.log('[TestView]Regestered'+e.portletId+' activated. '+new Date()+']');
		}
	}
);
```
### OSP.Event.OSP_LOAD_DATA
데이터를 로드하기 위한 함수입니다. 워크벤치를 기반으로 하여 시뮬레이션을 수행하는데 있어, 시뮬레이션이 성공적으로 종료되었거나 이전에 실행한 성공한 시뮬레이션 잡의 결과 데이터를 가져오기 위한 이벤트 처리 부분 입니다.

워크벤치에서 데이터를 로드라하고 이벤트를 발생시키고, 해당 이벤트를 받아 분석기에서는 데이터를 로드하여 분석할 수 있도록 시각화를 하면 됩니다.

- `<portlet:namespace/>initialize(e.data);`에서는 초기 데이터 셋팅 값을 받은 이벤트 데이터를 기반으로 설정합니다.
- `<portlet:namespace/>loadTestviewFile(<portlet:namespace/>initData.clone());`코드는 실제 데이터를 가져와 가시화를 하기 위한 코드입니다.
- `<portlet:namespace/>initializeFileExplorer();`코드는 현재 받은 이벤트 데이터를 기반으로 서버와 연결된 파일 익스프로러의 값을 재설정 하는 부분입니다.


```javascript
Liferay.on(
	OSP.Event.OSP_LOAD_DATA,
	function(e){
		var myId = '<%=portletDisplay.getId()%>';
		if( e.targetPortlet !== myId )
			return;

		<portlet:namespace/>initialize(e.data);
		<portlet:namespace/>loadTestviewFile(<portlet:namespace/>initData.clone());

		<portlet:namespace/>initializeFileExplorer();

	}
);
```

### OSP.Event.OSP_RESPONSE_DATA
사용자가 서버와 연동된 파일 익스플로러에서 선택한 파일에 대한 응답 이벤트 코드입니다. 사용자가 파일을 선택하면 해당 파일 데이터를 읽어오기 위한 이벤트 처리 부분입니다.
```javascript
Liferay.on(
	OSP.Event.OSP_RESPONSE_DATA,
	function( e ){
		var myId = '<%=portletDisplay.getId()%>';
		if( myId !== e.targetPortlet ) return;

		var inputData = new OSP.InputData( e.data );

		if( inputData.type() !== OSP.Enumeration.PathType.FILE ){
			alert( 'File should be selected!' );
			return;
		}else{
			<portlet:namespace/>loadTestviewFile( inputData );
			$<portlet:namespace/>fileExplorerDialogSection.dialog('close');
		}
	}		
);
```

### OSP.Event.OSP_REFRESH_OUTPUT_VIEW
포틀릿의 아이디를 공유하기 위한 이벤트 처리 부분입니다.
```javascript
Liferay.on(
		OSP.Event.OSP_REFRESH_OUTPUT_VIEW,
		function(e){
			var myId = '<%=portletDisplay.getId()%>';
			if( myId !== e.targetPortlet ) return;

			var eventData = {
					portletId: '<%=portletDisplay.getId()%>',
					targetPortlet: <portlet:namespace/>connector
			};

			Liferay.fire(OSP.Event.OSP_REQUEST_OUTPUT_PATH, eventData);
		}
);
```

### OSP.Event.OSP_INITIALIZE
처음 HANDSHAKE 이벤트를 처리하면서 내부저긍로 서버와 연동된 파일 익스플로러를 초기화 시키는 코드입니다.
```javascript
Liferay.on(
	OSP.Event.OSP_INITIALIZE,
	function(e){
		var myId = '<%=portletDisplay.getId()%>';
		if(myId !== e.targetPortlet) return;


		if( $.isEmptyObject(<portlet:namespace/>initData) )	return;
		<portlet:namespace/>initializeFileExplorer( <portlet:namespace/>initData.clone() );
	}
);
```
