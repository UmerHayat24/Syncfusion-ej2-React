---
title: "Menu with datasource and HTML tags"
component: "Menu"
description: "React Menu supports HTML elements for menu items, databinding with local data source, parent child data, array of JSON data, and remote service with query."
---

# Data source binding and Custom menu items

## Data binding

The Menu supports data source bindings such as array of JavaScript objects that can be structured as either `hierarchical` or `self-referential` data.

### Hierarchical data

The Menu can be populated with hierarchical data source by assigning it to the [`items`](../api/menu/menuItemModel#items) property, and the fields with corresponding keys can be mapped to the [`fields`](../api/menu/fieldSettingsModel) property.

#### JSON data

The Menu can generate its menu items through an array of complex data source by mapping fields from the [`fields`](../api/menu/fieldSettingsModel) property.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel, MenuComponent,  } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public dataSource: Array<{ [key: string]: any }> = [
        {
            continent: 'Asia',
            countries: [
                {
                    country: 'China',
                    languages: [
                        { language: 'Chinese' },
                        { language: 'Cantonese' }
                    ]
                },
                {
                    country: 'India',
                    languages: [
                        { language: 'English' },
                        { language: 'Hindi' },
                        { language: 'Tamil' }
                    ]
                },
                {
                    country: 'Japan',
                    languages: [
                        { language: 'Japanese' }
                    ]
                }
            ]
        },
        {
            continent: 'Africa',
            countries: [
                {
                    country: 'Nigeria',
                    languages: [
                        { language: 'English' },
                        { language: 'Hausa' }
                    ]
                },
                {
                    country: 'Egypt',
                    languages: [
                        { language: 'Arabic' }
                    ]
                },
                {
                    country: 'South Africa',
                    languages: [
                        { language: 'Tswana' },
                        { language: 'Swati' }
                    ]
                }
            ]
        },
        {
            continent: 'North America',
            countries: [
                {
                    country: 'Canada',
                    languages: [
                        { language: 'French' }
                    ]
                },
                {
                    country: 'Mexico',
                    languages: [
                        { language: 'Spanish' }
                    ]
                },
                {
                    country: 'USA',
                    languages: [
                        { language: 'English' }
                    ]
                }
            ]
        },
        {
            continent: 'South America',
            countries: [
                {
                    country: 'Brazil',
                    languages: [
                        { language: 'Portuguese' }
                    ]
                },
                {
                    country: 'Colombia',
                    languages: [
                        { language: 'Spanish' }
                    ]
                },
                {
                    country: 'Argentina',
                    languages: [
                        { language: 'Spanish' }
                    ]
                }
            ]
        },
        {
            continent: 'Oceania',
            countries: [
                {
                    country: 'Australia'
                },
                {
                    country: 'New Zealand'
                },
                {
                    country: 'Samoa'
                },
            ]
        }];

    // Menu fields definition
    public menuFields: FieldSettingsModel = {
        children: ['countries', 'languages'],
        text: ['continent', 'country', 'language']
    };

    public render() {
        return (
            <MenuComponent items={this.dataSource} fields={this.menuFields}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

#### Data Service

In application level, remote data binding can be achieved using [`DataManager`](https://ej2.syncfusion.com/angular/documentation/data).
To create Menu, assign items property with resultant data from
[`callback`](https://ej2.syncfusion.com/documentation/api/data/deferred#then) function.

The following example displays five employees' **FirstName** from **Employees** table
and **ShipName** details from **Orders** table of the `Northwind` Data Service.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DataManager, ODataAdaptor, Query, ReturnOption } from '@syncfusion/ej2-data';
import { FieldSettingsModel, MenuComponent } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

const SERVICE_URI: string = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/';

enableRipple(true);

class App extends React.Component<{}, {menuItems: Array<{ [key: string]: any }> }> {
    // Menu fields definition.
    public menuFields: FieldSettingsModel = {
        children: ['Orders'],
        text: ['FirstName', 'ShipName']
    };
    constructor(props: any) {
        super(props);
        this.state = { menuItems: [] };
    }
    public componentDidMount(): void {
        // Getting remote data using DataManager.
        const proxy = this;
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor, crossDomain: true })
            .executeQuery(
                new Query().from('Employees').take(5).hierarchy(
                    new Query()
                        .foreignKey('EmployeeID')
                        .from('Orders').take(13),
                        this.select
            ))
            .then((e: ReturnOption) => {
                proxy.setState({menuItems: e.result as Array<{ [key: string]: any }>});
        });
    }
    public select(): number [] {
        return [1,2,3,4,5];
    }
    public render() {
        return (
            <div>
                {
                    this.state.menuItems.length  ?
                    <MenuComponent items={this.state.menuItems} fields={this.menuFields}/> : ''
                }
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

### Self-referential data

Menu can be populated from self-referential data structure that contains array of JSON objects with `parentId` mapping.

In the following example, the **id**, **pId**, and **text** columns from self-referential data have been mapped to the [`itemId`](../api/menu/fieldSettingsModel/#itemid), [`parentId`](../api/menu/fieldSettingsModel/#parentid), and [`text`](../api/menu/fieldSettingsModel/#text) fields, respectively.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel, MenuComponent,  } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    // Menu datasource
    public data: Array<{[key: string]: any }> = [
        { id: 'parent1', text: 'Events' },
        { id: 'parent2', text: 'Movies' },
        { id: 'parent3', text: 'Directory' },
        { id: 'parent4', pId: null, text: 'Queries' },
        { id: 'parent5', pId: null, text: 'Services' },
        { id: 'parent6', pId: 'parent1', text: 'Conferences' },
        { id: 'parent7', pId: 'parent1', text: 'Music' },
        { id: 'parent8', pId: 'parent1', text: 'Workshops' },
        { id: 'parent9', pId: 'parent2', text: 'Now Showing' },
        { id: 'parent10', pId: 'parent2', text: 'Coming Soon' },
        { id: 'parent10', pId: 'parent3', text: 'Media Gallery' },
        { id: 'parent11', pId: 'parent3', text: 'Newsletters' },
        { id: 'parent12', pId: 'parent4', text: 'Our Policy' },
        { id: 'parent13', pId: 'parent4', text: 'Site Map' },
        { id: 'parent14', pId: 'parent7', text: 'Pop' },
        { id: 'parent15', pId: 'parent7', text: 'Folk' },
        { id: 'parent16', pId: 'parent7', text: 'Classical' }
    ];

    // Menu fields definition
    public menuFields: FieldSettingsModel = {
        itemId:'id',
        parentId: 'pId',
        text: 'text'
    };

    public render() {
        return (
            <MenuComponent items={this.data} fields={this.menuFields}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## Custom menu items

The Menu can be customized using Essential JS2 `Template engine` to render the elements.

To customize menu items in your application, set your customized template string to the [`template`](../api/menu#template) property. In the following example, the menu has been rendered with customized menu items.

{% tab template="menu/template",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel, MenuComponent } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(false);

class App extends React.Component<{}, {}> {
    // Menu fields definition
    public menuFields: FieldSettingsModel  = {
        children: ['options'],
        text: ['category', 'value']
    };
    // Menu data definition
    public data: Array<{ [key: string]: any }> = [
        {
            category: 'Products',
            options: [
                { value: 'JavaScript', url: 'javascript' },
                { value: 'Angular', url: 'angular' },
                { value: 'ASP.NET Core', url: 'core' },
                { value: 'ASP.NET MVC', url: 'mvc' }
            ]
        },
        {
            category: 'Services',
            options: [
                {
                    support: [
                        { id: 1, count: '1200+', value: 'Application Development' },
                        { id: 2, count: '3700+', value: 'Maintenance & Support' },
                        { id: 3, value: 'Quality Assurance' },
                        { id: 4, count: '900+', value: 'Cloud Integration' }
                    ]
                }
            ]
        },
        {
            category: 'About Us',
            options: [
                {
                    about: {
                        value: "We are on a mission to provide world-class best software solutions for web, mobile and desktop platforms. Around 900+ applications are desgined and delivered to our customers to make digital & strengthen their businesses."
                    }
                }
            ]
        },
        { category: 'Careers' },
        { category: 'Sign In' }
    ];

    public menuTemplate(data: any): JSX.Element {
        return (
            data.category ? <span>{data.category}</span> :
                (data.value && data.url) ?
                    <div className='e-avatar e-avatar-small image' style={{ backgroundImage: 'url(https://ej2.syncfusion.com/react/demos/src/menu/images/' + data.url + '.png)' }}>{data.value}</div> :
                    data.support ?
                        <ul>
                            {
                                data.support.map((supp: any) => <li key={supp.id}>
                                    {supp.value}
                                    {
                                        supp.count ? <span className='e-badge e-badge-success'>{supp.count}</span> : ""
                                    }
                                </li>)
                            }
                        </ul> :
                        <div tabIndex={0} className="e-card">
                            <div className="e-card-header">
                                <div className="e-card-header-caption">
                                    <div className="e-card-header-title">About Us</div>
                                </div>
                            </div>
                            <div className="e-card-content">
                                {data.about.value}
                            </div>
                            <div className="e-card-actions">
                                <button className="e-btn e-outline">
                                    Read More
                    </button>
                            </div>
                        </div>
        );
    }

    public render() {
        return (
            <div className="menu-section">
                <MenuComponent items={this.data} fields={this.menuFields} template={this.menuTemplate}/>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

>To prevent sub menu closing, set `args.cancel` to `true` in [`beforeClose`](../api/menu#beforeclose) event.

## See Also

* [Render menu with items](./getting-started#getting-started)
