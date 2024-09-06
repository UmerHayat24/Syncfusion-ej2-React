---
title: "Render other components in Accordion using template"
component: "Accordion"
description: "This example demonstrates how to render other Essential JS 2 components into Essential JS 2 Accordion component content using template."
---

# Render other components in Accordion using template

You can render other components inside Accordion using React **template**. Through this, we can add content as other components directly with all functionalities to our Accordion. Follow the below guidelines for using the other components as template in Accordion.

* Declare a template within the function returns jsx element. If the template does not need arguments no need to pass the properties.

* Assign the function as value for the template property.

{% tab template="accordion/direct-components", isDefaultActive=true, compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-react-navigations';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';
import { DatePickerComponent ,CalendarComponent} from '@syncfusion/ej2-react-calendars';


export class App extends React.Component<{}, {}> {

  public continents: { [key: string]: Object }[] = [
    {
        code: 'AF', name: 'Africa', countries: [
            { code: 'NGA', name: 'Nigeria' },
            { code: 'EGY', name: 'Egypt' },
            { code: 'ZAF', name: 'South Africa' }
        ]
    },
    {
        code: 'AS', name: 'Asia', expanded: true, countries: [
            { code: 'CHN', name: 'China' },
            { code: 'IND', name: 'India', selected: true },
            { code: 'JPN', name: 'Japan' }
        ]
    },
    {
        code: 'EU', name: 'Europe', countries: [
            { code: 'DNK', name: 'Denmark' },
            { code: 'FIN', name: 'Finland' },
            { code: 'AUT', name: 'Austria' }
        ]
    },
    {
        code: 'NA', name: 'North America', countries: [
            { code: 'USA', name: 'United States of America' },
            { code: 'CUB', name: 'Cuba' },
            { code: 'MEX', name: 'Mexico' }
        ]
    },
    {
        code: 'SA', name: 'South America', countries: [
            { code: 'BRA', name: 'Brazil' },
            { code: 'COL', name: 'Colombia' },
            { code: 'ARG', name: 'Argentina' }
        ]
    },
    {
        code: 'OC', name: 'Oceania', countries: [
            { code: 'AUS', name: 'Australia' },
            { code: 'NZL', name: 'New Zealand' },
            { code: 'WSM', name: 'Samoa' }
        ]
    },
    {
        code: 'AN', name: 'Antarctica', countries: [
            { code: 'BVT', name: 'Bouvet Island' },
            { code: 'ATF', name: 'French Southern Lands' }
        ]
    },
];
private field: object = { dataSource: this.continents, id: 'code', text: 'name', child: 'countries' }

  render() {
  let headertext: any;
 function contentTemplate1(): JSX.Element {
    return(<ButtonComponent>Click me</ButtonComponent>);
  }
  function contentTemplate2(): JSX.Element {
    return(<DatePickerComponent></DatePickerComponent>);
  }
  function contentTemplate3(): JSX.Element {
    return( <CalendarComponent ></CalendarComponent>);
  }
 function contentTemplate4(): JSX.Element {
    return(  <TreeViewComponent fields={this.field}></TreeViewComponent>);
  }
    return (
        <div id='container'>
        <AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective header='Button'  content= { contentTemplate1 } />
              <AccordionItemDirective header='DatePicker'  content= { contentTemplate2 } />
              <AccordionItemDirective header='Calendar'  content= { contentTemplate3 } />
              <AccordionItemDirective header='Treeview'  content= { contentTemplate4.bind(this) } />
            </AccordionItemsDirective>
        </AccordionComponent>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById("element"));

```

{% endtab %}
