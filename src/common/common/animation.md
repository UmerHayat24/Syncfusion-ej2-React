# Animation

The **Animation** library is used to perform animation effects on HTML elements by running a sequence of frames.

## Animate HTML Element

The [`animate`](https://ej2.syncfusion.com/documentation/api/base/animation#animate) method of `Animation` library
can be used to animate the HTML elements. This method can also take additional
[`AnimationModel`](https://ej2.syncfusion.com/documentation/api/base/animationModel). Refer the following code snippet
to animate a multiple DOM element

{% tab template="common/animation-multiple", compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { Animation } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
    public componentDidMount(): void {
      let animation: Animation = new Animation({ name: 'FadeIn', duration: 5000 });
      animation.animate(this.element1, { name: 'FadeOut' });
      animation.animate(this.element2, { name: 'ZoomOut' });
    }

    render() {
        return (
            <div id="container">
             <div id="element1" ref={(ele) => { this.element1 = ele; }}></div>
             <div id="element2" ref={(ele) => { this.element2 = ele; }}></div>
            </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));

```

{% endtab %}