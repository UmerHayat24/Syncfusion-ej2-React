---
title: "React functional component"
component: "NumericTextBox"
description: "This section explains how to use react hook methods in the functional component with Numeric TextBox"
---

# Render the Numeric textbox component in the functional component with react hooks methods

This section explains how to render the numeric textbox component in the functional component with react hooks methods. Please find the list of basic hook methods in the following table.

| Hooks | Description |
| ------------- | ------------- |
| `useState` | useState is a Hook that allows you to define the state in the functional components. If you pass the initial state to this function, then it will return a state variable with value and function to update this state value. Here, useState is used to store the value of total amount field. |
| `useEffect` | useEffect is a Hook that allows you to execute code after rendering and re-rendering the component. Here, defined the set of rules for the price of the item, number of items, and total amount fields and initiated the form validation to those fields. |
| `useRef` | useRef is a Hook function that allows to directly create a reference to the DOM element in the functional component. Here, assigned the price of the item field reference for updating the predefined price on initial loading. |
| `useReducer` | useReducer is a Hook function that accepts a reducer function and an initial state as argument. It returns a state value and another function to dispatch an action. Here, dispatched the update action to update the price and count state values. |

The following example shows how to render a simple numeric textbox with react hooks.

{% tab template="numeric-textbox/react-hooks", sourceFiles="app/App.tsx, style.css" %}

```typescript
import { useState, useEffect, useRef, useReducer } from 'react';
import * as React from 'react';
import { FormValidator } from '@syncfusion/ej2-inputs';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';

let formObject;
function App() {
  const [totalAmount, setTotalAmount] = useState('');
  const initialState = { price: '', count: '' };
  const priceValueRef = useRef(null);
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
    setTotalAmount(event.value);
  };

  const update = (field) => (event) => {
    //update action is dispatched and triggered state changes
    dispatch({ type: 'update', field, value: event.value });
  };

  useEffect(() => {
    priceValueRef.current.value = 100;
    const options = {
      // validation rules
      rules: {
        price: {
          required: [true, '* Please enter your price'],
        },
        count: {
          required: [true, '* Please enter your count'],
        },
        amount: {
          required: [true, '* Please enter your amount'],
        },
      },
    };
    // Initialize the form validator
    formObject = new FormValidator('#form1', options);
  }, []);

  return (
    <div>
      <div className="control_wrapper" id="control_wrapper">
        <h3 className="form-title">Purchase</h3>
        <div className="control_wrapper textbox-form">
          <form id="form1" method="post">
            <div className="form-group">
              <NumericTextBoxComponent
                ref={priceValueRef}
                name="price"
                value={state.price}
                change={update('price')}
                placeholder="Price of the item"
                floatLabelType="Auto"
                data-msg-containerid="errroForPrice"
              />
              <div id="errroForPrice" />
            </div>
            <div className="form-group">
              <NumericTextBoxComponent
                name="count"
                value={state.count}
                change={update('count')}
                placeholder="Number of items"
                floatLabelType="Auto"
                data-msg-containerid="errroForCount"
              />
              <div id="errroForCount" />
            </div>
            <div className="form-group">
              <NumericTextBoxComponent
                name="amount"
                value={totalAmount}
                change={changeHandler}
                multiline="true"
                placeholder="Total amount"
                floatLabelType="Auto"
                data-msg-containerid="errroForAmount"
              />
              <div id="errroForAmount" />
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