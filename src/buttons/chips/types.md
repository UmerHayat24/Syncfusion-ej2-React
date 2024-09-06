# Types

The ChipList control has the following types.

* Input Chip
* Choice Chip
* Filter Chip
* Action Chip

## Input Chip

Input Chip holds information in compact form. It converts user input into chips.

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
        <ChipListComponent id="chip-avatar" enableDelete={true} selection="Single">
            <ChipsDirective>
                <ChipDirective text="Andrew"></ChipDirective>
                <ChipDirective text="Janet"></ChipDirective>
                <ChipDirective text="Laura"></ChipDirective>
                <ChipDirective text="Margaret"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Choice Chip

Choice Chip allows you to select a single chip from the set of ChipList/ChipCollection. It can be enabled by setting the `selection` property to `Single`.

{% tab template="chips/default", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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
        <ChipListComponent id="chip-avatar" selection="Single">
            <ChipsDirective>
                <ChipDirective text="Small"></ChipDirective>
                <ChipDirective text="Medium"></ChipDirective>
                <ChipDirective text="Large"></ChipDirective>
                <ChipDirective text="Extra Large"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Filter Chip

Filter Chip allows you to select a multiple chip from the set of ChipList/ChipCollection. It can be enabled by setting the `selection` property to `Multiple`.

{% tab template="chips/default", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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
        <ChipListComponent id="chip-avatar" selection="Multiple">
            <ChipsDirective>
                <ChipDirective text="Chai"></ChipDirective>
                <ChipDirective text="Chung"></ChipDirective>
                <ChipDirective text="Aniseed Syrup"></ChipDirective>
                <ChipDirective text="Ikura"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

## Action Chip

The Action Chip triggers the event like click or delete, which helps doing action based on the event.

{% tab template="chips/default", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';


enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  chipClick(e: any) {
    alert('you have clicked ' + e.target.textContent);
  }

  render() {
    return (
      <ChipListComponent id="chip-avatar" onClick={this.chipClick.bind(this)}>
        <ChipsDirective>
          <ChipDirective text="Send a text" />
          <ChipDirective text="Set a remainder" />
          <ChipDirective text="Read my emails" />
          <ChipDirective text="Set alarm" />
        </ChipsDirective>
      </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}

### Deletable Chip

Deletable Chip allows you to delete a chip from ChipList/ChipCollection. It can be enabled by setting the `enableDelete` property to `true`.

{% tab template="chips/default", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';


enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  chipClick(e: any) {
    alert('you have clicked ' + e.target.textContent);
  }
  render() {
    return (
        <ChipListComponent id="chip-avatar" enableDelete={true}>
            <ChipsDirective>
                <ChipDirective text="Send a text"></ChipDirective>
                <ChipDirective text="Set a remainder"></ChipDirective>
                <ChipDirective text="Read my emails"></ChipDirective>
                <ChipDirective text="Set alarm"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}
