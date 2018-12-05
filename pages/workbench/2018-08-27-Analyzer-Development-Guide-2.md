---
title: "프로젝트 생성"
permalink: workbenchanalyzerguide2.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
---

EDISON 워크벤치 기반 분석기(Post-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.

## Java 코드 추가 1 (파일 관리)
생성된 프로젝트에서 포틀릿 클래스에 파일 전송 및 파일 다운로드 등을 위한 자바 코드를 추가 합니다. `MVCPortlet`을 `extends` 하게 되면 그 중 미리 선언되어 있는 `serveResource` 함수를 오버라이딩 하면 됩니다.
해당 코드는 수정할 필요없이 그대로 개발중인 프로젝트에 넣기만 하면됩니다. 이전 프로젝트 생성 부분에서 [SciencePlatform-hook-service.jar](/assets/OSPLibrary/SciencePlatform-hook-service.jar)라이브러리를 추가했다면 다음 자바 코드를 문제없이 호출할 수 있습니다.
```java
@Override
public void serveResource(ResourceRequest resourceRequest, ResourceResponse resourceResponse)
    throws IOException, PortletException{
    String fileName = ParamUtil.getString(resourceRequest, "fileName");
    String parentPath = ParamUtil.getString(resourceRequest, "parentPath");
    Path filePath = Paths.get(parentPath).resolve(fileName);
    String command = ParamUtil.getString(resourceRequest, "command");
    String repositoryType = ParamUtil.getString(resourceRequest, "repositoryType", OSPRepositoryTypes.USER_JOBS.toString());

    if(command.equalsIgnoreCase("GET_FILE")){
        try{
        	OSPFileUtil.getFile(resourceRequest, resourceResponse, filePath.toString(), repositoryType);
        }catch (PortalException | SystemException e){
            _log.error("[JSMOL] readFileContent(): " + filePath.toString());
            throw new PortletException();
        }
    }else if(command.equalsIgnoreCase("READ_IMAGE")){
        try{
        	OSPFileUtil.getFile(resourceRequest, resourceResponse, filePath.toString(), repositoryType);
        }catch (PortalException | SystemException e){
            _log.error("[JSMOL] readFileContent(): " + filePath.toString());
            throw new PortletException();
        }
    }else if(command.equalsIgnoreCase("READ_FIRST_FILE")){
        try{
        	OSPFileUtil.readFirstFileContent(resourceRequest, resourceResponse, parentPath, fileName, repositoryType);
        }catch (PortalException | SystemException e){
            _log.error("[JSMOL] readFileContent(): " + filePath.toString());
            throw new PortletException();
        }
    }else if(command.equalsIgnoreCase("GET_FIRST_FILE_NAME")){
        try{
        	System.out.println("[JSMOL] test get firstFileName");
        	OSPFileUtil.getFirstFileName(resourceRequest, resourceResponse, parentPath, fileName, repositoryType);
        }catch (PortalException | SystemException e){
            _log.error("[JSMOL] getFirstFileName(): " + filePath.toString());
            throw new PortletException();
        }
    }else if(command.equalsIgnoreCase("DOWNLOAD_FILE")){
        try{
        	OSPFileUtil.downloadFile(resourceRequest, resourceResponse, filePath.toString(), repositoryType);
        }catch (PortalException | SystemException e){
            _log.error("[JSMOL] checkValidFile(): " + filePath.toString());
            throw new PortletException();
        }
    }else{
        _log.error("Un-known command: " + command);
        throw new PortletException();
    }
}
```

## Java 코드 추가 2 (워크벤치 공유 변수)
워크벤치 실행을 위해 필요한 기본 값들을 설정하기 위한 자바 코드를 추가합니다. 워크벤치에서 개발하고 있는 분석기를 이용하여 시뮬레이션 환경을 구성할 때 필수적으로 확인하는 변수들의 값을 기본값으로 설정하는 부분입니다. 마찬가지로 `MVCPortlet`을 `extends` 하게 되면 그 중 미리 선언되어 있는 `doView` 함수를 오버라이딩 하면 됩니다.

```java
@Override
public void doView(RenderRequest renderRequest, RenderResponse renderResponse) throws IOException, PortletException{
  boolean eventEnable = ParamUtil.getBoolean(renderRequest, "eventEnable", true);
  String inputData = ParamUtil.getString(renderRequest, "inputData");
  String connector = ParamUtil.getString(renderRequest, "connector", "connector");
  String mode = ParamUtil.getString(renderRequest, "mode", "VIEW");

  renderRequest.setAttribute("eventEnable", eventEnable);
  renderRequest.setAttribute("inputData", inputData);
  renderRequest.setAttribute("connector", connector);
  renderRequest.setAttribute("mode", mode);

  super.doView(renderRequest, renderResponse);
}
```
지금까지 기본적인 java 소스 코드를 추가하였습니다. 해당 소스코드는 워크벤치와 연동 될 때, 파일 관리와 기본 변수 값을 체크하기 위해 필요한 부분입니다. 기본적으로 필요한 자바 소스코드 외에는 추가할 필요가 없는 부분이니 그냥 소소코드를 생성된 자바 파일에 복사해서 붙여넣기만 하면 됩니다.


**로그 변수 선언** <br>생성된 자바 파일 안에서 시스템에 필요한 로그를 선언하기 위해 변수를 선언할 필요가 있습니다.<br>`private static Log _log = LogFactoryUtil.getLog(TestAnalyzerPortlet.class);`
<br>해당 변수는 위와 같이 선언하며, 생성된 자바 포틀릿 클래스 명에 따라 클래스 명(`TestAnalyzerPortlet.class`)이 달라집니다.
{: .notice--info}


## Java 코드 라이브러리 확인
위의 절차에 따라 자바 소스 코드들을 추가하였다면, 라이브러리들을 해당 클레스에 import 해야 합다.

사용되는 클래스 라이브러리들은 아래와 같으니 동일한 이름의 다른 라이브러리를 호출하지 않도록 주의해야 합니다.


```java
import java.io.IOException;
import java.nio.file.Path;
import java.nio.file.Paths;

import javax.portlet.PortletException;
import javax.portlet.RenderRequest;
import javax.portlet.RenderResponse;
import javax.portlet.ResourceRequest;
import javax.portlet.ResourceResponse;

import com.kisti.osp.constants.OSPRepositoryTypes;
import com.kisti.osp.service.FileManagementLocalServiceUtil;
import com.kisti.osp.util.OSPFileUtil;
import com.liferay.portal.kernel.exception.PortalException;
import com.liferay.portal.kernel.exception.SystemException;
import com.liferay.portal.kernel.log.Log;
import com.liferay.portal.kernel.log.LogFactoryUtil;
import com.liferay.portal.kernel.util.ParamUtil;
import com.liferay.util.bridges.mvc.MVCPortlet;

```
