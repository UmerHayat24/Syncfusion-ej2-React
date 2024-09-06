---
title: "Views"
component: "File Manager"
description: "Views present in file manager"
---

# Views

View is the section where the files and folders are displayed for the user to browse. The [view](../api/file-manager/#view) API can also be used to change the initial view of the file manager.

 The file manager has two types of [views](../api/file-manager/#view) to display the files and folders.

* [LargeIcons View](#largeicons-view)
* [Details View](#details-view)

## LargeIcons View

By Default, File Manager is rendered with largeicons view. The following example demonstrate this.

{% tab template="file-manager/large-icon", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Details View

Details view is an injectable module in the file manager so, it should be injected before rendering the file manager to avail its functionality. The default appearance of the file manager can be changed from largeicons to details view by using the [view](../api/file-manager/#view) property. The following example demonstrate the file manager with details view.

{% tab template="file-manager/details-view", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}