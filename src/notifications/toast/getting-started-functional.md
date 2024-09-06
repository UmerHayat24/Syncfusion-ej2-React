---
title: "React Toast Getting Started"
component: "Toast"
description: "This section explains how to create the Essential JS 2 Toast control in React application with its basic features."
---

# Getting Started

This section briefly explains you the steps required to create a simple Toast and demonstrate the basic usage of the Toast component.

## Dependencies

The following list of dependencies are required to use the Toast component in your application.

```javascript
|-- @syncfusion/ej2-react-notifications
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-notifications
      |-- @syncfusion/ej2-base
      |-- @syncfusion/ej2-buttons
      |-- @syncfusion/ej2-react-buttons
      |-- @syncfusion/ej2-popups
```

## Installation and configuration

You can use [`Create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

<div class='tsx'>

```bash
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

Install the below required dependency package in order to use the `Toast` component in your application.

```bash
npm install @syncfusion/ej2-react-notifications –save
```

The above package installs [Toast dependencies](#dependencies) which are required
 to render the Toast component in React environment.

* Toast CSS files are available in the `ej2-react-notifications` package folder.
Import the Toast component's required CSS references as follows in `src/App.css`.

```css
@import '../../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-react-buttons/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-react-popups/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-react-notifications/styles/material.css';
```

## Initialize the Toast with message

The Toast message can be rendered by defining an `title` or `content`.

* Import the Toast component to your `src/App.tsx` file using following code.

```typescript
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";
import { useRef } from 'react';

function App() {
  const toastInstance = useRef<ToastComponent>(null);

  function toastCreated() {
    toastInstance.current.show();
  }

  return (
    <ToastComponent
      ref={toastInstance}
      title="Sample Toast Title"
      content="Sample Toast Content"
      created={toastCreated}
    />
  );
};

export default App;

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

* Run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="toast/toast", sourceFiles="app/App.tsx", isDefaultActive=true, compileJsx=true %}

```typescript
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";
import * as ReactDOM from 'react-dom';
import { useRef } from 'react';

function App() {
  const toastInstance = useRef<ToastComponent>(null);

  function toastCreated() {
    toastInstance.current.show();
  }

  return (
    <div>
      <ToastComponent
        ref={toastInstance}
        title="Matt sent you a friend request"
        content="Hey, wanna dress up as wizards and ride our hoverboards?"
        created={toastCreated}
      />
    </div>
  );
}

export default App;

```

{% endtab %}

## Initialize the Toast with target

By default toast can be rendered in document body, we can change the target position for toast rendering using `target` property.

> In the above sample code, `#element` is the `id` of the HTML element in a page to which the Toast is initialized.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";
import { useRef } from 'react';

function App() {
  const toastInstance = useRef<ToastComponent>(null);

  function toastCreated() {
    toastInstance.current.show();
  }

  return (
    <div id='#toast_target' />
      <ToastComponent
        id="toast_target"
        ref={toastInstance}
        title="Sample Toast Title"
        content="Sample Toast Content"
        created={toastCreated}
      />
    </div>
  );
}

export default App;

```

{% endtab %}

## See Also

* [Render different types of toast](./how-to/show-different-types-of-toast/)