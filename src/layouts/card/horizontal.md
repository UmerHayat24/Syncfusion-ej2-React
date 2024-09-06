---
title: "Horizontal Card"
component: "Card"
description: "This section explains how to align the Essential JS 2 cards vertically and differentiate from horizontal layout."
---

# Horizontal Card

By default, all the card elements are aligned vertically one after the other as in the DOM.
 You can achieve the element to align horizontally as well by adding the class `e-card-horizontal` in the root card element.

## Stacked cards

* An horizontally aligned card can push a specific column to align vertical using `e-card-stacked` class.
 This will align the stacked section vertically aligned differentiating from horizontal layout.

Class   | Description
------------ | -------------
`e-card-horizontal` | To align card elements horizontally.
`e-card-stacked` | To align elements vertically within the horizontal layout.

```html
        <div className="e-card e-card-horizontal">
            <img src="code1.png" alt="Sample">   --> Aligned in horizontal
            <div className="e-card-stacked">         --> Aligned in horizontal
               // Inside the element all are aligned vertical directions
            </div>
        </div>
```

{% tab template="card/card_horizontal", isDefaultActive=true, compileJsx=true  %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <div style={{ margin: `50px`, display: `flex`, flexDirection: `row`, justifyContent: `center` }}>
        <div className="e-card e-card-horizontal" style={{ width: `400px` }}>
            <img src="./Code.png" alt="Sample" style={{ height: `180px` }}/>
            <div className="e-card-stacked">
                <div className="e-card-header">
                    <div className="e-card-header-caption">
                        <div className="e-card-header-title">Philips Trimmer</div>
                    </div>
                </div>
                <div className="e-card-content">
                    Powered by the innovative DuraPower Technology which optimizes power consumption, Philips trimmers are designed to last longer
                    than 4 ordinary trimmers.
                </div>
            </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));
```

{% endtab %}
