---
title: "Getting Started"
component: "Card"
description: "This section explains how to create a Essential JS 2 Card control in the React application with its basic features."
---

# Getting Started

This section explains how to create a simple **Card** using Styles, and
how to configure the structure for the header section, Horizontal, action buttons, content section.

## Dependencies

The Card Component is pure CSS component so no specific dependencies to render the card.

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

### using TSX

```sh

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

### using JSX

```sh

create-react-app quickstart

cd quickstart

```

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.

Install the below required dependency package in order to use the `Card` component in your application.

```bash
npm install @syncfusion/ej2-layouts –save
```

* The Card CSS files are available in the `ej2-layouts` package folder.
This can be referenced in your application using the following code.

`[src/styles/styles.css]`

```css
@import '../node_modules/@syncfusion/ej2-layouts/styles/material.css';
```

## Adding a simple Card

* Add the HTML `div` element with `e-card` class into your `index.html`.

`[src/index.html]`

```html
        <div className = "e-card">
          Sample Card
        </div>
```

## Adding a header to the card

You can create cards with a header in a specific structure. For adding header you need to create `div` element and add `e-card-header` class.

* You can include heading inside the card header by adding an `div` element with
`e-card-header-caption` class, and also content will be added by adding element with
`e-card-content`. For detailed information, refer to the [Header and Content](./header-content/).

```html
    <div class = "e-card">                    --> Root Element
        <div class="e-card-header">           --> Root Header Element
            <div class="e-card-header-caption">    --> Root Heading Element
                <div class="e-card-header-title"></div>   --> Heading Title Element
            </div>
            <div class="e-card-content"></div>         --> Card content Element
        </div>
    </div>
```

* Now, run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="card/card_header", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className="e-card" id="basic">
          <div className="e-card-header">
            <div className="e-card-header-caption">
              <div className="e-card-title">Advanced UWP</div>
            </div>
          </div>
          <div className="e-card-content">
            Communicating with Windows 10 and Other Apps, the second in a five-part series written by Succinctly series
            author Matteo Pagani. To download the complete white paper, and other papers in the series, visit
            the White Paper section of Syncfusion’s Technology Resource Portal.
            </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));
```

{% endtab %}

## See Also

* [How to add a header and content](./header-content/)