---
title: "Rich text editor How To capture ctrl+s"
component: "Rich Text Editor"
description: "This section for Syncfusion React Rich Text Editor component explains how to capture the ctrl+s to update the value."
---

# Capture ctrl+s to update the value

To achieve this, we need to bind the `keydown` event to the RTE content and capture the `ctrl + s` key press using its keyCode.
In the `keydown` event handler, the `updateValue` method is called to update the [`value`](../../api/rich-text-editor/#value) property and then we can save the content in the required database using the same.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public rteObj: RichTextEditorComponent;

    public created(): void {
        const instance = this.rteObj;
        (this.rteObj as any).contentModule.getDocument().addEventListener("keydown",(e: any)=>{
            if(e.key === 's' && e.ctrlKey===true){
                e.preventDefault(); // to prevent default ctrl+s action
                instance.updateValue(); // to update the value after editing
                // const value: any= instance.value; // you can get the RTE content to save in the desired database

            }

        });
    }

  public render() {
    return (
      <RichTextEditorComponent ref={(richtexteditor) => { this.rteObj = richtexteditor! }} created={this.created = this.created.bind(this)} >
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