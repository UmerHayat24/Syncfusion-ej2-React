# Get iconCss dynamically in TreeView

In TreeView component, you can get the original bound data using the `getTreeData` method. For this method, if you pass the id of the tree node, it returns the corresponding node information, or otherwise the overall tree nodes information will be returned. You can use this method to get the bound iconCss class in the `nodeChecking` event. Please refer to the following sample.

{% tab template="tree-view/icon-css", sourceFiles="app/**/*.tsx,style.css"  %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeCheckEventArgs } from '@syncfusion/ej2-react-navigations';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

export default class App extends React.Component<{}, {}> {

   // Data source for TreeView component
   private treeData: Object[] = [
        {
        "nodeId": "01", "nodeText": "Music", "icon": "folder", "expanded": true, "nodeChild": [
            { "nodeId": "01-01", "nodeText": "Gouttes.mp3", "icon": "audio" }
          ]
        },
        {
          "nodeId": "02", "nodeText": "Videos", "icon": "folder", "expanded": true, "nodeChild": [
            { "nodeId": "02-01", "nodeText": "Naturals.mp4", "icon": "video" },
            { "nodeId": "02-02", "nodeText": "Wild.mpeg", "icon": "video" }
          ]
        }
    ];

    private field:Object ={  dataSource: this.treeData, id: 'nodeId', text: 'nodeText', child: 'nodeChild', iconCss: 'icon', expanded: 'expanded' };
    private showCheckBox: boolean = true;
    private autoCheck: boolean = false;
    public treeObj: TreeViewComponent;

    onNodeCheck(args: NodeCheckEventArgs): void {
      let nodeId = args.data[0].id.toString();
      // To get the iconCss
      let iconClass: any = this.treeObj.getTreeData(nodeId)[0].icon;
      alert('Icon class is ' + iconClass);
    }

    render() {
      return (
        <div className = 'control-pane'>
          <div className='control-section'>
            <div className='control_wrapper'>
              {/* Render TreeView */}
              <TreeViewComponent fields={this.field} nodeChecking={this.onNodeCheck.bind(this)} showCheckBox={this.showCheckBox} autoCheck={this.autoCheck} ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }}/>
            </div>
          </div>
        </div>
      )
    }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}