# Badge Customization

## Colour customization

Even though badges come with `8 predefined colors`, you can also customize the colour of the badge as desired.

{% tab template="badge/color", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <h1>Color Customization <span className="e-badge e-badge-primary e-badge-pill green">New</span></h1>
            <h1>Color Customization <span className="e-badge e-badge-primary e-badge-pill bue">New</span></h1>
            <h1>Color Customization <span className="e-badge e-badge-primary e-badge-pill purple">New</span></h1>
            <h1>Color Customization <span className="e-badge e-badge-primary e-badge-pill gradient">New</span></h1>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

## Customize badge size

Badges are designed to change its size based on the content. To change the size of a badge, adjust the
`font size` of the badge.

{% tab template="badge/size", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
            <div>
                <h1>Badge Component <span className="e-badge e-badge-primary size_1">New</span></h1>
                <h1>Badge Component <span className="e-badge e-badge-primary size_2">New</span></h1>
                <h1>Badge Component <span className="e-badge e-badge-primary size_3">New</span></h1>
            </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

## Custom position

Even though the badges support the conventional `top` and `bottom` positions, the position of the badges
can be changed as desired.
This can be done by adding a custom class to the badge element to override the default position applied from the source.

{% tab template="badge/custom-position", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
            <div>
                <div className="block">
                    <div className="badge-block">
                        <div className="firefox svg_icons"></div>
                        {/* Warning Colored Notification Badge*/}
                        <span className="e-badge e-badge-warning e-badge-notification e-badge-overlap leftTop">99+</span>
                    </div>

                    <div className="badge-block">
                        <div className="facebook svg_icons"></div>
                        {/* Danger Colored Notification Badge*/}
                        <span className="e-badge e-badge-danger e-badge-notification e-badge-overlap leftTop">99+</span>
                    </div>

                    <div className="badge-block">
                        <div className="skype svg_icons"></div>
                        {/* Secondary Colored Notification Badge*/}
                        <span className="e-badge e-badge-secondary e-badge-notification e-badge-overlap leftTop">18</span>
                    </div>
                </div>
                <div className="badge-block">
                    <div className="badge-block">
                        <div className="firefox svg_icons"></div>
                        {/* Warning Colored Notification Badge*/}
                        <span className="e-badge e-badge-warning e-badge-notification e-badge-overlap leftBottom">99+</span>
                    </div>

                    <div className="badge-block">
                        <div className="facebook svg_icons"></div>
                        {/* Danger Colored Notification Badge*/}
                        <span className="e-badge e-badge-danger e-badge-notification e-badge-overlap leftBottom">99+</span>
                    </div>

                    <div className="badge-block">
                        <div className="skype svg_icons"></div>
                        {/* Secondary Colored Notification Badge*/}
                        <span className="e-badge e-badge-secondary e-badge-notification e-badge-overlap leftBottom">18</span>
                    </div>
                </div>
            </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}
