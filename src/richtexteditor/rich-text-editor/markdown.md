---
title: "Rich Text Editor Markdown"
component: "Rich Text Editor"
description: "This section for Syncfusion react Rich Text Editor component explains the markdown editing and custom formatting."
---

# Markdown

When you format the word in Markdown format, you should add Markdown syntax to the word to indicate the words and phrases that looks different from each other.

Rich Text Editor supports markdown editing when the [editorMode](../api/rich-text-editor/#editormode) set as **markdown** and using both *keyboard interaction* and *toolbar action*, you can apply the formatting to text.

> To create Rich Text Editor with Markdown editing feature, inject the MarkdownEditor module to the RTE using the `RichTextEditor.Inject(MarkdownEditor)` method.

## Supported Commands

The React Markdown editor supports the following commands to format the markdown content:

|Commands|Syntax| Description |
|--------|------------------------------------------|------------|
| Bold | Sample content for `**`bold text`**`. | For bold, add `**` or `__` to front and back of the text. | For order list, precede each line with a number. |
| Italic | Sample content for `*`Italic text`*`. | For Italic, add `*` or `_` to front and back of the text. |
| Bold and Italics | Sample content for `***`bold and Italic text`***`. | For bold and Italics, add `***` to the front and back of the text. |
| Heading 1 | `#` Heading 1 content | For heading 1, add `#` to start of the line. |
| Heading 2 | `##` Heading 2 content | For heading 2, add `##` to start of the line. |
| Heading 3 | `###` Heading 3 content | For heading 3, add `###` to start of the line. |
| Heading 4 | `####` Heading 4 content | For heading 4, add `####` to start of the line. |
| Heading 5 | `#####` Heading 5 content | For heading 5, add `#####` to start of the line. |
| Heading 6 | `######` Heading 6 content | For heading 6, add `######` to start of the line. |
| Line Break | First line `<br>`Second line | For line break, press enter two times (or) add `<br>` in between the first and the second line. |
| Blockquotes | `>` Blockquotes text | For blockquotes, add `>` to start of the line. |
| Strike Through | Sample content for `~~`strike through text`~~`. | For strike through, add `~~` to front and back of the text. |
| Code (Single line) | \`Single line code\` | For single line code, add \` to front and back of the text. |
| Code block (Multi Line) | \`\`\`<br>Multi line code text<br>Multi line code text<br>\`\`\` | For multiple line code, add \`\`\` in the new line before and after the content. |
| Subscript | `<sub>`Subscript text`</sub>` | For subscript, add `<sub>` to the front and `</sub>` to the back of the text. |
| Superscript | `<sup>`Superscript text`</sup>` | For superscript, add `<sup>` to the front and `</sup>` to the back of the text. |
| Ordered List | `1.` First<br>`1.` Second | For ordered list, preceding one or more lines of text with `1.` |
| Unordered List | `*` First<br>`*` second | For unordered list, preceding one or more lines of text with `*`. |
| Links | **Link text without title text**<br>`[` Link text `](`URL`)`<br> **Link text with title text**<br>`[` Link text `](`URL , “title text”`)` | Create an inline link by wrapping link text in brackets `[ ]`, and then wrapping the URL as first parameter and title as second parameter in the parentheses `()`.<br>**Note:** The title text is optional, if needed it can be given manually.|
| Table | `|` Heading 1 `|` Heading 2 `|`<br>`|---------|---------|`<br>`|` Col A1 `|` Col A2 `|`<br>`|` Col B1 `|` Col B2 `|` | Create a table using the pipes and underscores as given in the syntax to create 2 x 2 table. |
| Horizontal Line | `***` (three asterix in new line)<br>(or)<br>`___` (three underscores in new line) | For horizontal line, add `***` or `___` to the start of the new line. |
| Image | `![](`URL path`)` | Create an image by wrapping the image source in parentheses `()`. |
| Image with alternate text | `![` alternate text `](`URL path`)` | Create an image with alternate text by wrapping an alternative text in brackets `[]`, and then link of the image source in parentheses `()`.<br>**Note:** When inserting the image using toolbar, the alternate text cannot be provided that needs to be given manually. |
| Escape tick marks supported | Sample text content with `**`bold and `**`not bold`**` text can be in the same line.`**` | In the syntax, the whole content is made as bold where the content `not bold` can be made as normal text by adding the bold syntax to the start and end of the respective text. Likewise you can do the same for various inline commands. |
| Escape Character | `\(`any syntax`)` | Escape any markdown syntax by prefix `\` to the syntax.<br>Example:<br>`\**`Bold text`**`|
| HTML Entities | Copyright: &copy; - `&copy;` <br>Trade mark: &trade; - `&trade;`<br>Registered: &reg; - `&reg;`<br>Ampersand: &amp; - `&amp;`<br>Less than: &lt; - `&lt;`<br>Greater than: &gt; - `&gt;` | For HTML entities, add & and ; to the front and back of the respective entities. |

> The above listed commands alone are supported in Syncfusion Markdown editor. For other unsupported commands, you can achieve using the HTML tags in Markdown editor. The foot notes, definitions, math, and check list markdown syntax are also not supported.

## Markdown to HTML

The Rich Text Editor allows you to preview markdown changes immediately using preview. In this sample, the third-party library [Marked](https://marked.js.org/#/README.md#README.md) is used to convert markdown into HTML content.

This sample demonstrates how to preview markdown changes in Rich Text Editor. Type or edit the display text, and apply format to view the preview of markdown. The [actionComplete](../api/rich-text-editor/#actioncomplete) event can be used to convert Markdown to HTML.

{% tab template="rich-text-editor/markdown", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Markdown to HTML Sample
 */
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { createElement, KeyboardEventArgs } from '@syncfusion/ej2-base';
import { Image, Link, MarkdownEditor, RichTextEditor, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
RichTextEditor.Inject(Image, Link, MarkdownEditor, Toolbar);

import * as React from 'react';

class App extends React.Component<{},{}> {
  public mdSource: any;
  public mdSplit: HTMLElement;
  public htmlPreview: any;
  public defaultRTE: RichTextEditor;
  public textArea: HTMLTextAreaElement;

  public value: string = `***Overview***
  The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor used to create and edit the content and return valid HTML markup or markdown (MD) of the content. The editor provides a standard toolbar to format content using its commands. Modular library features to load the necessary functionality on demand. The toolbar contains commands to align the text, insert link, insert image, insert list, undo/redo operation, HTML view, and more.

  ***Key features***
  - *Mode*: Provides IFRAME and DIV mode.
  - *Module*: Modular library to load the necessary functionality on demand.
  - *Toolbar*: Provide a fully customizable toolbar.
  - *Editing*: HTML view to edit the source directly for developers.
  - *Third-party Integration*: Supports to integrate third-party library.
  - *Preview*: Preview the modified content before saving it.
  - *Tools*: Handling images, hyperlinks, video, uploads and more.
  - *Undo and Redo*: Undo/redo manager.
  - *Lists*: Creates bulleted and numbered list.`;

  public componentDidMount(): void {
    this.defaultRTE = new RichTextEditor({
      actionComplete: (e: any) => {
        if (e.targetItem === 'Maximize' && isNullOrUndefined(e.args)) {
          this.fullPreview({ mode: true, type: '' });
        } else if (!(this.mdSplit as any).parentElement.classList.contains('e-overlay')) {
          if (e.targetItem === 'Minimize') {
            this.textArea.style.display = 'block';
            this.textArea.style.width = '100%';
            if (this.htmlPreview) { this.htmlPreview.style.display = 'none'; }
              this.mdSplit.classList.remove('e-active');
              this.mdSource.classList.remove('e-active');
          }
          this.markDownConversion();
        }
        setTimeout(() => {
          this.defaultRTE.toolbarModule.refreshToolbarOverflow();
        }, 400);
      },
      created: () => {
        this.textArea = (this.defaultRTE as any).contentModule.getEditPanel();
        this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
          this.markDownConversion();
        });

        this.mdSource = document.getElementById('preview-code') as any;
        this.mdSource.addEventListener('click', (e: MouseEvent) => {
        this.fullPreview({ mode: true, type: 'preview' });
        if ((e.currentTarget as HTMLElement).classList.contains('e-active')) {
          this.defaultRTE.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', 'Undo', 'Redo']);
          (e.currentTarget as any).parentElement.previousElementSibling.classList.add('e-overlay');
        } else {
          this.defaultRTE.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', 'Undo', 'Redo']);
          (e.currentTarget as any).parentElement.previousElementSibling.classList.remove('e-overlay');
        }
      });
      this.mdSplit = document.getElementById('MD_Preview') as any;
      this.mdSplit.addEventListener('click', (e: MouseEvent) => {
        if (this.defaultRTE.element.classList.contains('e-rte-full-screen')) {
          this.fullPreview({ mode: true, type: '' });
        }
        this.mdSource.classList.remove('e-active');
        if (!this.defaultRTE.element.classList.contains('e-rte-full-screen')) {
          this.defaultRTE.showFullScreen();
        }
      });
    },
      editorMode: 'Markdown',
      height: '300px',
      toolbarSettings: {
        items: [
          'Bold', 'Italic', 'StrikeThrough', '|', 'Formats', 'OrderedList', 'UnorderedList', '|',
          'CreateLink', 'Image', '|',
          {
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-md-preview e-preview e-icons"></span></button>',
            tooltipText: 'Preview'
          },
          {
            template: '<button id="MD_Preview" class="e-tbar-btn e-control e-btn e-icon-btn">' +
                      '<span class="e-btn-icon e-view-side e-icons"></span></button>',
            tooltipText: 'Split Editor',
          },
          'FullScreen', '|', 'Undo', 'Redo']
        },
      valueTemplate: this.value,
    });
    this.defaultRTE.appendTo('#markdownPreview');
  }

  public markDownConversion(): void {
    if (this.mdSplit.classList.contains('e-active')) {
      const id: string = this.defaultRTE.getID() + 'html-preview';
      const htmlPreview: any = this.defaultRTE.element.querySelector('#' + id);
      htmlPreview.innerHTML = marked(((this as any).defaultRTE.contentModule.getEditPanel()).value);
    }
  }

  public fullPreview(e: { [key: string]: string | boolean }): void {
    const id: string = this.defaultRTE.getID() + 'html-preview';
    this.htmlPreview = this.defaultRTE.element.querySelector('#' + id);
    if ((this.mdSource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
      this.mdSource.classList.remove('e-active');
      this.mdSplit.classList.remove('e-active');
      this.mdSource.parentElement.title = 'Preview';
      this.textArea.style.display = 'block';
      this.textArea.style.width = '100%';
      this.htmlPreview.style.display = 'none';
    } else {
      this.mdSource.classList.add('e-active');
      this.mdSplit.classList.add('e-active');
      if (!this.htmlPreview) {
        this.htmlPreview = createElement('div', { className: 'e-content' });
        this.htmlPreview.id = id;
        (this.textArea as any).parentNode.appendChild(this.htmlPreview);
      }
      if (e.type === 'preview') {
        this.textArea.style.display = 'none'; this.htmlPreview.classList.add('e-pre-source');
          this.htmlPreview.style.width = '100%';
      } else {
        this.htmlPreview.classList.remove('e-pre-source');
        this.textArea.style.width = '50%';
        this.htmlPreview.style.width = '50%';
      }
      this.htmlPreview.style.display = 'block';
      this.htmlPreview.innerHTML = marked(((this as any).defaultRTE.contentModule.getEditPanel()).value);
      this.mdSource.parentElement.title = 'Code View';
    }
  }

  public render() {
    return (
      <div id="rte-default" className='control-pane'>
        <div className='control-section' id="rtePreview">
          <div className="content-wrapper">
            <div id="markdownPreview"/>
          </div>
        </div>
      </div>
    );
  }
}

export default App;

```

{% endtab %}

## Table

Rich Text Editor allows to insert Markdown table in edit panel with 2 X 2 rows and columns along with the heading.
To use table tool, add the `CreateTable` item in toolbar items.

### Insert table

To insert the table in Rich Text Editor, click the `table` toolbar option to insert the table into Rich Text Editor content and this is the default way in all the devices.
Please refer the below sample and code snippets to add the table in Markdown editor

{% tab template="rich-text-editor/markdown", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Markdown to HTML Sample
 */
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { createElement, KeyboardEventArgs } from '@syncfusion/ej2-base';
import { Image, Link, MarkdownEditor, RichTextEditor, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
RichTextEditor.Inject(Image, Link, MarkdownEditor, Toolbar);
import * as React from 'react';

class App extends React.Component<{},{}> {
  public mdSource: HTMLElement;
  public mdSplit: HTMLElement;
  public htmlPreview: HTMLElement;
  public defaultRTE: RichTextEditor;
  public textArea: HTMLTextAreaElement;

  public value: string = `***Overview***
  The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor used to create and edit the content and return valid HTML markup or markdown (MD) of the content. The editor provides a standard toolbar to format content using its commands. Modular library features to load the necessary functionality on demand. The toolbar contains commands to align the text, insert link, insert image, insert list, undo/redo operation, HTML view, and more.

  ***Key features***
  - *Mode*: Provides IFRAME and DIV mode.
  - *Module*: Modular library to load the necessary functionality on demand.
  - *Toolbar*: Provide a fully customizable toolbar.
  - *Editing*: HTML view to edit the source directly for developers.
  - *Third-party Integration*: Supports to integrate third-party library.
  - *Preview*: Preview the modified content before saving it.
  - *Tools*: Handling images, hyperlinks, video, uploads and more.
  - *Undo and Redo*: Undo/redo manager.
  - *Lists*: Creates bulleted and numbered list.`;

  public componentDidMount(): void {
    this.defaultRTE = new RichTextEditor({
      actionComplete: (e: any) => {
        if (e.targetItem === 'Maximize' && isNullOrUndefined(e.args)) {
          this.fullPreview({ mode: true, type: '' });
        } else if (!(this as any).mdSplit.parentElement.classList.contains('e-overlay')) {
          if (e.targetItem === 'Minimize') {
            this.textArea.style.display = 'block';
            this.textArea.style.width = '100%';
            if (this.htmlPreview) { this.htmlPreview.style.display = 'none'; }
              this.mdSplit.classList.remove('e-active');
              this.mdSource.classList.remove('e-active');
          }
          this.markDownConversion();
        }
        setTimeout(() => {
          this.defaultRTE.toolbarModule.refreshToolbarOverflow();
        }, 400);
      },
      created: () => {
        this.textArea = (this.defaultRTE as any).contentModule.getEditPanel();
        this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
          this.markDownConversion();
        });
        this.mdSource = document.getElementById('preview-code') as any;
        this.mdSource.addEventListener('click', (e: MouseEvent) => {
        this.fullPreview({ mode: true, type: 'preview' });
        if ((e.currentTarget as HTMLElement).classList.contains('e-active')) {
          this.defaultRTE.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', 'Undo', 'Redo', 'CreateTable']);
          (e.currentTarget as any).parentElement.previousElementSibling.classList.add('e-overlay');
        } else {
          this.defaultRTE.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', 'Undo', 'Redo', 'CreateTable']);
          (e.currentTarget as any).parentElement.previousElementSibling.classList.remove('e-overlay');
        }
      });
      this.mdSplit = document.getElementById('MD_Preview') as any;
      this.mdSplit.addEventListener('click', (e: MouseEvent) => {
        if (this.defaultRTE.element.classList.contains('e-rte-full-screen')) {
          this.fullPreview({ mode: true, type: '' });
        }
        this.mdSource.classList.remove('e-active');
        if (!this.defaultRTE.element.classList.contains('e-rte-full-screen')) {
          this.defaultRTE.showFullScreen();
        }
      });
    },
      editorMode: 'Markdown',
      height: '300px',
      toolbarSettings: {
        items: [
          'Bold', 'Italic', 'StrikeThrough', '|', 'Formats', 'OrderedList', 'UnorderedList', '|',
          'CreateLink', 'Image', 'CreateTable', '|',
          {
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-md-preview e-preview e-icons"></span></button>',
            tooltipText: 'Preview'
          },
          {
            template: '<button id="MD_Preview" class="e-tbar-btn e-control e-btn e-icon-btn">' +
                      '<span class="e-btn-icon e-view-side e-icons"></span></button>',
            tooltipText: 'Split Editor'
          },
          'FullScreen', '|', 'Undo', 'Redo']
        },
      valueTemplate: this.value

    });
    this.defaultRTE.appendTo('#markdownPreview');
  }

  public markDownConversion(): void {
    if (this.mdSplit.classList.contains('e-active')) {
      const id: string = this.defaultRTE.getID() + 'html-preview';
      const htmlPreview: any = this.defaultRTE.element.querySelector('#' + id);
      htmlPreview.innerHTML = marked(((this.defaultRTE as any).contentModule.getEditPanel()).value);
    }
  }

  public fullPreview(e: { [key: string]: string | boolean }): void {
    const id: string = this.defaultRTE.getID() + 'html-preview';
    this.htmlPreview = this.defaultRTE.element.querySelector('#' + id);
    if ((this.mdSource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
      this.mdSource.classList.remove('e-active');
      this.mdSplit.classList.remove('e-active');
      this.mdSource.parentElement.title = 'Preview';
      this.textArea.style.display = 'block';
      this.textArea.style.width = '100%';
      this.htmlPreview.style.display = 'none';
    } else {
      this.mdSource.classList.add('e-active');
      this.mdSplit.classList.add('e-active');
      if (!this.htmlPreview) {
        this.htmlPreview = createElement('div', { className: 'e-content' });
        this.htmlPreview.id = id;
        (this.textArea as any).parentNode.appendChild(this.htmlPreview);
      }
      if (e.type === 'preview') {
        this.textArea.style.display = 'none'; this.htmlPreview.classList.add('e-pre-source');
          this.htmlPreview.style.width = '100%';
      } else {
        this.htmlPreview.classList.remove('e-pre-source');
        this.textArea.style.width = '50%';
        this.htmlPreview.style.width = '50%';
      }
      this.htmlPreview.style.display = 'block';
      this.htmlPreview.innerHTML = marked(((this as any).defaultRTE.contentModule.getEditPanel()).value);
      this.mdSource.parentElement.title = 'Code View';
    }
  }

  public render() {
    return (
      <div id="rte-default" className='control-pane'>
        <div className='control-section' id="rtePreview">
          <div className="content-wrapper">
            <div id="markdownPreview"/>
          </div>
        </div>
      </div>
    );
  }
}

export default App;

```

{% endtab %}

### Changing table constants

The Markdown table constants can be changed for the table heading and the column names.

{% tab template="rich-text-editor/markdown", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Markdown to HTML Sample
 */
import { L10n } from '@syncfusion/ej2-base';
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { createElement, KeyboardEventArgs } from '@syncfusion/ej2-base';
import { Image, Link, MarkdownEditor, RichTextEditor, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
RichTextEditor.Inject(Image, Link, MarkdownEditor, Toolbar);
import * as React from 'react';

L10n.load({
  'en-US': {
      'richtexteditor': {
          'TableColText': 'Cell',
          'TableHeadingText': 'Header'
       }
   }
});

class App extends React.Component<{},{}> {
  public mdSource: HTMLElement;
  public mdSplit: HTMLElement;
  public htmlPreview: HTMLElement;
  public defaultRTE: RichTextEditor;
  public textArea: HTMLTextAreaElement;

  public value: string = `***Overview***
  The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor used to create and edit the content and return valid HTML markup or markdown (MD) of the content. The editor provides a standard toolbar to format content using its commands. Modular library features to load the necessary functionality on demand. The toolbar contains commands to align the text, insert link, insert image, insert list, undo/redo operation, HTML view, and more.

  ***Key features***
  - *Mode*: Provides IFRAME and DIV mode.
  - *Module*: Modular library to load the necessary functionality on demand.
  - *Toolbar*: Provide a fully customizable toolbar.
  - *Editing*: HTML view to edit the source directly for developers.
  - *Third-party Integration*: Supports to integrate third-party library.
  - *Preview*: Preview the modified content before saving it.
  - *Tools*: Handling images, hyperlinks, video, uploads and more.
  - *Undo and Redo*: Undo/redo manager.
  - *Lists*: Creates bulleted and numbered list.`;

  public componentDidMount(): void {
    this.defaultRTE = new RichTextEditor({
      actionComplete: (e: any) => {
        if (e.targetItem === 'Maximize' && isNullOrUndefined(e.args)) {
          this.fullPreview({ mode: true, type: '' });
        } else if (!(this.mdSplit as any).parentElement.classList.contains('e-overlay')) {
          if (e.targetItem === 'Minimize') {
            this.textArea.style.display = 'block';
            this.textArea.style.width = '100%';
            if (this.htmlPreview) { this.htmlPreview.style.display = 'none'; }
              this.mdSplit.classList.remove('e-active');
              this.mdSource.classList.remove('e-active');
          }
          this.markDownConversion();
        }
        setTimeout(() => {
          this.defaultRTE.toolbarModule.refreshToolbarOverflow();
        }, 400);
      },
      created: () => {
        this.textArea = (this.defaultRTE as any).contentModule.getEditPanel();
        this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
          this.markDownConversion();
        });
        this.mdSource = document.getElementById('preview-code') as any;
        this.mdSource.addEventListener('click', (e: MouseEvent) => {
        this.fullPreview({ mode: true, type: 'preview' });
        if ((e.currentTarget as HTMLElement).classList.contains('e-active')) {
          this.defaultRTE.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', 'Undo', 'Redo', 'CreateTable']);
          (e.currentTarget as any).parentElement.previousElementSibling.classList.add('e-overlay');
        } else {
          this.defaultRTE.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', 'Undo', 'Redo', 'CreateTable']);
          (e.currentTarget as any).parentElement.previousElementSibling.classList.remove('e-overlay');
        }
      });
      this.mdSplit = document.getElementById('MD_Preview') as any;
      this.mdSplit.addEventListener('click', (e: MouseEvent) => {
        if (this.defaultRTE.element.classList.contains('e-rte-full-screen')) {
          this.fullPreview({ mode: true, type: '' });
        }
        this.mdSource.classList.remove('e-active');
        if (!this.defaultRTE.element.classList.contains('e-rte-full-screen')) {
          this.defaultRTE.showFullScreen();
        }
      });
    },
    editorMode: 'Markdown',
      height: '300px',
      toolbarSettings: {
        items: [
          'Bold', 'Italic', 'StrikeThrough', '|', 'Formats', 'OrderedList', 'UnorderedList', '|',
          'CreateLink', 'Image', 'CreateTable', '|',
          {
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-md-preview e-preview e-icons"></span></button>',
            tooltipText: 'Preview'
          },
          {
            template: '<button id="MD_Preview" class="e-tbar-btn e-control e-btn e-icon-btn">' +
                      '<span class="e-btn-icon e-view-side e-icons"></span></button>',
                      tooltipText: 'Split Editor'
          },
          'FullScreen', '|', 'Undo', 'Redo']
        },
      valueTemplate: this.value,

    });
    this.defaultRTE.appendTo('#markdownPreview');
  }

  public markDownConversion(): void {
    if (this.mdSplit.classList.contains('e-active')) {
      const id: string = this.defaultRTE.getID() + 'html-preview';
      const htmlPreview: HTMLElement = this.defaultRTE.element.querySelector('#' + id) as any;
      htmlPreview.innerHTML = marked(((this.defaultRTE as any).contentModule.getEditPanel()).value);
    }
  }

  public fullPreview(e: { [key: string]: string | boolean }): void {
    const id: string = this.defaultRTE.getID() + 'html-preview';
    this.htmlPreview = this.defaultRTE.element.querySelector('#' + id);
    if ((this.mdSource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
      this.mdSource.classList.remove('e-active');
      this.mdSplit.classList.remove('e-active');
      this.mdSource.parentElement.title = 'Preview';
      this.textArea.style.display = 'block';
      this.textArea.style.width = '100%';
      this.htmlPreview.style.display = 'none';
    } else {
      this.mdSource.classList.add('e-active');
      this.mdSplit.classList.add('e-active');
      if (!this.htmlPreview) {
        this.htmlPreview = createElement('div', { className: 'e-content' });
        this.htmlPreview.id = id;
        (this.textArea as any).parentNode.appendChild(this.htmlPreview);
      }
      if (e.type === 'preview') {
        this.textArea.style.display = 'none'; this.htmlPreview.classList.add('e-pre-source');
          this.htmlPreview.style.width = '100%';
      } else {
        this.htmlPreview.classList.remove('e-pre-source');
        this.textArea.style.width = '50%';
        this.htmlPreview.style.width = '50%';
      }
      this.htmlPreview.style.display = 'block';
      this.htmlPreview.innerHTML = marked(((this as any).defaultRTE.contentModule.getEditPanel()).value);
      this.mdSource.parentElement.title = 'Code View';
    }
  }

  public render() {
    return (
      <div id="rte-default" className='control-pane'>
        <div className='control-section' id="rtePreview">
          <div className="content-wrapper">
            <div id="markdownPreview"/>
          </div>
        </div>
      </div>
    );
  }
}

export default App;

```

{% endtab %}

## Custom format

The Rich Text Editor allows you to customize the markdown syntax by overriding its default syntax. Configure the customized markdown syntax using the [formatter](../api/rich-text-editor/#formatter) property.

This sample demonstrates how to customize tags of markdown formatting.

For example, apply `+` to Unordered list, apply `1., 2., 3.` to Ordered list, for bold, `__`, and for italic `_`.

{% tab template="rich-text-editor/markdown", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Markdown - Custom Format Sample
 */
import { createElement, KeyboardEventArgs } from '@syncfusion/ej2-base';
import { Image, Inject, Link, MarkdownEditor, MarkdownFormatter, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public rteObj: RichTextEditorComponent;

    // set the value to Rich Text Editor
    public template: string = `The sample is configured with customized markdown syntax using the __formatter__ property. Type the content and click the toolbar item to view customized markdown syntax. For unordered list, you need to add a plus sign before the word (e.g., + list1). Or To make a phrase bold, you need to add two underscores before and after the phrase (e.g., __this text is bold__).`;

    // Rich Text Editor items list
    public items: object = ['Bold', 'Italic', 'StrikeThrough', '|',
    'Formats', 'OrderedList', 'UnorderedList', '|',
    'CreateLink', 'Image', '|',
    {
        template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-icons e-md-preview"></span></button>',
            tooltipText: 'Preview',
    }, 'Undo', 'Redo'];

    public textArea: HTMLTextAreaElement;
    public mdsource: HTMLElement;
    public mdPreview: HTMLElement;

    // Rich Text Editor ToolbarSettings
    public toolbarSettings: object = {
        items: this.items
    };

    public formatter = new MarkdownFormatter({
        formatTags: {
            'Blockquote': '> '
        },
        listTags: { 'OL': '1., 2., 3.', 'UL': '+ ' },
        selectionTags: {'Bold': '__',  'Italic': '_'}
    });

    public markDownConversion(): void {
        if (this.mdsource.classList.contains('e-active')) {
            const id: string = (this.rteObj as any).getID() + 'html-view';
            const htmlPreview: HTMLElement = (this.rteObj as any).element.querySelector('#' + id);
            htmlPreview.innerHTML = marked(((this.rteObj as any).contentModule.getEditPanel()).value);
        }
    }
    public fullPreview(e: { [key: string]: string | boolean }): void {
    const id: string = this.defaultRTE.getID() + 'html-preview';
    this.htmlPreview = this.defaultRTE.element.querySelector('#' + id);
    if ((this.mdSource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
      this.mdSource.classList.remove('e-active');
      this.mdSplit.classList.remove('e-active');
      this.mdSource.parentElement.title = 'Preview';
      this.textArea.style.display = 'block';
      this.textArea.style.width = '100%';
      this.htmlPreview.style.display = 'none';
    } else {
      this.mdSource.classList.add('e-active');
      this.mdSplit.classList.add('e-active');
      if (!this.htmlPreview) {
        this.htmlPreview = createElement('div', { className: 'e-content' });
        this.htmlPreview.id = id;
        (this.textArea as any).parentNode.appendChild(this.htmlPreview);
      }
      if (e.type === 'preview') {
        this.textArea.style.display = 'none'; this.htmlPreview.classList.add('e-pre-source');
          this.htmlPreview.style.width = '100%';
      } else {
        this.htmlPreview.classList.remove('e-pre-source');
        this.textArea.style.width = '50%';
        this.htmlPreview.style.width = '50%';
      }
      this.htmlPreview.style.display = 'block';
      this.htmlPreview.innerHTML = marked(((this as any).defaultRTE.contentModule.getEditPanel()).value);
      this.mdSource.parentElement.title = 'Code View';
    }
  }
    public render() {
      return (
      <RichTextEditorComponent id="markdownRTE"
          ref={(richtexteditor) => { this.rteObj = richtexteditor! }}
          height='260px' editorMode='Markdown'
          formatter= {this.formatter}
          valueTemplate={this.template} toolbarSettings={this.toolbarSettings} >
          <Inject services={[MarkdownEditor, Toolbar, Image, Link, QuickToolbar]} />
      </RichTextEditorComponent>
      );
    }
}

export default App;

```

{% endtab %}