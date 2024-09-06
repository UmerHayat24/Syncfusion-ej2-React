---
title: "React functional component"
component: "MaskedTextBox"
description: "This section explains how to use react hook methods in the functional component with Masked TextBox"
---

# Render the Masked textbox component in the functional component with react hooks methods

This section explains how to render the masked textbox component in the functional component with react hooks methods. Please find the list of basic hook methods in the following table.

| Hooks | Description |
| ------------- | ------------- |
| `useState` | useState is a Hook that allows you to define the state in the functional components. If you pass the initial state to this function, then it will return a state variable with value and function to update this state value. Here, useState is used to store the value of product key field. |
| `useEffect` | useEffect is a Hook that allows you to execute code after rendering and re-rendering the component. Here, focusing the product key field on initial loading. |
| `useRef` | useRef is a Hook function that allows to directly create a reference to the DOM element in the functional component. Here, assigned the product key field reference for focusing the field on initial loading. |
| `useReducer` | useReducer is a Hook function that accepts a reducer function and an initial state as argument. It returns a state value and another function to dispatch an action. Here, dispatched the update action to update the mobile number and postal code state values. |

The following example shows how to render a simple masked textbox with react hooks.

{% tab template="masked-textbox/react-hooks", sourceFiles="app/App.tsx, style.css" %}

```typescript
import { useState, useEffect, useRef, useReducer } from 'react';
import * as React from 'react';
import { MaskedTextBoxComponent } from '@syncfusion/ej2-react-inputs';

function App() {
  const [productKey, setProductKey] = useState('124-234-765-234');
  const initialState = { mobileNo: '', postalCode: '' };
  const productValueRef = useRef(null);
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
    setProductKey(event.value);
  };

  const update = (field) => (event) => {
    //update action is dispatched and triggered state changes
    dispatch({ type: 'update', field, value: event.value });
  };

  useEffect(() => {
    productValueRef.current.focusIn();
  }, []);

  return (
    <div>
      <div className="control_wrapper" id="control_wrapper">
        <h3 className="form-title">Purchase</h3>
        <div className="control_wrapper textbox-form">
          <form id="form1" method="post">
            <div className="form-group">
              <MaskedTextBoxComponent
                ref={productValueRef}
                name="product"
                mask={'000-000-000-000'}
                value={productKey}
                change={changeHandler}
                multiline="true"
                placeholder="Product key"
                floatLabelType="Always"
                data-msg-containerid="errroForAmount"
              />
              <div id="errroForAmount" />
            </div>
            <div className="form-group">
              <MaskedTextBoxComponent
                name="mobile"
                mask={'00-0000-0000'}
                value={state.mobileNo}
                change={update('mobileNo')}
                placeholder="Mobile Number"
                floatLabelType="Always"
                data-msg-containerid="errroForMobileNo"
              />
              <div id="errroForMobileNo" />
            </div>
            <div className="form-group">
              <MaskedTextBoxComponent
                name="postal"
                mask={'000-000'}
                value={state.postalCode}
                change={update('postalCode')}
                placeholder="Postal code"
                floatLabelType="Always"
                data-msg-containerid="errroForPostalCode"
              />
              <div id="errroForPostalCode" />
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