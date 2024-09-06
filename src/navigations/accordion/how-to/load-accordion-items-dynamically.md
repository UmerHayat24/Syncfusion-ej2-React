---
title: "Load accordion items dynamically"
component: "Accordion"
description: "This example demonstrates how to dynamically load or add an accordion item in the Essential JS 2 Accordion control."
---

# Load accordion items dynamically

Accordion items can be added dynamically by passing the item and index value with the [`addItem`](../../api/accordion#additem) method.

In the following demo, you can add the accordion content by expanding any accordion header content using [`expanded`](../../api/accordion#expanded) event.

* Data is fetched from the data source.

* The data is formatted as a JSON object with [`header`](../../api/accordion/accordionItem#header) and [`content`](../../api/accordion/accordionItem#content) fields.

* Here last index is calculated to append the new accordion at the end.

{% tab template="accordion/accordion-items-dynamically", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective, ExpandEventArgs, AccordionItemModel } from '@syncfusion/ej2-react-navigations';
// @ts-ignore
import { accordion } from '../datasource.tsx';

let dbFlag: number = 0;
let dynamciAcrdnCount: number = 2;
export class ReactApp extends React.Component<{}, {}> {

  acrdnInstance: AccordionComponent | any;
  render() {
    return (
      <div className='control-pane'>
        <div className='control-section accordion-control-section'>
          <div className='control Accordion-sample'>
          {/* Render the Accoridon Component */}
            <AccordionComponent expanded= {this.expanded.bind(this)} ref={acrdn => this.acrdnInstance = acrdn}>
              <AccordionItemsDirective>
                <AccordionItemDirective header='ASP.NET' content='Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.' />
                <AccordionItemDirective header='ASP.NET Core' content='ASP.NET Core is a free and open-source web framework, and the next generation of ASP.NET, developed by Microsoft and the community. It is a modular framework that runs on both the full .NET Framework, on Windows, and the cross-platform .NET Core.' />
                <AccordionItemDirective header='ASP.NET MVC' content='The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.' />
              </AccordionItemsDirective>
            </AccordionComponent>
          </div></div>
      </div>

    );
  }
  public expanded (e: ExpandEventArgs) {
        let Elementindex = document.getElementsByClassName("e-expand-state e-selected e-active")[0];
        if([].slice.call((e.element as any).parentElement.children).indexOf(e.element) == [].slice.call((e.element as any).parentElement.children).indexOf(Elementindex)) {
          let array: AccordionItemModel[] = accordion as AccordionItemModel[];
          for(let i: number = 0 ; i < dynamciAcrdnCount; i++)
          {
            if (dbFlag === array.length) {
                return; }
            this.acrdnInstance.addItem( array[dbFlag] , this.acrdnInstance.items.length );
            ++dbFlag;
          }
        }
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('sample'));

```

{% endtab %}
