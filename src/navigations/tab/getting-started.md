---
title: "Tab Getting Started"
component: "Tab"
description: "This section explains how to create a Essential JS 2 Tab control in an React application with its basic features."
---

# Getting Started

This section briefly explains about how to create a simple **Tab** component and configuring the Tab header content in React.

## Dependencies

The following is the list of dependencies required to use the Tab component in your application.

```javascript
|-- @syncfusion/ej2-react-navigations
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-buttons
        |-- @syncfusion/ej2-popups
```

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

<div class='tsx'>

```sh

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
To install Tab component, use the following command

```sh
npm install @syncfusion/ej2-react-navigations --save
```

## Adding CSS reference

 Add components style as given below in `src/App.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-navigations/styles/material.css';

```

> To refer `App.css` in the application then import it in the `src/App.tsx` file

## Initialize the Tab using JSON items collection

The Tab can be rendered by defining a JSON array. The item is rendered with [`header`](../api/tab/tabItem#header)
text and [`content`](../api/tab/tabItem#content) for each Tab.

* Import the Tab component to your `src/App.tsx` file using following code.

{% tab template="tab/tab", isDefaultActive=true, compileJsx=true, sourceFiles="app/index.tsx,index.html" %}

```typescript
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public headerText: any = [{ text: "Twitter" }, { text: "Facebook" }, { text: "WhatsApp" }];

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

  public render() {
    return (
      <TabComponent heightAdjustMode='Auto'>
        <TabItemsDirective>
          <TabItemDirective header={this.headerText[0]} content={this.content0} />
          <TabItemDirective header={this.headerText[1]} content={this.content1} />
          <TabItemDirective header={this.headerText[2]} content={this.content2} />
        </TabItemsDirective>
      </TabComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

* Run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="tab/tab", isDefaultActive=true, sourceFiles="app/index.tsx,index.html", compileJsx=true %}

```typescript
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public headerText: any = [{ text: "Twitter" }, { text: "Facebook" }, { text: "WhatsApp" }];

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

  public render() {
    return (
      <TabComponent heightAdjustMode='Auto'>
        <TabItemsDirective>
          <TabItemDirective header={this.headerText[0]} content={this.content0} />
          <TabItemDirective header={this.headerText[1]} content={this.content1} />
          <TabItemDirective header={this.headerText[2]} content={this.content2} />
        </TabItemsDirective>
      </TabComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

> In the above sample code, `element` is the `id` of the HTML element in a page to which the Tab is initialized.

## Initialize the Tab using HTML elements

The Tab component can be rendered based on the given HTML element using `<TabComponent>` tag.
Header section must be enclosed with in a wrapper element using `e-tab-header` class and corresponding content must be mapped with `e-content` class.
You need to follow the below structure of HTML elements to render the Tab,

```html

  <TabComponent id='defaultTab'>   --> Root Tab element
    <div class="e-tab-header">      --> Tab header
       <div>   --> Header Item
       </div>
    </div>
    <div class="e-content">      --> Tab content
       <div>   --> Content Item
       </div>
    </div>
  </TabComponent>

```

{% tab template="tab/tab-container", compileJsx=true, sourceFiles="app/index.tsx,index.html" %}

```typescript
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <TabComponent id='defaultTab'>
             <div className="e-tab-header">
                <div> Twitter </div>
                <div> Facebook </div>
                <div> WhatsApp </div>
            </div>
            <div className="e-content">
                <div>
                        Twitter is an online social networking service that enables users to send and read short 140-character messages called 'tweets'. Registered users can read and post tweets, but those who are unregistered can only read them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion search queries per day.
                </div>
                <div>
                        Facebook is an online social networking service headquartered in Menlo Park, California. Its website was launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website's membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford University. It gradually added support for students at various other universities and later to high-school students.
                </div>
                <div>
                        WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates under a subscription business model. It uses the Internet to send text messages, images, video, user location and audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
                </div>
            </div>
          </TabComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [How to load tab with DataSource](./how-to/load-tab-with-data-source/)