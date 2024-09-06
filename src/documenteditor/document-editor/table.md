---
title: "Tables"
component: "DocumentEditor"
description: "Learn how to insert, select, or delete table, row(s), and column(s) in React document editor."
---

# Tables

Tables are an efficient way to present information. Document Editor can display and edit the tables. You can select and edit tables through keyboard, mouse, or touch interactions. Document Editor exposes a rich set of APIs to perform these operations programmatically.

## Create a table

You can create and insert a table at cursor position by specifying the required number of rows and columns.

Refer to the following sample code.

```typescript
 documenteditor.editor.insertTable(3,3);
```

The maximum size of row and column is limited to 32767 and 63 respectively.

## Insert rows

You can add a row (or several rows) above or below the row at cursor position by using the `insertRow` method. This method accepts the following parameters:

Parameter | Type | Description
----------|------|-------------
above(optional) | boolean | This is optional and if omitted, it takes the value as false and inserts below the row at cursor position.
count(optional) | number | This is optional and if omitted, it takes the value as 1.

Refer to the following sample code.

```typescript
//Inserts a row below the row at cursor position
documentedior.editor.insertRow();
//Inserts a row above the row at cursor position
documentedior.editor.insertRow(false);
//Inserts three rows below the row at cursor position
documentedior.editor.insertRow(true, 3)
```

## Insert columns

You can add a column (or several columns) to the left or right of the column at cursor position by using the `insertColumn` method. This method accepts the following parameters:

Parameter | Type | Description
----------|------|-------------
left(optional) | boolean| This is optional and if omitted, it takes the value as false and inserts to the right of column at cursor position.
count(optional) | number |  This is optional and if omitted, it takes the value as 1.

Refer to the following sample code.

```typescript
//Insert a column to the right of the column at cursor position.
documentedior.editor.insertColumn();
//Insert a column to the left of the column at cursor position.
documentedior.editor.insertColumn(false);
//Insert two columns to the left of the column at cursor position.
documentedior.editor.insertColumn(false, 2);
```

### Select an entire table

If the cursor position is inside a table, you can select the entire table by using the following sample code.

```typescript
documenteditor.selection.selectTable();
```

### Select row

You can select the entire row at cursor position by using the following sample code.

```typescript
documenteditor.selection.selectRow();
```

If current selection spans across cells of different rows, all these rows will be selected.

### Select column

You can select the entire column at cursor position by using the following sample code.

```typescript
documenteditor.selection.selectColumn();
```

If current selection spans across cells of different columns, all these columns will be selected.

### Select cell

You can select the cell at cursor position by using the following sample code.

```typescript
documenteditor.selection.selectCell();
```

## Delete table

Document Editor allows you to delete the entire table. You can use the `deleteTable()` method of editor instance, if selection is in table. Refer to the following sample code.

```typescript
documenteditor.editor.deleteTable();
```

## Delete row

Document Editor allows you to delete the selected number of rows. You can use the `deleteRow()` method of editor instance to delete the selected number of rows, if selection is in table. Refer to the following sample code.

```typescript
documenteditor.editor.deleteRow();
```

## Delete column

Document Editor allows you to delete the selected number of columns. You can use the `deleteColumn ()` method of editor instance to delete the selected number of columns, if selection is in table. Refer to the following sample code.

```typescript
documenteditor.editor.deleteColumn();
```

## Merge cells

You can merge cells vertically, horizontally, or combination of both to a single cell. To vertically merge the cells, the columns within selection should be even in left and right directions. To horizontally merge the cells, the rows within selection should be even in top and bottom direction.
Refer to the following sample code.

```typescript
documenteditor.editor.mergeCells()
```

## Positioning the table

Document Editor preserves the position properties of the table and displays the table based on position properties. It does not support modifying the position properties. Whereas the table will be automatically moved along with text edited if it is positioned relative to the paragraph.

## How to work with tables

The following sample demonstrates how to delete the table row or columns, merge cells and how to bind the API with button.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, Selection, Editor, EditorHistory, ContextMenu, TableDialog, } from '@syncfusion/ej2-react-documenteditor';
import { ToolbarComponent, ItemDirective, ItemsDirective, } from '@syncfusion/ej2-react-navigations';
//Inject require modules.
DocumentEditorComponent.Inject(Selection, Editor, EditorHistory, ContextMenu, TableDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        this.documenteditor.editor.insertTable(2, 2);
    }

    toolbarButtonClick(arg): void {
        switch (arg.item.id) {
            case 'table':
                //Insert table API to add table
                this.documenteditor.editor.insertTable(3, 2);
                break;
            case 'insert_above':
                //Insert the specified number of rows to the table above to the row at cursor position
                this.documenteditor.editor.insertRow(true, 2);
                break;
            case 'insert_below':
                //Insert the specified number of rows to the table below to the row at cursor position
                this.documenteditor.editor.insertRow();
                break;
            case 'insert_left':
                //Insert the specified number of columns to the table left to the column at cursor position
                this.documenteditor.editor.insertColumn(true, 2);
                break;
            case 'insert_right':
                //Insert the specified number of columns to the table right to the column at cursor position
                this.documenteditor.editor.insertColumn();
                break;
            case 'delete_table':
                //Delete the entire table
                this.documenteditor.editor.deleteTable();
                break;
            case 'delete_row':
                //Delete the selected number of rows
                this.documenteditor.editor.deleteRow();
                break;
            case 'delete_column':
                //Delete the selected number of columns
                this.documenteditor.editor.deleteColumn();
                break;
            case 'merge_cell':
                //Merge the selected cells into one (both vertically and horizontally)
                this.documenteditor.editor.mergeCells();
                break;
            case 'table_dialog':
                //Opens insert table dialog
                this.documenteditor.showDialog('Table');
                break;
        }
    }

    render() {
        return (
            <div>
                <ToolbarComponent clicked={this.toolbarButtonClick}>
                    <ItemsDirective>
                        <ItemDirective id="table" prefixIcon="e-de-ctnr-table e-icons" />
                        <ItemDirective type="Separator" />
                        <ItemDirective id="insert_above" prefixIcon="e-de-ctnr-insertabove e-icons" />
                        <ItemDirective id="insert_below" prefixIcon="e-de-ctnr-insertbelow e-icons" />
                        <ItemDirective type="Separator" />
                        <ItemDirective id="insert_left" prefixIcon="e-de-ctnr-insertleft e-icons" />
                        <ItemDirective id="insert_right" prefixIcon="e-de-ctnr-insertright e-icons" />
                        <ItemDirective type="Separator" />
                        <ItemDirective id="delete_table" prefixIcon="e-de-delete-table e-icons" />
                        <ItemDirective id="delete_rows" prefixIcon="e-de-ctnr-deleterows e-icons" />
                        <ItemDirective id="delete_columns" prefixIcon="e-de-ctnr-deletecolumns e-icons" />
                        <ItemDirective type="Separator" />
                        <ItemDirective text="Dialog" />
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
                    enableTableDialog={true}
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
* [Insert table dialog](../document-editor/dialog#table-dialog)