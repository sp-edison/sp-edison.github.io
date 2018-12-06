---
title: "이벤트처리"
permalink: workbenchan_alyzerguide4.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---

이전에 설정되었던 부분은 서버 사이드에서 실행되는 컨트롤 코드 부분이었습니다.
워크벤치 기반 분석기 개발을 위해서는 스크립트 단위의 이벤트 프로세싱을 통해 이루어 집니다.

따라서 뷰 부분의 스크립트 단위로 코드를 개발하며, 해당 뷰 부분에서 필요로 하는 기본 코드들이 있습니다. 따라서 그에 따른 스크립트 기본 소스 코드들을 추가하는 방법을 서술하도록 하겠습니다.

### `init.jsp` 파일 생성 및 코드 입력
생성된 프로젝트 내 `/html` 폴더 내 `init.jsp` 파일을 생성합니다.

생성된 `init.jsp` 파일 내 뷰 개발을 위한 필요 라이브러리 코드를 추가하고 라이프레이 기본 라이브러리들을 추가합니다.
추가해야 하는 코드는 아래와 같습니다.

```javascript
<%@ taglib uri="http://java.sun.com/portlet_2_0" prefix="portlet" %>
<%@ taglib uri="http://alloy.liferay.com/tld/aui" prefix="aui" %>
<%@ taglib uri="http://liferay.com/tld/ui" prefix="liferay-ui" %>
<%@ taglib uri="http://liferay.com/tld/theme" prefix="theme" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://liferay.com/tld/security" prefix="liferay-security" %>
<%@ taglib uri="http://liferay.com/tld/portlet" prefix="liferay-portlet" %>

<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>
<!-- JQuery -->
<script src="<%=request.getContextPath()%>/js/jquery/jquery-ui.min.js" ></script>
<script src="<%=request.getContextPath()%>/js/jquery/jquery.blockUI.js" ></script>
<link type="text/css" href="<%=request.getContextPath()%>/js/jquery/jquery-ui.css" rel="stylesheet" />

<link rel="stylesheet" type="text/css" href="<%=request.getContextPath()%>/css/main.css">
<link href="<%=request.getContextPath()%>/js/jquery/bootstrap-toggle.min.css" rel="stylesheet">
<script src="<%=request.getContextPath()%>/js/jquery/bootstrap-toggle.min.js"></script>

<!-- bootstrap -->
<link href="<%=request.getContextPath()%>/js/jquery/bootstrap.min.css" rel="stylesheet">
<script src="<%=request.getContextPath()%>/js/jquery/bootstrap.min.js"></script>


<portlet:defineObjects />
<theme:defineObjects />

```

**스크립트 라이브러리:** <br>jqueryxxx.min.js 사용 (워크벤치 시스템과 충돌) 스크립트 라이브러리 충돌이 나서 워크벤치 시뮬레이션이 동작하지 않을 수 있습니다. 따라서 jqery 스크립트를 비롯한 대부분의 스크립트 파일은 `init.jsp` 파일에 추가하지 마시기 바랍니다. 하지만 JQuery 스크립트는 플랫폼에 설치되어 있으니 라이브러리를 사용할 수 있습니다.
{: .notice--danger}


### 워크벤치 연동을 위한 CSS 설정

`main.css` 파일에서 [osp-analyzer.css](/assets/OSPLibrary/osp-analyzer.css "분석기 스타일")파일을 호출합니다.
```css
@import url("./osp-analyzer.css");
```

`osp-analyzer.css`파일을 `main.css`파일과 같은 폴더(`/css`)안에 추가합니다.
`osp-analyzer.css` 스타일 코드는 아래와 같습니다.
```css
.osp-analyzer {
	border:none;
	height: 100%;
   	min-height:800px;
   	margin: 0;
}
.osp-analyzer .header{
	height: 40px;
	margin:10px 5px 10px 5px;
}
.osp-analyzer .header [class*="col-"]{
	padding-left: 0;
	padding-right: 0;
}
.osp-analyzer .no-header-frame{
	vertical-align:middle;
	border:none;
	height: 100%;
}
.osp-analyzer .frame{
	vertical-align:middle;
	border:none;
	height: 90%;
}
.osp-analyzer .canvas {
   	border:none;
   	height:100%;
   	margin:0;
   	padding:0;

   	overflow:auto;
}
.osp-analyzer .iframe-canvas {
   	border:none;
   	height:100%;
   	margin:0;
   	padding:0;

   	overflow:hidden;
}

.osp-analyzer .icon-menu {
  font-size: 15px;
  color: #5cb2d7;
  border: 2px solid;
  border-radius: 3px;
  padding-left: 2px;
  padding-right: 3px;
  vertical-align: middle;
}

.osp-analyzer .hidden {
	display: none;
}
```

### jsp 파일 뷰와 분석기 호출부 처리
기본 워크벤치 연동을 위한 이벤트 처리를 하는 jsp 파일(testview.jsp)과 실제 분석하는 부분을 사용자에게 서비스하고 데이터를 가시화하여 제공하는 부분의 jsp 파일(loadAnalyzer.jsp)를 프로젝트 내 생성하여 데이터를 처리한다. 파일명은 임의로 설정할 수 있지만 `portlet.xml` 파일에서 설정을 잘 잡아주어야 합니다. 이벤트 처리를 하는 jsp 파일을 포틀릿과 연결된 초기 jsp 파라미터로 설정해 주어야 합니다.

이벤트 처리를 하는 jsp 파일의 파일명을 testview.jsp로 했다면, `portlet.xml` 파일의 설정은 다음과 같습니다.

```xml
<init-param>
	<name>view-template</name>
	<value>/html/testanalyzer/testview.jsp</value>
</init-param>
```


지금까지 설정에 따른 전체 프로젝트의 구조는 다음과 같습니다.
```terminal
├AnalyzerExample-portlet/
├─docroot/
├──css/
├───main.css
├───osp-analyzer.css
├──html/
├───testanalyzer/
├────testview.jsp
├────loadAnalyzer.jsp
├──js/
├───main.js
├──META-INF/
├───MANIFEST.MF
├──WEB-INF/
├───lib/
├────commons-beanutils.jar
├────commons-collections.jar
├────commons-exec-1.1.jar
├────commons-fileupload.jar
├────commons-io.jar
├────commons-lang.jar
├────SciencePlatform-hook-service.jar
├───tlb/
├───liferay-display.xml
├───liferay-plugin-packkage.properties
├───liferay-portlet.xml
├───portlet.xml
├───web.xml
```

이외에 추가로 파일이 더 있을 수도 있지만 필수적으로 필요한 파일들은 위의 구조와 같으니 비교하여 체크해 보시기 바랍니다.
