# Apply hover background color in the whole multi-line of a tree node

This section demonstrates how to hover and select a multi-line tree node. Here, you can set the row height (element class: `e-fullrow`) to be the same as the row content (element class: `e-text-content`)

{% tab template="tree-view/multi-line-tree", sourceFiles="app/**/*.tsx,style.css"  %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeSelectEventArgs } from '@syncfusion/ej2-react-navigations';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

export default class App extends React.Component<{}, {}> {

    constructor(props: any){
        super(props);
        this.setHeight=this.setHeight.bind(this);
    }

   // Data source for TreeView component
   private hierarchicalData: { [key: string]: Object }[]= [
      {
            id: 1, name: 'Web Control sWeb ControlsWeb ControlsWeb ControlsWeb ControlsWeb ControlsWeb ControlsWeb Controls', expanded: true,
            child: [
                {
                    id: 2, name: 'CalendarCalendarCalendarCalendarCalendarCalendarCalendarCalendarCalendarCalendarCalendarCalendarCalendar', child: [
                        { id: 7,  name: 'Constructors' },
                        { id: 8,  name: 'Properties' },
                        { id: 9,  name: 'Methods' },
                        { id: 10, name: 'Events' }
                    ]
                },
                {
                    id: 3, name: 'Data Grid', child: [
                        { id: 11, name: 'Constructors' },
                        { id: 12, name: 'Fields' },
                        { id: 13, name: 'Properties' },
                        { id: 14, name: 'Methods' },
                        { id: 15, name: 'Events' }
                    ]
                },
                {
                    id: 4, name: 'DropDownList', child: [
                        { id: 16, name: 'Constructors' },
                        { id: 17, name: 'Properties' },
                        { id: 18, name: 'Methods' }
                    ]
                },
                {
                    id: 5,  name: 'Menu', child: [
                        { id: 19, name: 'Constructors' },
                        { id: 20, name: 'Fields' },
                        { id: 21, name: 'Properties' },
                        { id: 22, name: 'Methods' },
                        { id: 23, name: 'Events' }
                    ]
                }
            ]
        },
        {
            id: 24, name: 'Web Controls',
            child: [
                {
                    id: 25, name: 'Calendar', child: [
                        { id: 26, name: 'Constructors' },
                        { id: 27, name: 'Properties' },
                        { id: 28, name: 'Methods' },
                        { id: 29, name: 'Events' }
                    ]
                },
                {
                    id: 30, name: 'Data Grid', child: [
                        { id: 31,  name: 'Constructors' },
                        { id: 32,  name: 'Fields' },
                        { id: 33,  name: 'Properties' },
                        { id: 34,  name: 'Methods' },
                        { id: 35,  name: 'Events' }
                    ]
                }
            ]
        }
    ];


    private field:Object ={  dataSource: this.hierarchicalData , id: 'id', text: 'name', child: 'child' };

    private style: string="customTree";
    public treeObj: TreeViewComponent;

    // Sets e-fullrow to be the same as e-text-content
     setHeight(element: any) {
      if(this.treeObj.fullRowSelect) {
        if(element.classList.contains("e-treeview")) {
          element = element.querySelector(".e-node-focus").querySelector(".e-fullrow");
        }
        else if(element.classList.contains("e-list-parent")) {
          element = element.querySelector(".e-fullrow");
        }
        else if(element.classList.value != ("e-fullrow") && element.closest(".e-list-item")) {
          element = element.closest(".e-list-item").querySelector(".e-fullrow");
        }
        if(element.nextElementSibling)
          element.style.height = element.nextElementSibling.offsetHeight +"px";
      }
    }
    // Triggers on node selection
    onSelect(args: NodeSelectEventArgs): void {
      this.setHeight(args.node);
    }
    created(){
    // Triggers on mouse hover/keydown event
     this.treeObj.element.addEventListener('mouseover', (event: any)=>{
            this.setHeight(event.target);
        });
    }

    render() {
        return (
            <div className = 'control-pane'>
                <div className='control-section'>
                    <div className='control_wrapper'>
                        {/* Render TreeView */}
                        <TreeViewComponent fields={this.field} created={this.created.bind(this)} nodeSelecting={this.onSelect.bind(this)} cssClass={this.style}  ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }} />
                    </div>
                </div>
            </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}