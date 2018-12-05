---
title: "스크립트 단위의 뷰 설정"
permalink: workbenchanalyzerguide5.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---


EDISON 워크벤치와 연동을 하며 워크벤치에서 요구하는 이벤트를 처리하기 위해서는 기본적으로 셋팅이 완료되어야 하는 몇 가지 초기 값이 있습니다.


### 데이터 전송 및 라이브러리 사용
다음은 데이터 전송 및 기타 라이브러리들을 사용하기 위한 기본 코드 입니다.
`testview.jsp`파일 내부에 제일 위쪽 부분에 해당 라이브러리 호출 부분을 포함합니다.
```javascript
<%@page import="com.kisti.osp.constants.OSPRepositoryTypes"%>
<%@page import="com.liferay.portal.kernel.util.GetterUtil"%>
<%@page import="com.liferay.portal.util.PortalUtil"%>
<%@page import="com.liferay.portal.kernel.portlet.LiferayWindowState"%>
<%@page import="javax.portlet.PortletPreferences"%>
<%@include file="../init.jsp"%>
```


### 라이프레이 URL 추가
라이프레이 데이터 전송 방식을 사용하기 위한 URL을 추가합니다.

데이터 전송을 위한 Liferay 포틀릿의 URL은 resourceURL입니다.
```javascript
<portlet:resourceURL var="serveResourceURL"></portlet:resourceURL>
<portlet:renderURL var="renderURL">
    <portlet:param name="jspPage" value="/html/testanalyzer/testview.jsp"/>
</portlet:renderURL>
```

### 초기 데이터 셋팅을 위한 코드 추가
워크벤치와 연동외어 동작하기 위해 필요한 기본값들의 초기 셋팅 값입니다.
이벤트 처리를 하는 워크벤치와 연동을 할 것인지 아니면 독립적으로 사용자에게 제공되어 동작할 것인지 호출하고 세팅하는 값이 포함되어 있습니다.
```javascript
<%
PortletPreferences preferences = portletDisplay.getPortletSetup();
preferences.setValue("portletSetupShowBorders", String.valueOf(Boolean.FALSE));
preferences.store();

String inputData = GetterUtil.getString(renderRequest.getAttribute("inputData"), "{}");
String connector = (String)renderRequest.getAttribute("connector");
String mode = GetterUtil.getString(renderRequest.getAttribute("mode"), "VIEW");
boolean eventEnable = GetterUtil.getBoolean(renderRequest.getAttribute("eventEnable"), true);
%>
```


### 가시화 태그
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
