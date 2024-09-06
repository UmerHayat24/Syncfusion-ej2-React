---
title: "Drag and Drop"
component: "File Manager"
description: "Drag and Drop Support in file manager"
---

# Drag And Drop

The file manager allows files or folders to be moved from one folder to another by using the  [allowDragAndDrop](../api/file-manager/#allowdraganddrop) property. It also supports uploading a file by dragging it from Windows Explorer to  FileManager control. You can enable or disable this support by using the [allowDragAndDrop](../api/file-manager/#allowdraganddrop) property of file manager.

The event triggered in drag and drop support are

* [fileDragStart](../api/file-manager/#filedragstart) - Triggers when the file/folder dragging is started.
* [fileDragging](../api/file-manager/#filedragging) - Triggers while dragging the file/folder.
* [fileDragStop](../api/file-manager/#filedragstop) - Triggers when the file/folder is about to be dropped at the target.
* [fileDropped](../api/file-manager/#filedropped) - Triggers when the file/folder is dropped.

{% tab template="file-manager/drag-and-drop", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}