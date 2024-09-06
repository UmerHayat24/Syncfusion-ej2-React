---
title: "Working with Text Formatting"
component: "DocumentEditor"
description: "Learn text formatting supported in React document editor and how to apply it for selected contents."
---

# Working with Text Formatting

Document Editor supports several formatting options for text like bold, italic, font color, highlight color, and more. This section describes how to modify the formatting for selected text in detail.

## Bold

The bold formatting for selected text can be get or set by using the following sample code.

{% tab compileJsx=true%}

```typescript

//Gets the value for bold formatting of selected text.
let bold : boolean = documenteditor.selection.characterFormat.bold;
//Sets bold formatting for selected text.
documenteditor.selection.characterFormat.bold = true;

```

{% endtab %}

You can toggle the bold formatting based on existing value at selection. Refer to the following sample code.

```typescript
documenteditor.editor.toggleBold();
```

## Italic

The Italic formatting for selected text can be get or set by using the following sample code.

```typescript
documenteditor.selection.characterFormat.italic= true|false;
```

You can toggle the Italic formatting based on existing value at selection. Refer to the following sample code.

```typescript
documenteditor.editor.toggleItalic();
```

## Underline property

The underline style for selected text can be get or set by using the following sample code.

```typescript
documenteditor.selection.characterFormat.underline='Single' | 'None';
```

You can toggle the underline style of selected text based on existing value at selection by specifying a value. Refer to the following sample code.

```typescript
documenteditor.editor.toggleUnderline('Single');
```

## Strikethrough property

The strikethrough style for selected text can be get or set by using the following sample code.

```typescript
documenteditor.selection.characterFormat.strikethrough='Single' | 'Normal';
```

You can toggle the strikethrough style of selected text based on existing value at selection by specifying a value. Refer to the following sample code.

```typescript
documenteditor.editor.toggleStrikethrough();
```

## Superscript property

The selected text can be made superscript by using the following sample code.

```typescript
documenteditor.selection.characterFormat.baselineAlignment='Superscript';
```

Toggle the selected text as superscript or normal using the following sample code.

```typescript
documenteditor.editor.toggleSuperscript();
```

## Subscript property

The selected text can be made subscript by using the following sample code.

```typescript
documenteditor.selection.characterFormat.baselineAlignment='Subscript';
```

Toggle the selected text as subscript or normal using the following sample code.

```typescript
documenteditor.editor.toggleSubscript();
```

You can make a subscript or superscript text as normal using the following code.

```typescript
documenteditor.selection.characterFormat.baselineAlignment='Normal';
```

## Size

The size of selected text can be get or set using the following code.

```typescript
documenteditor.selection.characterFormat.fontSize= 32;
```

## Color

The color of selected text can be get or set using the following code.

```typescript
documenteditor.selection.characterFormat.fontColor= 'Pink';
documenteditor.selection.characterFormat.fontColor= '#FFC0CB';
```

## Font

The font style of selected text can be get or set using the following sample code.

```typescript
documenteditor.selection.characterFormat.fontFamily= 'Arial';
```

## Highlight color

The highlight color of the selected text can be get or set using the following sample code.

```typescript
documenteditor.selection.characterFormat.highlightColor= 'Pink';
documenteditor.selection.characterFormat.highlightColor= '#FFC0CB';
```

## Toolbar with options for text formatting

Refer to the following example.

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, Selection, Editor, EditorHistory, ContextMenu } from '@syncfusion/ej2-react-documenteditor';
import { ToolbarComponent, ItemDirective, ItemsDirective } from '@syncfusion/ej2-react-navigations';
import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';

DocumentEditorComponent.Inject(Selection, Editor, EditorHistory, ContextMenu);

