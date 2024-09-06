---
title: "Open a dialog on popup item click"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Open a dialog on popup item click

This section explains about how to open a dialog on DropdownButton popup item click.
This can be achieved by handling dialog open in
[`select`](../../api/drop-down-button#select) event of the DropdownButton.

In the following example, Dialog will open while selecting `Other Folder...` item.

{% tab template= "drop-down-button/dialog", sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { DropDownButtonComponent, ItemModel, MenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {
  public position: any = {X: 100, Y: 100};
  public dialog: DialogComponent;
  public alertDlgButtons: any = [{
    buttonModel: {
      content: 'Submit',
      cssClass: 'e-flat',
      isPrimary: true
    },
    'click' : () => {
      this.dialog.hide()
    }
  }];
  public items: ItemModel[] = [
    {
      text: 'Archive'
    },
    {
      text: 'Inbox'
    },
    {
      text: 'HR Portal'
    },
    {
      separator: true
    },
    {
      text: 'Other Folder...'
    },
    {
      text: 'Copy to Folder'
    }];
  constructor(props: any) {
    super(props);
    this.onSelect = this.onSelect.bind(this);
  }
  // To open dialog on selecting `Other Folder...` item.
  public onSelect (args: MenuEventArgs) {
    if (args.item.text === 'Other Folder...') {
      this.dialog.show();
    }
  }
  
  public render() {
    return (
      <div>
        <DialogComponent ref={(scope) => { this.dialog = scope as DialogComponent; }} width='250px' id='dialog' content='Move Items To "Web Team"' header='Move Items' buttons={this.alertDlgButtons} position={this.position} visible={false}/>
        <DropDownButtonComponent items = {this.items} select={this.onSelect} iconCss='ddb-icons e-folder' cssClass='e-vertical' iconPosition='Top'>Move</DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}