---
title: "React functional component"
component: "FormValidator"
description: "This section explains how to use react hook methods in the functional component with form validator"
---

# React functional component

## Use react hooks in the functional component with form validator

This section explains how to use react hook methods in the functional component with form validator. Please find the list of basic hook methods in the following table.

| Hooks | Description |
| ------------- | ------------- |
| `useState` | useState is a Hook that allows you to define the state in the functional components. If you pass the initial state to this function, then it will return a state variable with value and function to update this state value. Here, useState is used to store the value of date of birth field. |
| `useEffect` | useEffect is a Hook that allows you to execute code after rendering and re-rendering the component. Here, defined the set of rules for the email, password, and date of birth fields and initiated the form validation to those fields. |
| `useRef` | useRef is a Hook function that allows to directly create a reference to the DOM element in the functional component. Here, assigned the username field reference for focusing the field on initial loading. |
| `useReducer` | useReducer is a Hook function that accepts a reducer function and an initial state as argument. It returns a state value and another function to dispatch an action. Here, dispatched the update action to update the email and password state values. |

The following example shows how to render a simple validation form with react hooks.

{% tab template="form-validator/react-hooks", sourceFiles="app/App.tsx, style.css" %}

```typescript
import { useState, useEffect, useRef, useReducer } from 'react';
import * as React from "react";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { FormValidator } from '@syncfusion/ej2-inputs';
import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';

let formObject;
function App() {
  const userNameRef = useRef(null);
  const [dateOfBirth, setDateOfBirth] = useState('');
  const initialState = { email: '', password: '' };
  const reducer = (state, action) => {
    switch (action.type) {
      case 'update':
        return { ...state, [action.field]: action.value };

      default:
        return initialState;
    }
  };
  const [state, dispatch] = useReducer(reducer, initialState);

  const dateChangeHandler = (event) => {
    setDateOfBirth(event.value);
  };

  const update = (field) => (event) => {
    //update action is dispatched to update the email and password state value
    dispatch({ type: 'update', field, value: event.value });
  };

  useEffect(() => {
    userNameRef.current.focusIn();
    const options = {
      // validation rules
      rules: {
        email: {
          required: [true, '* Please enter your email'],
        },
        password: {
          required: [true, '* Please enter your password'],
        },
        date: {
          required: [true, '* Please enter your date of birth'],
        },
      },
    };
    // Initialize the form validator
    formObject = new FormValidator('#form1', options);
  }, []);

  const onSubmit = () => {
    formObject.validate();
    if (formObject.validate()) {
      (formObject as any).element.reset();
    }
  };

  return (
    <div>
      <div className="control_wrapper" id="control_wrapper">
        <h3 className="form-title">User Login</h3>
        <div className="control_wrapper textbox-form">
          <form id="form1" method="post">
            <div className="form-group">
              <TextBoxComponent
                ref={userNameRef}
                type="email"
                name="email"
                value={state.email}
                change={update('email')}
                placeholder="Username"
                floatLabelType="Auto"
                data-msg-containerid="errroForEmail"
              />
              <div id="errroForEmail" />
            </div>
            <div className="form-group">
              <TextBoxComponent
                type="password"
                name="password"
                value={state.password}
                change={update('password')}
                placeholder="Password"
                floatLabelType="Auto"
                data-msg-containerid="errroForPassword"
              />
              <div id="errroForPassword" />
            </div>
            <div className="form-group">
              <DatePickerComponent
                name="date"
                value={dateOfBirth}
                change={dateChangeHandler}
                placeholder="Date of Birth"
                floatLabelType="Auto"
                data-msg-containerid="errroForDateOfBirth"
              />
              <div id="errroForDateOfBirth" />
            </div>
          </form>
          <div className="submitBtn">
            <ButtonComponent onClick={onSubmit}>Submit</ButtonComponent>
          </div>
        </div>
        <br />
        <br />
      </div>
    </div>
  );
}
export default App;
```

{% endtab %}