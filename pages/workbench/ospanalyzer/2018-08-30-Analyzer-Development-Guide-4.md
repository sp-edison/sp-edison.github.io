---
title: "분석기 구조 설명"
permalink: workbenchan_alyzerguide4.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---
DISON 플랫폼에서 워크벤치와 연동되는 분석기는 모듈 단위로 개발 될 수 있으며, 각 모듈은 Liferay 포틀릿으로 구분됩다.
각 포틀릿에서 생성된 가시화 및 서비스 등은 EDISON 플랫폼에서 제공되는 서비스와 연동되어 개발될 수 있습니다.


### 분석기와 EDISON 연동 시스템 구조
EDSION 워크벤치 시뮬레이션 시스템과 연동되는 시스템 구조는 다음 그림과 같이 표현될 수 있습니다.


![imagetestYejin](/images/analyzerguide/analyzer architecture.png "연동 구조")<br>

분석기는 전체 이벤트를 처리하는 이벤트 처리부분과 내부적으로 데이터를 가시화하고 분석 할 수 있는 Analyzer 구현 부분으로 나눠질 수 있습니다.

EDISON 플랫폼에서 파생되는 이벤트를 받아들이고 적절한 시기에 사용자에게 데이터 분석을 위한 툴을 제공하는 부분을 포함하고 있습니다.

따라서 EDISON 워크벤치와 연동되는 분석기 모듈을 개발하기 위해서는 이벤트를 처리하는 부분과 실제 데이터 가시활르 위한 부분을 나눠서 개발을 해야 합니다.


### 분석기 이벤트 처리 부분
워크벤치의 분석기를 개발 하는데 있어 이벤트를 처리하는 부분은 자바 스크립트로 이루어져 있으며, Liferay 포틀릿 기반으로 이벤트를 받아들입니다.

다음 예제 코드는 워크벤치가 실행되면서 분석기를 호출하고 이에 대한 응답을 하는 코드입니다.
Liferay 에서 제공하는 `Liferay.fire()`함수와 `Liferay.on()`기반으로 이벤트 프로세싱을 제공합니다.

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

- `Liferay.fire()` : 이벤트를 발생시키는 Liferay 자바스크립트 라이브러리 함수입니다.
- `Liferay.on()` : 이벤트를 리스닝 하는 Liferay 자바스크립트 라이브러리 함수입니다.

### 데이터 처리 부분

실제 서버에서 계산과학공학 시뮬레이션이 실행되고 결과 값을 분석하기 위해서는 시뮬레이션 결과를 호출하고 적절한 데이터를 받아 가시화 하는 데이터 처리 구현 부분입니다.
계산 결과 데이터를 수신하고 가시화 하기 위해서는 데이터 호출 및 응답에 대한 코드 구현이 필수적입니다.

이미 이전 단계에서 추가한 OSP 라이브러리를 기반으로 데이터를 호출하고 적절한 데이터를 받는 코드 부분이 구현 되어야 합니다.

이러한 데이터를 구현하기 위해서는 다양한 스크립트 함수들이 필요하며, 해당 함수들을 순차대로 정리하면 다음과 같습니다.


### 데이터 처리를 위해 정의가 필요한 함수


| 함수명                            | 정의                                                                                                                                                           |
|:----------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------|
|loadXXXXFile(OSPInputData)         |  실제 서버 사이드의 파일을 읽어오는 방법에 대한 정의<br>Output 포트의  path  타입에 따라 케이스를 나눠 처리 방법에 대한 정의가 되어 있음<br> 폴더/확장자/파일  |
|getFirstFileName(OSPInputData)     |  결과 포트의 path  타일이 폴더 또는 확장자인 경우, 해당 폴더 내 첫번째 파일을 읽어오는 역할이 정의                                                             |

{: rules="groups"}

{{site.data.alerts.callout_info}}<b>데이터 처리 방법</b> <br> 서버에서 시뮬레이션 결과로 생성된 결과 데이터는 OSP 라이브러리를 이용하여 전송받을 수 있으며, 해당 데이터를 받은 다음 iframe 으로 연결된 실제 데이터 가시봐 부분에 데이터를 전공하는 방법으로 분석기가 동작하게 됩니다.
