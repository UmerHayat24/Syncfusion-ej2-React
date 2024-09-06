---
title: "DropDownButton Popup Items"
component: "DropDownButton"
description: "React DropDownButton allows the end user to customize the whole popup or action items in popup using templates, navigate to other pages on action item click."
---

# Popup Items

## Icons

The Popup action item have an icon/image in it to provide visual representation of the action. To place the icon on a popup item,
set the [`iconCss`](../api/drop-down-button#iconcss) property to `e-icons` with the required icon CSS. By default, the icon is
positioned to the left side of the popup action item.

In the following sample, the icons for Edit, Delete, Mark As Read  and Like Message menu items are
added using the iconCss property.

{% tab template= "drop-down-button/popup-icon", sourceFiles="app/**/*.tsx,index.html,styles.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public  items: ItemModel[] = [
    {
        text: 'Edit',
        iconCss: 'ddb-icons e-edit'
    },
    {
        text: 'Delete',
        iconCss: 'ddb-icons e-delete'
    },
    {
        text: 'Mark As Read',
        iconCss: 'ddb-icons e-read'
    },
    {
        text: 'Like Message',
        iconCss: 'ddb-icons e-like'
    }];

  public render() {
    return (
      <div>
        <DropDownButtonComponent items = {this.items} iconCss= 'ddb-icons e-message'> Message </DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}

## Navigations

Actions in DropDownButton is usage to navigate to the other web
page when action item is clicked. This can be achieved by
providing link to the action item using the `url` property.
In the following sample, Navigation URL for Flipkart, Amazon, and
Snapdeal action items are added using the `url` property.

{% tab template= "drop-down-button/action", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel, MenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
      iconCss: 'e-cart-icon e-link',
      text: 'Flipkart',
      url: 'https://www.google.co.in/search?q=flipkart'
    },
    {
      iconCss: 'e-cart-icon e-link',
      text: 'Amazon',
      url: 'https://www.google.co.in/search?q=amazon'
    },
    {
      iconCss: 'e-cart-icon e-link',
      text: 'Snapdeal',
      url: 'https://www.google.co.in/search?q=snapdeal'
    }];
  public itemBeforeEvent(args: MenuEventArgs) {
    args.element.getElementsByTagName('a')[0].setAttribute('target', '_blank');
  }
  public render() {
    return (
    <div>
         <DropDownButtonComponent items = {this.items} iconCss= 'e-cart-icon e-shopping' beforeItemRender={this.itemBeforeEvent} > Shop By </DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

## Template

### Item Templating

Popup items can be customized by using the [`beforeItemRender`](../api/drop-down-button#beforeitemrender) event.
The item render event triggers while rendering each Popup action item. The event argument will be used to identify the action item and
customize it based on the requirement.

{% tab template= "drop-down-button/template", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel, MenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

    public items:ItemModel[] =  [
      {
          text: 'Edit'
      },
      {
          text: 'Cut'
      }];
  
      public itemBeforeEvent (args: MenuEventArgs) {
        if (args.item.text === 'Edit') {
            args.element.innerHTML = '<span></span><div><b>Paste Text</b><div>Provides option to paste only the<br>selected text.</div></div>';
            args.element.style.height = '80px';
            const span = args.element.children[0];
            span.setAttribute('class','e-cm-icons e-pastetext e-align');
            const div = args.element.children[1];
            div.setAttribute('class', 'e-div-align');
        } else {
            args.element.innerHTML = '<span></span><div><b>Paste Special</b><div>Provides options to paste formulas,<br> values, comments, validations etc...</div></div>';
            args.element.style.height = '80px';
            const span = args.element.children[0];
            span.setAttribute('class','e-cm-icons e-pastespecial e-align');
            const div = args.element.children[1];
            div.setAttribute('class', 'e-div-align');
        }
      }
      public render() {
        return (
            <div>
                <DropDownButtonComponent items = {this.items} iconCss= 'e-ddb-icons e-paste' cssClass='e-vertical' iconPosition='Top' beforeItemRender={this.itemBeforeEvent} >Paste</DropDownButtonComponent>
            </div>
      );
    }
  }
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}

### Popup Templating

The whole popup can be customized as per the requirement and it can be customized by handling
it in [`target`](../api/drop-down-button#target) property.

In the following sample, the whole popup item is customized as table template by giving `div` as target and it can be achieved
using `target` property.

{% tab template= "drop-down-button/popup", sourceFiles="app/**/*.tsx,index.html,styles.css", es5Template="popup-template", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, MenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

    public itemBeforeEvent(args: MenuEventArgs) {
      args.element.style.height = '105px';
    }
    public render() {
      return (
        <div>
          <div id="target">
            <table>
              <caption><b>Insert Table</b></caption>
              <tbody>
               <tr className='e-row'>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               </tr>
               <tr className='e-row'>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               </tr>
               <tr className='e-row'>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               </tr>
               <tr className='e-row'>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               </tr>
               <tr className='e-row'>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               </tr>
               <tr className='e-row'>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               <td className='e-data'/>
               </tr>
              </tbody>
            </table>
          </div>
          <DropDownButtonComponent  target='#target'   iconCss='e-icons e-table' iconPosition='Top' cssClass='e-vertical' beforeItemRender={this.itemBeforeEvent} >Table</DropDownButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

## Separator

The Separators are the horizontal lines that are used to separate the popup items. You `cannot` select the separators.
You can enable separators to group the popup items using the `separator` property.

In the following sample, cut, copy, and paste popup items are grouped using the separator property:

{% tab template= "drop-down-button/accessibility",sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
      iconCss: 'e-db-icons e-cut',
      text: 'Cut'
    },
    {
      iconCss: 'e-icons e-copy',
      text: 'Copy'
    },
    {
      iconCss: 'e-db-icons e-paste',
      text: 'Paste'
    },
    {
        separator: true
    },
    {
      iconCss: 'e-db-icons e-font',
      text: 'Font'
    },
    {
      iconCss: 'e-db-icons e-paragraph',
      text: 'Paragraph'
    }];

  public render() {
    return (
    <div>
       <DropDownButtonComponent items = {this.items} iconCss= 'e-icons e-edit'> Clipboard </DropDownButtonComponent>

      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}

## See Also

* [Integration with ListView component](./how-to/group-popup-items-with-listview-component)