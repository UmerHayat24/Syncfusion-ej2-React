# Remove the check box of the parent nodes alone in TreeView

By enabling the `showCheckBox` property, you can render check box before each node of TreeView. However, some application needs to render check box in child nodes alone. In such case, you can remove the check box of the parent node by customizing the CSS.

{% tab template="tree-view/remove-parent-checkbox", sourceFiles="app/**/*.tsx,style.css"   %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeSelectEventArgs } from '@syncfusion/ej2-react-navigations';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

export default class App extends React.Component<{}, {}> {

   // Data source for TreeView component
   private Countries: { [key: string]: Object }[] = [
    { id: 1, name: 'India', hasChild: true, expanded: true },
    { id: 2, pid: 1, name: 'Assam' },
    { id: 3, pid: 1, name: 'Bihar' },
    { id: 4, pid: 1, name: 'Tamil Nadu' },
    { id: 6, pid: 1, name: 'Punjab' },
    { id: 7, name: 'Brazil', hasChild: true },
    { id: 8, pid: 7, name: 'Paraná' },
    { id: 9, pid: 7, name: 'Ceará' },
    { id: 10, pid: 7, name: 'Acre' },
    { id: 11, name: 'France', hasChild: true },
    { id: 12, pid: 11, name: 'Pays de la Loire' },
    { id: 13, pid: 11, name: 'Aquitaine' },
    { id: 14, pid: 11, name: 'Brittany' },
    { id: 15, pid: 11, name: 'Lorraine' },
    { id: 16, name: 'Australia', hasChild: true },
    { id: 17, pid: 16, name: 'New South Wales' },
    { id: 18, pid: 16, name: 'Victoria' },
    { id: 19, pid: 16, name: 'South Australia' },
    { id: 20, pid: 16, name: 'Western Australia' },
    { id: 21, name: 'China', hasChild: true },
    { id: 22, pid: 21, name: 'Guangzhou' },
    { id: 23, pid: 21, name: 'Shanghai' },
    { id: 24, pid: 21, name: 'Beijing' },
    { id: 25, pid: 21, name: 'Shantou' }
   ]

    private field:Object ={  dataSource: this.Countries, id: 'id', text: 'name', parentID: 'pid', hasChildren: 'hasChild' };
    private cssClass="custom";
    private showCheckBox: boolean = true;

    render() {
      return (
        <div className = 'control-pane'>
          <div className='control-section'>
            <div className='control_wrapper'>
              {/* Render TreeView */}
              <TreeViewComponent fields={this.field} cssClass={this.cssClass}  showCheckBox={this.showCheckBox} />
            </div>
          </div>
        </div>
      )
    }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}