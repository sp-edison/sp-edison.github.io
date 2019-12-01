---
title: "포틀릿 xml 파일 설정"
permalink: workbench_analyzerguide3.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
summary: 에디슨 워크벤치 기반 후처리기(Post-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 분석기(Post-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## 1. liferay-portlet.xml 설정
포틀릿 구성 정보의 설정을 위해 xml 파일 설정을 합니다.
이전 단계에서 설명한 바와 같이 포틀릿의 구성 정보를 설정하는 `TestVisualizerConfiguration.java` 파일을 추가하였습니다. <br>
해당 파일과 포틀릿을 연결시키기 위해 `liferay-portlet.xml`파일에 해당 내용을 추가합니다.<br>

추가해야 하는 내용은 다음과 같습니다.<br>
```xml
<configuration-action-class>org.kisti.post.visualizer.TestVisualizerConfiguration</configuration-action-class>
```
`configuration-action-class`로 이전 단계에서 생성한 `TestVisualizerConfiguration` 클래스를 생성합니다.
또한 생성된 포틀릿의 내부 태그 안에 포합시켜야 합니다.<br>

또한 개발하려는 포틀릿이 워크벤치 서비스에서 호출되어 사용되기 위해서는, 외부 코드에서 포틀릿의 호출이 가능해야 합니다.<br>
개발되는 포틀릿을 기본 라이프레이의 리소스로 설정하는 코드는 아래와 같습니다.
```xml
<add-default-resource>true</add-default-resource>
```

전체 `liferay-portlet.xml`의 코드를 확인하면 다음과 같습니다.<br>
```xml
<?xml version="1.0"?>
<!DOCTYPE liferay-portlet-app PUBLIC "-//Liferay//DTD Portlet Application 6.2.0//EN" "http://www.liferay.com/dtd/liferay-portlet-app_6_2_0.dtd">

<liferay-portlet-app>
	
	<portlet>
		<portlet-name>test-visualizer</portlet-name>
		<icon>/icon.png</icon>
		<configuration-action-class>org.kisti.post.visualizer.TestVisualizerConfiguration</configuration-action-class>
		<header-portlet-css>/css/main.css</header-portlet-css>
		<footer-portlet-javascript>
			/js/main.js
		</footer-portlet-javascript>
		<css-class-wrapper>test-visualizer-portlet</css-class-wrapper>
		<add-default-resource>true</add-default-resource>
	</portlet>
	<role-mapper>
		<role-name>administrator</role-name>
		<role-link>Administrator</role-link>
	</role-mapper>
	<role-mapper>
		<role-name>guest</role-name>
		<role-link>Guest</role-link>
	</role-mapper>
	<role-mapper>
		<role-name>power-user</role-name>
		<role-link>Power User</role-link>
	</role-mapper>
	<role-mapper>
		<role-name>user</role-name>
		<role-link>User</role-link>
	</role-mapper>
</liferay-portlet-app>
```

## 2. Configuration.jsp 파일 생성
라이프레이 기본적으로 구성되는 프로젝트 구조에서 `/html/testvisualizer`폴더 내에 Configuration.jsp 파일을 추가합니다.
공용으로 사용되는 파일로, 동일한 소스코드를 추가하면 됩니다.<br>


포틀릿의 높이, 너비를 설정하고, 파일 관련 메뉴를 추가하거나 설정을 취소할 수 있습니다.<br>
```html
<%@page import="com.kisti.osp.constants.OSPRepositoryTypes"%>
<%@page import="com.liferay.portal.kernel.util.Constants"%>
<%@page import="com.liferay.portal.kernel.util.StringPool"%>
<%@page import="com.liferay.portal.kernel.util.GetterUtil"%>
<%@ include file="../init.jsp" %>

<liferay-portlet:actionURL portletConfiguration="true" var="configurationURL" />

<%  
String portletWidth = GetterUtil.getString(portletPreferences.getValue("portletWidth", "100%"));
String portletHeight = GetterUtil.getString(portletPreferences.getValue("portletHeight", "400px"));
String portletScroll = GetterUtil.getString(portletPreferences.getValue("portletScroll", "hidden"));
boolean menu = GetterUtil.getBoolean(portletPreferences.getValue("menu", "true"));
boolean sample = GetterUtil.getBoolean(portletPreferences.getValue("sample", "true"));
boolean openLocalFile = GetterUtil.getBoolean(portletPreferences.getValue("openLocalFile", "true"));
boolean openServerFile = GetterUtil.getBoolean(portletPreferences.getValue("openServerFile", "true"));
boolean save = GetterUtil.getBoolean(portletPreferences.getValue("save", "true"));
boolean saveAtLocal = GetterUtil.getBoolean(portletPreferences.getValue("saveAtLocal", "true"));
boolean download = GetterUtil.getBoolean(portletPreferences.getValue("download", "true"));
boolean upload = GetterUtil.getBoolean(portletPreferences.getValue("upload", "true"));
boolean hidden = portletScroll.equals("hidden");
boolean auto = portletScroll.equals("auto");

String portletRepository = GetterUtil.getString(portletPreferences.getValue("portletRepository", OSPRepositoryTypes.USER_HOME.toString()));
%>

<aui:form action="<%= configurationURL %>" method="post" name="fm"> 
<aui:input name="<%= Constants.CMD %>" type="hidden" value="<%= Constants.UPDATE %>" />

<!-- Preference control goes here -->
<div class="container-fluid">

<div class="row-fluid">
<div class="col-sm-6">
<fieldset>
	<legend>Portlet Size</legend>
	<div class="row-fluid">
	<div class="col-sm-6">
	<aui:input label="Portlet Width:" name="preferences--portletWidth--" type="text" value="<%= portletWidth %>" />
	</div>
	<div class="col-sm-6">
	<aui:input label="Portlet Height:"  name="preferences--portletHeight--" type="text" value="<%= portletHeight %>" />
	</div>
	</div>
</fieldset><br>

<div class="row-fluid">  
<div class="col-sm-6">
	<fieldset>
		<legend>Scrolls</legend>
		<aui:select label="Portlet Scroll:" name="preferences--portletScroll--">
		<aui:option value="hidden" selected="<%=hidden %>">hidden</aui:option>
		<aui:option value="auto" selected="<%=auto %>">auto</aui:option>
		</aui:select>
	</fieldset>
</div>
</div>
<br>
</div>

<div class="col-sm-6">
	<fieldset>
		<legend>Show Menu</legend>
		<aui:input type="checkbox" name="preferences--menu--" value="<%=menu%>" label="Menu"/>
		<div style="border:solid grey 1px;">
		<aui:input type="checkbox" name="preferences--sample--" value="<%=sample%>" label="Sample"/>
		<aui:input type="checkbox" name="preferences--openLocalFile--" value="<%=openLocalFile%>" label="Open Local File"/>
		<aui:input type="checkbox" name="preferences--openServerFile--" value="<%=openServerFile%>" label="Open Server File"/>
		<aui:input type="checkbox" name="preferences--save--" value="<%=save%>" label="Save At Server"/>
		<aui:input type="checkbox" name="preferences--saveAtLocal--" value="<%=saveAtLocal%>" label="Save At Local"/>
		<aui:input type="checkbox" name="preferences--download--" value="<%=download%>" label="Download"/>
		<aui:input type="checkbox" name="preferences--upload--" value="<%=upload%>" label="Upload"/>
		</div>
	</fieldset>
	<br>
	</div>
</div>


<div class="row-fluid">
<div class="col-sm-6">
	<fieldset id="fieldset">
		<legend>Repository</legend>
		<aui:select label="Portlet Repository" name="preferences--portletRepository--">
		<aui:option value="<%= OSPRepositoryTypes.USER_HOME.toString() %>"
		selected="<%=portletRepository.equals(OSPRepositoryTypes.USER_HOME.toString()) %>">User Home</aui:option>
		<aui:option value="<%= OSPRepositoryTypes.USER_JOBS.toString() %>"
		selected="<%=portletRepository.equals(OSPRepositoryTypes.USER_JOBS.toString()) %>">User Jobs</aui:option>
		</aui:select>
	</fieldset>
</div>
</div>

<div class="row-fluid">
	<div class="col-sm-12 text-center">
		<aui:button type="submit" value="Save" class="btn btn-primaryl"/>
	</div>
</div>
</div>
</aui:form>

</script>
```



## 3. portlet.xml 파일 설정
`liferay-portlet.xml`에서 포틀릿 구성정보 설정을 위한 클래스 연결을 지정하였습니다.
이와 마찬가지로 `portlet.xml`내에 configuration 파라밑터를 설정해야 합니다.
추가해야 하는 xml 코드는 다음과 같습니다.<br>

```xml
<init-param>
		<name>config-template</name>
		<value>/html/testvisualizer/configuration.jsp</value>
</init-param>
```

전체 코드를 확인하면 다음과 같습니다.<br>
```xml
<?xml version="1.0"?>

<portlet-app xmlns="http://java.sun.com/xml/ns/portlet/portlet-app_2_0.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://java.sun.com/xml/ns/portlet/portlet-app_2_0.xsd http://java.sun.com/xml/ns/portlet/portlet-app_2_0.xsd" version="2.0">
	
	<portlet>
		<portlet-name>test-visualizer</portlet-name>
		<display-name>Test Visualizer</display-name>
		<portlet-class>
			org.kisti.post.visualizer.TestVisualizer
		</portlet-class>
		<init-param>
			<name>view-template</name>
			<value>/html/testvisualizer/view.jsp</value>
		</init-param>
		<init-param>
			<name>config-template</name>
			<value>/html/testvisualizer/configuration.jsp</value>
		</init-param>
		<expiration-cache>0</expiration-cache>
		<supports>
			<mime-type>text/html</mime-type>
			<portlet-mode>view</portlet-mode>
		</supports>
		<portlet-info>
			<title>Test Visualizer</title>
			<short-title>Test Visualizer</short-title>
			<keywords></keywords>
		</portlet-info>
		<security-role-ref>
			<role-name>administrator</role-name>
		</security-role-ref>
		<security-role-ref>
			<role-name>guest</role-name>
		</security-role-ref>
		<security-role-ref>
			<role-name>power-user</role-name>
		</security-role-ref>
		<security-role-ref>
			<role-name>user</role-name>
		</security-role-ref>
	</portlet>
</portlet-app>
```