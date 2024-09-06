---
title: "Getting Started"
component: "In-place Editor"
description: "Learn how to create an Essential JS 2 React In-place Editor component with its basic features."
---

# Getting Started

This section briefly explains about how to create a simple In-place Editor and demonstrate the basic usage of the In-place Editor component.

## Dependencies

The following is the list of dependencies required to use the In-place Editor component in your application.

```javascript
|-- @syncfusion/ej2-react-inplace-editor
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-calendars
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-dropdowns
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-richtexteditor
```

## Set up your development environment

Before starting, need to install [`Create-react-app`](https://github.com/facebookincubator/create-react-app) command line interface into your machine globally by using following command.

```bash
npm install -g create-react-app
```

Create a new project using create-react-app command as follows

<div class='tsx'>

```bash
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

Install the below required dependency package in order to use the `In-place Editor` component in your application.

```bash
npm install @syncfusion/ej2-react-inplace-editor –save
```

The above package installs [In-place Editor dependencies](#dependencies) which are required
 to render the In-place Editor component in React environment.

* In-place Editor CSS files are available in the `ej2-react-inplace-editor` package folder.
Import the In-place Editor component's required CSS references as follows in `src/App.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-richtexteditor/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-inplace-editor/styles/material.css';
```

## Add the In-place Editor with Textbox

By default, Essential JS2 React TextBox component is rendered in In-place Editor with [`type`](../api/inplace-editor/inputType/) property sets as Text.

* Import the In-place Editor component to your `src/App.tsx` file using following code.

{% compileJsx= true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public model = { placeholder: 'Enter employee name' };
  public render() {
    return (
     <InPlaceEditorComponent id='element' model={this.model} type='Text' value='Andrew'/>
    );
  }
}

export default App;

```

{% endtab %}

## Configuring DropDownList

You can render Essential JS 2 React DropDownList by changing [`type`](../api/inplace-editor/inputType/) property as [`DropDownList`](../api/drop-down-list) and configure its properties and methods using `model` property.

In the below sample, [`type`](../api/inplace-editor/inputType/) and [`model`](../api/inplace-editor#model) values are configured to render the [`DropDownList`](../api/drop-down-list) component.

{% compileJsx= true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public genderData = ['Male', 'Female'];
  public model = { placeholder: 'Select gender', dataSource: this.genderData };
  public render() {
    return (
     <InPlaceEditorComponent id='element' model={this.model} type='DropDownList' mode='Inline'/>
    );
  }
}

export default App;

```

{% endtab %}

## Integrate DatePicker

You can render Essential JS2 [DatePicker](../api/datepicker/) by changing [`type`](../api/inplace-editor/inputType/) property as [`Date`](../api/inplace-editor/inputType/) and also configure its properties and methods using [`model`](../api/inplace-editor#model) property.

In the below sample, [`type`](../api/inplace-editor/inputType/) and [`model`](../api/inplace-editor#model) values are configured to render the [DatePicker](../api/datepicker) component.

{% compileJsx= true %}

```typescript

import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public model = { showTodayButton: true };
  public value = new Date('04/12/2018');
  public render() {
    return (
     <InPlaceEditorComponent id='element' model={this.model} type='Date' value={this.value}/>
    );
  }
}

export default App;

```

{% endtab %}

## Run the application

* Run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="in-place-editor/getting-started-form", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public genderData = ['Male', 'Female'];
  public dateModel = { showTodayButton: true, placeholder: 'Select date of birth' };
  public dateValue = new Date('04/12/2018');
  public elementModel = { placeholder: 'Enter your name' };
  public genderModel = {  dataSource: this.genderData, placeholder: 'Select gender' };
  public render() {
    return (
      <div id='container'>
      <div className="control-group">
           <div className="e-heading">
            <h3> Modify Basic Details </h3>
            </div>
            <table>
                <tr>
                    <td>Name</td>
                    <td className='left'>
                        <InPlaceEditorComponent id='element' mode='Inline' value='Andrew' model={this.elementModel}/>
                    </td>
                </tr>
                <tr>
                    <td>Date of Birth</td>
                    <td className='left'>
                        <InPlaceEditorComponent id='dateofbirth' type="Date" mode='Inline' value={this.dateValue} model={this.dateModel}/>
                    </td>
                </tr>
                <tr>
                    <td>Gender</td>
                    <td className='left'>
                        <InPlaceEditorComponent id='gender' type="DropDownList" mode='Inline' value='Male' model={this.genderModel}/>
                    </td>
                </tr>
            </table>
        </div>
        </div>
    );
  }
}

export default App;
```

{% endtab %}

## Submitting data to the server (save)

You can submit editor value to server by configuring the [`url`](../api/inplace-editor#url), [`adaptor`](../api/inplace-editor/adaptorType/) and [`primaryKey`](../api/inplace-editor#primarykey) property.

| Property   | Usage                                           |
|------------|---------------------------------------------------------|
| **`url`**        | Gets the url for server submit action.        |
| **`adaptor`**    | Specifies the adaptor type that are used by DataManager to communicate with DataSource.  |
| **`primarykey`** | Defines the unique primary key of editable field which can be used for saving data in data-base. |

> [`primaryKey`](../api/inplace-editor#primarykey) property is mandatory. If it's not set, edited data are not sent to the server.

## Refresh with modified value

The edited data is submitted to the server and you can see the new values getting reflected in the In-place Editor.

{% tab template="in-place-editor/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{}, {}> {
public frameWorkList = ['Andrew Fuller', 'Janet Leverling', 'Laura Callahan', 'Margaret Hamilt', 'Michael Suyama', 'Nancy Davloio', 'Robert King'];
public model = {  dataSource: this.frameWorkList, placeholder: 'Select employee', popupHeight: '200px' };
public url = "https://ej2services.syncfusion.com/development/web-services/api/Editor/UpdateData";

public actionSuccess(e: any) {
    const newEle = document.getElementById('newValue') as HTMLElement;
    const oldEle = document.getElementById('oldValue') as HTMLElement;
    oldEle.textContent = newEle.textContent;
    newEle.textContent = e.value;
}

public render() {
  return (
  <div id='container'>
      <div className="control-group">
            Best Employee of the year: <InPlaceEditorComponent id='element' type="DropDownList" mode='Inline' value='Andrew Fuller' name='Employee' url={this.url} primaryKey="Employee" adaptor="UrlAdaptor" model={this.model} actionSuccess={this.actionSuccess} />
       </div>
       <table style={{'margin':'auto','width':'50%'}}>
           <tr>
              <td style={{textAlign: 'left'}}>
                 Old Value :
              </td>
              <td id="oldValue" style={{textAlign: 'left'}}/>
           </tr>
           <tr>
               <td style={{textAlign: 'left'}}>
                    New Value :
               </td>
               <td id="newValue" style={{textAlign: 'left'}}>
                    Andrew Fuller
               </td>
            </tr>
         </table>
   </div>
  );
}
}
export default App;
```

{% endtab %}

## See Also

* [Types of rendering the editor](./integration/)
