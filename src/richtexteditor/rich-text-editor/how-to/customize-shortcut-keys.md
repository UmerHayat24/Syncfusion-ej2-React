---
title: " Rich text editor How To customize the shorcut key"
component: "Rich Text Editor"
description: "This section for Syncfusion React Rich Text Editor component explains on how to customize the shortcut keys."
---

# Customize keyboard shortcut

It can be achieved by using [`formatter`](../../api/rich-text-editor/#formatter) property. We need to create `customformatterModel` to configure the `keyConfig` using `IHtmlFormatterModel` class and assign the same to the formatter property. Here, `ctrl+q` is configured to open the `Insert Hyperlink` dialog.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

import { Count, HtmlEditor, HTMLFormatter, IHtmlFormatterModel, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public customHTMLModel: IHtmlFormatterModel = {
    // formatter is used to configure the custom key
    keyConfig: {
    'insert-link': 'ctrl+q', // confite the desired key
    }
  };

  public formatter: any =  new HTMLFormatter(this.customHTMLModel);
  // to configure custom key

public render() {
    return (
      <RichTextEditorComponent formatter={this.formatter}>
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
          <li>
            <p>Contains a modular library to load the necessary functionality on demand.</p>
          </li>
          <li>
            <p>Provides a fully customizable toolbar.</p>
          </li>
        </ul>
        <Inject services={[Toolbar, Count, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}

> We need to import `IHtmlFormatterModel` and `HTMLFormatter` to configure the shortcut key.
