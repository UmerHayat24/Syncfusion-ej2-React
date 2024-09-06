# Auto-hide/show the expand/collapse icon of TreeView

You can display the expand icon by hovering the mouse over TreeView and hide the expand icon by leaving the mouse from TreeView. Refer to the following code sample to hide/show the expand/collapse icon automatically using the mouse.

{% tab template="tree-view/auto-hide-icons", sourceFiles="app/**/*.tsx" %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

export default class App extends React.Component<{}, {}> {

  constructor(props: any){
    super(props);
    this.showIcon = this.showIcon.bind(this);
    this.hideIcon = this.hideIcon.bind(this);
  }

   // Data source for TreeView component
  private countries: { [key: string]: Object }[]= [
         { id: 1, name: 'India', hasChild: true },
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
    ];
    private field:Object ={ dataSource: this.countries, id: 'id', text: 'name', parentID: 'pid', hasChildren: 'hasChild' };
    public treeObj: TreeViewComponent;

     onCreate(): void {
        let collapse: NodeListOf<Element> = this.treeObj.element.querySelectorAll('.e-icons.e-icon-collapsible');
        let expand: NodeListOf<Element> = this.treeObj.element.querySelectorAll('.e-icons.e-icon-expandable');
        this.hideIcon(expand, collapse);
        this.treeObj.element.addEventListener('mouseenter', (event:any) => {
          this.showIcon(expand, collapse);
        });
        this.treeObj.element.addEventListener('mouseleave', (event:any) => {
          this.hideIcon(expand, collapse);
        });
    }
    // hides expand/collapse icon on hovering the mouse
     hideIcon(expand: any,collapse: any): void {
        for(let i: number = 0; i < collapse.length; i++ ){
          collapse[i].setAttribute('style','visibility: hidden');
        }
        for(let j: number = 0; j < expand.length; j++ ){
          expand[j].setAttribute('style','visibility: hidden');
        }
    }

  // shows expand/collapse icon while leaving the mouse
   showIcon(expand: any, collapse: any): void {
      for(let i: number = 0; i < collapse.length; i++ ){
        collapse[i].setAttribute('style',"visibility", "");
      }
      for(let j: number = 0; j < expand.length; j++ ){
        expand[j].setAttribute('style',"visibility", "");
      }
  }

  render() {
    return (
      <div className = 'control-pane'>
        <div className='control-section'>
        <div className='control_wrapper'>
            {/* Render TreeView */}
            <TreeViewComponent fields={this.field}  ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }} created={this.onCreate.bind(this)}/>
        </div>
        </div>
      </div>
    )
  }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}