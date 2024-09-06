---
title: "Rich text editor How To change the default font-family"
component: "Rich Text Editor"
description: "This section for Syncfusion React Rich Text Editor component explains on how to change the default `fontFamily`."
---

# Change default font-family

By using [`default`](../../api/rich-text-editor/#fontfamily) property, you can change the default font-family of the RTE. To change the font-family of the RTE content while loading, we need to give the font-family in the style section with the help of [`cssClass`](../../api/rich-text-editor/#cssclass) property.

{% tab template="rich-text-editor/how-to-default-font", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

import { Count, HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  private fontFamily: object = {
       default:"Noto Sans", // to define default font-family
        items:[
          {text: "Segoe UI", value: "Segoe UI", class: "e-segoe-ui",  command: "Font", subCommand: "FontName"},
          {text: "Roboto", value: "Roboto",  command: "Font", subCommand: "FontName"},
          {text: "Great vibes", value: "Great Vibes,cursive",  command: "Font", subCommand: "FontName"},
          {text: "Noto Sans", value: "Noto Sans",  command: "Font", subCommand: "FontName"},
          {text: "Impact", value: "Impact,Charcoal,sans-serif", class: "e-impact", command: "Font", subCommand: "FontName"},
          {text: "Tahoma", value: "Tahoma,Geneva,sans-serif", class: "e-tahoma", command: "Font", subCommand: "FontName"},
        ]
      };
  private toolbarSettings: object = {
            items: ['Bold', 'Italic', 'Underline', 'StrikeThrough','|',
                'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
                'LowerCase', 'UpperCase', '|',
                'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
                'Outdent', 'Indent', '|',
                'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
                'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
        };
        private cssClass: string = "customClass";

public render() {
    return (
      <RichTextEditorComponent toolbarSettings={this.toolbarSettings} fontFamily={this.fontFamily} cssClass={this.cssClass}>
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