---
title: "Set the Disabled State"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Set the Disabled State

Disable the TextBox by adding the `e-disabled` to the input parent element and set `disabled` attribute to the input element.

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
export default class App extends React.Component<{}, {}> {
    public render() {
        return (
            <div>
                <input className="e-input" type="text" placeholder="Enter Name" disabled={true}/>
                <div className="e-float-input e-disabled">
                    <input type='text' required = {true}  disabled = {true}/>
                    <span className="e-float-line"/>
                    <label className="e-float-text">Enter Name</label>
                </div>
            </div>
        )
    }
};
ReactDOM.render(<App />, document.getElementById('input-container'));

```

{% endtab %}