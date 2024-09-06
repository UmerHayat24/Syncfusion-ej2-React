---
title: "Customization"
component: "File Manager"
description: "Customizing File Manager functionalities"
---

# Customizing File Manager functionalities

The file manager component allows customizing its functionalities like, context menu, searching, uploading, toolbar using APIs. Given below are some of the functionalities that can be customized in the File Manager,

* [Context menu customization](#context-menu-customization)
* [Details view customization](#details-view-customization)
* [Navigation pane customization](#navigation-pane-customization)
* [Show/Hide file extension](#showhide-file-extension)
* [Show/Hide hidden items](#showhide-hidden-items)
* [Show/Hide thumbnail images in large icons view](#showhide-thumbnail-images-in-large-icons-view)
* [Toolbar customization](#toolbar-customization)
* [Upload customization](#upload-customization)
* [Tooltip customization](#tooltip-customization)

## Context menu customization

The context menu settings like, items to be displayed on files, folders and layout click and visibility can be customized using [contextMenuSettings](../api/file-manager/#contextmenusettings) property.

{% tab template="file-manager/contextmenu-items", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Details view customization

The details view settings like, column width, header text, template for each field can be customized using [detailsViewSettings](../api/file-manager/#detailsviewsettings) property.

{% tab template="file-manager/detailsview", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Navigation pane customization

The navigation pane settings like, minimum and maximum width and visibility can be customized using [navigationPaneSettings](../api/file-manager/#navigationpanesettings) property.

{% tab template="file-manager/navigationpane", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Show/Hide file extension

The file extensions are displayed in the File Manager by default. This can be hidden by disabling the [showFileExtension](../api/file-manager/#showfileextension) property.

In File Manager [fileLoad](../api/file-manager/#fileload) and [fileOpen](../api/file-manager/#fileopen) events are triggered before the file/folder is rendered and before the file/folder is opened respectively. These events can be utilized to perform operations before a file/folder is rendered or opened.

{% tab template="file-manager/fileextension", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Show/Hide hidden items

The File Manager provides support to show/hide the hidden items by enabling/disabling the [showHiddenItems](../api/file-manager/#showhiddenitems) property.

{% tab template="file-manager/hiddenitems", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Show/Hide thumbnail images in large icons view

The thumbnail images are displayed in the File Manager's large icons view by default. This can be hidden by disabling the [showThumbnail](../api/file-manager/#showthumbnail) property.

{% tab template="file-manager/disablethumbnail", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Toolbar customization

The toolbar settings like, items to be displayed in toolbar and visibility can be customized using [toolbarSettings](../api/file-manager/#toolbarsettings) property.

{% tab template="file-manager/toolbar-items", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Upload customization

The upload settings like, minimum and maximum file size and enabling auto upload can be customized using [uploadSettings](../api/file-manager/#uploadsettings) property.

{% tab template="file-manager/upload", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}

## Tooltip customization

The tooltip value can be customized by adding extra content to the title of the toolbar, navigation pane, details view and large icons of the file manager element.

{% tab template="file-manager/tooltip", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}
