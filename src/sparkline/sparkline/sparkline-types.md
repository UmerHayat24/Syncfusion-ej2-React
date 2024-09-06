# Sparkline Types

Different types of shapes can be used to represent the sparkline. You can change the sparkline type by setting the type property. Sparkline supports the following types:

* Line
* Column
* Win-Loss
* Pie
* Area

The following code sample shows different types of sparklines.

<!-- markdownlint-disable MD036 -->

**Line**

The [`Line`] type is used to render the sparkline series as line.

{% tab template= "sparkline/sparkline-types", compileJsx=true, sourceFiles="app/**/*.tsx",  isDefaultActive=true ,  es5Template="es5Line" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='100px' width='70%'
    dataSource= { [
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ] }
    // Assign the dataSource values to series of sparkline 'xName and yName'
    xName= 'xval' yName= 'yval'
    // Assign 'Line' as type of the sparkline
    type= 'Line' >
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

**Column**

The [`Column`] type is used to render the sparkline series as column.

{% tab template= "sparkline/sparkline-types", compileJsx=true, sourceFiles="app/**/*.tsx",  isDefaultActive=true , es5Template="es5Column" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='150px' width='200px'
    dataSource= { [
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ] }
    // Assign the dataSource values to series of sparkline 'xName and yName'
    xName= 'xval' yName= 'yval'
    // Assign 'Column' as type of the sparkline
    type= 'Column' >
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

**Pie**

The [`Pie`] type is used to render the sparkline series as pie.

{% tab template= "sparkline/sparkline-types", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template="es5Pie" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='70%'
    dataSource= { [
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ] }
    // Assign the dataSource values to series of sparkline 'xName and yName'
    xName= 'xval' yName= 'yval'
    // Assign 'Pie' as type of the sparkline
    type= 'Pie' >
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

**Win Loss**

The [`WinLoss`] type is used to render the sparkline series as Win Loss.

{% tab template= "sparkline/sparkline-types", compileJsx=true, sourceFiles="app/**/*.tsx",  isDefaultActive=true ,  es5Template="es5WinLoss" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='100px' width='70%'
    dataSource= { [
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: -20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: -21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: -22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ] }
    // Assign the dataSource values to series of sparkline 'xName and yName'
    xName= 'xval' yName= 'yval'
    // Assign 'WinLoss' as type of the sparkline
    type= 'WinLoss' >
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

**Area**

The [`Area`] type is used to render the sparkline series as area.

{% tab template= "sparkline/sparkline-types", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Area" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='100px' width='70%'
    dataSource= { [
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ] }
    // Assign the dataSource values to series of sparkline 'xName and yName'
    xName= 'xval' yName= 'yval'
    // Assign 'Area' as type of the sparkline
    type= 'Area' >
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}