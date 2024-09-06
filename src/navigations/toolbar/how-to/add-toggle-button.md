---
title: "Add Toggle Button"
component: "Toolbar"
description: "This example demonstrates how to add the Essential JS 2 Toggle Button into Essential JS Toolbar items."
---

# Add Toggle Button

Toolbar supports to add a toggle Button by using the [`template`](../../../api/toolbar/item#template) property. Refer below steps

* By using Toolbar template property, pass required HTML String to render toggle button.

```typescript
  <ItemDirective template='<button class="e-btn" id="media_btn"></button>' />
```

* Now render the toggle Button into the targeted element in Toolbar [`created`](../../api/toolbar#created) event handler and bind click event for it.
On clicking the toggle Button, change the required icon and content based on current active state.

{% tab template="toolbar/toggle-button", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ToolbarComponent, ItemsDirective, ItemDirective } from '@syncfusion/ej2-react-navigations';
import { Button } from '@syncfusion/ej2-react-buttons';

export class ReactApp extends React.Component<{}, {}> {
  public undoBtn: any;
  public zoomBtn: any;
  public mediaBtn: any;
  public filterBtn: any;
  public visibleBtn: any;

  public tbCreated(): void {
    this.zoomBtn = new Button({ cssClass: `e-flat`, iconCss: 'e-icons e-zoomin-icon', isToggle: true });
    this.zoomBtn.appendTo('#zoom_btn');

    this.mediaBtn = new Button({ cssClass: `e-flat`, iconCss: 'e-icons e-play-icon', isToggle: true });
    this.mediaBtn.appendTo('#media_btn');

    this.undoBtn = new Button({ cssClass: `e-flat`, iconCss: 'e-icons e-undo-icon', isToggle: true });
    this.undoBtn.appendTo('#undo_btn');

    this.filterBtn = new Button({ cssClass: `e-flat`, iconCss: 'e-icons e-filter-icon', isToggle: true });
    this.filterBtn.appendTo('#filter_btn');

    this.visibleBtn = new Button({ cssClass: `e-flat`, iconCss: 'e-icons e-hide-icon', isToggle: true, content:'Hide'});
    this.visibleBtn.appendTo('#visible_btn');

    //Toggle button click event handlers
    this.zoomBtn.element.onclick = (): void => {
        if (this.zoomBtn.element.classList.contains('e-active')) {
            this.zoomBtn.iconCss = 'e-icons e-zoomout-icon';
        } else {
            this.zoomBtn.iconCss = 'e-icons e-zoomin-icon';
        }
    };

    this.mediaBtn.element.onclick = (): void => {
        if (this.mediaBtn.element.classList.contains('e-active')) {
            this.mediaBtn.iconCss = 'e-icons e-pause-icon';
        } else {
            this.mediaBtn.iconCss = 'e-icons e-play-icon';
        }
    };

    this.undoBtn.element.onclick = (): void => {
        if (this.undoBtn.element.classList.contains('e-active')) {
            this.undoBtn.iconCss = 'e-icons e-redo-icon';
        } else {
            this.undoBtn.iconCss = 'e-icons e-undo-icon';
        }
    };

    this.filterBtn.element.onclick = (): void => {
        if (this.filterBtn.element.classList.contains('e-active')) {
            this.filterBtn.iconCss = 'e-icons e-filternone-icon';
        } else {
            this.filterBtn.iconCss = 'e-icons e-filter-icon';
        }
    };

    this.visibleBtn.element.onclick = (): void => {
        if (this.visibleBtn.element.classList.contains('e-active')) {
            document.getElementById('content').style.display = 'none';
            this.visibleBtn.content = 'Show';
            this.visibleBtn.iconCss = 'e-icons e-show-icon';
        } else {
            document.getElementById('content').style.display = 'block';
            this.visibleBtn.content = 'Hide';
            this.visibleBtn.iconCss = 'e-icons e-hide-icon';
        }
    };
  }

  render () {
    const divMargin = { margin: '25px 0' };

    return (
      <div className='control-pane'>
        <div className='control-section tbar-control-section'>
          <div className='control toolbar-sample tbar-sample' style={divMargin}>
            <ToolbarComponent id="ej2Toolbar" created={this.tbCreated}>
              <ItemsDirective>
                <ItemDirective template='<button class="e-btn" id="media_btn"></button>' />
                <ItemDirective type = 'Separator'/>
                <ItemDirective template='<button class="e-btn" id="zoom_btn"></button>' />
                <ItemDirective type = 'Separator'/>
                <ItemDirective template='<button class="e-btn" id="undo_btn"></button>' />
                <ItemDirective type = 'Separator'/>
                <ItemDirective template='<button class="e-btn" id="filter_btn"></button>' />
                <ItemDirective type = 'Separator'/>
                <ItemDirective template='<button class="e-btn" id="visible_btn"></button>' />
              </ItemsDirective>
            </ToolbarComponent>
          </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('toolbar'));

```

{% endtab %}