# Icons Library

The Syncfusion React library provides the set of `base64` formatted font icons, that can be utilized in the web application.

## Steps to use Icons library

1. Add the class name `e-icons` to the HTML element which needs to render the icon. This class contains the font-family and common property of font icons.

2. Add the icon class with corresponding icon content from the [available icons](#available-icons). For example, the below code snippet represents the search icon class.

    ```css
    .e-search:before{
        content:'\e993';
    }
    ```

3. Add `e-icons` and `e-search` class to the HTML element.

    ```html
    <span class="e-icons e-search"></span>
    ```

4. Add the CDN link reference of icons library in the `~index.html` file.

    ```html
    <link href="https://cdn.syncfusion.com/ej2/ej2-base/styles/material.css" rel="stylesheet" />
    ```

    The below code snippet represents the complete example of icon usage.

    ```tsx
    import * as React from 'react';

    var icons = `
    .e-search:before {
        content:'\\e993';
    }
    .e-upload:before {
        content: '\\e725';
    }
    .e-font:before {
        content: '\\e34c';
    }
    `
    export default class App extends React.Component<{}, {}> {
        render() {
            var iconList = ['e-search', 'e-upload', 'e-font'];
            const listItems = iconList.map((icon, index) =>
                <li><span className={`e-icons ${icon}`} key={index}></span></li>
            );

            return (
                <div>
                    <style>{icons}</style>
                    <div className="icons">
                        <ul>
                            {listItems}
                        </ul>
                    </div>
                </div>
            );
        }
    }
    ```

## Customization

* The Syncfusion React icon library can be customized its color and size by overriding the `e-icons` class.

    ```tsx
    import * as React from 'react';

    var icons = `
    .e-icons {
        color: #00ffff;
        font-size: 26px;
    }
    .e-search:before {
        content:'\\e993';
    }
    .e-upload:before {
        content: '\\e725';
    }
    .e-font:before {
        content: '\\e34c';
    }
    `
    export default class App extends React.Component<{}, {}> {
        render() {
            var iconList = ['e-search', 'e-upload', 'e-font'];
            const listItems = iconList.map((icon, index) =>
                <li><span className={`e-icons ${icon}`} key={index}></span></li>
            );

            return (
                <div>
                    <style>{icons}</style>
                    <div className="icons">
                        <ul>
                            {listItems}
                        </ul>
                    </div>
                </div>
            );
        }
    }
    ```

## Available Icons

The complete package of Essential JS 2 icons is listed in the following table. The corresponding icon content can be referred in the content section.

<!-- markdownlint-disable MD033 -->

### Material

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/material/demo.html" style="height:1000px;"></iframe>

### Fabric

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/fabric/demo.html" style="height:1000px;"></iframe>

### Bootstrap

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/bootstrap/demo.html" style="height:1000px;"></iframe>

### Bootstrap 4

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/bootstrap4/demo.html" style="height:1000px;"></iframe>

### High Contrast

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/highcontrast/demo.html" style="height:1000px;"></iframe>