# Chip Customization

This section explains the customization of styles, leading icons, avatar, and trailing icons in Chip control.

## Styles

The Chip control has the following predefined styles that can be defined using the `cssClass` property.

| Class | Description |
| -------- | -------- |
| e-primary | Represents a primary chip. |
| e-success | Represents a positive chip. |
| e-info |  Represents an informative chip. |
| e-warning | Represents a chip with caution. |
| e-danger | Represents a negative chip. |

{% tab template="chips/default", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true,compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ChipListComponent id="chip-avatar">
            <ChipsDirective>
                <ChipDirective text="Primary" cssClass="e-primary"></ChipDirective>
                <ChipDirective text="Success" cssClass="e-success"></ChipDirective>
                <ChipDirective text="Info" cssClass="e-info"></ChipDirective>
                <ChipDirective text="Warning" cssClass="e-warning"></ChipDirective>
                <ChipDirective text="Danger" cssClass="e-danger"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Leading Icon

You can add and customize the leading icon of chip using the `leadingIconCss` property.

{% tab template="chips/avatar", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ChipListComponent id="chip-avatar">
            <ChipsDirective>
                <ChipDirective text="Andrew" leadingIconCss='andrew'></ChipDirective>
                <ChipDirective text="Janet" leadingIconCss='janet'></ChipDirective>
                <ChipDirective text="Laura" leadingIconCss='laura'></ChipDirective>
                <ChipDirective text="Margaret" leadingIconCss='margaret'></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Avatar

You can add and customize the avatar of chip using the `avatarIconCss` property.

{% tab template="chips/avatar", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ChipListComponent id="chip-avatar">
            <ChipsDirective>
                <ChipDirective text="Andrew" avatarIconCss='andrew'></ChipDirective>
                <ChipDirective text="Janet" avatarIconCss='janet'></ChipDirective>
                <ChipDirective text="Laura" avatarIconCss='laura'></ChipDirective>
                <ChipDirective text="Margaret" avatarIconCss='margaret'></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Avatar Content

You can add and customize the avatar content of chip using the `avatarText` property.

{% tab template="chips/avatar", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ChipListComponent id="chip-avatar">
            <ChipsDirective>
                <ChipDirective text="Andrew" avatarText='A'></ChipDirective>
                <ChipDirective text="Janet" avatarText='J'></ChipDirective>
                <ChipDirective text="Laura" avatarText='L'></ChipDirective>
                <ChipDirective text="Margaret" avatarText='M'></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Trailing Icon

You can add and customize the trailing icon of chip using the `trailingIconCss` property.

{% tab template="chips/avatar", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true,compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ChipListComponent id="chip-avatar">
            <ChipsDirective>
                <ChipDirective text="Andrew" trailingIconCss= 'e-dlt-btn'></ChipDirective>
                <ChipDirective text="Janet" trailingIconCss= 'e-dlt-btn'></ChipDirective>
                <ChipDirective text="Laura" trailingIconCss= 'e-dlt-btn'></ChipDirective>
                <ChipDirective text="Margaret" trailingIconCss= 'e-dlt-btn'></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Outline Chip

Outline chip has the border with the background transparent. It can be set using the `cssClass` property.

{% tab template="chips/avatar", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
    <div>
        <ChipListComponent id="chip-avatar" cssClass="e-outline">
            <ChipsDirective>
                <ChipDirective text="Chai"></ChipDirective>
                <ChipDirective text="Chang"></ChipDirective>
                <ChipDirective text="Aniseed Syrup"></ChipDirective>
                <ChipDirective text="Ikura"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
        <ChipListComponent id="chip-avatar" cssClass="e-outline" enableDelete={true}>
            <ChipsDirective>
                <ChipDirective text="Andrew"></ChipDirective>
                <ChipDirective text="Janet"></ChipDirective>
                <ChipDirective text="Laura"></ChipDirective>
                <ChipDirective text="Margaret"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}
