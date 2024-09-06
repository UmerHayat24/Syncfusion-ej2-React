---
title: "Avatar Types and Styles"
component: "Avatar"
description: "Avatar, a CSS component supports many types of media formats used like image, SVG, initials, font icon & word for various application scenarios."
---

# Types and Styles

This section explains different types of avatar.

## Avatar size

The Essential JS 2 Avatar has the following predefined sizes that can be used with the `.e-avatar` class to change the appearance of the avatar.

| Class Name         | Description
| :-------------:    |:-------------:
| e-avatar-xlarge    | Displays xlarge size avatar.
| e-avatar-large     | Displays apply large size avatar.
| e-avatar           | Displays apply default size avatar.
| e-avatar-small     | Displays apply small size avatar.
| e-avatar-xsmall    | Displays apply xsmall size avatar.

{% tab template="avatar/size", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true%}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <span className="e-avatar e-avatar-xlarge"></span>
            <span className="e-avatar e-avatar-large"></span>
            <span className="e-avatar"></span>
            <span className="e-avatar e-avatar-small"></span>
            <span className="e-avatar e-avatar-xsmall"></span>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## Avatar types

The types of Essential JS 2 avatar are:

* Default
* Circle

### Default

The default style of the avatar is rectangular shape with rounded corners, which can be applied from adding the modifier
class `.e-avatar` to the target element.

{% tab template="avatar/default", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true%}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <span className="e-avatar e-avatar-xlarge">RT</span>
            <span className="e-avatar e-avatar-large">RT</span>
            <span className="e-avatar">RT</span>
            <span className="e-avatar e-avatar-small">RT</span>
            <span className="e-avatar e-avatar-xsmall">RT</span>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

### Circle

The circle avatar style can be applied by adding the modifier class `.e-avatar-circle` to the target element.

{% tab template="avatar/circle", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true%}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <span className="e-avatar e-avatar-xlarge e-avatar-circle">SJ</span>
            <span className="e-avatar e-avatar-large e-avatar-circle">SJ</span>
            <span className="e-avatar e-avatar-circle">SJ</span>
            <span className="e-avatar e-avatar-small e-avatar-circle">SJ</span>
            <span className="e-avatar e-avatar-xsmall e-avatar-circle">SJ</span>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}
