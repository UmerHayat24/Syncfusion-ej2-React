---
title: "Rich text editor how to format code block using toolbar button"
component: "Rich Text Editor"
description: "This section for Syncfusion React Rich Text Editor component explains about how to format code block using toolbar button."
---

# Format code block using toolbar button

You can configure code block formatting as a separate toolbar button by adding the **InsertCode** keyword within the [toolbarSettings](./../../api/rich-text-editor/toolbarSettings/#toolbarsettings) items property.

The InsertCode button has a toggle state to apply code block formatting to the editor and remove code block formatting from the editor.

The following sample demonstrates how to config the InsertCode button in toolbar and set the background color to “pre” tag for highlighting the code block.

{% tab template="rich-text-editor/how-to-format-code", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { HtmlEditor, Inject, Link, RichTextEditorComponent,QuickToolbar, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  private tools: object = {
    items: ['InsertCode']
  }
  public render() {
    return (
      <RichTextEditorComponent toolbarSettings={this.tools}>
        <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
          Users can format their content using standard toolbar commands.</p>
        <p><b>Key features:</b></p>
        <ul>
          <li>
            <p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p>
          </li>
          <li>
            <p>Capable of handling markdown editing.</p>
          </li>
        </ul>
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}