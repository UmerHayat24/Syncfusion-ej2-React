---
title: "React Rich text editor Toolbar configuration"
component: "Rich Text Editor"
description: "This section for Syncfusion react Rich Text Editor component explains the toolbar which provides a set of commands for editing and formatting the content."
---

# Toolbar

The Rich Text Editor toolbar contains a collection of tools such as bold, italic, and text alignment buttons that are used to format the content. However, in most integrations, you can customize the toolbar configurations easily to suit your needs.

To create Rich Text Editor with Markdown editing feature, inject the toolbar module to the RTE using the `RichTextEditor.Inject(Toolbar)` method.

The Rich Text Editor allows you to configure the different types of toolbar using the toolbarSettings.type property. The types of toolbar are:

* Expand
* MultiRow

## Expand Toolbar

The default mode of [toolbarSettings.type](/rich-text-editor/api-toolbarSettings.html#type) is Expand to hide the overflowing items in the next row. By clicking the expand arrow, view the overflowing toolbar items.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Expand Toolbar Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public toolbarSettings: object = {
    items: ['Bold', 'Italic', 'Underline', 'StrikeThrough',
      'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
      'LowerCase', 'UpperCase', '|',
      'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
      'Outdent', 'Indent', '|',
      'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
      'SourceCode', 'FullScreen', '|', 'Undo', 'Redo'
    ],
    type: 'Expand'
  }

  public render() {
    return (
      <RichTextEditorComponent height={450} toolbarSettings={this.toolbarSettings}>
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

## MultiRow toolbar

Set the [`toolbarSettings.type`](/rich-text-editor/api-toolbarSettings.html#type) as MultiRow to hide the overflowing items in the next row. All toolbar items are visible.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - MultiRow Toolbar Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  private toolbarSettings: object = {
    items: ['Bold', 'Italic', 'Underline', 'StrikeThrough',
      'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
      'LowerCase', 'UpperCase', '|',
      'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
      'Outdent', 'Indent', '|',
      'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
      'SourceCode', 'FullScreen', '|', 'Undo', 'Redo'
    ],
    type: 'MultiRow'
  }

  public render() {
    return (
      <RichTextEditorComponent height={450} toolbarSettings={this.toolbarSettings}>
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

## Floating toolbar

By default, the toolbar is floating at the top of the Rich Text Editor on scrolling. It can be customized by specifying the offset of the floating toolbar from documents top position using [floatingToolbarOffset](../api/rich-text-editor/#floatingtoolbaroffset).

Enable or disable the floating toolbar using [enableFloating](/rich-text-editor/api-toolbarSettings.html#enablefloating) of the toolbarSetting property.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Floating Toolbar Sample
 */
import { ChangeEventArgs } from '@syncfusion/ej2-buttons';
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public checkboxObj: CheckBoxComponent;
  public rteObj: RichTextEditorComponent;

  public toolbarSettings: object = {
    enableFloating: false
  }

  public onChange(args: ChangeEventArgs): void {
    this.rteObj.toolbarSettings.enableFloating = args.checked;
    this.rteObj.dataBind();
  }

  public render() {
    return (
      <div>
        <CheckBoxComponent checked={false} label='Enable Floating' ref={(scope) => { this.checkboxObj = scope! }} change={ this.onChange=this.onChange.bind(this) } />
        <br />
        <br />
        <br />
        <RichTextEditorComponent ref={(scope) => { this.rteObj = scope! }} height={450} toolbarSettings={this.toolbarSettings}>
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
      </div>
    );
  }
}

export default App;

```

{% endtab %}

## Toolbar items

The following table lists the tools available in the toolbar.

| **Name** | **Summary** | **Initialization** |
| --- | --- | --- |
| Undo | Allows to undo the actions. | toolbarSettings: { <br /> items: ['Undo'] <br /> } |
| Redo | Allows to redo the actions. | toolbarSettings: { <br /> items: ['Redo'] <br /> } |
| Alignment | Align the content with left, center, and right margin. | toolbarSettings: { <br /> items: ['Alignments'] <br /> } |
| OrderedList | Create a new list item (numbered). | toolbarSettings: { <br /> items: ['OrderedList'] <br /> } |
| UnorderedList | Create a new list item (bulleted). | toolbarSettings: { <br /> items: ['UnorderedList'] <br /> } |
| Indent |Allows to increase the indent level of the content. | toolbarSettings: { <br /> items: ['Indent'] <br /> } |
| Outdent | Allows to decrease the indent level of the content. | toolbarSettings: { <br /> items: ['Outdent'] <br /> } |
| Hyperlink | Creates a hyperlink to a text or image to a specific location in the content. | toolbarSettings: { <br /> items: ['CreateLink'] <br /> } |
| Images | Inserts an image from an online source or local computer. | toolbarSettings: { <br /> items: ['Image'] <br /> } |
| LowerCase | Change the case of selected text to lower in the content. | toolbarSettings: { <br /> items: ['LowerCase'] <br /> } |
| UpperCase | Change the case of selected text to upper in the content. | toolbarSettings: { <br /> items: ['UpperCase'] <br /> } |
| SubScript | Makes the selected text as subscript (lower). | toolbarSettings: { <br /> items: ['SubScript'] <br /> } |
| SuperScript | Makes the selected text as superscript (higher). | toolbarSettings: { <br /> items: ['SuperScript'] <br /> } |
| Print  | Allows to print the editor content. | toolbarSettings: { <br /> items: ['Print'] <br /> } |
| FontName | Defines the fonts that appear under the Font Family DropDownList from the Rich Text Editor's toolbar. | toolbarSettings: { <br /> items: ['FontName'] <br /> } |
| FontSize | Defines the font sizes that appear under the Font Size DropDownList from the Rich Text Editor's toolbar. | toolbarSettings: { <br /> items: ['FontSize'] <br /> } |
| FontColor | Specifies an array of colors can be used in the colors pop-up for font color. | toolbarSettings: { <br /> items: ['FontColor'] <br /> } |
| BackgroundColor | Specifies an array of colors can be used in the colors pop-up for background color. | toolbarSettings: { <br /> items: ['BackgroundColor'] <br /> } |
| Format | An object with the options that will appear in the paragraph format drop-down from the toolbar. | toolbarSettings: { <br /> items: ['Formats'] <br /> } |
| StrikeThrough | Apply double line strike through formatting for the selected text. | toolbarSettings: { <br /> items: ['StrikeThrough'] <br /> } |
| ClearFormat | The clear format tool is used to remove all formatting styles (such as bold, italic, underline, color, superscript, subscript, and more) from currently selected text. As a result, all the formatting text will be cleared and return to its default formatting styles. | toolbarSettings: { <br /> items: ['ClearFormat'] <br /> } |
| FullScreen | Stretches the editor to the maximum width and height of the browser window. | toolbarSettings: { <br /> items: ['FullScreen'] <br /> } |
| SourceCode | The RichTextBox includes the ability for users to directly edit the HTML code via Source View. If you made any modification in source view directly, synchronize with design view. | toolbarSettings: { <br /> items: ['SourceCode'] <br /> } |
| NumberFormatList | Allows to create list items with various list style types(numbered).|toolbarSettings: { <br /> items: ['NumberFormatList'] <br /> } |
| BulletFormatList | Allows to create list items with various list style types(bulleted).|toolbarSettings: { <br /> items: ['BulletFormatList'] <br /> } |
| JustifyLeft | Allows each line to begin at the same distance from the editor’s left-hand side. | toolbarSettings: { <br /> items: ['JustifyLeft'] <br /> }  |
| JustifyCenter |There is an even space on each side of each line since the text is not aligned to the left or right margins. | toolbarSettings: { <br /> items: ['JustifyCenter'] <br /> }  |
| JustifyRight | Allows each line to end at the same distance from the editor’s right-hand side. | toolbarSettings: { <br /> items: ['JustifyRight'] <br /> } |
| JustifyFull |The text is aligned with both right and left margins. | toolbarSettings: { <br /> items: ['JustifyFull'] <br /> }  |
| Bold | Text that is thicker and darker than usual. | toolbarSettings: { <br /> items: ['Bold'] <br /> }  |
| Italic |Shows a text that is leaned to the right. | toolbarSettings: { <br /> items: ['Italic'] <br /> }  |
| Underline | The underline is added to the selected text. | toolbarSettings: { <br /> items: ['Italic'] <br /> }  |
| ClearAll | Removes all styles that have been applied to the selected text.| toolbarSettings: { <br /> items: ['ClearAll'] <br /> }  |
| Cut | Removes the text from its current location and places it into the clipboard. | toolbarSettings: { <br /> items: ['Cut'] <br /> }  |
| Copy | The selected item is copied and pasted into the clipboard. | toolbarSettings: { <br /> items: ['Copy'] <br /> }  |
| Paste | Allows you to insert a clipboard item into a specific location. | toolbarSettings: { <br /> items: ['Paste'] <br /> }  |
| OpenLink | To open the URL link that is  attached to the selected text. | toolbarSettings: { <br /> items: ['OpenLink'] <br /> }  |
| EditLink | Allows you to change the URL that has been attached to a specific item. | toolbarSettings: { <br /> items: ['EditLink'] <br /> }  |
| CreateTable | Create a table with defined columns and rows. | toolbarSettings: { <br /> items: ['CreateTable'] <br /> }  |
| RemoveTable | Removes the selected table and its contents. | toolbarSettings: { <br /> items: ['RemoveTable'] <br /> }  |
| Replace | Replace the selected image with another image. | toolbarSettings: { <br /> items: ['Replace'] <br /> } |
| Align | The image can be aligned to the right, left, or center. | toolbarSettings: { <br /> items: ['Align'] <br /> }  |
| Remove | Allows to remove the selected image from the editor. | toolbarSettings: { <br /> items: ['Remove'] <br /> }  |
| OpenImageLink | Opens the link that is attached to the selected image. | toolbarSettings: { <br /> items: ['OpenImageLink'] <br /> }  |
| EditImageLink | Allows to edit the link that is attached to the selected image. |toolbarSettings: { <br /> items: ['EditImageLink'] <br /> }  |
| RemoveImageLink | Removes the link that is attached to the selected image. | toolbarSettings: { <br /> items: ['RemoveImageLink'] <br /> }  |
| InsertLink |Allows users to add a link to a particular item. | toolbarSettings: { <br /> items: ['InsertLink'] <br /> }  |
| Display | Allows you to choose whether an image should be shown inline or as a block. | toolbarSettings: { <br /> items: ['Display'] <br /> }  |
| AltText | To display image description when an image on a Web page cannot be displayed. | toolbarSettings: { <br /> items: ['AltText'] <br /> }  |
| Dimension | Allows you to customize the image’s height and width. | toolbarSettings: { <br /> items: ['Dimension'] <br /> }  |
| Maximize | Stretches the editor to the maximum width and height of the browser window. | toolbarSettings: { <br /> items: ['Maximize'] <br /> }  |
| Minimize | Shrinks the editor to the default width and height. | toolbarSettings: { <br /> items: ['Minimize'] <br /> }  |
| Preview | Allows to see how the editor’s content looks in a browser. | toolbarSettings: { <br /> items: ['Preview'] <br /> }  |
| InsertCode |Represents preformatted text which is to be presented exactly as written in the HTML file. | toolbarSettings: { <br /> items: ['InsertCode'] <br /> }  |
| RemoveLink | Allows you to remove the applied link from the selected item. | toolbarSettings: { <br /> items: ['RemoveLink'] <br /> }  |
| TableHeader | Allows you to add a table header. | toolbarSettings: { <br /> items: ['TableHeader'] <br /> }  |
| TableColumns | Shows the dropdown to insert a column or delete the selected column. | toolbarSettings: { <br /> items: ['TableColumns'] <br /> } |
| TableRows | Shows the dropdown to insert a row ors delete the selected row. | toolbarSettings: { <br /> items: ['TableRows'] <br /> } |
| TableCellBackground | Summary | toolbarSettings: { <br /> items: ['TableCellBackground'] <br /> }  |
| TableCellHorizontalAlign | Allows the table cell content to be aligned horizontally. | toolbarSettings: { <br /> items: ['TableCellHorizontalAlign'] <br /> }  |
| TableCellVerticalAlign | Allows the table cell content to be aligned vertically. | toolbarSettings: toolbarSettings: { <br /> items: ['TableCellVerticalAlign'] <br /> } |
| TableEditProperties | Allows you to change the table width, padding, and cell spacing styles. | toolbarSettings: { <br /> items: ['TableEditProperties'] <br /> }  |

By default, tools will be arranged in the following order.

``` javascript
  items: ['Bold', 'Italic', 'Underline', '|', 'Formats', 'Alignments', 'OrderedList', 'UnorderedList', '|', 'CreateLink', 'Image', '|', 'SourceCode', 'Undo', 'Redo']
```

The tools order can be customized as our application requirement. If you are not specifying any tools order, the editor will create the toolbar with default items.

## Custom tool

The Rich Text Editor allows you to configure your own commands to its toolbar using the [toolbarSettings](/rich-text-editor/api-toolbarSettings.html) property. The command can be plain text, icon, or HTML template. The order and the group can also be defined where the command should be included. Bind the action to the command by getting its instance.

This sample shows how to add your own commands to the toolbar of the Rich Text Editor. The **Ω** command is added to insert special characters in the editor. By clicking the **Ω** command, it will show the special characters list, and then choose the character to be inserted in the editor.

The following code snippet illustrates custom tool with tooltip text which will be included in [items](/rich-text-editor/api-toolbarSettings.html#items) field of the toolbarSettings property.

In the following sample, once Rich Text Editor control is [created](../api/rich-text-editor/#created), the concern event will be created; the Dialog component can be rendered and target as RTE content.

```javascript
    {
      template: '<button class="e-tbar-btn e-btn" tabindex="-1" id="custom_tbar"  style="width:100%"><div class="e-tbar-btn-text" style="font-weight: 500;"> &#937;</div></button>',
      undo: true,
      click: this.onClick.bind(this),
      tooltipText: 'Insert Symbol'
    }

```

{% tab template="rich-text-editor/custom-tool", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Custom Tool Sample
 */
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { HtmlEditor, Image, Inject, Link, NodeSelection, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public rteObj: RichTextEditorComponent;
  // set the value to Rich Text Editor
  public template: string = `<div style="display:block;"><p style="margin-right:10px">The custom command "insert special character" is configured as the last item of the toolbar. Click on the command and choose the special character you want to include from the popup.</p></div>`;

  public selection: NodeSelection = new NodeSelection();
  public ranges: Range;
  public dialogObj: DialogComponent;
  // Rich Text Editor items list
  public items: object = ['Bold', 'Italic', 'Underline', '|', 'Formats', 'Alignments', 'OrderedList',
    'UnorderedList', '|', 'CreateLink', 'Image', '|', 'SourceCode',
    {
      template: '<button class="e-tbar-btn e-btn" tabindex="-1" id="custom_tbar"  style="width:100%"><div class="e-tbar-btn-text" style="font-weight: 500;"> &#937;</div></button>',
      undo: true,
      click: this.onClick.bind(this),
      tooltipText: 'Insert Symbol'
    }, '|', 'Undo', 'Redo'
  ];

  // Rich Text Editor ToolbarSettings
  public toolbarSettings: object = {
    items: this.items
  };

  public dlgButtons: any = [
    { buttonModel: { content: "Insert", isPrimary: true }, click: this.onInsert.bind(this) },
    { buttonModel: { content: 'Cancel' }, click: this.onCancel }
  ];
  public header: string = 'Special Characters';
  public target: Element = document.getElementById('rteSection') as any;
  public height: any = 'auto';


  public dialogCreate(): void {
    const dialogCtn: HTMLElement = document.getElementById('rteSpecial_char') as HTMLElement;
    dialogCtn.onclick = (e: Event) => {
      const target: HTMLElement = e.target as HTMLElement;
      const activeEle: Element = this.dialogObj.element.querySelector('.char_block.e-active') as HTMLElement;
      if (target.classList.contains('char_block')) {
        target.classList.add('e-active');
        if (activeEle) {
          activeEle.classList.remove('e-active');
        }
      }
    };
  }

  public onInsert(): void {
    const activeEle: Element = this.dialogObj.element.querySelector('.char_block.e-active') as any;
    if (activeEle) {
      this.ranges.insertNode(document.createTextNode(activeEle.textContent as string));
    }
    this.dialogOverlay();
  }

  public onClick(): void {
      this.ranges = this.selection.getRange(document);
      this.dialogObj.width = (this.rteObj as any).element.offsetWidth * 0.5;
      this.dialogObj.content = document.getElementById('rteSpecial_char') as HTMLElement;
      this.dialogObj.dataBind();
      this.dialogObj.show();
  }

  public dialogOverlay(): void {
    const activeEle: Element = this.dialogObj.element.querySelector('.char_block.e-active') as HTMLElement;
    if (activeEle) {
      activeEle.classList.remove('e-active');
    }
    this.dialogObj.hide();
  }

  public onCancel(e: any): void {
    const activeEle: Element = (this as any).element.querySelector('.char_block.e-active');
    if (activeEle) {
      activeEle.classList.remove('e-active');
    }
    (this as any).hide();
  }

  public render() {
    const hideDiv = { display: "none" };
    return (
      <div className='control-pane'>
        <div className='control-section e-rte-custom-tbar-section' id="rteCustomTool">
          <div className='rte-control-section' id='rteSection'>
            <RichTextEditorComponent id="defaultRTE" ref={(scope) => { this.rteObj = scope! }}
              valueTemplate={this.template} toolbarSettings={this.toolbarSettings}>
              <Inject services={[HtmlEditor, Toolbar, Link, Image, QuickToolbar]} />
            </RichTextEditorComponent>
            <DialogComponent id='customTbarDlg' ref={(scope) => { this.dialogObj = scope! }}
              buttons={this.dlgButtons} overlayClick={this.dialogOverlay = this.dialogOverlay.bind(this) } header={this.header} visible={false}
              showCloseIcon={false} target={'#rteSection'} height={this.height} created={this.dialogCreate = this.dialogCreate.bind(this)} isModal={true} />
            <div id="customTbarDialog" style={hideDiv}>
              <div id="rteSpecial_char">
                <div className="char_block" title="&#94;">&#94;</div>
                <div className="char_block" title="&#95;">&#95;</div>
                <div className="char_block" title="&#96;">&#96;</div>
                <div className="char_block" title="&#123;">&#123;</div>
                <div className="char_block" title="&#124;">&#124;</div>
                <div className="char_block" title="&#125;">&#125;</div>
                <div className="char_block" title="&#126;">&#126;</div>
                <div className="char_block" title="&#160;">&#160;</div>
                <div className="char_block" title="&#161;">&#161;</div>
                <div className="char_block" title="&#162;">&#162;</div>
                <div className="char_block" title="&#163;">&#163;</div>
                <div className="char_block" title="&#164;">&#164;</div>
                <div className="char_block" title="&#165;">&#165;</div>
                <div className="char_block" title="&#x20B9;">&#x20B9;</div>
                <div className="char_block" title="&#166;">&#166;</div>
                <div className="char_block" title="&#167;">&#167;</div>
                <div className="char_block" title="&#168;">&#168;</div>
                <div className="char_block" title="&#169;">&#169;</div>
                <div className="char_block" title="&#170;">&#170;</div>
                <div className="char_block" title="&#171;">&#171;</div>
                <div className="char_block" title="&#172;">&#172;</div>
                <div className="char_block" title="&#173;">&#173;</div>
                <div className="char_block" title="&#174;">&#174;</div>
                <div className="char_block" title="&#175;">&#175;</div>
                <div className="char_block" title="&#176;">&#176;</div>
                <div className="char_block" title="&#177;">&#177;</div>
                <div className="char_block" title="&#178;">&#178;</div>
                <div className="char_block" title="&#179;">&#179;</div>
                <div className="char_block" title="&#180;">&#180;</div>
                <div className="char_block" title="&#181;">&#181;</div>
                <div className="char_block" title="&#182;">&#182;</div>
                <div className="char_block" title="&#183;">&#183;</div>
                <div className="char_block" title="&#184;">&#184;</div>
                <div className="char_block" title="&#185;">&#185;</div>
                <div className="char_block" title="&#186;">&#186;</div>
                <div className="char_block" title="&#187;">&#187;</div>
                <div className="char_block" title="&#188;">&#188;</div>
                <div className="char_block" title="&#189;">&#189;</div>
                <div className="char_block" title="&#190;">&#190;</div>
                <div className="char_block" title="&#191;">&#191;</div>
                <div className="char_block" title="&#192;">&#192;</div>
                <div className="char_block" title="&#193;">&#193;</div>
                <div className="char_block" title="&#194;">&#194;</div>
                <div className="char_block" title="&#195;">&#195;</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

export default App;

```

{% endtab %}

## Quick inline toolbar

Quick commands are opened as context-menu on clicking the corresponding element. The commands must be passed as string collection to image, text, and link attributes of the [quickToolbarSettings](/rich-text-editor/api-quickToolbarSettings.html) property.

| **Target element** | **Default quick toolbar items** |
| --- | --- |
| Image | 'Replace', 'Align', 'Caption', 'Remove', 'InsertLink', 'Display', 'AltText', and 'Dimension' |
| Link | 'Open', 'Edit', and 'UnLink' |
| Text (`Deprecated`) | 'Cut', 'Copy', and 'Paste' |

Custom tool can be added to the corresponding quick toolbar, using the [quickToolbarSettings](/rich-text-editor/api-quickToolbarSettings.html)  property.

The following sample demonstrates the option to insert the image to the Rich Text Editor content as well as option to rotate the image through the quick toolbar. The image rotation functionalities have been achieved through the [toolbarClick](../api/rich-text-editor/#toolbarclick) event.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Quick Inline Toolbar Sample
 */
import { HtmlEditor, Image, Inject, Link, NodeSelection, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public rteObj: RichTextEditorComponent;
  public quickToolbarSettings: object = {
    image: [
      'Replace', 'Align', 'Caption', 'Remove', 'InsertLink', 'OpenImageLink', '-',
      'EditImageLink', 'RemoveImageLink', 'Display', 'AltText', 'Dimension',
      {
        template: '<button class="e-tbar-btn e-btn" id="roatateLeft"><span class="e-btn-icon e-icons e-rotate-left"></span>',
        tooltipText: 'Rotate Left'
      },
      {
        template: '<button class="e-tbar-btn e-btn" id="roatateRight"><span class="e-btn-icon e-icons e-rotate-right"></span>',
        tooltipText: 'Rotate Right'
      }
    ]
  }

  public onToolbarClick(e: any): void {
    const nodeObj: NodeSelection = new NodeSelection();
    const range: Range = nodeObj.getRange((this.rteObj as any).contentModule.getDocument());
    const imgEle: HTMLElement = nodeObj.getNodeCollection(range)[0] as HTMLElement;
    if (e.item.tooltipText === 'Rotate Right') {
      const transform: number = (imgEle.style.transform === '') ? 0 :
      parseInt((imgEle as any).style.transform.split('(')[1].split(')')[0], 10);
      imgEle.style.transform = 'rotate(' + (transform + 90) + 'deg)';
    } else if (e.item.tooltipText === 'Rotate Left') {
      const transform: number = (imgEle.style.transform === '') ? 0 :
      Math.abs(parseInt((imgEle as any).style.transform.split('(')[1].split(')')[0], 10));
      imgEle.style.transform = 'rotate(-' + (transform + 90) + 'deg)';
    }
  }

  public render() {
    return (
      <RichTextEditorComponent height={450} ref={(richtexteditor) => { this.rteObj = richtexteditor! }} quickToolbarSettings={this.quickToolbarSettings} toolbarClick={this.onToolbarClick = this.onToolbarClick.bind(this)}>
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

> Rich Text Editor features are segregated into individual feature-wise modules. To use quick toolbar, inject the quick toolbar module using the `RichTextEditor.Inject(image, link)`.