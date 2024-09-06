---
title: "Types Of Badge"
component: "Badge"
description: "React pure CSS Badge component has eight (8) types of badges, namely circle, pill, link, notification, overlap, dot, and position."
---

# Types and Styles

This section explains different styles and types of the badges.

## Badge styles

The Essential JS 2 Badge has the following predefined styles that can be used with `.e-badge` class to change
the appearance of a badge.

| Class Name        | Description
| :-------------    |:-------------
| e-badge-primary   | Represents a primary notification.
| e-badge-secondary | Represents a secondary notification.
| e-badge-success   | Represents a positive notification.
| e-badge-danger    | Represents a negative notification.
| e-badge-warning   | Represents notification with caution.
| e-badge-info      | Represents an informative notification.
| e-badge-light     | Represents notification in light variant.
| e-badge-dark      | Represents notification in dark variant.

{% tab template="badge/types", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div className="sample_container">
            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <div>
                            <span className="e-badge e-badge-primary">Primary</span>
                        </div>
                    </div>
                    <div className="e-card-content">
                        <div>
                            <code>.e-badge-primary</code>
                        </div>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-secondary">Secondary</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-secondary</code>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-success">Success</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-success</code>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-danger">Danger</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-danger</code>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-warning">Warning</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-warning</code>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-info">Info</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-info</code>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-light">Light</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-light</code>
                    </div>
                </div>
            </div>

            <div className="block">
                <div className="e-card e-badge-showcase">
                    <div className="e-card-content">
                        <span className="e-badge e-badge-dark">Dark</span>
                    </div>
                    <div className="e-card-content">
                        <code>.e-badge-dark</code>
                    </div>
                </div>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

## Badge types

The types of Essential JS 2 badges are as follows:

* Circle
* Pill
* Link
* Notification
* Overlap
* Dot
* Position

### Circle

The circle badge style can be applied by adding the modifier class `.e-badge-circle` to the target element.

{% tab template="badge/circle", isDefaultActive=true, compileJsx=true   %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="badge-block">
                <div className="skype svg_icons"></div>
                <span className="e-badge e-badge-success e-badge-overlap e-badge-notification e-badge-circle">18</span>
            </div>

            <div className="badge-block">
                <div className="twitter svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-notification e-badge-circle">9</span>
            </div>

            <div className="badge-block">
                <div className="facebook svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-notification e-badge-circle">2</span>
            </div>

            <div className="badge-block">
                <div className="firefox svg_icons"></div>
                <span className="e-badge e-badge-danger e-badge-overlap e-badge-notification e-badge-circle">35</span>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

### Pill

The pill badge style can be applied by adding the modifier class `.e-badge-pill` to the target element.

{% tab template="badge/pill", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <h1>Badge Component <span className="e-badge e-badge-primary e-badge-pill">New</span></h1>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

### Link

When badge modifier classes are applied to the anchor tag, the badge’s appearance will change from normal
state to hover state on mouseover.

{% tab template="badge/link", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div className="badge-block">
            <a href="#" className="e-badge e-badge-primary">Link Badge</a>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

### Notification

The notification badge style can be applied by adding the modifier class `.e-badge-notification` to the
target element. Notification badges are used when a content or a context needs special attention. While using
the notification badge, set the parent element to `position: relative`.

{% tab template="badge/notification", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="badge-block">
                <div className="skype svg_icons"></div>
                <span className="e-badge e-badge-success e-badge-overlap e-badge-notification">99+</span>
            </div>

            <div className="badge-block">
                <div className="twitter svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-notification">27</span>
            </div>

            <div className="badge-block">
                <div className="facebook svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-notification">2</span>
            </div>

            <div className="badge-block">
                <div className="firefox svg_icons"></div>
                <span className="e-badge e-badge-danger e-badge-overlap e-badge-notification">35</span>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

### Dot

Dot can be applied by adding the modifier class `.e-badge-dot` to the target element. Dot badges are similar to
notification badges, but in a minimalistic way. While using the dot badge, set the parent element to
`position:relative` .

{% tab template="badge/dot", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="badge-block">
                <div className="skype svg_icons"></div>
                <span className="e-badge e-badge-success e-badge-overlap e-badge-dot"></span>
            </div>

            <div className="badge-block">
                <div className="twitter svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-dot"></span>
            </div>

            <div className="badge-block">
                <div className="facebook svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-dot"></span>
            </div>

            <div className="badge-block">
                <div className="firefox svg_icons"></div>
                <span className="e-badge e-badge-danger e-badge-overlap e-badge-dot"></span>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

### Overlap

The overlap badge can be used with `notification` or `dot` badge, which overlaps with the target element by
adding the modifier class `.e-badge-overlap`. While using the overlap badge, set the parent element to
`position: relative`.

{% tab template="badge/overlap", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="badge-block">
                <div className="skype svg_icons"></div>
                <span className="e-badge e-badge-success e-badge-overlap e-badge-notification">99+</span>
            </div>

            <div className="badge-block">
                <div className="twitter svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-notification">27</span>
            </div>

            <div className="badge-block">
                <div className="facebook svg_icons"></div>
                <span className="e-badge e-badge-info e-badge-overlap e-badge-notification">2</span>
            </div>

            <div className="badge-block">
                <div className="firefox svg_icons"></div>
                <span className="e-badge e-badge-danger e-badge-overlap e-badge-notification">35</span>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

### Position

The default position of the `notification` or `dot` badge is top. But, the position can be changed to `bottom`
using the modifier class `.e-badge-bottom`. For example, the bottom class modifier is used with dot badge to display
the status in the avatar as shown in the following sample.

{% tab template="badge/position", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="badge-block">
                <div className="firefox svg_icons"></div>
                {/* Success Colored Bottom Dot Badge */}
                <span className="e-badge e-badge-success e-badge-overlap e-badge-dot e-badge-bottom"></span>
            </div>

            <div className="badge-block">
                <div className="skype svg_icons"></div>
                {/* Info Colored Bottom Dot Badge */}
                <span className="e-badge e-badge-info e-badge-overlap e-badge-dot e-badge-bottom"></span>
            </div>

            <div className="badge-block">
                <div className="facebook svg_icons"></div>
                {/* Info Colored Dot Badge */}
                <span className="e-badge e-badge-info e-badge-overlap e-badge-dot"></span>
            </div>

            <div className="badge-block">
                <div className="twitter svg_icons"></div>
                {/* Danger Colored Dot Badge */}
                <span className="e-badge e-badge-danger e-badge-overlap e-badge-dot e-badge-bottom"></span>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}
