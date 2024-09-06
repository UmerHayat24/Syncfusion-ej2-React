---
title: "Rich text editor Editor modes"
component: "Rich Text Editor"
description: "This section for Syncfusion react Rich Text Editor component explains the markdown editing and HTML editing of the content through out the page."
---

# Editor modes

The Rich Text Editor component used to create and edit the content and return valid HTML markup or markdown (MD) of the content. It supports the following two editing formation.

* HTML editor
* Markdown editor

## HTML editor

Rich Text Editor is a WYSIWYG editing control for formatting the word content as HTML.

The HTML editing mode is the default mode in Rich Text Editor to format the content through the available toolbar items to return the valid HTML markup. Set the [editorMode](../api/rich-text-editor/#editormode) property as **HTML**.

> To create Rich Text Editor with HTML editing feature, inject the `HtmlEditor` module to the RTE using the `RichTextEditor.Inject(HtmlEditor)` method.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - HTMLEditor Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public render() {
    return (
      <RichTextEditorComponent height={450}>
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
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}

## Markdown editor

Set the [editorMode](../api/rich-text-editor/#editormode) property as **Markdown**, to create or edit the content and apply formatting to view markdown formatted content.

The third-party library such as `Marked` or any other library is used to convert markdown into HTML content.

* Supported tags are `h6`, `h5`, `h4`, `h3`, `h2`, `h1`, `blockquote`, `pre`, `p`, `OL`, and `UL`.
* Supported selection tags are `Bold`, `Italic`, `StrikeThrough`, `InlineCode`, `SubScript`, `SuperScript`, `UpperCase`, and `LowerCase`.

{% tab template="rich-text-editor/markdown", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - MarkdownEditor Sample
 */
import { createElement, KeyboardEventArgs } from '@syncfusion/ej2-base';
import { Image, Inject, Link, MarkdownEditor, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as Marked from 'marked';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public rteObj: RichTextEditorComponent;

    // Rich Text Editor items list
    public items: object = ['Bold', 'Italic', 'StrikeThrough', '|',
    'Formats', 'OrderedList', 'UnorderedList', '|',
    'CreateLink', 'Image', '|',
    {
        template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
        '<span class="e-btn-icon e-md-preview e-icons"></span></button>',
        tooltipText: 'Preview',
    }, '|', 'Undo', 'Redo'];

  public textArea: HTMLTextAreaElement;
  public mdsource: any;
  public mdPreview: HTMLElement;

  // Rich Text Editor ToolbarSettings
  public toolbarSettings: object = {
      items: this.items
  };
  // set the value to Rich Text Editor
  public template(): JSX.Element {
    return(<div>
    The sample is added to showcase **markdown editing**.
  Type or edit the content and apply formatting to view markdown formatted content.
  We can add our own custom formation syntax for the Markdown formation, [sample link](https://ej2.syncfusion.com/home/).
  The third-party library <b>Marked</b> is used in this sample to convert markdown into HTML content.
      </div>);
  };

    public markDownConversion(): void {
        if (this.mdsource.classList.contains('e-active')) {
            const id: string = this.rteObj.getID() + 'html-view';
            const htmlPreview: HTMLElement = this.rteObj.element.querySelector('#' + id) as any;
            htmlPreview.innerHTML = Marked(((this.rteObj as any).contentModule.getEditPanel() as HTMLTextAreaElement).value);
        }
    }
    public fullPreview(): void {
        const id: string = this.rteObj.getID() + 'html-preview';
        let htmlPreview: HTMLElement = (this.rteObj as any).element.querySelector('#' + id);
        if (this.mdsource.classList.contains('e-active')) {
            this.mdsource.classList.remove('e-active');
            this.mdsource.parentElement.title = 'Preview';
            this.textArea.style.display = 'block';
            htmlPreview.style.display = 'none';
        } else {
            this.mdsource.classList.add('e-active');
            if (!htmlPreview) {
                htmlPreview = createElement('div', { className: 'e-content e-pre-source' });
                htmlPreview.id = id;
                (this.textArea as any).parentNode.appendChild(htmlPreview);
            }
            this.textArea.style.display = 'none';
            htmlPreview.style.display = 'block';
            htmlPreview.innerHTML = Marked(((this.rteObj as any).contentModule.getEditPanel() as HTMLTextAreaElement).value);
            this.mdsource.parentElement.title = 'Code View';
        }
    }
    public rendereComplete(): void {
        this.textArea = (this.rteObj as any).contentModule.getEditPanel() as HTMLTextAreaElement;
        this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
            this.markDownConversion();
        });
        this.mdsource = document.getElementById('preview-code');
        this.mdsource.addEventListener('click', (e: MouseEvent) => {
            this.fullPreview();
            if ((e.currentTarget as HTMLElement).classList.contains('e-active')) {
                this.rteObj.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image', 'Formats', 'Undo', 'Redo']);
            } else {
                this.rteObj.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image', 'Formats', 'Undo', 'Redo']);
            }
        });
    }
    public render() {
        return (
          <RichTextEditorComponent id="markdownRTE" ref={(richtexteditor) => { this.rteObj = richtexteditor! }} editorMode='Markdown'
              height='250px' valueTemplate={this.template} toolbarSettings={this.toolbarSettings} >
              <Inject services={[MarkdownEditor, Toolbar, Image, Link, QuickToolbar]} />
              </RichTextEditorComponent>
        );
    }
}

export default App;

```

{% endtab %}

> To create Rich Text Editor with Markdown editing feature, inject the `MarkdownEditor` module to the RTE using the `RichTextEditor.Inject(MarkdownEditor)` method.

For further details on Markdown editing, refer to the [`Markdown`](/rich-text-editor/markdown.html) section.