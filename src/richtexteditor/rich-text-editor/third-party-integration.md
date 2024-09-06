---
title: "React Rich Text Editor Third Party Integration"
component: "Rich Text Editor"
description: "This section for Syncfusion react Rich Text Editor compoennt explains on how to integrate additional third-party libraries to enhance the content."
---

# Third-Party Integration

The Rich Text Editor can be integrated with third-party to suite the application scenario.

## CodeMirror Integration

Rich Text Editor comes with a basic HTML source editor through the view-source property. CodeMirror plugin can be used to highlight the syntax of HTML. CodeMirror plugin for Rich Text Editor makes editing of HTML source code with a pleasant experience.

Import necessary CSS and JS files of CodeMirror to the HTML page.

Required JS files of code mirror.

``` javascript
    <script src="scripts/CodeMirror/codemirror.js" type="text/javascript"></script>
    <script src="scripts/CodeMirror/javascript.js" type="text/javascript"></script>
    <script src="scripts/CodeMirror/css.js" type="text/javascript"></script>
    <script src="scripts/CodeMirror/htmlmixed.js" type="text/javascript"></script>
```

Required CSS file of code mirror.

``` javascript
    <link href="scripts/CodeMirror/codemirror.min.css" rel="stylesheet" />
```

Add a custom icon for HTML source editor in the toolbar of Rich Text Editor using the template option of ToolbarSettings, define the code mirror plugins, and then pass the Rich Text Editor content as argument in the [actionComplete](/api/rich-text-editor/#actioncomplete) event.

{% tab template="rich-text-editor/code-mirror", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Code Mirror sample
 */
import { createElement } from '@syncfusion/ej2-base';
import { Count, HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import CodeMirror from 'codemirror';
import 'codemirror/mode/css/css.js';
import 'codemirror/mode/htmlmixed/htmlmixed.js';
import 'codemirror/mode/javascript/javascript';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public myCodeMirror: any;
  public textArea: HTMLElement;
  public rteObj: RichTextEditorComponent;

  public toolbarSettings: object = {
    items: ['SourceCode']
  }
  public value: string = `
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
  `;

  public mirrorConversion(e: any): void {
    const id: string = this.rteObj.getID() + 'mirror-view';
    let mirrorView: HTMLElement = this.rteObj.element.querySelector('#' + id) as HTMLElement;
    const charCount: HTMLElement = this.rteObj.element.querySelector('.e-rte-character-count') as HTMLElement;
    if (e.targetItem === 'Preview') {
      this.textArea.style.display = 'block';
      mirrorView.style.display = 'none';
      this.textArea.innerHTML = this.myCodeMirror.getValue();
      charCount.style.display = 'block';
    } else {
      if (!mirrorView) {
          mirrorView = createElement('div', { className: 'e-content' });
          mirrorView.id = id;
          (this.textArea as any).parentNode.appendChild(mirrorView);
      } else {
          mirrorView.innerHTML = '';
      }
      this.textArea.style.display = 'none';
      mirrorView.style.display = 'block';
      this.renderCodeMirror(mirrorView, this.rteObj.value);
      charCount.style.display = 'none';
    }
  }

  public renderCodeMirror(mirrorView: HTMLElement, content: string): void {
    this.myCodeMirror = CodeMirror(mirrorView, {
      lineNumbers: true,
      lineWrapping: true,
      mode: 'text/html',
      value: content
    });
  }

  public actionComplete(e: any) {
    if (e.targetItem && (e.targetItem === 'SourceCode' || e.targetItem === 'Preview')) {
      (this.rteObj as any).sourceCodeModule.getPanel().style.display = 'none';
      this.mirrorConversion(e);
    } else {
      setTimeout(() => {
        this.rteObj.toolbarModule.refreshToolbarOverflow();
      }, 400);
    }
  }

  public created(): void{
    this.textArea = (this.rteObj as any).contentModule.getEditPanel() as HTMLElement;
  }

  public render() {
    return (
      <RichTextEditorComponent ref={(richtexteditor) => { this.rteObj = richtexteditor! }} height={450} toolbarSettings={this.toolbarSettings} showCharCount={true} actionComplete={this.actionComplete = this.actionComplete.bind(this)} created={this.created = this.created.bind(this)}>
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
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar, Count]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}

## At.js Integration

Rich Text Editor can easily be integrated with At.js library. To display the autocomplete list, type `@`.

Include At.JS style.

``` javascript
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/at.js/1.4.0/css/jquery.atwho.min.css">
```

Include At.JS javascript.

``` javascript
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/at.js/1.4.0/js/jquery.atwho.min.js"></script>
```

Define the At.js configuration.

``` typescript
    var config = {
        at: "@",
        data: [email id of employees list],
        displayTpl: '<li>${name} <small>${email}</small></li>',
        limit: 200
    }
```

Populate the employee’s email id from local or remote data and set the result to the data of At.js configuration.

## Embed.ly Integration

Rich Text Editor easily integrate with embed.ly which is probably the best service when it comes to embed the rich content such as Twitter, Facebook, Instagram, and lots of other publishing platform embeds.

``` javascript
    <script src="https://cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>
```

In the following sample, the Embed.ly class `embedly-card` has been added to `a` tag in the [actionComplete](/rich-text-editor/api-richTextEditor.html#actioncomplete) event.