---
title: "React functional component"
component: "TextBox"
description: "This section explains how to use react hook methods in the functional component with TextBox"
---

# Render the textbox component in the functional component with react hooks methods

This section explains how to render the textbox component in the functional component with react hooks methods. Please find the list of basic hook methods in the following table.

| Hooks | Description |
| ------------- | ------------- |
| `useState` | useState is a Hook that allows you to define the state in the functional components. If you pass the initial state to this function, then it will return a state variable with value and function to update this state value. Here, useState is used to store the value of description field. |
| `useEffect` | useEffect is a Hook that allows you to execute code after rendering and re-rendering the component. Here, defined the set of rules for the name, and email fields and initiated the form validation to those fields. |
| `useRef` | useRef is a Hook function that allows to directly create a reference to the DOM element in the functional component. Here, assigned the name field reference for focusing the field on initial loading. |
| `useReducer` | useReducer is a Hook function that accepts a reducer function and an initial state as argument. It returns a state value and another function to dispatch an action. Here, dispatched the update action to update the name and email state values. |

The following example shows how to render a simple textbox component with react hooks.

{% tab template="textbox/react-hooks", sourceFiles="app/App.tsx, style.css" %}

```typescript
import { useState, useEffect, useRef, useReducer } from 'react';
import * as React from 'react';
import { FormValidator } from '@syncfusion/ej2-inputs';
import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';

let formObject;
function App() {
  const [description, setDescription] = useState('');
  const initialState = { name: '', email: '' };
  const userNameRef = useRef(null);
  const reducer = (state, action) => {
    switch (action.type) {
      case 'update':
        return { ...state, [action.field]: action.value };

      default:
        return initialState;
    }
  };
  const [state, dispatch] = useReducer(reducer, initialState);

  const changeHandler = (event) => {
    setDescription(event.value);
  };

  const update = (field) => (event) => {
    //update action is dispatched and triggered state changes
    dispatch({ type: 'update', field, value: event.value });
  };

  useEffect(() => {
    userNameRef.current.focusIn();
    const options = {
      // validation rules
      rules: {
        name: {
          required: [true, '* Please enter your name'],
        },
        email: {
          required: [true, '* Please enter your email'],
        },
        message: {
          required: [true, '* Please enter your message'],
        },
      },
    };
    // Initialize the form validator
    formObject = new FormValidator('#form1', options);
  }, []);

  return (
    <div>
      <div className="control_wrapper" id="control_wrapper">
        <h3 className="form-title">User Detail</h3>
        <div className="control_wrapper textbox-form">
          <form id="form1" method="post">
            <div className="form-group">
              <TextBoxComponent
                ref={userNameRef}
                name="name"
                value={state.name}
                change={update('name')}
                placeholder="Name"
                floatLabelType="Auto"
                data-msg-containerid="errroForName"
              />
              <div id="errroForName" />
            </div>
            <div className="form-group">
              <TextBoxComponent
                type="email"
                name="email"
                value={state.email}
                change={update('email')}
                placeholder="Email"
                floatLabelType="Auto"
                data-msg-containerid="errroForEmail"
              />
              <div id="errroForEmail" />
            </div>
            <div className="form-group">
              <TextBoxComponent
                name="message"
                value={description}
                change={changeHandler}
                multiline="true"
                placeholder="Description"
                floatLabelType="Auto"
                data-msg-containerid="errroForMessage"
              />
              <div id="errroForMessage" />
            </div>
          </form>
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