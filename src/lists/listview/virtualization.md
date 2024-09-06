---
title: "ListView UI Virtualization"
component: "ListView"
description: "React listView allows UI virtualization by loading viewable items in view port to improves listview performance when loading large data."
---

# UI Virtualization

UI virtualization loads only viewable list items in a view port which will increase ListView performance on loading large number of data.

## Module injection

In order to use UI Virtualization, we need to inject its `virtualization` service in the App. This modules
should be injected into the ListView using the `Inject` directive as like the below code snippet.

{% tab compileJsx=true%}

```typescript

import { ListViewComponent, Inject, Virtualization } from '@syncfusion/ej2-react-lists';

....
....

render() {
        return (
            // specifies the tag to render the ListView component
            <ListViewComponent id='ui-list' dataSource={this.listData} enableVirtualization={true} >
                <Inject services={[Virtualization]} />
            </ListViewComponent>
        );
    }

```

{% endtab %}

## Getting started

UI virtualization can be enabled in ListView by setting
[`enableVirtualization`](../api/list-view/#enablevirtualization)
property to true.

It has two type of scroller

**Window scroll** - This scroller is used in ListView by default.

**Container scroll** - This will be used, if the height property of ListView was set.

{% tab template="listview/virtualization/flat-list", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent, Inject, Virtualization } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  // define the array of Json
  public listData: { [key: string]: string | object }[];

  constructor(props: any) {
    super(props);
    this.listData = [
      { text: "Nancy", id: "0" },
      { text: "Andrew", id: "1" },
      { text: "Janet", id: "2" },
      { text: "Margaret", id: "3" },
      { text: "Steven", id: "4" },
      { text: "Laura", id: "5" },
      { text: "Robert", id: "6" },
      { text: "Michael", id: "7" },
      { text: "Albert", id: "8" },
      { text: "Nolan", id: "9" }
    ];
    for (let i: number = 10; i <= 1010; i++) {
      let index: number = parseInt((Math.random() * 10).toString());
      this.listData.push({ text: this.listData[index].text, id: i.toString() });
    }
  }

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id="ui-list" dataSource={this.listData} enableVirtualization={true}>
        <Inject services={[Virtualization]} />
      </ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

We can use `template` property to customize list items in UI virtualization.

{% tab template="listview/virtualization/template", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent, Inject, Virtualization } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
    // define the array of Json
    public listData: { [key: string]: string | object }[];
    constructor() {
        super();
        this.listData = [
            { name: 'Nancy', icon: 'N', id: '0', },
            { name: 'Andrew', icon: 'A', id: '1' },
            { name: 'Janet', icon: 'J', id: '2' },
            { name: 'Margaret', imgUrl: './margaret.png', id: '3' },
            { name: 'Steven', icon: 'S', id: '4' },
            { name: 'Laura', imgUrl: './laura.png', id: '5' },
            { name: 'Robert', icon: 'R', id: '6' },
            { name: 'Michael', icon: 'M', id: '7' },
            { name: 'Albert', imgUrl: './albert.png', id: '8' },
            { name: 'Nolan', icon: 'N', id: '9' }
        ];
        for (let i: number = 10; i <= 1010; i++) {
            let index: number = parseInt((Math.random() * 10).toString());
            this.listData.push({ name: this.listData[index].name, icon: this.listData[index].icon, imgUrl: this.listData[index].imgUrl, id: i.toString() });
        }
    }

    public template: string = '<div class="list-container"><div id="icon" class="${$imgUrl ? \'img\' : $icon }">' +
        '<span class="${$imgUrl ? \'hideUI\' : \'showUI\' }"> ${icon}</span>' +
        '<img class="${$imgUrl ? \'showUI\' : \'hideUI\' }" width = 45 height = 45 src="${$imgUrl ?  $imgUrl : \' \' }" /></div><div class="name">${name}</div></div>';

    render() {
        return (
            // specifies the tag to render the ListView component
            <ListViewComponent id='ui-list' dataSource={this.listData} enableVirtualization={true} template={this.template} height={500} headerTitle="contacts" showHeader={true}>
                <Inject services={[Virtualization]} />
            </ListViewComponent>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Conditional rendering

We have also provided following conditional rendering support for template and groupTemplate.

| Name | Syntax |
| --- | --- | --- |
| conditional class | `<div class="${ $id % 2 === 0 ? 'even-list' : 'odd-list'}"></div>`  |
| conditional attribute | `<div id="${ $id % 2 === 0 ? 'even-list' : 'odd-list'}"></div>`  |
| conditional text content | `<div>${ $id % 2 === 0 ? 'even-list' : 'odd-list'}</div>`  |

In the below sample, we have applied light blue for even list and light coral for odd list based on the conditional class.

{% tab template="listview/virtualization/conditional-ui", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent, Inject, Virtualization } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  // define the array of Json
  public listData: { [key: string]: string | object }[];

  constructor() {
    super({});
    this.listData = [
      { text: "Nancy", id: "0" },
      { text: "Andrew", id: "1" },
      { text: "Janet", id: "2" },
      { text: "Margaret", id: "3" },
      { text: "Steven", id: "4" },
      { text: "Laura", id: "5" },
      { text: "Robert", id: "6" },
      { text: "Michael", id: "7" },
      { text: "Albert", id: "8" },
      { text: "Nolan", id: "9" }
    ];
    for (let i: number = 10; i <= 1010; i++) {
      let index: number = parseInt((Math.random() * 10).toString());
      this.listData.push({ text: this.listData[index].text, id: i.toString() });
    }
  }

  public template: string =
    "<div id=\"list-container\" class=\"${ $id % 2 === 0 ? 'even-list' : 'odd-list' }\" > ${text} </div>";

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent
        id="ui-list"
        dataSource={this.listData}
        enableVirtualization={true}
        template={this.template}
        height={500}
      >
        <Inject services={[Virtualization]} />
      </ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
