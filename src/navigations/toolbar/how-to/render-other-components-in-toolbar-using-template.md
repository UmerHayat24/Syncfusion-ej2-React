---
title: "Render other components in Toolbar using template"
component: "Accordion"
description: "This example demonstrates how to render other Essential JS 2 components into Essential JS 2 Toolbar component items using template."
---

# Render other components in Toolbar using template

You can render other components inside Toolbar using React **template**. Through this, we can add content as other components directly with all functionalities to our Toolbar. Follow the below guidelines for using the other components as template in Toolbar.

* Declare a template within the function returns jsx element. If the template does not need arguments no need to pass the properties.

* Assign the function as value for the template property.

{% tab template="toolbar/direct-components", isDefaultActive=true, compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ToolbarComponent, ItemsDirective, ItemDirective } from '@syncfusion/ej2-react-navigations';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import { DatePickerComponent ,CalendarComponent} from '@syncfusion/ej2-react-calendars';


export default class App extends React.Component<{}, {}> {

  render() {

  function contentTemplate1(): JSX.Element {
    return(<ButtonComponent>Click me</ButtonComponent>);
  }
  function contentTemplate2(): JSX.Element {
    return(<DatePickerComponent></DatePickerComponent>);
  }
    return (
        <div id='container'>
         <ToolbarComponent id="toolbar">
         <ItemsDirective>
            <ItemDirective template = { contentTemplate1 } />
            <ItemDirective template = { contentTemplate2 } />
            <ItemDirective text="Cut" />
            <ItemDirective text="Copy"/>
            <ItemDirective text="Paste"/>
            <ItemDirective type="Separator"/>
            <ItemDirective text="Bold"/>
            <ItemDirective text="Italic"/>
            <ItemDirective text="Underline"/>
          </ItemsDirective>
      </ToolbarComponent>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}