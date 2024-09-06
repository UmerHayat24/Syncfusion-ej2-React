---
title: "Rich Text Editor File Browser"
component: "Rich Text Editor"
description: "This section  explains about how to enable the file browser feature in the Syncfusion react Rich Text Editor component."
---

# File Browser

Rich Text Editor allows to browse and insert images in the edit panel using the file browser. File browser allows the users to browse and select a file or folder from the file system and it supports various cloud services.

## Required additional dependency

The following list of additional dependencies are required to use the file browser feature in the Rich Text Editor.

```js

|-- @syncfusion/ej2-react-richtexteditor
    |-- @syncfusion/ej2-layouts
    |-- @syncfusion/ej2-grids
    |-- @syncfusion/ej2-filemanager

```

## Additional CSS Reference

Additionally add the below styles in the `[src/App.css]` file.

```css
  @import "../../node_modules/@syncfusion/ej2-layouts/styles/material.css";
  @import "../../node_modules/@syncfusion/ej2-grids/styles/material.css";
  @import "../../node_modules/@syncfusion/ej2-filemanager/styles/material.css";
```

The following example explains about how to configure the file browser within the Rich Text Editor component.

* Configure the `FileManager` toolbar item in the `toolbarSettings` API `items` property.
* Set [`enable`](/rich-text-editor/api-fileManagerSettings.html#enable) property as `true` on [`fileManagerSettings`](/rich-text-editor/api-fileManagerSettings.html) property to make the file browser in the Rich Text Editor to appear on the `FileManager` toolbar click action.

> Rich Text Editor features are segregated into individual feature-wise modules. To use the file browser tool, inject the `FileManager` module using services.

{% tab template="rich-text-editor/file-browser", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - File Browser Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar, FileManager } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  private fileManagerSettings: object = {
    enable: true,
    path: '/Pictures/Food',
    ajaxSettings: {
      url: 'https://ej2-aspcore-service.azurewebsites.net/api/FileManager/FileOperations',
      getImageUrl: 'https://ej2-aspcore-service.azurewebsites.net/api/FileManager/GetImage',
      uploadUrl: 'https://ej2-aspcore-service.azurewebsites.net/api/FileManager/Upload',
      downloadUrl: 'https://ej2-aspcore-service.azurewebsites.net/api/FileManager/Download'
    }
  }

  private toolbarSettings: object = {
    items: ['FileManager']
  }

  public render() {
    return (
      <RichTextEditorComponent fileManagerSettings={this.fileManagerSettings} toolbarSettings={this.toolbarSettings}>
        <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content. Users can format their content using standard toolbar commands.</p>
        <p><b>Key features:</b></p>
        <ul>
          <li>
            <p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p>
          </li>
          <li>
            <p>Capable of handling markdown editing.</p>
          </li>
          <li>
            <p>Contains a modular library to load the necessary functionality on demand.</p>
          </li>
          <li>
            <p>Provides a fully customizable toolbar.</p>
          </li>
          <li>
            <p>Provides HTML view to edit the source directly for developers.</p>
          </li>
          <li>
            <p>Supports third-party library integration.</p>
          </li>
          <li>
            <p>Allows preview of modified content before saving it.</p>
          </li>
          <li>
            <p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p>
          </li>
          <li>
            <p>Contains undo/redo manager.</p>
          </li>
          <li>
            <p>Creates bulleted and numbered lists.</p>
          </li>
        </ul>
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar, FileManager]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}