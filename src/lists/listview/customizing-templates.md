---
title: "ListView Customizing Templates"
component: "ListView"
description: "React listView allows customization of list item, header, and category group header using template and group header API."
---

# Customizing Templates

The ListView component is designed to customize list items, group title and header title.

## Header template

The ListView header can be customized with the help of [`headerTemplate`](../api/list-view/#headertemplate) property.

To customize header template in your application, Declare a custom react elements within the function which returns `JSX.Element` and assign it to `headerTemplate` property along with [`showHeader`](../api/list-view/#showheader) property as `true` to display the ListView header.

{% tab compileJsx=true%}

```typescript

headerTemplate(data): JSX.Element {
    return (
        <div className="header-content">
          <span>Header</span>
        </div>
  )};

render() {
        return (
        <ListViewComponent id='list'
                dataSource={this.listData}
                headerTemplate= {this.headerTemplate}
                showHeader = {true} >
        </ListViewComponent>
        )
    }

```

{% endtab %}

In the below example, we have rendered Listview with customized header which contains search, add and sort buttons.

{% tab template="listview/header-template", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

export default class App extends React.Component<{}, {}> {
    //Define an array of JSON data
    public fruitsData: { [key: string]: Object }[] = [
        { text: 'Date', id: '1', imgUrl: './dates.jpg' },
        { text: 'Fig', id: '2', imgUrl: './fig.jpg' },
        { text: 'Apple', id: '3', imgUrl: './apple.png' },
        { text: 'Apricot', id: '4', imgUrl: './apricot.jpg' },
        { text: 'Grape', id: '5', imgUrl: './grape.jpg' },
        { text: 'Strawberry', id: '6', imgUrl: './strawberry.jpg' },
        { text: 'Pineapple', id: '7', imgUrl: './pineapple.jpg' },
        { text: 'Melon', id: '8', imgUrl: './melon.jpg' },
        { text: 'Lemon', id: '9', imgUrl: './lemon.jpg' },
        { text: 'Cherry', id: '10', imgUrl: './cherry.jpg' },
    ];

    headerTemplate(data: any): JSX.Element {
        return (
            <div className="headerContainer">
                <span className="fruitHeader">Fruits</span>
                <ButtonComponent
                    id="search"
                    cssClass="e-small e-round"
                    isPrimary={true}
                    iconCss="e-icons e-search-icon"
                />
                <ButtonComponent
                    id="add"
                    cssClass="e-small e-round"
                    isPrimary={true}
                    iconCss="e-icons e-add-icon"
                />
                <ButtonComponent
                    id="sort"
                    cssClass="e-small e-round"
                    isPrimary={true}
                    iconCss="e-icons e-sort-icon"
                />
            </div>
        );
    }

    render() {
        return (
            <ListViewComponent
                id="list"
                dataSource={this.fruitsData}
                showHeader={true}
                headerTemplate={this.headerTemplate as any}
            />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Template

The ListView items can be customized with the help of [`template`](../api/list-view/#template) property.

To customize list items in your application, Declare a custom react elements within the function which returns `JSX.Element` and assign it to `template` property.

{% tab compileJsx=true%}

```typescript

template(data): JSX.Element {
    return (
        <div className="list-tem">
          <span>{data.text}</span>
        </div>
  )};

render() {
        return (
        <ListViewComponent id='list'
                dataSource={this.listData}
                template= {this.template} >
        </ListViewComponent>
        )
    }

```

{% endtab %}

We provided the following built-in CSS classes to customize the list-items. Refer to the following table.

| CSS class        | Description           |
| ------------- |-------------|
| e-list-template, e-list-wrapper | These classes are used to differentiate normal and template rendering, which are mandatory for template rendering. The `e-list-template` class should be added to the root of the ListView element and `e-list-wrapper` class should be added to the template element wrapper <br/><br/>`<ListViewComponent`<br/> `cssClass="e-list-template"`<br/>`template={this.template}>`<br/> `</ListViewComponent>`<br/><br/>`template(data): JSX.Element {`<br/> `return (`<br/>`<div className="e-list-wrapper"></div>`<br/>`)};`
| e-list-content | This class is used to align list content and it should be added to the content element <br/><br/> `template(data): JSX.Element {`<br/>`return (` <br/>`<div className="e-list-wrapper">`<br/>`<span className="e-list-content">ListItem</span>`<br/>`</div>`<br/>`)};`|
| e-list-avatar | This class is used for avatar customization. It should be added to the template element wrapper. After adding it, we can customize our element with [Avatar](https://ej2.syncfusion.com/documentation/avatar/getting-started.html?lang=typescript) classes <br/> <br/> `template(data): JSX.Element {`<br/> `return (`<br/> `<div className="e-list-wrapper e-list-avatar">`<br/> `<span className="e-avatar e-avatar-circle">MR</span>`<br/> `<span className="e-list-content">ListItem</span>`<br/> `</div>`<br/> `)};`
| e-list-avatar-right | This class is used to align avatar to right side of the list item. It should be added to the template element wrapper. After adding it, we can customize our element with [Avatar](https://ej2.syncfusion.com/documentation/avatar/getting-started.html?lang=typescript) classes <br/><br/> `<div className="e-list-wrapper``e-list-avatar-right``">` <br/> `<span className="e-list-content">ListItem</span>`<br/>`<span className="e-avatar e-avatar-circle">MR</span>`<br/> `</div>`|
| e-list-badge | This class is used for badge customization .It should be added to the template element wrapper. After adding it, we can customize our element with [Badge](https://ej2.syncfusion.com/documentation/badge/getting-started.html?lang=typescript) classes <br/><br/>`template(data): JSX.Element {`<br/> `return (`<br/>`<div className="e-list-wrapper e-list-avatar-right">`<br/>`<span className="e-list-content">ListItem</span>`<br/>`<span className="e-avatar e-avatar-circle">MR</span>`<br/>`</div>`<br/>`)};`|
| e-list-multi-line | This class is used for multi-line customization. It should be added to the template element wrapper. After adding it, we can customize List item's header and description <br/><br/>`template(data): JSX.Element {`<br/>`return (`<br/>`<div className="e-list-wrapper e-list-multi-line">`<br/>`<span className="e-list-content">ListItem</span>`<br/>`</div>`<br/>`)};`|
| e-list-item-header |This class is used to align a list header and it should be added to the header element along with the multi-line class <br/><br/> `template(data): JSX.Element {`<br/> `return (`<br/> `<div className="e-list-wrapper e-list-multi-line">`<br/> `<span className="e-list-item-header">ListItem Header</span>`<br/> `<span className="e-list-content">ListItem</span>`<br/> `</div>`<br/> `)};`

* If you are using `Avatar` in ListView templates, we need to add `Layouts` component's styles as given below in `src/App.css` file

```css
@import "../node_modules/@syncfusion/ej2-layouts/styles/material.css";
```

In the below example, we have customized list items like `Contact` app with our avatar component.

{% tab template="listview/avatar-temp", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
      //Define an array of JSON data
    public data: { [key: string]: Object }[] = [
        {
            text: "Jenifer",
            contact: "(206) 555-985774",
            id: "1",
            avatar: "",
            pic: "pic01"
        },
        { text: "Amenda", contact: "(206) 555-3412", id: "2", avatar: "A", pic: "" },
        {
            text: "Isabella",
            contact: "(206) 555-8122",
            id: "4",
            avatar: "",
            pic: "pic02"
        },
        {
            text: "William ",
            contact: "(206) 555-9482",
            id: "5",
            avatar: "W",
            pic: ""
        },
        {
            text: "Jacob",
            contact: "(71) 555-4848",
            id: "6",
            avatar: "",
            pic: "pic04"
        },
        { text: "Matthew", contact: "(71) 555-7773", id: "7", avatar: "M", pic: "" },
        {
            text: "Oliver",
            contact: "(71) 555-5598",
            id: "8",
            avatar: "",
            pic: "pic03"
        },
        {
            text: "Charlotte",
            contact: "(206) 555-1189",
            id: "9",
            avatar: "C",
            pic: ""
        }
    ];
    public fields: any = { text: "Name" };

    public listTemplate(data: any): JSX.Element {
        let letterAvatar = <span className='e-avatar e-avatar-circle'>{data.avatar}</span>
        let imageAvatar = <span className={`${data.pic} e-avatar e-avatar-circle`}></span>

        return (
            <div className='e-list-wrapper e-list-multi-line e-list-avatar'>
                {data.avatar !== "" ? (letterAvatar) : (imageAvatar)}
                <span className="e-list-item-header">{data.text}</span>
                <span className="e-list-content">{data.contact}</span>
            </div>
        );
    }

    render() {
        return (
           <div>
                <ListViewComponent id='list' dataSource={this.data} headerTitle='Contacts' showHeader={true}
                    sortOrder="Ascending" width='350px' template={this.listTemplate as any}
                    fields={this.fields as any} cssClass='e-list-template'></ListViewComponent>
            </div>

        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Group template

The ListView group header can be customized with the help of [`groupTemplate`](../api/list-view/#grouptemplate) property.

To customize the group template in your application, Declare a custom react elements within the function which returns `JSX.Element` and assign it to `groupTemplate` property.

{% tab compileJsx=true%}

```typescript

groupTemplate(data: any): JSX.Element {
    return(
        <div>
            <span className='category'>{data.items[0].category}</span>
            <span className="count"> {data.items.length} Item(s)</span>
        </div>
    );
}
render() {
    return (
    <ListViewComponent id='list'
            dataSource={this.listData}
            groupTemplate= {this.groupTemplate} >
    </ListViewComponent>
    )
}

```

{% endtab %}

In the below example, we have grouped Listview based on the category. The category of each list item should be mapped with [`groupBy`] field of the data. We have also displayed grouped list items count in the group list header.

{% tab template="listview/item-count-temp", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {

        //Define an array of JSON data
    private data: { [key: string]: Object }[]  = [
        { Name: 'Nancy', contact:'(206) 555-985774', id: '1', image: 'https://ej2.syncfusion.com/demos/src/grid/images/1.png',  category: 'Experience'},
        { Name: 'Janet', contact: '(206) 555-3412', id: '2', image: 'https://ej2.syncfusion.com/demos/src/grid/images/3.png', category: 'Fresher' },
        { Name: 'Margaret', contact:'(206) 555-8122', id:'4', image: 'https://ej2.syncfusion.com/demos/src/grid/images/4.png', category: 'Experience' },
        { Name: 'Andrew ', contact:'(206) 555-9482', id: '5', image: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', category: 'Experience'},
        { Name: 'Steven', contact:'(71) 555-4848', id: '6', image: 'https://ej2.syncfusion.com/demos/src/grid/images/5.png', category: 'Fresher' },
        { Name: 'Michael', contact:'(71) 555-7773', id: '7', image: 'https://ej2.syncfusion.com/demos/src/grid/images/6.png', category: 'Experience' },
        { Name: 'Robert', contact:'(71) 555-5598', id: '8', image: 'https://ej2.syncfusion.com/demos/src/grid/images/7.png', category: 'Fresher' },
        { Name: 'Laura', contact:'(206) 555-1189', id: '9', image: 'https://ej2.syncfusion.com/demos/src/grid/images/8.png', category: 'Experience' },
    ];

    private fields: object =  { text: 'Name', groupBy: 'category' };
     //Set customized list template
    listTemplate(data: any): JSX.Element {
        return(
            <div className="e-list-wrapper e-list-multi-line e-list-avatar">
                <img className="e-avatar e-avatar-circle" src={data.image} />
                <span className="e-list-item-header">{data.Name}</span>
                <span className="e-list-content">{data.contact}</span>
            </div>
        );
    }
    //Set customized group-header template
    groupTemplate(data: any): JSX.Element {
        return(
            <div>
                <span className='category'>{data.items[0].category}</span>
                <span className="count"> {data.items.length} Item(s)</span>
            </div>
        );
    }
    render() {
        return (
            <div>
                <ListViewComponent id='list' dataSource={this.data} fields={this.fields} template={this.listTemplate as any}
                groupTemplate={this.groupTemplate as any} width='350px' cssClass='e-list-template'>
                </ListViewComponent>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
