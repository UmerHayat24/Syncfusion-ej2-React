# Drag and Drop

Drag and Drop is supported through two libraries. Those are
[`Draggable`](https://ej2.syncfusion.com/documentation/api/base/draggable) and [`Droppable`](https://ej2.syncfusion.com/documentation/api/base/droppable). Draggable makes DOM to be
dragged using mouse or touch gestures and Droppable mark required DOM as droppable zone.

## Initializing draggable

You can make any element draggable by passing the element to Draggable constructor. Refer
the following code snippet to enable draggable for the DOM element

 {% tab template="common/draggable-default" compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { Draggable } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
    public componentDidMount(): void {
        let draggable:Draggable = new Draggable(document.getElementById('element'),{clone: false});
        }

  render() {
      return (
          <div id='container'>
          <div id='element'><p>Draggable Element</p></div>
          </div>
      );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));

```

 {% endtab %}

## Creating droppable zone

You can convert any DOM element as a droppable zone, which accepts the draggable elements. Refer the
following code snippet to enable droppable zone.

{% tab template="common/droppable-default" compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { Droppable } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
    public componentDidMount(): void {
        let droppable: Droppable = new Droppable(document.getElementById('droppable'));
    }

  render() {
      return (
          <div id='container'>
          <div id='droppable'><p>Droppable Element</p></div>
          </div>
      );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));

```

 {% endtab %}

## Defining Drop Action

To define a drop action set [`drop`](https://ej2.syncfusion.com/documentation/api/base/droppable#drop) callback function during droppable object
creation. You can get details of dropped element through dropped element property in event argument.
Refer the following  code snippet to use basic drag and drop action

{% tab template="common/drag-drop-action" compileJsx=true%}

 ```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { Draggable, Droppable, DropEventArgs } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
    public componentDidMount(): void {
        let draggable:Draggable = new Draggable(document.getElementById('draggable'),{clone: false});
        let droppable: Droppable = new Droppable(document.getElementById('droppable'), {
            drop: (e: DropEventArgs) => {
                e.droppedElement.querySelector('#drag').textContent = 'Dropped';
            }
        });
    }

  render() {
      return (
          <div id='container'>
           <div id='droppable'><p>Droppable Target </p></div>
           <div id='draggable'><p id='drag'>Draggable Element </p></div>
          </div>
      );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));

 ```

 {% endtab %}