export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        this.documenteditor.selectionChange = () => {
            setTimeout(() => { this.onSelectionChange(); }, 20);
        };
    }

    toolbarButtonClick(arg): void {
        switch (arg.item.id) {
            case 'bold':
                //Toggles the bold of selected content
                this.documenteditor.editor.toggleBold();
                break;
            case 'italic':
                //Toggles the Italic of selected content
                this.documenteditor.editor.toggleItalic();
                break;
            case 'underline':
                //Toggles the underline of selected content
                this.documenteditor.editor.toggleUnderline('Single');
                break;
            case 'strikethrough':
                //Toggles the strikethrough of selected content
                this.documenteditor.editor.toggleStrikethrough();
                break;
            case 'subscript':
                //Toggles the subscript of selected content
                this.documenteditor.editor.toggleSubscript();
                break;
            case 'superscript':
                //Toggles the superscript of selected content
                this.documenteditor.editor.toggleSuperscript();
                break;
        }
    }
    //To change the font Style of selected content
    public changeFontFamily(args): void {
        this.documenteditor.selection.characterFormat.fontFamily = args.value;
        this.documenteditor.focusIn();
    }
    //To Change the font Size of selected content
    public changeFontSize(args): void {
        this.documenteditor.selection.characterFormat.fontSize = args.value;
        this.documenteditor.focusIn();
    }
    //To Change the font Color of selected content
    public changeFontColor(args) {
        this.documenteditor.selection.characterFormat.fontColor = args.currentValue.hex;
        this.documenteditor.focusIn();
    }

    //Selection change to retrieve formatting
    public onSelectionChange(): void {
        if (this.documenteditor.selection) {
            this.enableDisableFontOptions();
            // #endregion
        }
    }
    public enableDisableFontOptions(): void {
        var characterformat = this.documenteditor.selection.characterFormat;
        var properties = [characterformat.bold, characterformat.italic, characterformat.underline, characterformat.strikeThrough];
        var toggleBtnId = ["bold", "italic", "underline", "strikethrough"];
        for (let i = 0; i < properties.length; i++) {
            this.changeActiveState(properties[i], toggleBtnId[i]);
        }
    }
    public changeActiveState(property, btnId): void {
        let toggleBtn: HTMLElement = document.getElementById(btnId);
        if ((typeof (property) == 'boolean' && property == true) || (typeof (property) == 'string' && property !== 'None'))
            toggleBtn.classList.add("e-btn-toggle");
        else {
            if (toggleBtn.classList.contains("e-btn-toggle"))
                toggleBtn.classList.remove("e-btn-toggle");
        }
    }
    private fontStyle: string[] = ['Algerian', 'Arial', 'Calibri', 'Cambria', 'Cambria Math', 'Candara', 'Courier New', 'Georgia', 'Impact', 'Segoe Print', 'Segoe Script', 'Segoe UI', 'Symbol', 'Times New Roman', 'Verdana', 'Windings'
    ];
    private fontSize: string[] = ['8', '9', '10', '11', '12', '14', '16', '18',
        '20', '22', '24', '26', '28', '36', '48', '72', '96'];
    public contentTemplate1() {
        return (<ColorPickerComponent showButtons={true} value='#000000' change={this.changeFontColor.bind(this)}></ColorPickerComponent>);
    }
    public contentTemplate2() {
        return (<ComboBoxComponent dataSource={this.fontStyle} change={this.changeFontFamily.bind(this)} index={2} allowCustom={true} showClearButton={false} ></ComboBoxComponent>);
    }
    public contentTemplate3() {
        return (<ComboBoxComponent dataSource={this.fontSize} change={this.changeFontSize.bind(this)} index={2} allowCustom={true} showClearButton={false} ></ComboBoxComponent>);
    }
    render() {
        return (
            <div>
                <ToolbarComponent id='toolbar' clicked={this.toolbarButtonClick.bind(this)}>
                    <ItemsDirective>
                        <ItemDirective id="bold" prefixIcon="e-de-icon-Bold" tooltipText="Bold" />
                        <ItemDirective id="italic" prefixIcon="e-de-icon-Italic" tooltipText="Italic" />
                        <ItemDirective id="underline" prefixIcon="e-de-icon-Underline" tooltipText="Underline" />
                        <ItemDirective id="strikethrough" prefixIcon="e-de-icon-Strikethrough" tooltipText="Strikethrough" />
                        <ItemDirective id="subscript" prefixIcon="e-de-icon-Subscript" tooltipText="Subscript" />
                        <ItemDirective id="superscript" prefixIcon="e-de-icon-Superscript" tooltipText="Superscript" />
                        <ItemDirective type="Separator" />
                        <ItemDirective template={this.contentTemplate1} />
                        <ItemDirective type="Separator" />
                        <ItemDirective template={this.contentTemplate2} />
                        <ItemDirective template={this.contentTemplate3} />
                    </ItemsDirective>
                </ToolbarComponent>

                <DocumentEditorComponent
                    id="container"
                    height={'330px'}
                    ref={scope => {
                        this.documenteditor = scope;
                    }}
                    isReadOnly={false}
                    enableSelection={true}
                    enableEditor={true}
                    enableEditorHistory={true}
                    enableContextMenu={true}
                />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));
```

{% endtab %}

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Font dialog](../document-editor/dialog#font-dialog)
* [Keyboard shortcuts](../document-editor/keyboard-shortcut#text-formatting)