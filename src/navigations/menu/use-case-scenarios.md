---
title: "Menu use case scenarios"
component: "Menu"
description: "React Menu how to section, toolbar menu, mobile menu, custom menu, scrollable menu."
---

# Use case scenarios

## Scrollable menu

The menu component supports horizontal and vertical scrolling to render large menus and submenus in an adaptive way. This can be achieved by enabling the [`enableScrolling`](../api/menu/#enablescrolling) property and by restricting the corresponding menu/submenu size.

{% tab template="menu/scroll",  sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { closest, enableRipple } from '@syncfusion/ej2-base';
import { BeforeOpenCloseMenuEventArgs, MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    // Menu items definition
    public menuItems: MenuItemModel[] = [
        {
            items: [
                {
                    items: [
                        { text: 'Electric Cookers' },
                        { text: 'Coffee Makers' },
                        { text: 'Blenders' },
                        { text: 'Microwave Ovens' }
                    ],
                    text: 'Kitchen'
                },
                {
                    items: [
                        { text: 'Our Exclusive TVs' },
                        { text: 'Smart TVs' },
                        { text: 'Big Screen TVs' }
                    ],
                    text: 'Television'
                },
                {
                    text: 'Washing Machine'
                },
                {
                    text: 'Refrigerators'
                },
                {
                    items: [
                        { text: 'Inverter ACs' },
                        { text: 'Split ACs' },
                        { text: 'Window ACs' },
                    ],
                    text: 'Air Conditioners'
                },
                {
                    text: 'Water Purifiers'
                },
                {
                    text: 'Air Purifiers'
                },
                {
                    text: 'Chimneys'
                },
                {
                    text: 'Inverters'
                },
                {
                    text: 'Healthy Living'
                },
                {
                    text: 'Vacuum Cleaners'
                },
                {
                    text: 'Room Heaters'
                },
                {
                    text: 'New Launches'
                }
            ],
            text: 'Appliances'
        },
        {
            items: [
                {
                    items: [
                        { text: 'Headphones' },
                        { text: 'Memory Cards' },
                        { text: 'Power Banks' },
                        { text: 'Mobile Cases' },
                        { text: 'Screen Protectors' }
                    ],
                     text: 'Mobile'
                },
                {
                    text: 'Laptops'
                },
                {
                    items: [
                        { text: 'Pendrives' },
                        { text: 'External Hard Disks' },
                        { text: 'Monitors' },
                        { text: 'Keyboards' }
                    ],
                    text: 'Desktop PC'
                },
                {
                    items: [
                        { text: 'Lens' },
                        { text: 'Tripods' }
                    ],
                    text: 'Camera'
                }
            ],
            text: 'Accessories'
        },
        {
            items: [
                {
                    text: 'Men'
                },
                {
                    text: 'Women'
                }
            ],
             text: 'Fashion'
        },
        {
            items: [
                {
                    text: 'Furniture'
                },
                {
                    text: 'Decor'
                },
                {
                    text: 'Smart Home Automation'
                },
                {
                    text: 'Dining & Serving'
                }
            ],
            text: 'Home & Living'
        },
        {
            items: [
                {
                    text: 'Televisions'
                },
                {
                    text: 'Home Theatres'
                },
                {
                    text: 'Gaming Laptops'
                }
            ],
             text: 'Entertainment'
        },
        {
            text: 'Contact Us'
        },
        {
            text: 'Help'
        }
    ];

    public onBeforeOpen(args: BeforeOpenCloseMenuEventArgs) {
        // Restricting sub menu wrapper height
        if (args.parentItem.text === 'Appliances') {
            (closest(args.element, '.e-menu-wrapper') as HTMLElement).style.height = '230px';
        }
    }

    public render() {
        return (
            <MenuComponent items={this.menuItems} cssClass='e-scrollable-menu' enableScrolling={true} beforeOpen={this.onBeforeOpen}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## Menu in toolbar

The following example demonstrates how to integrate Menu with Toolbar component.

{% tab template="menu/toolbar-menu",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel, ItemDirective, ItemsDirective, MenuComponent, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public tbObj: ToolbarComponent;

    // Menu items definition
    public data: Array<{[key: string]: any }> = [
        {
            header: 'Events',
            subItems: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ]
        },
        {
            header: 'Movies',
            subItems: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ]
        },
        {
            header: 'Directory',
            subItems: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ]
        },
        {
            header: 'Queries',
            subItems: [
                { text: 'Our Policy' },
                { text: 'Site Map'},
                { text: '24x7 Support'}
            ]
        },
        { header: 'Services' }
    ];

    public menuFields: FieldSettingsModel = {
        children: ['subItems', 'options'],
        text: ['header', 'text', 'value']
    };

    public animation: any = { effect: 'None' };
    constructor(props: any) {
        super(props);
        this.onCreated = this.onCreated.bind(this);
        this.menuTemplate = this.menuTemplate.bind(this);
    }
    public menuTemplate(): JSX.Element {
        return (
            <MenuComponent id="menu" items={this.data} fields={this.menuFields} animationSettings={this.animation} />
        );
    }

    public onCreated(): void {
        this.tbObj.refreshOverflow();
    }

    public render() {
        return (
            <div className="toolbar-menu-control">
                <ToolbarComponent id="toolbar" created={this.onCreated} ref={(scope) => { this.tbObj = scope as ToolbarComponent; }} >
                    <ItemsDirective>
                        <ItemDirective template={this.menuTemplate} />
                        <ItemDirective prefixIcon='em-icons e-shopping-cart' align='Right' />
                    </ItemsDirective>
                </ToolbarComponent>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## Hamburger menu

The following example demonstrates the use case of menu with Accordion component integrated in SideBar.

{% tab template="menu/sidebar-menu",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { AccordionClickArgs, AccordionComponent, AccordionItemDirective, AccordionItemsDirective, ExpandEventArgs, SidebarComponent, SidebarType } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public sidebarObj: SidebarComponent;
    public accordionObj: AccordionComponent;
    public nestedAccordionObj: AccordionComponent;

    public width: string = '200px';
    public type: SidebarType = 'Over';

    constructor(props: any) {
        super(props);
        this.close = this.close.bind(this);
        this.expand = this.expand.bind(this);
        this.nestedExpand = this.nestedExpand.bind(this);
        this.clicked = this.clicked.bind(this);
        this.hamburgerClick = this.hamburgerClick.bind(this);
    }

    public clicked(e: AccordionClickArgs): void {
        const target = (e.originalEvent as Event).target as HTMLElement;
        if (!e.item && !(target.closest('.e-acrdn-item') as HTMLElement).getElementsByClassName('e-tgl-collapse-icon').length) {
            this.sidebarObj.hide();
        }
    }

    public appliancesAccordion(): void {
        return ReactDom.render(
            <AccordionComponent ref={scope => this.nestedAccordionObj = scope as AccordionComponent} expanding={this.nestedExpand} clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Kitchen' content='<div id="Appliances_Kitchen_Items"></div>' />
                    <AccordionItemDirective header='Washing Machine' content='<div id="Appliances_Washing_Items"></div>' />
                    <AccordionItemDirective header='Air Conditioners' content='<div id="Appliances_Conditioners_Items"></div>' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Appliances_Items"));
    }

    public kitchenAccordion(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Electric Cookers' />
                    <AccordionItemDirective header='Coffee Makers' />
                    <AccordionItemDirective header='Blenders' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Appliances_Kitchen_Items"));
    }

    public acAccordion(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Inverter ACs' />
                    <AccordionItemDirective header='Split ACs' />
                    <AccordionItemDirective header='Window ACs' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Appliances_Conditioners_Items"));
    }

    public washingAccordian(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Fully Automatic' />
                    <AccordionItemDirective header='Semi Automatic' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Appliances_Washing_Items"));
    }

     public accessoriesAccordion(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Mobile' />
                    <AccordionItemDirective header='Computer' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Accessories_Items"));
    }

    public homeAccordion(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Furniture' />
                    <AccordionItemDirective header='Decor' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Home_Living_Items"));
    }

    public fashionAccordion(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Men' />
                    <AccordionItemDirective header='Women' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Fashion_Items"));
    }

    public entertainmentAccordion(): void {
        return ReactDom.render(
            <AccordionComponent clicked={this.clicked}>
                <AccordionItemsDirective>
                    <AccordionItemDirective header='Televisions' />
                    <AccordionItemDirective header='Home Theatres' />
                    <AccordionItemDirective header='Gaming Laptops' />
                </AccordionItemsDirective>
            </AccordionComponent>,
            document.getElementById("Entertainment_Items"));
    }

    // Expanding Event function for main Accordion component.
    public expand(e: ExpandEventArgs): void {
        if (e.isExpanded && [].indexOf.call(this.accordionObj.items, e.item) === 0) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.appliancesAccordion();
        } else if (e.isExpanded && [].indexOf.call(this.accordionObj.items, e.item) === 1) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.accessoriesAccordion();
        } else if (e.isExpanded && [].indexOf.call(this.accordionObj.items, e.item) === 2) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.fashionAccordion();
        } else if (e.isExpanded && [].indexOf.call(this.accordionObj.items, e.item) === 3) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.homeAccordion();
        } else if (e.isExpanded && [].indexOf.call(this.accordionObj.items, e.item) === 4) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.entertainmentAccordion();
        }
    }

    // Expanding Event function for nested Accordion component.
    public nestedExpand(e: ExpandEventArgs): void {
        if (e.isExpanded && [].indexOf.call(this.nestedAccordionObj.items, e.item) === 0) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.kitchenAccordion();
        } else if (e.isExpanded && [].indexOf.call(this.nestedAccordionObj.items, e.item) === 1) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.washingAccordian();
        } else if (e.isExpanded && [].indexOf.call(this.nestedAccordionObj.items, e.item) === 2) {
            if ((e.element as Element).querySelectorAll('.e-accordion').length > 0) {
                return;
            }
            this.acAccordion();
        }
    }

    public hamburgerClick(): void {
        this.sidebarObj.show();
        this.accordionObj.refresh();
    }

    public close(): void {
        this.sidebarObj.hide();
    }

    public render() {
        return (
            <div>
                <div className="header">
                    <span id="hamburger" className="e-icons menu default" onClick={this.hamburgerClick}/>
                    <div className="content">Header content</div>
                </div>
                <SidebarComponent id='default-sidebar' width={this.width} type={this.type} ref={scope => this.sidebarObj = scope as SidebarComponent}>
                    <div className="title-header">
                        <div style={{display:'inline-block'}}>Menu</div>
                        <span  id="close" className="e-icons" onClick={this.close}/>
                    </div>
                    <div className="content-area">
                        <AccordionComponent ref={scope => this.accordionObj = scope as AccordionComponent} expanding={this.expand} clicked={this.clicked}>
                            <AccordionItemsDirective>
                                <AccordionItemDirective header='Appliances' content='<div id="Appliances_Items"></div>' />
                                <AccordionItemDirective header='Accessories' content='<div id="Accessories_Items"></div>' />
                                <AccordionItemDirective header='Fashion' content='<div id="Fashion_Items"></div>' />
                                <AccordionItemDirective header='Home & Living' content='<div id="Home_Living_Items"></div>' />
                                <AccordionItemDirective header='Entertainment' content='<div id="Entertainment_Items"></div>' />
                            </AccordionItemsDirective>
                        </AccordionComponent>
                    </div>
                </SidebarComponent>
                <div>
                    <div className="main-content">Main content</div>
                </div>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## Mobile view

The following example demonstrates the use case of Menu in Mobile mode by using ListView component with hamburger.

{% tab template="menu/listview",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { Animation, enableRipple } from '@syncfusion/ej2-base';
import { ListViewComponent, SelectEventArgs } from '@syncfusion/ej2-react-lists';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public listObj: ListViewComponent;
    public listViewDisplay: any = { display: 'none' };
    public closeSpanDisplay: any = { display: 'none' };
    public dataSource: Array<{ [key: string]: any }> = [
        {
            child: [
            {
                child: [
                    { id: 'list1_1_1', text: 'Electric Cookers' },
                    { id: 'list1_1_2', text: 'Coffee Makers' },
                    { id: 'list1_1_3', text: 'Blenders' },
                ],
                id: 'list1_1',
                text: 'Kitchen'
            },
            {
                child: [
                    { id: 'list1_2_1', text: 'Fully Automatic' },
                    { id: 'list1_2_2', text: 'Semi Automatic' }
                ],
                id: 'list1_2',
                text: 'Washing Machine'
            },
            {
                child: [
                    { id: 'list1_3_1', text: 'Inverter ACs' },
                    { id: 'list1_3_2', text: 'Split ACs' },
                    { id: 'list1_3_3', text: 'Window ACs' },
                ],
                id: 'list1_3',
                text: 'Air Conditioners'
            }],
            id: 'list1',
            text: 'Appliances'
        },
        {
            child: [
            {
                child: [
                    { id: 'list2_1_1', text: 'Headphones' },
                    { id: 'list2_1_2', text: 'Memory Cards' },
                    { id: 'list2_1_3', text: 'Power Banks' }
                ],
                id: 'list2_1',
                text: 'Mobile'
            },
            {
                child: [
                    { id: 'list2_2_1', text: 'Pendrives' },
                    { id: 'list2_2_2', text: 'External Hard Disks' },
                    { id: 'list2_2_3', text: 'Monitors' }
                ],
                id: 'list2_2',
                text: 'Computer'
            }],
            id: 'list2',
            text: 'Accessories'
        },
        {
            child: [
                { id: 'list3_1', text: 'Men' },
                { id: 'list3_2', text: 'Women' }
            ],
            id: 'list3',
            text: 'Fashion'
        },
        {
            child: [
                { id: 'list4_1', text: 'Furniture' },
                { id: 'list4_2', text: 'Decor' }
            ],
            id: 'list4',
            text: 'Home & Living'
        },
        {
            child: [
                { id: 'list5_1', text: 'Televisions' },
                { id: 'list5_2', text: 'Home Theatres' },
                { id: 'list5_3', text: 'Gaming Laptops' }
            ],
            id: 'list5',
            text: 'Entertainment'
        }
    ];
    constructor(props: any) {
        super(props);
        this.onSelect = this.onSelect.bind(this);
        this.onClick = this.onClick.bind(this);
        this.hamburgerClick = this.hamburgerClick.bind(this);
    }
    public onSelect(e: SelectEventArgs): void {
        if (e.data && !(e.data as { child: object }).child) {
            this.listViewDisplay = { display: 'none' };
            this.closeSpanDisplay = { display: 'none' };
            this.listObj.refresh();
        }
    }

    public onClick(): void {
        this.listViewDisplay = { display: 'none' };
        this.closeSpanDisplay = { display: 'none' };
    }

    public hamburgerClick(): void {
        const animation = new Animation({ duration: 500 });
        animation.animate(this.listObj.element, {
            begin: () => {
                this.listViewDisplay = { display: 'block' };
                this.closeSpanDisplay = { display: 'block' };
            },
            name: 'SlideDown'
        });
    }

    public render() {
        return (
            <div className='layoutWrapper'>
                <div className='speaker'>
                    <div className='camera'/>
                </div>
                <div className='layout'>
                    <div id='container'>
                        <div id='header'>
                            <span id='hamburger' onClick={this.hamburgerClick} className='e-icons menu default'/>
                            <div className='content'>Header</div>
                        </div>
                        <ListViewComponent id='listview' ref={scope => this.listObj = scope as ListViewComponent} dataSource={this.dataSource} showHeader={true} headerTitle='Menu' select={this.onSelect}/>
                        <span id='close' onClick={this.onClick} className='e-icons' style={this.closeSpanDisplay}/>
                    </div>
                </div>
                <div className='outerButton'/>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}