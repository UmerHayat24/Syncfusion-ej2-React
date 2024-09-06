---
title: "Tab Header"
component: "Tab"
description: "This section explains how to create a Essential JS 2 Tab control header with different styles in an React application."
---

# Header

This section explains about modifying the style of Tab header, and configuring its icons and positions.

## Styles

You can customize header styles by adding predefined classes in the Tab root element. The pre-defined CSS class names are as follows:

* **e-fill**: The Selected Tab header background is set as solid fill.
* **e-background**: Tab header has a solid fill background, and the selected header has a highlighted border.
* **e-background e-accent**: Tab header has a solid fill background, and the selected header has a highlighted border with accent color.

> If the above custom style classes are not included in the root element, the default style is applied to the Tab items.

{% tab template="tab/tab-style", sourceFiles="app/**/*.tsx,index.css", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public tabObj: TabComponent;
  public headerText: any = [{ text: "Twitter" }, { text: "Facebook" }, { text: "WhatsApp" }];
  public fields: object = { text: 'text', value: 'value' };
  public headerData: any = [
    { 'value': 'default', 'text': 'Default' }, { 'value': 'fill', 'text': 'Fill' },
    { 'value': 'background', 'text': 'Background' }, { 'value': 'accent', 'text': 'Accent' }
  ];
  public hdrVal: string = 'default';

  public changeHeaderStyles(e: ChangeEventArgs): void {
    this.removeStyleClass();
    const name: string = (document.getElementById('headerStyles') as HTMLSelectElement).value;
    if (name === 'Fill') {
      this.tabObj.element.classList.add('e-fill');
    } else if (name === 'Background') {
      this.tabObj.element.classList.add('e-background');
    } else if (name === 'Accent') {
      this.tabObj.element.classList.add('e-background');
      this.tabObj.element.classList.add('e-accent');
    }
  }

  public removeStyleClass(): void {
    this.tabObj.element.classList.remove('e-fill');
    this.tabObj.element.classList.remove('e-background');
    this.tabObj.element.classList.remove('e-accent');
  }

  public content0() {
    return <div>
      Twitter is an online social networking service that enables users to send and read short 140-character
      messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read
      them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San
      Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey,
      Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity,
      with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion
      search queries per day.
      </div>;
  }
  public content1() {
    return <div>
      Facebook is an online social networking service headquartered in Menlo Park, California. Its website was
      launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo
      Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website\'\s
      membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford
      University. It gradually added support for students at various other universities and later to high-school students.
      </div>;
  }
  public content2() {
    return <div>
      WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates
      under a subscription business model. It uses the Internet to send text messages, images, video, user location and
      audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user
      base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in
      Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
      </div>;
  }

  public render() {
    return (
      <div>
        <DropDownListComponent id='headerStyles' dataSource={this.headerData} fields={this.fields} value={this.hdrVal} width={'150'} change={this.changeHeaderStyles = this.changeHeaderStyles.bind(this)} />
        <br /><br />
        <TabComponent heightAdjustMode='Auto' height={320} ref={tab => this.tabObj = tab!}>
          <TabItemsDirective>
            <TabItemDirective header={this.headerText[0]} content={this.content0} />
            <TabItemDirective header={this.headerText[1]} content={this.content1} />
            <TabItemDirective header={this.headerText[2]} content={this.content2} />
          </TabItemsDirective>
        </TabComponent>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

## Icon positions

You can customize the position of the Tab header icons using the [`iconPosition`](../api/tab/header#iconposition) property.  This property depends on the header items [`iconCss`](../api/tab/header#iconcss) property.  By default, Tab header icon is placed on left position.  The position values are as follows:

* **Left**: Icon is placed on the left of the Tab header item.
* **Right**: Icon is placed on the right of the Tab header item.
* **Top**: Icon is placed on the top of the Tab header item.
* **Bottom**: Icon is placed on the bottom of the Tab header item.

{% tab template="tab/icon-position", sourceFiles="app/**/*.tsx,index.css", compileJsx=true %}

```typescript
import { Effect } from '@syncfusion/ej2-base';
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public headerText: any = [{ text: "Twitter", iconCss: 'e-twitter' }, { text: "Facebook", iconCss: 'e-facebook' }, { text: "WhatsApp", iconCss: 'e-whatsapp' }];
  public tabInstance: TabComponent;
  public dropInstance: DropDownListComponent;
  public fields: object = { text: 'text', value: 'value' };
  public headerData: any = [
    { 'value': 'left', 'text': 'Left' }, { 'value': 'right', 'text': 'Right' },
    { 'value': 'top', 'text': 'Top' }, { 'value': 'bottom', 'text': 'Bottom' }
  ];
  public value: string = 'left';

  public content0() {
    return <div>
      Twitter is an online social networking service that enables users to send and read short 140-character messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion search queries per day.
      </div>;
  }
  public content1() {
    return <div>
      Facebook is an online social networking service headquartered in Menlo Park, California. Its website was launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford University. It gradually added support for students at various other universities and later to high-school students.
      </div>;
  }
  public content2() {
    return <div>
      WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates under a subscription business model. It uses the Internet to send text messages, images, video, user location and audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
      </div>;
  }
  public onChange(): void {
    let items: any = this.tabInstance.items;
    for(let i: number = 0; i < items.length; i++) {
        items[i].header.iconPosition = this.dropInstance.value;
    };
  }

  public render() {
    return (
    <div>
        <DropDownListComponent ref={drop => this.dropInstance = drop!} id='headerStyles' dataSource={this.headerData} fields={this.fields} value={this.value} width={'150'} change={this.onChange = this.onChange.bind(this)} />
        <br /><br />
      <TabComponent ref={tab => this.tabInstance = tab!}>
        <TabItemsDirective>
          <TabItemDirective header={this.headerText[0]} content={this.content0} />
          <TabItemDirective header={this.headerText[1]} content={this.content1} />
          <TabItemDirective header={this.headerText[2]} content={this.content2} />
        </TabItemsDirective>
      </TabComponent>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [How to customize selected tab styles](./how-to/customize-selected-tab-styles/)