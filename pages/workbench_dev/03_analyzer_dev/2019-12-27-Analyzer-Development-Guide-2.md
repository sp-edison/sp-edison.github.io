---
title: "자바 파일 설정"
permalink: workbench_analyzerguide2.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
summary: 에디슨 워크벤치 기반 후처리기(Post-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 분석기(Post-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## 1. 포틀릿 자바 파일 설정
처음 라이프레이 플러그인 프로젝트를 생성할 때, 프로젝트 명은 `ExamplePost`로 설정하였고, 생성된 포틀릿은 `TestVisualizer`로 파일명을 지정하였습니다.<br>
프로젝트 내에 `TestVisualizer.java`를 선택하여 `serveResource`메소드를 오버라이드 합니다. 해당 그림은 다음과 같습니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/7.png" %}<br>

다음 소스 코드와 같이 워크벤치 시뮬레이션 파일 서비스와 연동하는 라이브러리 함수를 호출합니다. 
이전 단계에서 `SciencePlatform-hook-service.jar` 라이브러리를 추가하였기 때문에 자동으로 메소드가 추가됩니다.
<br>

```java
public class TestVisualizer extends MVCPortlet {

	@Override
	public void serveResource(ResourceRequest resourceRequest, ResourceResponse resourceResponse)
			throws IOException, PortletException {
		// TODO Auto-generated method stub
		//super.serveResource(resourceRequest, resourceResponse);
		OSPFileLocalServiceUtil.processOSPResourceAction(resourceRequest, resourceResponse);
	}

}
```


## 2. 포틀릿 구성 정보 설정을 위한 자바 파일 추가
포틀릿 구성 정보의 설정을 위한 자바 파일을 추가 합니다. `TestVisualizer.java`파일이 포함된 같은 패키지 내에 새로운 클래스 파일을 추가합니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/8.png" %}<br>

파일을 추가하면 아래와 같은 화면을 볼 수 있습니다. 해당 자바 파일의 이름은 임의로 지정할 수 있습니다.
포틀릿의 구성 정보를 처리하는 루틴을 포함시키기 위해 Configuration 자바 파일의 Super Class를 `com.liferay.portla.kernel.portlet.DefaultConfigurationAction`를 상속하는 내용을 추가합니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/9.png" %}<br>
또한 `inherited abstract methods`를 선택하면 다음과 같은 화면을 확인할 수 있습니다.
많은 메소드 중에서 `processAction`메소드를 오버라이드 체크를 선택하고 OK 버튼을 클릭합니다.<br>
{% include image.html file="workbench_dev/analyzer_dev/10.png" %}<br>

최종으로 구성된 자바 클래스 소스 코드는 다음과 같습니다.

```java
public class TestVisualizerConfiguration extends DefaultConfigurationAction {

	@Override
	public void processAction(PortletConfig portletConfig, ActionRequest actionRequest, ActionResponse actionResponse)
			throws Exception {
		// TODO Auto-generated method stub
		super.processAction(portletConfig, actionRequest, actionResponse);
	}

}
```