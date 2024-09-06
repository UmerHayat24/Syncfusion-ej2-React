---
title: "ButtonGroup Types and Styles"
component: "Button"
description: "React Button component supports different types, predefined styles, sizes and also has support for icons."
---

# Types and Styles

This section explains the different styles and types of Buttons.

## Button styles

The Essential JS 2 Button has the following predefined styles that can be defined using
[`cssClass`](../api/button#cssclass) property.

| Class | Description |
| -------- | -------- |
| e-primary | Used to represent a primary action. |
| e-success | Used to represent a positive action. |
| e-info |  Used to represent an informative action. |
| e-warning | Used to represent an action with caution. |
| e-danger | Used to represent a negative action. |
| e-link |  Changes the appearance of the Button like a hyperlink. |

{% tab template="button/button-style", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

class App extends React.Component<{}, {}> {
  render() {
    return (
        <div>
            { /* Primary Button - Used to represent a primary action. */ }
            <ButtonComponent cssClass='e-primary'>Primary</ButtonComponent>

            { /* Success Button - Used to represent a positive action. */ }
            <ButtonComponent cssClass='e-success'>Success</ButtonComponent>

            { /* Info Button - Used to represent an informative action. */ }
            <ButtonComponent cssClass='e-info'>Info</ButtonComponent>

            { /* Warning Button - Used to represent an action with caution.*/ }
            <ButtonComponent cssClass='e-warning'>Warning</ButtonComponent>

            { /* Danger Button - Used to represent a negative action.*/ }
            <ButtonComponent cssClass='e-danger'>Danger</ButtonComponent>

            { /* Link Button - Changes the appearance of the Button like a hyperlink.*/ }
            <ButtonComponent cssClass='e-link'>Link</ButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

> Predefined Button styles provide only the visual indication. So, Button content should define the Button
style for the users of assistive technologies such as screen readers.
> Primary action button can also be achieved by setting [`isPrimary`](../api/button#isprimary) property as `true`.

## Button types

The types of Essential JS 2 Button are as follows:

* Basic types
* Flat Button
* Outline Button
* Round Button
* Toggle Button

### Basic types

The basic Button types are explained below.

| Type | Description |
| -------- | -------- |
| Button | Defines a click Button. |
| Submit | This Button submits the form data to the server. |
| Reset |  This Button resets all the controls of the form elements to their initial values. |

{% tab template="button/basic-types", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

class App extends React.Component<{}, {}> {
  render() {
    return (
        <form>
            { /* Submit.*/ }
            <ButtonComponent type='submit'>Submit</ButtonComponent>

            { /* Reset.*/ }
            <ButtonComponent type='reset'>Reset</ButtonComponent>
        </form>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

### Flat Button

The Flat Button is styled with no background color. To create a flat Button,
set the [`cssClass`](../api/button#cssclass) property to `e-flat`.

### Outline Button

An outline Button has border with transparent background. To create an outline Button,
set the [`cssClass`](../api/button#cssclass) property as `e-outline`.

### Round Button

A round Button is shaped like a circle. Usually, it contains an icon representing its action.
To create a round Button, set the [`cssClass`](../api/button#cssclass) property to `e-round`.

{% tab template="button/button-type", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div>
            { /* Flat Button. */ }
            <ButtonComponent cssClass='e-flat'>Flat</ButtonComponent>

            { /* Outline Button. */ }
            <ButtonComponent cssClass='e-outline'>Outline</ButtonComponent>

            { /* Round Button - Icon can be loaded by setting "e-icons e-plus-icon" in "iconCss" property.
            Use "e-icons" class name to load Essential JS 2 built-in icons.
            Use "e-plus-icon" class name to load plus icon, that you can refer in "styles.css". */ }
            <ButtonComponent cssClass='e-round' iconCss='e-icons e-plus-icon' isPrimary={true}/>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

### Toggle Button

A toggle Button allows you to change between the two states. The Button is active in toggled state and
can be recognized through the `e-active` class. The functionality of the toggle Button is handled
by  click event. To create a toggle Button, set the [`isToggle`](../api/button#istoggle)
property to `true`. In the following code snippet, the toggle Button text changes to play/pause based on the
state of the Button with the use of click event.

{% tab template="button/toggle-button", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from "react";
import * as ReactDOM from "react-dom";

enableRipple(true);

export default class App extends React.Component<{}, {content: string, iconCss: string}> {
    constructor(props: any) {
        super(props);
        this.state = { content: 'Play' , iconCss: 'e-btn-sb-icon e-play-icon' };
        this.btnClick = this.btnClick.bind(this);
    }
    // Click Event.
    public btnClick(): void {
        if (this.state.content === "Play") {
            this.setState({ content: 'Pause', iconCss:'e-btn-sb-icon e-pause-icon'});
        }
        else {
            this.setState({ content: 'Play',iconCss:'e-btn-sb-icon e-play-icon' });
        }
    }
    // Button is active in toggled state.
    public render() {
        return (
            <ButtonComponent cssClass='e-flat' iconCss={this.state.iconCss} content= {this.state.content} isToggle={true} onClick={ this.btnClick.bind(this) }/>
        )
    }
}
ReactDOM.render(<App />, document.getElementById('button'));
```

{% endtab %}

## Change Button type

To change the default Button to flat Button, set the [`cssClass`](../api/button#cssclass) property to `e-flat` and text content of the Button is set using [`content`](../api/button#content) property.

{% tab template="button/default", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

//To change the Button type.
class App extends React.Component<{}, {}> {
  render() {
    return (
      <ButtonComponent cssClass='e-flat' content='Button'></ButtonComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

## Icons

### Button with font icons

The Button can have an icon to provide the visual representation of the action. To place the icon on a Button,
set the [`iconCss`](../api/button#iconcss) property with the required icon CSS.
By default, the icon is positioned to the left side of the Button. You can customize the icon's position by
using the [`iconPosition`](../api/button#iconposition) property.

{% tab template="button/icon", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div>
            { /* To position the icon to the left of the text on a Button. */ }
            <ButtonComponent iconCss='e-btn-sb-icon e-prev-icon'>Previous</ButtonComponent>

            { /* To position the icon to the right of the text on a Button. */ }
            <ButtonComponent iconCss='e-btn-sb-icon e-stop-icon' iconPosition='Right'>Stop</ButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

### Button with SVG image

SVG image can be added to the Button using [`iconCss`](../api/button#iconcss) property.

In the following example, SVG image is added using the iconCss class `e-search-icon` by setting `height` and `width`.

{% tab template="button/svg", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div>
            <ButtonComponent iconCss='e-search-icon'/>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the
element. You can also use third party icons on the Button using the [`iconCss`](../api/button#iconcss) property.

## Button size

The two types of Button sizes are default and small. To change the size of the
default Button to small Button, set the [`cssClass`](../api/button#cssclass) property to `e-small`.

{% tab template="button/size", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div>
            { /* Small Button. */ }
            <ButtonComponent cssClass='e-small'>Small</ButtonComponent>

            { /* Normal Button. */ }
            <ButtonComponent>Normal</ButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

## See Also

* [Customize Button appearance](./how-to/customize-button-appearance)
* [How to create block button](./how-to/create-a-block-button)
* [How to create repeat button](./how-to/repeat-button)