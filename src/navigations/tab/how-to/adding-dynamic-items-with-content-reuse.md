---
title: "Adding dynamic items with content reuse"
component: "Tab"
description: "This example demonstrates how to add the Essential JS 2 Tabs control with react control content reuse."
---

# Adding dynamic items with content reuse

You can add dynamic tabs by reusing the content using React **template**. Tabs can be added dynamically by passing array of items and index value to the [`addTab`](../../api/tab#addtab) method.

Content reuse can be achieved by using the following steps:
1. Declare a template within the function returns jsx element. If the template does not need arguments no need to pass the properties.
2. Assign the function as value for the template property.
3. Provide separate template declaration for each react component
and pass content by dynamically adding tab. It will reuse the content of react component.

Refer to the following sample.

{% tab template="tab/content-reuse", isDefaultActive=true, compileJsx=true, sourceFiles="app/**/*.tsx" %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { Dropdown } from './Dropdown';

export default class App extends React.Component<{}, {}> {

  public addButtonClicked(e: any): void {
    let newTabItem = [
      {
        header: { text: 'DynamicTabItem' },
        content: this.thirdDropdownTemplate
      }
    ];
    this.tabObj.addTab(newTabItem, 1);
  }

  public removeButtonClicked(e: any): void {
    this.tabObj.removeTab(1);
  }

  public firstDropdownTemplate() {
    let sportsData = [
      'Badminton',
      'Basketball',
      'Cricket',
      'Golf',
      'Hockey',
      'Rugby'
    ];
    return <Dropdown data={sportsData} />;
  }

  public secondDropdownTemplate() {
    let sportsData = [
      'Cricket',
      'Golf',
      'Hockey',
      'Rugby',
      'Badminton',
      'Basketball'
    ];
    return <Dropdown data={sportsData} />;
  }

  public thirdDropdownTemplate() {
    let sportsData = [
      'Rugby',
      'Badminton',
      'Basketball',
      'Cricket',
      'Golf',
      'Hockey'
    ];
    return <Dropdown data={sportsData} />;
  }

  public datePickerTemplate() {
    let target: string = document.querySelector('.e-toolbar-item.e-active .e-tab-text')
      .innerHTML;
    return (
      <div>
        <h1>{target} Content</h1>
        <br />
        <DatePickerComponent />
      </div>
    );
  }

  render() {
    let tabItemsHeaderText: any = [
      { text: 'DatePicker' },
      { text: 'Dropdown' },
      { text: 'Reused Dropdown' }
    ];
    return (
        <div id='container'>
          <button
            id="add"
            className="e-btn"
            onClick={this.addButtonClicked.bind(this)}
          >
            Click to add
          </button>
          <button
            id="remove"
            className="e-btn"
            onClick={this.removeButtonClicked.bind(this)}
          >
            Click to remove
          </button>
          <TabComponent
            id="tabElement"
            ref={tab => {
              this.tabObj = tab;
            }}
          >
            <TabItemsDirective>
              <TabItemDirective
                header={tabItemsHeaderText[0]}
                content={this.datePickerTemplate}
              />
              <TabItemDirective
                header={tabItemsHeaderText[1]}
                content={this.firstDropdownTemplate}
              />
              <TabItemDirective
                header={tabItemsHeaderText[2]}
                content={this.secondDropdownTemplate}
              />
            </TabItemsDirective>
          </TabComponent>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}