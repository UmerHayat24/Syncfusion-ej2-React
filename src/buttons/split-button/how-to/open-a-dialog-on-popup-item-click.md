---
title: "Open a dialog on popup item click"
component: "SplitButton"
description: "React SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Open a dialog on popup item click

This section explains about how to open a dialog on SplitButton popup item click. This can be achieved by
handling dialog open in [`select`](../../api/split-button#select) event of the SplitButton.

In the following example, Dialog will open while selecting `Update...` item.

{% tab template= "split-button/dialog", sourceFiles="app/**/*.tsx,index.html,style.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { ItemModel, MenuEventArgs, SplitButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render SplitButton.
class App extends React.Component<{}, {}> {
    public dialog: DialogComponent;
    public items: ItemModel[] = [
    {
        text: 'Help'
    },
    {
        text: 'About'
    },
    {
        text: 'Update...'
    }];

    public alertDlgButtons: any [] = [{
        buttonModel: {
            content: 'Ok',
            isPrimary: true
        },
        'click': () => {
            this.hide();
        }
    },
    {
        buttonModel: {
            content: 'Cancel',
            isPrimary: true
        },
        'click': () => {
            this.hide();
        }
    }];
    constructor(props: any) {
        super(props);
        this.select = this.select.bind(this);
    }
    public hide() {
        this.dialog.hide();
    }
    public select (args: MenuEventArgs) {
        if (args.item.text === 'Update...') {
            this.dialog.show();
        }
    }

  public render() {
    return (
    <div>
       <DialogComponent ref={dialog => this.dialog = dialog as DialogComponent} width='250px' id='dialog' content='Are you sure want to update?' header='Software Update' buttons={this.alertDlgButtons} visible={false}/>
       <SplitButtonComponent items = {this.items} select={this.select}>Help</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}