# Getting Started

This section explains the steps required to create the ProgressBar control using React and configure its properties.

## Dependencies

Below is the list of minimum dependencies required to use the progress bar component.

```javascript
    |-- @syncfusion/ej2-react-progressbar
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-svg-base
```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-react-progressbar --save
```

## Add Progressbar to the Project

Now, you can start adding Progress bar component in the application.
For getting started, add the Progress bar component in `src/App.tsx` file using following code.

```typescript
import {ProgressBarComponent} from '@syncfusion/ej2-react-progressbar';
import * as React from 'react';

class App extends React.Component {
render() {
  return ( <ProgressBarComponent/>);
 }
}
export default App;

```

## Run the application

Now, we might create a simple progress bar sample as shown below.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="linear"
                        type='Linear'
                        height='60'
                        value={40}
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```