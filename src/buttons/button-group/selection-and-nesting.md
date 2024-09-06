---
title: "ButtonGroup Selection and Nesting"
component: "ButtonGroup"
description: "ButtonGroup supports single selection, multiple selection, nesting with dropdownbutton and splitbutton components."
---

# Selection and Nesting

## Selection

### Single selection

ButtonGroup supports radio type selection in which only one button can be selected. This can be achieved by adding input element
along with `id` attribute with its corresponding label along with `htmlFor` attribute inside the target element. In this ButtonGroup,
the type of the input element should be `radio` and `e-btn` is added to the `label` element.

The following example illustrates the single selection behavior in ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render radio type ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className='e-btn-group'>
            <input type="radio" id="radioleft" name="align" value="left" />
            <label className="e-btn" htmlFor="radioleft">Left</label>
            <input type="radio" id="radiomiddle" name="align" value="middle" />
            <label className="e-btn" htmlFor="radiomiddle">Center</label>
            <input type="radio" id="radioright" name="align" value="right"/>
            <label className="e-btn" htmlFor="radioright">Right</label>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}

### Multiple selection

ButtonGroup supports checkbox type selection in which multiple button can be selected. This can be achieved by adding input element
along with `id` attribute with its corresponding label along with `htmlFor` attribute inside the target element. In this ButtonGroup,
the type of the input element should be `checkbox` and `e-btn` is added to the `label` element.

The following example illustrates the multiple selection behavior in ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render checkbox type ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className='e-btn-group'>
            <input type="checkbox" id="checkbold" name="font" value="bold"/>
            <label className="e-btn" htmlFor="checkbold">Bold</label>
            <input type="checkbox" id="checkitalic" name="font" value="italic" />
            <label className="e-btn" htmlFor="checkitalic">Italic</label>
            <input type="checkbox" id="checkline" name="font" value="underline"/>
            <label className="e-btn" htmlFor="checkline">Underline</label>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}

## Nesting

Nesting with other components can be possible in ButtonGroup. The following components can be nested in ButtonGroup,
* DropDownButton
* SplitButton

For nesting support, [`SplitButton dependencies`](./../split-button/getting-started#dependencies) should be configured and
it should be added in `system.config.js`.

### DropDownButton

To initialize DropDownButton component, refer [`DropDownButton Getting Started documentation`](./../drop-down-button/getting-started).

In the following example, DropDownButton component is added in `src/App.tsx` by importing it from `ej2-react-splitbuttons`.

{% tab template="button-group/nesting", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';

// To render ButtonGroup with DropDownButton nesting.
class App extends React.Component<{}, {}> {
  public items: ItemModel[] = [
    {
        text: 'Learn SQL'
    },
    {
        text: 'Learn PHP'
    },
    {
        text: 'Learn Bootstrap'
    }];

  render() {
    return (
      <div>
        <div className='e-btn-group'>
           <ButtonComponent>HTML</ButtonComponent>
           <ButtonComponent>CSS</ButtonComponent>
           <ButtonComponent>Javascript</ButtonComponent>
           <DropDownButtonComponent id="dropdownelement" items={this.items}> More </DropDownButtonComponent>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}

### SplitButton

To initialize SplitButton component, refer [`SplitButton Getting Started documentation`](../split-button/getting-started).

In the following example, SplitButton component is added in `src/App.tsx` by importing it from `ej2-react-splitbuttons`.

{% tab template="button-group/nesting", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { SplitButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';

// To render ButtonGroup with SplitButton nesting.
class App extends React.Component<{}, {}> {
    public items: ItemModel[] = [
    {
        text: 'Paste'
    },
    {
        text: 'Paste Text'
    },
    {
        text: 'Paste Special'
    }];

  render() {
    return (
      <div>
        <div className='e-btn-group'>
           <ButtonComponent>Cut</ButtonComponent>
           <ButtonComponent>Copy</ButtonComponent>
           <SplitButtonComponent id="splitbuttonelement" items={this.items}> Paste </SplitButtonComponent>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}

## See Also

* [Show ButtonGroup selected state on initial render](./how-to/show-buttongroup-selected-state-on-initial-render)
