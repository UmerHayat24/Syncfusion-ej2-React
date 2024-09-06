---
title: "Menu Customizations using Events"
component: "Menu"
description: "This section helps to learn how to customize Menu Items using events."
---

# Customize menu using events

The Menu provides a set of [`events`](../api/menu#events) to enable users to customize it.

The available events are [`beforeOpen`](../../api/menu/#beforeclose), [`beforeClose`](../..api//menu/#beforeopen), [`onClose`](../../api/menu/#onclose), [`onOpen`](../../api/menu/#onopen), and [`select`](../..api//menu/#select).

{% tab template="menu/handle-event",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { BeforeOpenCloseMenuEventArgs, MenuComponent, MenuEventArgs, MenuItemModel, OpenCloseMenuEventArgs } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, { eventTrace: string }> {
    public menuItems: MenuItemModel[] = [
        {
            items: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ],
            text: 'Events'
        },
        {
            items: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ],
            text: 'Movies'
        },
        {
            items: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ],
            text: 'Directory'
        },
        {
            items: [
                { text: 'Our Policy' },
                { text: 'Site Map' }
            ],
            text: 'Queries'
        },
        { text: 'Services' }
    ];
    constructor(props: any) {
        super(props);
        this.state = {
            eventTrace: ''
        }
        this.beforeOpen = this.beforeOpen.bind(this);
        this.beforeClose = this.beforeClose.bind(this);
        this.select = this.select.bind(this);
        this.onOpen = this.onOpen.bind(this);
        this.onClose = this.onClose.bind(this);
        this.btnClick = this.btnClick.bind(this);
    }
    public beforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    public beforeClose(args: BeforeOpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    public onClose(args: OpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    public onOpen(args: OpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    public select(args: MenuEventArgs): void {
        this.updateEventLog(args);
    }

    public updateEventLog(args: any): void {
       this.setState({ eventTrace: this.state.eventTrace + args.name + ' Event triggered. <br />' });
    }

    public btnClick(): void {
        this.setState({ eventTrace: '' });
    }

    public render() {
        return (
            <div className='control-section'>
                <div className='menu-section'>
                    <MenuComponent id='menu' items={this.menuItems} beforeOpen={this.beforeOpen} beforeClose={this.beforeClose} onClose={this.onClose} onOpen={this.onOpen} select={this.select}/>
                </div>
                <div className='property-section'>
                    <table id='propertyTable' title='Event trace'>
                        <tbody>
                            <th>Event trace:-</th>
                            <tr>
                                <td dangerouslySetInnerHTML={{__html: this.state.eventTrace}}/>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <ButtonComponent id='clear' cssClass='e-small' content='Clear' onClick={this.btnClick}/>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
