---
title: "자바 파일 설정"
permalink: workbench_editorguide2.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, editor]
folder: workbench
summary: 에디슨 워크벤치 기발 에디터(Pre-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 전처리기(Pre-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## 1. 포틀릿 자바 파일 설정
처음 라이프레이 플러그인 프로젝트를 생성할 때, 프로젝트 명은 `OSPTextEditorExample`로 설정하였고, 생성된 포틀릿은 `TextEditorPortlet`으로 파일명을 지정하였습니다.<br>
프로젝트 내에 `TextEditorPortlet.java`를 선택하여 `serveResource`메소드를 오버라이드 합니다. 해당 그림은 다음과 같습니다.<br>
{% include image.html file="workbench_dev/editor_dev/6.png" %}<br>

다음 소스 코드와 같이 워크벤치 시뮬레이션 파일 서비스와 연동하는 라이브러리 함수를 호출합니다. 
이전 단계에서 `SciencePlatform-hook-service.jar` 라이브러리를 추가하였기 때문에 자동으로 메소드가 추가됩니다.
<br>

```java
public class TextEditorPortlet extends MVCPortlet {
	private static Log _log = LogFactoryUtil.getLog(TextEditorPortlet.class);

	@Override
	public void serveResource(ResourceRequest resourceRequest,
			ResourceResponse resourceResponse) throws IOException,
			PortletException {

		OSPFileLocalServiceUtil.processOSPResourceAction(resourceRequest, resourceResponse);
		
		super.serveResource(resourceRequest, resourceResponse);
	}
}
```


## 2. 포틀릿 구성 정보 설정을 위한 자바 파일 추가
포틀릿 구성 정보의 설정을 위한 자바 파일을 추가 합니다. `TextEditorPortlet.java`파일이 포함된 같은 패키지 내에 새로운 클래스 파일을 추가합니다.<br>
파일을 추가하면 아래와 같은 화면을 볼 수 있습니다. 
{% include image.html file="workbench_dev/editor_dev/7.png" %}<br>

해당 자바 파일의 이름은 `TextEdirotPortleConfigAction`로 지정 하였습니다.
{% include image.html file="workbench_dev/editor_dev/8.png" %}<br>

포틀릿의 구성 정보를 처리하는 루틴을 포함시키기 위해 Configuration 자바 파일의 Super Class를 `com.liferay.portla.kernel.portlet.DefaultConfigurationAction`를 상속하는 내용을 추가합니다.<br>
`superclass`부분에서 `Browse..`버튼을 클릭하고 `DefaultConfigurationAction`을 검색하면 다음과 같은 그림을 확인 할 수 있습니다.
{% include image.html file="workbench_dev/editor_dev/9.png" %}<br>
바로 `OK`버튼을 클릭하면 다음 그림과 같이 `superclass`가 자동으로 지정됩니다.
{% include image.html file="workbench_dev/editor_dev/10.png" %}<br>
`Finish`버튼을 클릭하고 클래스를 추가합니다.<br>

해당 클래스에 상속받은 메소들르 추가합니다. 메소드는 클래스안에서 오른쯕 클릭을 하면 뜨는 팝업 메뉴중에서 `Source->Overide/Implement Method...`를 선택하여 뜨는 팝업창입니다.
{% include image.html file="workbench_dev/editor_dev/11.png" %}<br>


최종으로 구성된 자바 클래스 소스 코드는 다음과 같습니다.

```java
public class TextEditorPortletConfigAction extends DefaultConfigurationAction {

	@Override
	public void processAction(PortletConfig portletConfig, ActionRequest actionRequest, ActionResponse actionResponse)
			throws Exception {
		// TODO Auto-generated method stub
		super.processAction(portletConfig, actionRequest, actionResponse);
	}

}
```