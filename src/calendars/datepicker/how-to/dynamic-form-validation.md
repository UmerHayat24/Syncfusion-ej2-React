---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Dynamic form validation

Dynamic form can be very useful and more economical to create the forms based on JSON data and without need for adding/changing any code.

* For the dynamic forms, we can create a new React tsx called `dynamic-form.tsx` which is responsible for rendering a dynamic form based on the Json data.

The following example demonstrates how to create the sign up form dynamically.

{% tab template="datepicker/dynamic-form-validator", sourceFiles="app/**/*.tsx", iframeHeight="475px" %}

```typescript

import { data } from './data';
import DynamicForm from './dynamicform';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    public data : any;

    constructor(props: any) {
        super(props);
        this.data = data;
    }

    public render() {
        return (
            <div className = "wrap">
                <div className= "outerbox">
                    <div className = "formValue">
                        <DynamicForm dataObject = {data} />
                    </div>
                </div>
            </div>
        );
     }
 }

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}