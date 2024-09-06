---
title: "Open Dialog in ContextMenu Click"
component: "ContextMenu"
description: "This section helps to learn how to open a dialog in ContextMenu."
---

# Open a dialog on ContextMenu item click

This section explains about how to open a dialog on ContextMenu item click. This can be achieved by
handling dialog open in `select` event of the ContextMenu.

In the following sample, Dialog will open while clicking `Save As...` item:

{% tab template= "context-menu/dialog-open", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component {
    public dialogInstance: DialogComponent;
    public position: any = { X: 100, Y: 100 };
    public visible: boolean = false;
    public buttons: any = [{
        buttonModel: {
            content: 'Submit',
            cssClass: 'e-flat',
            isPrimary: true
        },
        'click': () => {
            this.hide();
        }
    }];
    private menuItems: MenuItemModel[] = [
        {
            text: 'Back'
        },
        {
            text: 'Forward'
        },
        {
            text: 'Reload'
        },
        {
            separator: true
        },
        {
            text: 'Save As...'
        },
        {
            text: 'Print'
        },
        {
            text: 'Cast'
        }];
    constructor(props: any) {
        super(props);
        this.select = this.select.bind(this);
    }
    public hide (): void {
        this.dialogInstance.hide();
    }
    public select: any = (args: MenuEventArgs) => {
        if (args.item.text === 'Save As...') {
            this.dialogInstance.show();
        }
    }
    public render() {
        return (
            <div className="container">
                <div id='target'>Right click / Touch hold to open the ContextMenu</div>
                <DialogComponent width='200px' height='110px' content='This file can be saved as PDF' buttons={this.buttons} visible={this.visible} position={this.position} ref={dialog => this.dialogInstance = dialog as DialogComponent} />
                <ContextMenuComponent id='contextmenu' target='#target' items={this.menuItems} select={this.select}/>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));

```

{% endtab %}
