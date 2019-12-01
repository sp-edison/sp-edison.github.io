---
title: "가시화 파일 설정"
permalink: workbench_analyzerguide5.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, analyzer]
folder: workbench
summary: 에디슨 워크벤치 기반 후처리기(Post-Processor)를 개발하기 위한 프로젝트 생성 및 기본 설정에 대한 매뉴얼
---

[EDISON](https://edison.re.kr) 워크벤치 기반 분석기(Post-Processor) 개발 매뉴얼 입니다.

Liferay 6.2.5 포틀릿 기반으로 개발 하는 방법에 대해 순차적으로 설명 되어 있습니다.


## 1. load_visual.jsp 파일 설정

이전 단계에서 실제 데이터를 가시화하는 후처리 모듈을 `<iframe>`태그 안에서 호출을 하였습니다.
해당 코드 부분은 다음과 같습니다.

```html
<iframe 
	class ="col-sm-12 osp-iframe-canvas" 
	id="<portlet:namespace/>canvas" style="<%=visualizerConfig.getDisplayStyle()%>"
	src="<%=request.getContextPath()%>/html/testvisualizer/load_visual.jsp">
</iframe>
```
<br>
위의 내용과 마찬가지로 현재 같은 폴더 내에 `load_visual.jsp` 파일을 새로 생성하여 가시화 하는 소스코드를 추가합니다.
기본적인 구조는 html 파일과 마찬가지로 동작할 수 있습니다. 외부 스크립트 라이브러리를 추가하고 싶은 경우에는 아래 코드와 같이 추가합니다.

```html
<!-- 데이터를 visualize 하는 스크립팅 파일 추가  -->
<script src="<%=request.getContextPath()%>/js/jsmol/JSmol.min.js"></script>
```

## 2. loadVisualFile 함수 설정

앞선 단계에서 파일이나 파일의 url을 전달하면 해당 파일에 대해 가시화 하는 모듈을 추가하였습니다. 
워크벤치 시뮬레이션에서 파일 로드를 호출하면 자동으로 호출되는 로드 함수를 앞선 단계에서 `<portlet:namespace/>visualizer.callIframeFunc( 'loadVisualFile', null, jsonData.content_ );`의 코드에서 정의하였습니다.
따라서 결과 데이터 가시화 사용자 요청이 들어오게 되면 바로 아래의 함수를 호출하게 됩니다. <br>
```html
function loadVisualFile( urlToLoad ){
//url을 기반으로 파일을 받아와 비주얼을 진행하는 부분

}
```

분자 및 원자 모듈의 가시화를 하는 `JSMol`포틀릿의 예제를 보면 아래와 같은 코드로 데이터를 호출받아 가시화 한다.
```html
function loadJSMolFile( urlToLoad ){
        console.log( '[JSMOL]URL To Load: '+ urlToLoad );
        if( !urlToLoad )    return;
        currentUrl = urlToLoad;
        
        var Info = {
                  color: '#000000',
                  height: $('body').height(),
                  width: $('body').width(),
                  //script: "load "+"/jsmol-portlet/temp/ospjm2548440710626419920.tmp",
                  //script: "load "+ fileInfos.tempFilePath.replace(/\\/g, '/'),
                  script: 'load '+ currentUrl,
                  //script: "load " + '/jsmol-portlet/js/jsmol/data/1crn.pdb',
                  use: 'HTML5',
                  j2sPath: '<%=request.getContextPath()%>/js/jsmol/j2s',
                  jarPath: '<%=request.getContextPath()%>/js/jsmol/java',
                  jarFile: 'JmolAppletSigned0.jar',
                  isSigned: true,
                  serverURL: '<%=request.getContextPath()%>/js/jsmol/php/jsmol.php',
                  disableInitialConsole: true
        };
       
       
      
        if(myJmol && myJmol._applet){
        	console.log("[JSMOL] test update 1 ", myJmol);
        	  console.log("[JSMOL] test if : "+ myJmol._applet);
        	//Jmol.setInfo(myJmol, Info, true);
        	//Jmol.loadFile(myJmol, currentUrl, Info);
        	//Jmol.script(myJmol,Info);
        	console.log("[JSMOL] update file 1");
        	Jmol.loadFile(myJmol, currentUrl);
        	console.log("[JSMOL] update file 2");
		}
		else{
			console.log("[JSMOL] test update 2 create ");
			Jmol.setDocument(0);
			myJmol = Jmol.getApplet('myJmol', Info);
			console.log("[JSMOL] create jmol object", myJmol);
			$('#canvas').html( Jmol.getAppletHtml(myJmol) );
		}
```



## 3. 전체 코드


전체 코드를 확인하면 다음과 같습니다.
```html
<!DOCTYPE html>
<html style="height:100%; overflow:hidden;">
<head>
<!-- 데이터를 visualize 하는 스크립팅 파일 추가  -->
    <script src="<%=request.getContextPath()%>/js/jsmol/JSmol.min.js"></script>
</head>
<body style="height:100%; padding:0px; margin:0px; ">

    <div id="canvas"></div>

    <script>

    var currentUrl;



/***********************************************************************
 * Golbal functions
 ***********************************************************************/
$(window).resize( function(e){
	if(myJmol){
		//$('#canvas').empty();
		//console.log("[JSMol] resize Applet : "+ $('body').width() +' : '+$('body').height());
		//parent.jsMolresize();
		Jmol.resizeApplet(myJmol, [$('body').width(), $('body').height()]);
		//console.log("[JSMol] resize Applet end.");
	}
	
});
function loadVisualFile( urlToLoad ){
//url을 기반으로 파일을 받아와 비주얼을 진행하는 부분

}

function clearVisual(){
//visual 부분을 초기화 하는 부분
}

</script>

</body>
</html>
```


샘플 코드는 아래의 링크를 통해 다운로드 받을 수 있습니다.
- [ExamplePost-portlet.zip](OSPLibrary/ExamplePost-portlet.zip)