---
title: RESPONSE DATA EVENT
permalink: /even_responsedata.html
sidebar: workbench_sidebar
categories: workbench
tags: [workbench, event]
folder: opsevent
summary:
---

### OSP RESPONSE DATA 이벤트

- 샘플 예제
```javascript
Liferay.on(
		OSP.Event.OSP_RESPONSE_DATA,
		function( e ){
			var myId = '<%=portletDisplay.getId()%>';
			if( e.targetPortlet !== myId )	return;
			console.log("[ATOM EDITOR] OSP OSP_RESPONSE_DATA :", e );
			var iframe = document.getElementById('<portlet:namespace/>TBox');
			var filePath = new OSP.InputData( e.data );
			if( filePath.type() !== OSP.Enumeration.PathType.FILE ){
				alert('File Name is not available. Choose another one.');
				return;
			}

			if( !<portlet:namespace/>saveAction ){
				<portlet:namespace/>loadText( filePath, true );
				$<portlet:namespace/>fileExplorerDialogSection.dialog('close');
			}
			else{
				$('#<portlet:namespace/>uploadFileName').val(filePath.name());
				filePath.type( OSP.Enumeration.PathType.FILE_CONTENT );
				filePath.context( iframe.contentWindow.getParameters() );

				$.ajax({
					url: '<%=serveResourceURL.toString()%>',
					type: 'POST',
					dataType: 'json',
					data:{
						<portlet:namespace/>command: "CHECK_DUPLICATED",
						<portlet:namespace/>repositoryType: filePath.repositoryType(),
						<portlet:namespace/>parentPath: filePath.parent(),
						<portlet:namespace/>fileName: filePath.name()
					},
					success: function(result){
						var duplicated = result.duplicated;
						if( duplicated ){
							var confirmDialog = $('#<portlet:namespace/>confirmDialog');
							confirmDialog.dialog(
									{
										resizable: false,
										height: "auto",
										width: 400,
										modal: true,
										buttons: {
												'OK': function() {
															$( this ).dialog( 'destroy' );
															<portlet:namespace/>saveContentAs ( filePath );
															$<portlet:namespace/>fileExplorerDialogSection.dialog('close');
												},
												Cancel: function() {
															$( this ).dialog( 'destroy' );
												}
										}
									}
							);
						}
						else{
							<portlet:namespace/>saveContentAs ( filePath );
							$<portlet:namespace/>fileExplorerDialogSection.dialog('close');
						}
					},
					error: function( e, d ){
						console.log(' [ATOM EDITOR] file save error', e, d);
					}
				});
			}
		}
);
```
