---
title: "Rich Text Editor Inline editing mode"
component: "Rich Text Editor"
description: "This section for Syncfusion react Rich Text Editor component demonstrates on how to enable the inline mode editor on demand while editing the content."
---

# Inline Mode

This is the inline example for the Rich Text Editor. For this you must set the [inlineMode](../api/rich-text-editor/#inlinemode) property.

Inline edition allows you to select any editable element or click the element on the page and edit it in-place.

Inline editing is a true WYSIWYG formation and on the contrary to Rich Text Editor HTML/MD editing, the styles that are used for edited content comes directly from the document stylesheet. This means that inline editors ignore the default Rich Text Editor content styles.

## Show on select/click

Enabling the [onSelection](/rich-text-editor/api-inlineModeModel.html#onselection) option of inlineMode makes the inline Rich Text Editor to appear.  You can select the text in the editable area otherwise the inline Rich Text Editor will be appear once click into the editable area.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - InlineMode Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  private inlineMode: object = {
    enable: true,
    onSelection: true
  }

  private toolbarSettings: object = {
    items: [
      'Bold', 'Italic', 'Underline', 'Formats', '-',
      'Alignments', 'OrderedList', 'UnorderedList', 'CreateLink'
    ]
  }

  public render() {
    return (
      <RichTextEditorComponent  height={450} inlineMode={this.inlineMode} toolbarSettings={this.toolbarSettings}>
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
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}