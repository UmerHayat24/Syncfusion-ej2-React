---
title: "Accordion Getting Started"
component: "Accordion"
description: "This section explains how to create Accordion control in an React application with its basic features."
---

# Getting Started

This section briefly explains you the steps required to create a simple Accordion and demonstrate the basic usage of the Accordion control.

## Dependencies

The following list of dependencies are required to use the Accordion component in your application.

```js
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
To install Accordion component, use the following command

```sh
npm install @syncfusion/ej2-react-navigations --save
```

## Adding CSS reference

 Add components style as given below in `src/App.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-navigations/styles/material.css';

```

> To refer `App.css` in the application then import it in the `src/App.tsx` file.

## Initialize the Accordion using Items

The Accordion can be rendered by defining an array of [`items`](../api/accordion#items).

* Import the Accordion component to your `src/App.tsx` file using following code.

{% tab compileJsx=true %}

```typescript
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective  } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public content0() {
    return <div>
        Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.
      </div>;
  }
  public content1() {
    return <div>
        The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.
      </div>;
  }
  public content2() {
    return <div>
        JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.
      </div>;
  }
  public render() {
    return (
        <AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective expanded='true' header='ASP.NET' content={this.content0} />
              <AccordionItemDirective header='ASP.NET MVC' content={this.content1} />
              <AccordionItemDirective header='JavaScript' content={this.content2} />
            </AccordionItemsDirective>
        </AccordionComponent>
    );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));

```

{% endtab %}

* Run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="accordion/accordion", compileJsx=true , isDefaultActive=true  %}

```typescript
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective  } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public content0() {
    return <div>
        Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.
      </div>;
  }
  public content1() {
    return <div>
        The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.
      </div>;
  }
  public content2() {
    return <div>
        JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.
      </div>;
  }
  public render() {
    return (
        <AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective expanded='true' header='ASP.NET' content={this.content0} />
              <AccordionItemDirective header='ASP.NET MVC' content={this.content1} />
              <AccordionItemDirective header='JavaScript' content={this.content2} />
            </AccordionItemsDirective>
        </AccordionComponent>
    );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

> In the above sample code, `#element` is the `id` of the HTML element in a page to which the Accordion is initialized.

## Initialize the Accordion using HTML elements

The Accordion component can be rendered based on the given HTML element using `id` as `target` property.
You need to follow the below structure of HTML elements to render the Accordion.

```html
  <div id='accordion_html_markup'>   --> Root Accordion Element
       <div>      --> Accordion Item Container
            <div>   --> Accordion Header Container
                <div> </div> --> Accordion Header
            </div>
            <div>  --> Accordion Panel Container
                <div> </div> --> Accordion Content
             </div>
        </div>
  </div>
```

{% tab template="accordion/accordion", compileJsx=true , isDefaultActive=true %}

```typescript
import { AccordionComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <AccordionComponent>
        <div>
          <div>
            <div> ASP.NET </div>
          </div>
          <div>
            <div>
              Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.
            </div>
          </div>
        </div>
        <div>
          <div>
            <div> ASP.NET MVC </div>
          </div>
          <div>
            <div>
              The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.
            </div>
          </div>
        </div>
        <div>
          <div>
            <div> JavaScript </div>
          </div>
          <div>
            <div>
              JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser.
            </div>
          </div>
        </div>
      </AccordionComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));
```

{% endtab %}

> You can add the custom class into Accordion component using [`cssClass`](../api/accordion/accordionItem#cssclass) property which is used to customize the Accordion component.

## See Also

* [How to load accordion items dynamically](./how-to/load-accordion-items-dynamically/)