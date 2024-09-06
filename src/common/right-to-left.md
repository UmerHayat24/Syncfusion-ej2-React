# Right-To-Left

Right To Left (RTL) can be enabled to the Syncfusion React UI components by adding a `enableRtl` property as `true`. This will render all Syncfusion React components in right to left direction.

{% tab template="common/right-to-left", compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { enableRtl } from '@syncfusion/ej2-base'
// Enables Right to left alignment for all controls
enableRtl(true);

export default class App extends React.Component<{}, {}> {
  private data = ["Artwork", "Abstract", "Modern Painting", "Ceramics", "Animation Art", "Oil Painting"];

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id='list' dataSource={this.data} showHeader = 'true' headerTitle = 'Painting types' ></ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Enable RTL to individual component

To enable the RTL to an individual control, set the `enableRtl` property directly in its model options. For illustration, the `enableRtl` is added to the ListView control in following code snippet.

{% tab template="common/individual-rtl", compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  private data = ["Artwork", "Abstract", "Modern Painting", "Ceramics", "Animation Art", "Oil Painting"];

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id='list' dataSource={this.data} showHeader = 'true' headerTitle = 'Painting types' enableRtl = 'true' ></ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}